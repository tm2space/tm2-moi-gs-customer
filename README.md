# MCC QuickStart

## Prerequisites

* Docker and Docker Compose

## Configuration

The MCC system can be configured using environment variables. Copy the example file to get started:

```sh
cp .env.example .env
```

### Available Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `OBC_HOST` | Hostname/IP address for OBC connection | `localhost` |
| `OBC_TM_PORT` | Port for receiving OBC telemetry | `10015` |
| `OBC_TC_PORT` | Port for sending OBC telecommands | `10014` |
| `YAMCS_PORT` | Port for Yamcs HTTP server | `8090` |
| `YAMCS_HOST` | Host address for Yamcs HTTP server | `0.0.0.0` |

## Running with Docker Compose

### Setup

1. Copy the environment example file:
   ```sh
   cp .env.example .env
   ```

2. Edit the `.env` file with your configuration values:
   ```sh
   vim .env
   ```

3. Run the system using Docker Compose:
   ```sh
   docker-compose up
   ```

To run in detached mode:
```sh
docker-compose up -d
```

To stop the system:
```sh
docker-compose down
```

### Docker Compose Environment

The Docker Compose setup automatically uses the `.env` file for configuration. Make sure to create your `.env` file from the example before running.

## Accessing Yamcs

Once running, you can access the Yamcs web interface at:

```
URL: http://localhost:8090/
Default Login Credentials: admin/admin
```

## Telecommanding

This project defines a few example CCSDS telecommands. They are received on UDP port `10014`. Commands have no side effects and are used for testing the telecommand interface.

The system also receives telemetry packets on UDP port `10015` at a configurable rate (default 1Hz) from your OBC or simulator.

## Configuration Examples

### Running with Default Configuration

Use the default configuration for local development:

```sh
cp .env.example .env
docker-compose up
```

This will connect to OBC at `localhost:10015` (telemetry) and `localhost:10014` (commands), with Yamcs running on `localhost:8090`.

### Running with Custom Configuration

Create and edit a `.env` file:

```sh
cp .env.example .env
# Edit .env with your custom values
vim .env
```

Then run with Docker Compose:

```sh
docker-compose up
```

Example `.env` file for connecting to a remote OBC:

```sh
OBC_HOST="192.168.1.100"
OBC_TM_PORT="1235"
OBC_TC_PORT="1234"
YAMCS_PORT="8090"
YAMCS_HOST="0.0.0.0"
```
