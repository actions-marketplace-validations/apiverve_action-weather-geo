# APIVerve Weather & Geo Action

> Get weather data, timezone information, and geographic calculations

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Weather_%26_Geo-blue?logo=github)](https://github.com/apiverve/action-weather-geo)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Browse All APIs](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=weather-geo)** | **[Get Free API Key](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=weather-geo)** | **[Documentation](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=weather-geo)**

---

## What does this action do?

This action provides access to APIVerve's Weather & Geo APIs directly in your GitHub workflows:

- Get current weather conditions
- Get time in different timezones
- Calculate distances between locations
- Get sunrise/sunset times

### Available APIs

| API | Description |
|-----|-------------|
| `weatherforecast` | Weather reports current weather conditions for any city name or zip code. It provides real-time temperature and wind speed along with compass direction in both metric and imperial units. |
| `worldtime` | World Time looks up the current local time, date, and timezone for any city. Search by city name to get matching locations with country codes, IANA timezone identifiers, and formatted times in 12-hour and 24-hour formats. |
| `timezonelookup` | Timezone Lookup resolves any city or IANA zone name to its local time, UTC offset, and calendar date. Responses include 12-hour and 24-hour clocks plus the minute offset from GMT. |
| `distancecalculator` | Distance Calculator computes the distance between two coordinate pairs in miles and kilometers. Supply two latitude and longitude points to receive distances and resolved city and state names for both locations. |
| `sunrisesunset` | Sunrise Sunset calculates exact sunrise and sunset times, twilight stages, and golden hour windows for any latitude and longitude coordinates. Paid plans can specify custom dates and receive solar noon. |

---

## Quick Start

```yaml
- name: Weather & Geo
  uses: apiverve/action-weather-geo@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: weatherforecast
    params: '{"city": "New York"}'
```

---

## Setup

### 1. Get Your API Key

Sign up for a free account at [dashboard.apiverve.com/signup](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=weather-geo) and create an API key.

### 2. Add Secret to Repository

Go to your repository **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

- Name: `APIVERVE_KEY`
- Value: Your API key from the dashboard

### 3. Use in Workflow

```yaml
- name: Weather & Geo
  uses: apiverve/action-weather-geo@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: weatherforecast
    params: '{"your": "parameters"}'
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api_key` | Your APIVerve API key (or set `APIVERVE_API_KEY` env var) | Yes* | - |
| `api` | API to use: `weatherforecast`, `worldtime`, `timezonelookup`, `distancecalculator`, `sunrisesunset` | No | `weatherforecast` |
| `params` | JSON parameters for the API | No | `{}` |
| `output_file` | Path to save binary output (images, PDFs) | No | - |
| `format` | Response format: `json`, `yaml`, or `xml` | No | `json` |
| `fail_on_error` | Fail workflow if API returns error | No | `true` |
*\*API key is required but can be provided via input OR `APIVERVE_API_KEY` / `APIVERVE_KEY` environment variable.*

## Outputs

| Output | Description |
|--------|-------------|
| `result` | Full API response as JSON |
| `data` | The `data` field from response as JSON |
| `status` | API status (`ok` or `error`) |
| `file` | Path to downloaded file (if `output_file` was used) |
---

## Examples

### Weather Check

Get current weather for a location

```yaml
- name: Weather Check
  id: weather-geo-0
  uses: apiverve/action-weather-geo@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: weatherforecast
    params: '{"city": "New York"}'

- name: Use result
  run: echo "Result: ${{ steps.weather-geo-0.outputs.data }}"
```

### World Time

Get current time in a timezone

```yaml
- name: World Time
  id: weather-geo-1
  uses: apiverve/action-weather-geo@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: worldtime
    params: '{"city": "New York"}'

- name: Use result
  run: echo "Result: ${{ steps.weather-geo-1.outputs.data }}"
```


---

## Full Workflow Example

```yaml
name: Weather & Geo Workflow

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  weather-geo:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Weather & Geo
        id: result
        uses: apiverve/action-weather-geo@v1
        with:
          api_key: ${{ secrets.APIVERVE_KEY }}
          api: weatherforecast
          params: '{"city": "New York"}'

      - name: Show result
        run: |
          echo "Status: ${{ steps.result.outputs.status }}"
          echo "Data: ${{ steps.result.outputs.data }}"
```

---

## Related Actions

Looking for more APIVerve actions?

- [apiverve/action](https://github.com/apiverve/action) - Generic action for all 350+ APIs
- [apiverve/action-release-assets](https://github.com/apiverve/action-release-assets) - Generate QR codes, barcodes, and badges for your GitHub releases
- [apiverve/action-visual-testing](https://github.com/apiverve/action-visual-testing) - Capture screenshots and generate PDFs for visual regression testing and documentation
- [apiverve/action-dns-monitor](https://github.com/apiverve/action-dns-monitor) - Verify DNS configuration, check propagation, and validate DNSSEC after deployments

**[Browse all APIVerve Actions →](https://github.com/marketplace?query=apiverve)**

---

## Pricing

- **Free tier** - Get started with generous free limits
- **Pro plans** - Higher rate limits and priority support for production use

Check out [pricing details](https://apiverve.com/pricing?utm_source=github&utm_medium=action&utm_campaign=weather-geo).

---

## Resources

- **API Documentation**: [docs.apiverve.com](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=weather-geo)
- **API Marketplace**: [apiverve.com/marketplace](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=weather-geo)
- **Issues & Support**: [GitHub Issues](https://github.com/apiverve/action-weather-geo/issues)
- **Email**: support@apiverve.com

---

## License

MIT - see [LICENSE](LICENSE)

---

Built by [APIVerve](https://apiverve.com?utm_source=github&utm_medium=action&utm_campaign=weather-geo) - 350+ APIs for developers
