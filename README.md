# Sitespeed.io Performance Testing Workflow

This repository contains a GitHub Actions workflow for automated web performance testing using Sitespeed.io. The workflow runs performance tests, stores results in InfluxDB, and automatically publishes detailed reports to GitHub Pages.

## Features

- 🚀 Automated performance testing with Sitespeed.io
- 📊 Results storage in InfluxDB for trend analysis
- 📈 Automatic report publishing to GitHub Pages
- 🔄 Configurable manual and automated triggers
- 🕒 Timestamp-based run tracking
- 📝 Historical report mapping and access

## Prerequisites

Before using this workflow, ensure you have:

1. An InfluxDB instance set up and accessible
2. The following secrets configured in your GitHub repository:
   - `INFLUXDB_TOKEN`: Your InfluxDB authentication token

## Workflow Configuration

The workflow is triggered by:
- Push events to the `main` branch
- Manual trigger using GitHub Actions UI (workflow_dispatch)

### InfluxDB Configuration

The workflow is configured to use InfluxDB v2 with the following default settings:
- Organization: vega
- Bucket: sitespeed
- Tags are automatically added with the run ID

## Workflow Steps

1. **Repository Checkout**: Clones the repository
2. **Run ID Generation**: Creates unique identifiers for each test run
3. **InfluxDB Plugin Setup**: Installs and configures the Sitespeed.io InfluxDB plugin
4. **Sitespeed.io Test**: Runs performance tests using Docker
5. **Results Processing**: Manages test results and file permissions
6. **GitHub Pages Deployment**: Publishes reports and maintains a report index

## Reports Access

After the workflow runs successfully:

1. Reports are published to GitHub Pages at:
   `https://[your-username].github.io/[repository-name]/[run-id]/index.html`

2. A `report-mapping.json` file maintains an index of all reports with:
   - Run IDs
   - Timestamps
   - Direct URLs to reports

## Customization

To customize the workflow:

1. Modify the target URL in the Sitespeed.io command:
   ```yaml
   sitespeedio/sitespeed.io:latest \
   https://vegastack.com \ # Change this URL
   ```

2. Adjust Sitespeed.io parameters in the workflow file:
   - Browser configurations
   - Test scenarios
   - Output options

## Troubleshooting

Common issues and solutions:

1. **Permission Issues**: Ensure the `GITHUB_TOKEN` has proper permissions
2. **InfluxDB Connection**: Verify network connectivity and token validity
3. **Report Generation**: Check Docker logs if reports aren't generating

