# Diagrama Entidad-Relación - SmartERP

## Entidades principales

```text
┌──────────────┐
│    ROLES     │
├──────────────┤
│ PK id        │
│ name         │
│ description  │
└──────┬───────┘
       │ 1:N
       ▼
┌──────────────┐
│    USERS     │
├──────────────┤
│ PK id        │
│ FK role_id   │
│ name         │
│ email        │
│ password     │
│ status       │
└──┬─────┬─────┘
   │     │
   │     ├───────────────────────┐
   │     │                       │
   │     ▼                       ▼
   │  ┌──────────────┐    ┌──────────────────────┐
   │  │    SALES     │    │ INVENTORY_MOVEMENTS  │
   │  ├──────────────┤    ├──────────────────────┤
   │  │ PK id        │    │ PK id                │
   │  │ FK user_id   │    │ FK product_id        │
   │  │ FK customer_id│   │ FK user_id           │
   │  │ sale_date    │    │ type                 │
   │  │ subtotal     │    │ quantity             │
   │  │ tax          │    │ reference_type       │
   │  │ total        │    │ reference_id         │
   │  │ status       │    │ notes                │
   │  └──────┬───────┘    └──────────┬───────────┘
   │         │ 1:N                   │
   │         ▼                       │ N:1
   │  ┌──────────────┐               │
   │  │SALE_DETAILS  │               │
   │  ├──────────────┤               │
   │  │ PK id        │               │
   │  │ FK sale_id   │               │
   │  │ FK product_id│               │
   │  │ quantity     │               │
   │  │ unit_price   │               │
   │  │ subtotal     │               │
   │  └──────┬───────┘               │
   │         │ N:1                   │
   │         ▼                       │
   │  ┌──────────────┐               │
   │  │   PRODUCTS   │◄──────────────┘
   │  ├──────────────┤
   │  │ PK id        │
   │  │ FK category_id│
   │  │ code         │
   │  │ name         │
   │  │ purchase_price│
   │  │ sale_price   │
   │  │ stock        │
   │  │ minimum_stock│
   │  │ status       │
   │  └──────┬───────┘
   │         │ N:1
   │         ▼
   │  ┌──────────────┐
   │  │ CATEGORIES   │
   │  ├──────────────┤
   │  │ PK id        │
   │  │ name         │
   │  │ description  │
   │  │ status       │
   │  └──────────────┘
   │
   │
   │
   ▼
┌──────────────┐
│   PURCHASES  │
├──────────────┤
│ PK id        │
│ FK supplier_id│
│ FK user_id   │
│ purchase_date│
│ subtotal     │
│ tax          │
│ total        │
│ status       │
└──────┬───────┘
       │ 1:N
       ▼
┌─────────────────┐
│PURCHASE_DETAILS │
├─────────────────┤
│ PK id           │
│ FK purchase_id  │
│ FK product_id   │
│ quantity        │
│ unit_price      │
│ subtotal        │
└────────┬────────┘
         │ N:1
         ▼
      PRODUCTS


┌──────────────┐
│  CUSTOMERS   │
├──────────────┤
│ PK id        │
│ first_name   │
│ last_name    │
│ identification│
│ phone        │
│ email        │
│ address      │
│ status       │
└──────┬───────┘
       │ 1:N
       ▼
     SALES


┌──────────────┐
│  SUPPLIERS   │
├──────────────┤
│ PK id        │
│ company_name │
│ contact_name │
│ phone        │
│ email        │
│ status       │
└──────┬───────┘
       │ 1:N
       ▼
   PURCHASES