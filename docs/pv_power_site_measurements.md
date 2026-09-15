# Premium PV Site Measurements

The `pv_power_site_measurements` module manages measured power data for Premium PV Power sites.

All measurement records use ISO-8601 timestamps. Site measurement power is measured in MW. See the [Premium PV Power API documentation](https://docs.solcast.com.au/) for the complete request and response schemas.

| Method | Purpose |
|---|---|
| `create_pv_site_measurements` | Submit site measurements. |
| `get_pv_site_measurements` | Retrieve site measurements, with optional `start` and `end` filters. |
| `delete_pv_site_measurements` | Delete site measurements between required `start` and `end` timestamps. |
| `create_pv_sub_unit_site_measurements` | Submit measurements for labelled site sub-units. |
| `get_pv_sub_unit_site_measurements` | Retrieve sub-unit measurements, optionally filtered by `sub_unit`, `start`, and `end`. |
| `delete_pv_sub_unit_site_measurements` | Delete sub-unit measurements between required `start` and `end` timestamps. |

## Create site measurements

```python
from solcast import pv_power_site_measurements

response = pv_power_site_measurements.create_pv_site_measurements(
    resource_id="your-premium-pv-site",
    measurements=[
        {
            "period_end": "2026-01-01T00:30:00Z",
            "period": "PT30M",
            "power": 1.25,
        }
    ],
)
```

Create sub-unit measurements with a `sub_unit` value on every record:

```python
response = pv_power_site_measurements.create_pv_sub_unit_site_measurements(
    resource_id="your-premium-pv-site",
    measurements=[
        {
            "sub_unit": "inverter-1",
            "period_end": "2026-01-01T00:30:00Z",
            "period": "PT30M",
            "power": 1.25,
        }
    ],
)
```

All methods return the SDK `Response` object. Use `response.to_dict()` to inspect the JSON response.
