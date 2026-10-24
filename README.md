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
