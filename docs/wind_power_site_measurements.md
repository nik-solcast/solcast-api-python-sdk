# Premium Wind Site Measurements

The `wind_power_site_measurements` module manages measured power data for Premium Wind Power sites.

All measurement records use ISO-8601 timestamps. Site measurement power is measured in MW. See the [Premium Wind Power API documentation](https://docs.solcast.com.au/) for the complete request and response schemas.

| Method | Purpose |
|---|---|
| `create_wind_site_measurements` | Submit site measurements. |
| `get_wind_site_measurements` | Retrieve site measurements, with optional `start` and `end` filters. |
| `delete_wind_site_measurements` | Delete site measurements between required `start` and `end` timestamps. |
| `create_wind_sub_unit_site_measurements` | Submit measurements for labelled site sub-units. |
| `get_wind_sub_unit_site_measurements` | Retrieve sub-unit measurements, optionally filtered by `sub_unit`, `start`, and `end`. |
| `delete_wind_sub_unit_site_measurements` | Delete sub-unit measurements between required `start` and `end` timestamps. |

## Create site measurements

```python
from solcast import wind_power_site_measurements

response = wind_power_site_measurements.create_wind_site_measurements(
    resource_id="your-premium-wind-site",
    measurements=[
        {
            "period_end": "2026-01-01T00:30:00Z",
            "period": "PT30M",
            "power": 2.5,
            "wind_speed_hub_height": 8.2,
            "wind_direction_hub_height": 180,
        }
    ],
)
```

Create sub-unit measurements with a `sub_unit` value on every record:

```python
response = wind_power_site_measurements.create_wind_sub_unit_site_measurements(
    resource_id="your-premium-wind-site",
    measurements=[
        {
            "sub_unit": "turbine-1",
            "period_end": "2026-01-01T00:30:00Z",
            "period": "PT30M",
            "power": 2.5,
            "wind_speed_hub_height": 8.2,
        }
    ],
)
```

All methods return the SDK `Response` object. Use `response.to_dict()` to inspect the JSON response.
