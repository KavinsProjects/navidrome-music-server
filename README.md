# 🎵 kavstream

<img width="1743" height="1079" alt="Screenshot 2026-08-31 090335" src="https://github.com/user-attachments/assets/8f62b6cc-8d74-48d1-bee4-8c42be18bd5a" />


A self-hosted personal music streaming server powered by [Navidrome](https://www.navidrome.org/) and Docker. Stream your own music library from anywhere, manage playlists, and connect with any Subsonic-compatible app.

---

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Windows)
- Your music files stored locally

---

## Folder Structure

```
kavstream/
├── docker-compose.yml
├── data/                  # Navidrome database & cache (auto-created)
└── music/                 # Your music library
```

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/yourusername/kavstream.git
cd kavstream
```

### 2. Add your music

Copy your music files into the `music/` folder, or update the volume path in `docker-compose.yml` to point to your existing library.

### 3. Start the server

```bash
docker compose up -d
```

Open your browser and go to `http://localhost:4533`

### 4. Create your admin account

On first launch, Navidrome will prompt you to create an admin account. Do this immediately — the prompt only appears when no users exist.

---

## docker-compose.yml

```yaml
version: "3"

services:
  navidrome:
    image: deluan/navidrome:latest
    ports:
      - "4533:4533"

    environment:
     # ND_UILOGINBACKGROUNDURL: "https://freeimage.host/i/ui-bg.n9Y5cRj"
      ND_UIWELCOMEMESSAGE: "Welcome to kavinn Music Server"
      ND_SCANSCHEDULE: 3m
      ND_LOGLEVEL: info
      ND_MUSICFOLDER: /music
      ND_PLAYLISTSPATH: "Playlists"

    volumes:
      - "./data:/data"
      - "C:/Users/username/OneDrive/Documents/music/music:/music:ro"

      
```

---
<!-- 
## Connecting Mobile / Desktop Apps

Navidrome supports any **Subsonic-compatible** client. Some good ones:

| App | Platform |
|---|---|
| [Symfonium](https://symfonium.app/) | Android |
| [Substreamer](https://substreamerapp.com/) | iOS |
| [Sonixd](https://github.com/jeffvli/sonixd) | Windows / macOS / Linux |
| [Feishin](https://github.com/jeffvli/feishin) | Windows / macOS / Linux |

Use these settings to connect:
- **Server URL:** `http://localhost:4533` (or your machine's local IP for remote access)
- **Username / Password:** your Navidrome credentials -->

---

## Useful Commands

```bash
# Start
docker compose up -d

# Stop
docker compose down

# View logs
docker compose logs -f navidrome

# Force rescan music library
docker compose restart navidrome
```

---

## License

MIT
