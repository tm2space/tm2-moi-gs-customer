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
| `ADMIN_PASSWORD` | Admin password for Yamcs interface | `your_secure_admin_password_here` |
| `{CUSTOMER}_HOST` | Customer instance hostname/IP | `<OBC_IP_ADDRESS>` |
| `{CUSTOMER}_TM_PORT` | Customer telemetry port (YAMCS) | `<YAMCS_PORT>` |
| `{CUSTOMER}_TC_PORT` | Customer telecommand port (OBC) | `<OBC_PORT>` |
| `YAMCS_PORT` | Port for Yamcs HTTP server | `8090` |
| `YAMCS_HOST` | Host address for Yamcs HTTP server | `0.0.0.0` |

## Running with Docker Compose

### Setup

1. Copy the environment example file:
   ```sh
   cp .env.example .env
   ```

2. Create the required persistent directories:
   ```sh
   mkdir -p data/yamcs-data data/yamcs-logs data/yamcs-cache
   ```

3. Edit the `.env` file with your configuration values:
   ```sh
   vim .env
   ```

4. Run the system using Docker Compose:
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
Default Login Credentials: admin/<ADMIN_PASSWORD>
```

## Telecommanding

This project defines a few example CCSDS telecommands. They are received on configurable UDP ports. Commands have no side effects and are used for testing the telecommand interface.

The system also receives telemetry packets at configurable rates from your customer instances or simulators.

## Configuration Examples

### Running with Default Configuration

Use the default configuration for local development:

```sh
cp .env.example .env
docker-compose up
```

This will connect to customer instances with their configured ports, with Yamcs running on `localhost:8090`.

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

Example `.env` file for connecting to a remote customer instance:

```sh
{CUSTOMER}_HOST="192.168.1.100"
{CUSTOMER}_TM_PORT="1235"
{CUSTOMER}_TC_PORT="1234"
YAMCS_PORT="8090"
YAMCS_HOST="0.0.0.0"
ADMIN_PASSWORD="your_secure_password"
```
