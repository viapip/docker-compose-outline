# Outline Server Installer

This repository contains a Bash script for installing the Outline Server and a Watchtower container to keep it updated. The Outline Server uses Shadowsocks for creating a secure VPN.

### Important Note on Docker Compose

This installation script (`install_server.sh`) is customized to generate a Docker Compose file (`docker-compose.yml`) for managing the Outline Server and Watchtower containers. This approach simplifies updates and management but might introduce complexities if you're planning extensive customizations or modifications to the Docker setup. 

**If the creation of a Docker Compose file is not necessary for your use case, or if you prefer a more straightforward deployment without it, consider using the Outline Server [source code](https://github.com/Jigsaw-Code/outline-server/blob/master/src/shadowbox/README.md) directly for your customizations.** This direct approach gives you full control over the Docker commands and configurations, making it better suited for advanced customizations or when integrating Outline Server into an existing Docker environment.


## Prerequisites

- [Docker](https://docs.docker.com/engine/install/)

**Building a Custom Image:**
- [Node](https://nodejs.org/en/download/) LTS (`lts/hydrogen`, version `18.16.0`) // [NVM](https://github.com/nvm-sh/nvm)
- [NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) (version `9.5.1`)

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

## Remote with Outline Manager
https://getoutline.org/get-started/

## Security Considerations

While the script attempts to secure your Outline Server by default, consider the following:

- Review firewall settings to ensure the API and access key ports are accessible.
- Regularly update your server system packages to keep the environment secure.


For detailed logs, refer to the `SENTRY_LOG_FILE` specified during installation or the default location.

## Building a Custom Outline Server Image

If you wish to customize the Outline Server or contribute to its development, you can build your own Docker image from the [source code](https://github.com/Jigsaw-Code/outline-server/blob/master/src/shadowbox/README.md) .
1. **Clone stable version:**
``` bash
git clone -b server-v1.8.1 --depth 1 https://github.com/Jigsaw-Code/outline-server.git && cd outline-server
   ```
   - **Help**

     ```sh
     npm install
     npm run action:help
     ```
-  **Build:**
   
     ```sh
     npm run action shadowbox/docker/build
     ```
     An image will be created ```localhost/outline/shadowbox```



Based on https://github.com/Jigsaw-Code/outline-server
