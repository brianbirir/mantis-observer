# Mantis

An easy to deploy observability platform based on the LGTM stack (Loki, Grafana, Tempo and Prometheus) with OpenTelemetry Collector integration. This is a personal project to help monitor personal systems and applications but feel free to use it for your own needs.

## Features

- **OpenTelemetry Collector** - Unified telemetry collection, processing, and routing
- **Loki** - Log aggregation and querying
- **Grafana** - Visualization and dashboarding
- **Tempo** - Distributed tracing
- **Prometheus** - Metrics collection and alerting
- Pre-configured datasources with automatic correlation (metrics → logs → traces)
- Pre-configured alert rules for monitoring
- Docker Compose setup for easy deployment
- Vendor-agnostic architecture via OpenTelemetry

## Architecture

The stack follows an OpenTelemetry Collector-based architecture where all telemetry data (metrics, logs, traces) flows through the OTel Collector before being routed to appropriate backends:

```text
Application → OTel Collector → Prometheus (metrics)
                             → Loki (logs)
                             → Tempo (traces)
                             ↓
                          Grafana (visualization)
```

This architecture provides flexibility, vendor neutrality, and centralized telemetry processing.

## Quick Start

### Prerequisites

- Docker Engine 20.10 or higher
- Docker Compose 2.0 or higher
- At least 4GB of available RAM
- Ports 3000, 3100, 3200, 4317, 4318, 8888, 8889, 9090 available

### Setup

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd mantis
   ```

1. Create environment file (optional):

   ```bash
   cp .env.example .env
   # Edit .env if you want to customize settings
   ```

1. Start the stack:

   ```bash
   docker-compose up -d
   ```

1. Verify all services are running:

   ```bash
   docker-compose ps
   ```

All services should show as "healthy" after a minute or two.

### Accessing the Services

Once the stack is running, you can access:

- **Grafana**: <http://localhost:3000>
  - Default credentials: admin/admin (change after first login)
  - Pre-configured datasources for Prometheus, Loki, and Tempo

- **Prometheus**: <http://localhost:9090>
  - Metrics storage and querying
  - Alert rules configured

- **Loki**: <http://localhost:3100>
  - Log aggregation (API endpoint)

- **Tempo**: <http://localhost:3200>
  - Distributed tracing (API endpoint)

- **OpenTelemetry Collector**:
  - OTLP gRPC: `localhost:4317`
  - OTLP HTTP: `localhost:4318`
  - Metrics: <http://localhost:8888/metrics>
  - Health: <http://localhost:13133>

### Sending Telemetry Data

The OpenTelemetry Collector is ready to receive telemetry via OTLP:

- Send metrics, logs, and traces to `http://localhost:4318` (HTTP) or `localhost:4317` (gRPC)
- Use OpenTelemetry SDKs in your applications
- Phase 2 will include a Flask test application demonstrating this integration

### Stopping the Stack

```bash
docker-compose down
```

To stop and remove all data:

```bash
docker-compose down -v
```

## Project Status

- ✅ **Phase 1: Infrastructure Setup** - Complete
  - Docker Compose configuration
  - OpenTelemetry Collector setup
  - Prometheus configuration
  - Loki configuration
  - Tempo configuration
  - Grafana datasource provisioning

- 🔜 **Phase 2: Flask Test Application** - Coming next
- 🔜 **Phase 3: Dashboards & Queries** - Planned
- 🔜 **Phase 4: Deployment & Documentation** - Planned

## Documentation

- [Implementation Plan](IMPLEMENTATION_PLAN.md) - Detailed implementation roadmap
- [Architecture](ARCHITECTURE.md) - Architecture documentation
- [Project Context](CLAUDE.md) - Development context
