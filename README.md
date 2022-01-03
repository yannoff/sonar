# sonar

Sonarqube server &amp; scanner scripts using the dockerized versions

## Requirements

- bash
- docker

## Installation

### Example

Installing in the `/opt/sonar` directory.

```bash
# Since /opt is a system dir, execute the commands as root
sudo su

# Clone the project in the target directory
cd /opt
git clone https://github.com/yannoff/sonar

# Optionally create symlinks to allow system-wide script evocation
cd /usr/bin
ln -s /opt/sonar/bin/server sonar-server
ln -s /opt/sonar/bin/scan sonar-scan
```

## Usage

1. Start the server

    ```bash
    # Start the sonarqube server
    /opt/sonar/bin/server start
    # Watch the server logs an wait until bootstrap complete
    /opt/sonar/bin/server log
    ```

2. Visit the sonarqube local website at `http://localhost:9999`

    > Default credentials for the first connection:
    > - username: `admin`
    > - password: `admin`

3. Create a new key and token to use with the project to scan
4. Launch the scanner from the local project directory, using the previously created key and token

    _Example_

    ```bash
    /opt/sonar/bin/scan --sources=src/ --project=acme:key --login=1e3a987cde65fdd74118
    ```

### Scan options

_The following options may be used to override the `sonar-scanner` defaults or the settings defined in the `sonar-project.properties` file._


#### `--project`

The project key.

#### `--sources`

Path to the project sources.

#### `--login`

The project token.

#### `--host`

Alternative host for the sonarqube server. _(defaults: **sonar-server**)_

#### `--port`

Alternative port for the sonarqube server. _(defaults: **9999**)_

## Advanced config

_Additional settings may be configured via the [`.sonarrc`](.sonarrc) file._

Variable|Description|Default
---|---|---
`SONAR_HOME`|Top-level dir for the server data storage|`$(dirname .sonarrc)/var`
`SONAR_PORT`|Listening port for the sonar server (both internal & exposed)|`9999`
`SONAR_HOST`|Hostname for the sonar server docker service|`sonar-server`
`SONAR_NETWORK`|Network name for the sonar server docker service|`sonar`


## License

Licensed under the [MIT License](LICENSE).

