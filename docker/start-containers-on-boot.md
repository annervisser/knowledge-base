# Start a docker compose project on boot
## Setup
```shell
crontab -e
```

Add line:
```shell
@reboot sleep 5 && cd /path/to/docker/compose/project && /usr/bin/docker compose up -d
```
Or with notifications:
```shell
@reboot sleep 5 && notify-send --icon=emblem-synchronizing Docker "Starting containers..." && cd /path/to/docker/compose/project && /usr/bin/docker compose up -d && notify-send --icon=emblem-default Docker "Containers started!" || notify-send --icon=emblem-unreadable Docker "Failed starting containers"
```

#### Troubleshooting
Check if `/usr/bin/docker` is the right path:
```shell
which docker
```
