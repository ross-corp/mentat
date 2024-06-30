# mentat

Observe the known (media) universe, and find us the files.

Wraps the following services:

- Plex (Media Server)
- Transmission w/ OpenVPN (Torrent Client)
- Sonarr (Orchestrator for downloading TV shows)
- Radarr (Orchestrator for downloading Movies)
- Overseerr (Web client for specifying media to download)
- Watchtower (automatically pulls new image updates, then restarts services)

# Startup

Manually running this is easy:

```bash
# From within the repo directory
$> docker compose up
```

If you want this to be run in the background automatically upon startup, on linux systems you can use `systemctl` with this using a file like so:

```
[Unit]
Description=Mentat Service
After=docker.service
Requires=docker.service

[Service]
Type=simple
User=<your username here>
WorkingDirectory=<path to your repostitory>
ExecStart=/usr/bin/docker compose -f <path to your repostitory>/docker-compose.yaml up
ExecStop=/usr/bin/docker compose -f <path to your repostitory>/docker-compose.yaml down
Restart=always
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

Then, you can enable the service like so, which will register it to run at startup:

```bash
$> sudo systemctl enable mentat.service
```

You can view logs with the following:

```bash
$> journalctl -r -u mentat.service
```

# Setup

Setting up Plex requires navigating to it from the host it's operating on. Set it up by navigating to `localhost:32400`, then follow the setup instructions.

The rest of the services can be setup remotely if needed, by navigating to the ports specified in the docker-compose file in this repo.
