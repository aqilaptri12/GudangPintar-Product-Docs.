# í´Œ API Reference: Inventory Management

Dokumentasi ini menjelaskan *endpoint* untuk mengelola data stok secara programatik.

**Base URL:** `https://api.gudangpintar.com/v1`  
**Authentication:** Bearer Token (JWT)

---

## 1. Get Stock Level
Mengambil data stok terkini berdasarkan SKU atau Lokasi.

* **Endpoint:** `GET /inventory/stock`
* **Access:** `Read-Only`

### Request Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `sku_code` | String | No | Filter berdasarkan kode unik produk. |
| `warehouse_id` | Integer | Yes | ID Gudang (Contoh: 101 untuk Cikarang). |

### Example Request
```bash
curl -X GET "https://api.gudangpintar.com/v1/inventory/stock?warehouse_id=101&sku_code=ACC-001" \
     -H "Authorization: Bearer YOUR_TOKEN"
```

### Example Response (200 OK)
```json
{
  "status": "success",
  "data": {
    "sku": "ACC-001",
    "product_name": "Kabel Data Type-C",
    "quantity": 1500,
    "unit": "PCS",
    "last_updated": "2025-11-18T10:00:00Z"
  }
}
```

---

## 2. Update Stock (Adjustment)
Melakukan penyesuaian stok manual (misal: barang hilang/rusak).

* **Endpoint:** `POST /inventory/adjust`
* **Access:** `Write-Admin`

### Example Body
```json
{
  "sku": "ACC-001",
  "qty_change": -5,
  "reason": "Damaged in warehouse",
  "adjusted_by": "User_123"
}
```
