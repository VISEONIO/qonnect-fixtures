# Qonnect test fixtures

Synthetic data only, for testing VISEON Qonnect and the VISEON DuckDB extension. It contains no real customers, transactions or client data.

## fixture-orders.parquet

There are 45,100 generated orders, with these columns:

| Column | Type | Meaning |
|---|---|---|
| `customer` | text | `C00001`–`C25100` |
| `year` | integer | 2025 or 2026 |
| `sales` | integer | 10 in 2025, 20 in 2026 |
| `cost` | integer | 60% of sales |

Rows 1–25,000 are customers 1–25,000 in 2025. Rows 25,001–45,000 are customers 1–20,000 in 2026. Rows 45,001–45,100 are customers 25,001–25,100 in 2026.

The rules are deterministic, so every expected answer can be computed rather than recorded. Total sales are 652,000.

## iceberg/

Static Apache Iceberg tables for the VISEON Iceberg extension, read without a catalog via their `.metadata.json` URL. The paths inside the metadata are jsDelivr URLs pinned to the `iceberg-v1` tag, which serves byte ranges with open CORS. Both tables are partitioned by `year`.

| Table | Rows | Source | Current metadata |
|---|---|---|---|
| `fixture-orders` | 45,100 | `fixture-orders.parquet` above | `iceberg/fixture-orders/metadata/00002-7f5d6135-5fe0-43e1-961c-f2b45b7cbbc2.metadata.json` |
| `bench-orders-10m` | 10,000,000 | `customer_id` 1–1,000,000 and `year` 2025–2026, 5 orders per pair; `sales = i % 97 + 1`, `cost = sales * 6 // 10` | `iceberg/bench-orders-10m/metadata/00002-0ee87916-4170-44f5-9b53-48fb201c32c5.metadata.json` |

The metadata URLs are under `https://cdn.jsdelivr.net/gh/VISEONIO/qonnect-fixtures@iceberg-v1/`.
