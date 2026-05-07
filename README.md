# stormglass-influxdb-writer

Fetches historical (hindcast) weather and ocean data from the [Storm Glass API](https://stormglass.io/) and writes it to an InfluxDB Cloud bucket in line protocol format.

## What It Does

For each beach location defined in `beach_meta.csv`, the script:
1. Pulls the last 5 days of hourly hindcast weather data from NOAA via Storm Glass
2. Converts each hour into an InfluxDB data point with location tags and 9 weather fields
3. Writes the points to your InfluxDB Cloud bucket

### Weather Fields Collected

| Field | Unit | Description |
|-------|------|-------------|
| `air_temp` | °C | Air temperature |
| `water_temp` | °C | Water temperature |
| `wave_height` | m | Wave height |
| `swell_height` | m | Swell height |
| `wind_speed` | m/s | Wind speed |
| `wind_direction` | ° | Wind direction |
| `pressure` | hPa | Atmospheric pressure |
| `humidity` | % | Relative humidity |
| `cloud_cover` | % | Cloud cover |

## Setup

1. **Install dependencies:**
   ```bash
   pip install influxdb-client requests arrow
   ```

2. **Configure credentials** in `config.py`:
   - [InfluxDB Cloud](https://cloud2.influxdata.com/signup) — free tier works fine
   - [Storm Glass](https://dashboard.stormglass.io/register) — base account allows 50 API requests/day

3. **Add locations** to `beach_meta.csv` (name, state, county, lat, lon)

4. **Run:**
   ```bash
   python stormglass.py
   ```

## Files

| File | Description |
|------|-------------|
| `stormglass.py` | Main script — fetches data and writes to InfluxDB |
| `config.py` | Configuration file for API credentials and paths |
| `beach_meta.csv` | CSV of beach locations to pull weather data for |

