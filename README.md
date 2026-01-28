# target-cinch
Singer.io target for Cinch API

## Configuration

### Required Parameters
- `email`: API user email
- `password`: API user password
- `environment`: Target environment (`dev`, `local`, or production)

### Optional Parameters

#### `sort_batches` (boolean, default: false)
Sorts batches by `company_id`, `entity_source`, and `entity_ref` before sending to the API. This ensures consistent lock ordering in the database and prevents deadlocks when multiple threads or workers process concurrent requests.

**When to enable:**
- You're experiencing deadlock errors during bulk imports
- Multiple tap processes run concurrently for the same company
- Django is running with multiple workers or threading enabled

**Example config:**
```json
{
  "email": "user@example.com",
  "password": "password",
  "environment": "dev",
  "sort_batches": true
}
```

**Performance impact:** Negligible (sorting 500 records takes microseconds)
