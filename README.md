# APIVerve Weather &amp; Geo Action

> Get weather data, timezone information, and geographic calculations

> **Beta Release** - This action is in beta. We'd love your feedback! [Open an issue](https://github.com/apiverve/action-weather-geo/issues) if you encounter any problems.

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Weather &amp; Geo-blue?logo=github)](https://github.com/marketplace/actions/apiverve-weather-geo)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Browse All APIs](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=weather-geo)** | **[Get Free API Key](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=weather-geo)** | **[Documentation](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=weather-geo)**

---

## What does this action do?

This action provides access to APIVerve's Weather &amp; Geo APIs directly in your GitHub workflows:

- Get current weather conditions
- Get time in different timezones
- Calculate distances between locations
- Get sunrise/sunset times

### Available APIs

| API | Description |
|-----|-------------|
| `weather` | weather API |
| `worldtime` | World Time is a simple tool for getting the current time in any city. It returns the current time, date, and more. |
| `timezonelookup` | Timezone Lookup is a simple tool for looking up timezone data. It returns the timezone name, offset, and more. |
| `distancecalculator` | Distance Calculator is a simple tool for calculating the distance between two locations. It returns the distance in miles and kilometers. |
| `sunrisesunset` | Sunrise Sunset is a simple tool for getting the sunrise and sunset times. It returns the sunrise and sunset times for a given location and date. |

---

## Quick Start

```yaml
- name: Weather &amp; Geo
  uses: apiverve/action-weather-geo@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: weather
    params: '{&quot;city&quot;: &quot;New York&quot;}'
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
- name: Weather &amp; Geo
  uses: apiverve/action-weather-geo@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: weather
    params: '{"your": "parameters"}'
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api_key` | Your APIVerve API key (or set `APIVERVE_API_KEY` env var) | Yes* | - |
| `api` | API to use: `weather`, `worldtime`, `timezonelookup`, `distancecalculator`, `sunrisesunset` | No | `weather` |
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
    api: weather
    params: '{&quot;city&quot;: &quot;New York&quot;}'

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
    params: '{&quot;timezone&quot;: &quot;America/New_York&quot;}'

- name: Use result
  run: echo "Result: ${{ steps.weather-geo-1.outputs.data }}"
```


---

## Full Workflow Example

```yaml
name: Weather &amp; Geo Workflow

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  weather-geo:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Weather &amp; Geo
        id: result
        uses: apiverve/action-weather-geo@v1
        with:
          api_key: ${{ secrets.APIVERVE_KEY }}
          api: weather
          params: '{&quot;city&quot;: &quot;New York&quot;}'

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
