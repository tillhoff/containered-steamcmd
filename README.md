![GitHub Workflow Status](https://img.shields.io/github/workflow/status/tillhoff/containered-steamcmd/Publish%20image%20to%20docker%20hub)

# steamcmd

A generic image for steamcmd on debian.

## Usage

```
docker run \
  -it \
  --net=host \
  --name=<gamename> \
  --expose <serverport> \
  --expose <secondserverport> \
  -v $PWD/server:/game \
  tillhoff/steamcmd \
  bash -c "/usr/games/steamcmd \
    +login anonymous \
    +force_install_dir /game \
    +app_update <appid> \
    +quit && \
  cd /game/<path/to/executable> && \
    ./<executable> <parameters> \
  || \
  echo 'Creating backup...' && \
    tar -cfz $(date '+%Y-%m-%d-%H:%M').tar.gz /game/<path/to/savegame>"
```

> This will create an automatic backup after pressing ctrl+c.

## Restore backup

Run `tar -xf <%Y-%m-%d-%H:%M>.tar.gz`.
