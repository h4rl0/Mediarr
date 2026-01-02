# 📦 Mediarr Docker Compose

A clean Docker Compose setup for Sonarr, Radarr, Prowlarr, and Bazarr.

---

## ⚙️ Services

| Service    | Purpose                               |
|-----------|----------------------------------------|
| Sonarr    | TV show management                     |
| Radarr    | Movie management                       |
| Prowlarr  | Indexer manager for Sonarr/Radarr      |
| Bazarr    | Subtitle management                    |

---
## 📂 Required Folder Layout

All services mount the same `/data` directory to allow **hardlinks** and **instant moves**.

```text
/data
├── downloads
│   ├── incomplete
│   └── complete
└── media
    ├── movies
    └── tv
```                                           
---
## Docker Compose
```yaml
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /data:/data
    ports:
      - 8989:8989
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /data:/data
    ports:
      - 7878:7878
    restart: unless-stopped

  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /data:/data
    ports:
      - 9696:9696
    restart: unless-stopped

  bazarr:
    image: lscr.io/linuxserver/bazarr:latest
    container_name: bazarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
    volumes:
      - /data:/data
    ports:
      - 6767:6767
    restart: unless-stopped

networks:
  default:
    name: arrstack



