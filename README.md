# Outline Server Installer

This repository contains a Bash script for installing the Outline Server and a Watchtower container to keep it updated. The Outline Server uses Shadowsocks for creating a secure VPN.

## Prerequisites

- A Linux server with `curl` and `docker` installed.
- Root access or a user with sudo privileges.

## Installation

``` bash 
sudo bash -c "$(wget -qO- https://raw.githubusercontent.com/viapip/docker-compose-outline/master/install.sh)"
```

You can customize the installation with environment variables or by editing the script directly. Some of the configurable options include:

- `SB_IMAGE`: Specify the Docker image for the Outline Server (default `quay.io/outline/shadowbox:nightly`).
- `CONTAINER_NAME`: Set the Docker container name for Shadowbox (default `shadowbox`). If you're running multiple instances, change `SHADOWBOX_DIR` to a different location.
- `SHADOWBOX_DIR`: Directory for persistent Outline Server state.
- `ACCESS_CONFIG`: Location of the access config text file.
- `SB_DEFAULT_SERVER_NAME`: Default server name, e.g., "Outline Server New York".
- `SENTRY_LOG_FILE`: File for logs that may be reported to Sentry in case of an install error. Should not contain personally identifiable information.
- `WATCHTOWER_REFRESH_SECONDS`: Interval in seconds for Watchtower to check for updates (default 3600).

## Script Options

The script supports several flags:

- `--hostname <hostname>`: The hostname used to access the management API and access keys.
- `--api-port <port>`: Port number for the management API.
- `--keys-port <port>`: Port number for access keys.


## Security Considerations

While the script attempts to secure your Outline Server by default, consider the following:

- Review firewall settings to ensure the API and access key ports are accessible.
- Regularly update your server system packages to keep the environment secure.


For detailed logs, refer to the `SENTRY_LOG_FILE` specified during installation or the default location.

## Building a Custom Outline Server Image

If you wish to customize the Outline Server or contribute to its development, you can build your own Docker image from the [source code](https://github.com/Jigsaw-Code/outline-server) .


Based on https://github.com/Jigsaw-Code/outline-server
