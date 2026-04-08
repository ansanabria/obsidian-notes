---
notebook:
  - "[[Mantenimicros]]"
  - "[[Félix]]"
tags:
  - proyecto
---

# Automatización de Correos para Mantenimicros

## Resumen

Mantenimicros es intermediario: recibe inventario de proveedores y pedidos de clientes, todo por email. El objetivo es automatizar la extracción de datos de esos emails con un LLM y luego cruzar oferta vs. demanda para identificar oportunidades de venta o faltantes de inventario.

---

## Arquitectura General

Arquitectura **orientada a eventos**: cada email dispara un procesamiento asíncrono que termina en una notificación al equipo comercial.

| Componente | Función |
|------------|---------|
| Email Connector | Recibe emails (IMAP/webhook) |
| LLM | Extrae datos estructurados del texto |
| Base de datos | Inventario, órdenes, matches |
| Matching Engine | Cruza demanda vs. oferta |
| Dashboard + Alertas | Muestra oportunidades al vendedor |

---

## 1. Contexto del Sistema

```mermaid
flowchart LR
    Proveedor -->|inventario| Email
    Cliente -->|pedido| Email
    Email --> Sistema
    Sistema -->|oportunidades| Vendedor
    Sistema -->|faltantes| Vendedor
```

Proveedores envían inventario y clientes envían pedidos por email. El sistema procesa ambos y le entrega al vendedor: oportunidades listas para vender, y alertas de lo que falta en inventario.

---

## 2. Arquitectura Interna

```mermaid
flowchart LR
    Email --> Ingesta --> LLM --> BD
    BD --> Matching --> Alertas
    BD --> Dashboard
```

Flujo lineal y simple:
1. **Ingesta** recibe el email
2. **LLM** extrae los datos (marca, modelo, cantidad, precio)
3. **BD** guarda inventario u orden
4. **Matching** cruza oferta con demanda
5. **Dashboard** y **Alertas** muestran resultados

---

## 3. Flujo de Procesamiento

```mermaid
flowchart TD
    A[Email recibido] --> B{Proveedor o Cliente?}
    B -->|Proveedor| C[Extraer inventario con LLM]
    B -->|Cliente| D[Extraer pedido con LLM]
    C --> E[Guardar en tabla inventario]
    D --> F[Guardar en tabla orden]
    E --> G[Cruzar con ordenes pendientes]
    F --> H[Cruzar con inventario disponible]
    G --> I{Hay match?}
    H --> I
    I -->|Si| J[Crear oportunidad y notificar]
    I -->|No| K[Registrar como faltante]
```

---

## 4. Modelo de Datos

```mermaid
erDiagram
    PROVEEDOR ||--o{ INVENTARIO : provee
    CLIENTE ||--o{ ORDEN : solicita
    INVENTARIO ||--o{ OPORTUNIDAD : genera
    ORDEN ||--o{ OPORTUNIDAD : crea

    PROVEEDOR {
        int id PK
        string nombre
        string email
    }

    CLIENTE {
        int id PK
        string nombre
        string email
    }

    INVENTARIO {
        int id PK
        int proveedor_id FK
        string marca
        string modelo
        string sku
        int cantidad
        decimal precio
    }

    ORDEN {
        int id PK
        int cliente_id FK
        string modelo_solicitado
        int cantidad
        string urgencia
    }

    OPORTUNIDAD {
        int id PK
        int inventario_id FK
        int orden_id FK
        string tipo_match
        decimal margen
    }
```

---

## 5. Secuencia: Email de Proveedor

```mermaid
sequenceDiagram
    actor P as Proveedor
    participant S as Sistema
    actor V as Vendedor

    P->>S: Email con inventario
    S->>S: LLM extrae marcas, modelos, cantidades
    S->>S: Guardar en tabla inventario
    S->>S: Cruzar con ordenes pendientes
    alt Hay match
        S->>V: Oportunidad de venta
    else No hay match
        S->>S: Inventario disponible queda registrado
    end
```

---

## 6. Secuencia: Email de Cliente

```mermaid
sequenceDiagram
    actor C as Cliente
    participant S as Sistema
    actor V as Vendedor

    C->>S: Email con pedido
    S->>S: LLM extrae modelo, cantidad, urgencia
    S->>S: Guardar en tabla orden
    S->>S: Cruzar con inventario disponible
    alt Hay match
        S->>V: Oportunidad inmediata
    else No hay match
        S->>V: Alerta de faltante
    end
```

---

## 7. Lógica de Matching

```mermaid
flowchart LR
    Inventario --> E[Exacto: mismo SKU]
    Inventario --> S[Similar: embeddings]
    Orden --> E
    Orden --> S
    E --> Score
    S --> Score
    Score -->|alto| Oportunidad
    Score -->|bajo| Faltante
```

Tres niveles de matching:
- **Exacto**: mismo SKU o modelo
- **Similar**: por embeddings (ej: "ThinkPad T14" ≈ "ThinkPad T14s")
- **Sin coincidencia**: se registra como faltante para negociar con proveedores

---

## 8. Stack Sugerido (para empezar rápido)

| Componente        | Herramienta           |
| ----------------- | --------------------- |
| Ingesta de emails | n8n + Gmail API       |
| LLM               | OpenAI GPT-4          |
| Base de datos     | PostgreSQL + pgvector |
| Backend/API       | Node.js / FastAPI     |
| Dashboard         | Next.js               |
| Alertas           | Email / Slack         |

---

## 9. Roadmap

```mermaid
flowchart LR
    A[Fase 1: MVP<br/>4 semanas] --> B[Fase 2: Matching<br/>4 semanas]
    B --> C[Fase 3: Escalar<br/>4 semanas]
    C --> D[Fase 4: Optimizar<br/>4 semanas]
```

- **Fase 1** — Ingesta de emails + extracción con LLM + BD básica
- **Fase 2** — Matching exacto + notificaciones + dashboard
- **Fase 3** — Matching semántico con embeddings + scoring + reportes de faltantes
- **Fase 4** — Predicción de demanda + integración con ERP/contabilidad

---

## Próximos Pasos

1. Validar arquitectura con el equipo
2. Definir MVP: ¿qué tan rápido necesitan ver resultados?
3. Elegir stack según presupuesto y expertise
4. Diseñar prompt de LLM para extracción
5. Prototipar con n8n

## Prompt de Extracción (referencia)

```
Eres un extractor de datos de emails de comercio de equipos de cómputo.
Analiza el siguiente email y extrae información estructurada.

TIPO DE EMAIL: [PROVEEDOR o CLIENTE]

Si es PROVEEDOR, extrae:
- Lista de productos: marca, modelo, SKU, cantidad, precio, condición

Si es CLIENTE, extrae:
- Producto solicitado: marca, modelo/especificaciones, cantidad, presupuesto, urgencia

Responde SOLO en JSON.
```

---

*Documento para Mantenimicros - Automatización de Correos*