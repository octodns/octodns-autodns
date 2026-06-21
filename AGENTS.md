# Developer Agent Guide for octoDNS AutoDNS Provider

This repository contains the AutoDNS provider for octoDNS. It enables planning, syncing, and applying DNS record states directly to the InternetX AutoDNS API.

> [!IMPORTANT]
> **Core Workflow and Guidelines**
>
> All agents working on this repository must read and follow the general instructions and workflow guidelines defined in the core octoDNS `AGENTS.md` file.
> - **Local check**: Look for the file at `../octodns/AGENTS.md`.
> - **Remote check**: If the local file is not available, fetch it from GitHub: [octoDNS Core AGENTS.md](https://github.com/octodns/octodns/raw/refs/heads/main/AGENTS.md).
>
> You must align your code structure, style, pull request guidelines, and overall development workflows with the instructions specified there.

## Repository & Module Information

### Key Components

- **Provider Class**: [AutoDNSProvider](file:///home/ross/octodns/octodns-autodns/octodns_autodns/__init__.py#L90-L336) (defined in [octodns_autodns/__init__.py](file:///home/ross/octodns/octodns-autodns/octodns_autodns/__init__.py)). This is the primary provider class mapping records and executing updates via stream modifications.
- **Client Class**: [AutoDNSClient](file:///home/ross/octodns/octodns-autodns/octodns_autodns/__init__.py#L44-L88) manages HTTP communication with the AutoDNS API v1 (`https://api.autodns.com/v1`).
- **Authentication**: Authenticates using Basic Authentication headers (username/password) via the `username`, `password`, and `context` properties.

### Key Workflows & Features

1. **Supported Record Types**: `A`, `AAAA`, `CAA`, `TXT`, `CNAME`, `MX`, `NS`, `SRV`, `ALIAS`.
2. **System Name Server Dependency**: The AutoDNS API requires specifying a primary name server for a zone in request URLs (e.g. `/zone/{name}/{system_name_server}`). This must be configured using the `system_name_server` argument.
3. **Dynamic Routing**: Not supported (`SUPPORTS_DYNAMIC=False`, `SUPPORTS_GEO=False`).
4. **Dynamic Subnets**: Not supported (`SUPPORTS_DYNAMIC_SUBNETS=False`).
5. **Pool Value Status**: Not supported (`SUPPORTS_POOL_VALUE_STATUS=False`).

## Development & Testing

- **Setup Script**: Run `./script/bootstrap` to create a virtual environment, install dependencies (including `black`, `isort`, `pyflakes`, and `pytest`), and configure pre-commit hooks.
- **Test Suite**: Run unit tests using `pytest` via `./script/test` (or `pytest tests/`). Test files are located in [tests/](file:///home/ross/octodns/octodns-autodns/tests).
- **Code Coverage**: Verify code coverage using `./script/coverage`.

## Key Constraints & Behaviors

- **Python Version**: Targets Python `>=3.9`.
- **Formatting**: Code formatting is enforced via `black` (version `>=26.0.0,<27.0.0`) and `isort`.
