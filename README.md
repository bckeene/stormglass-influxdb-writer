# stormglass_influxdb_writer

Fetches historical weather and ocean data from the [Storm Glass API](https://stormglass.io/) and writes it to an InfluxDB Cloud bucket in line protocol format.

## What It Does

For each beach location defined in `beach_meta.csv`, the script:
1. Pulls the last 5 days of hourly weather data (temperature, wave height, wind, etc.)
2. Converts each hour into an InfluxDB data point with location tags
3. Writes the points to your InfluxDB Cloud bucket

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

