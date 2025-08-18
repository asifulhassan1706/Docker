# Docker Compose Guide

## 1️⃣ Smallest Example (Nginx Web Server)

**docker-compose.yml**:

```yaml
version: "3.8"                 # Compose file format version. 3.8 is commonly used.
services:                      # Start of services list (each service = one container)

  web:                         # Service name ('web' represents the web server)
    image: nginx:alpine        # Which image to use for the container — here, official nginx, small alpine variant
    container_name: my_nginx   # (Optional) Name for the container
    ports:                     # Map host machine port ↔ container port
      - "8080:80"              # Host:Container → 8080:80 (access nginx at localhost:8080)
    volumes:                   # Share files/folders (host ↔ container)
      - ./site:/usr/share/nginx/html:ro
````
How to Test:

```bash
docker compose up
```
* Open your browser: ``http://localhost:8080``

* Place an ``index.html`` file inside the ``./site folder`` and it will be displayed by ``nginx``.

## 2️⃣ Two-Service Example (Flask + Redis “Hit Counter”)

```yaml
version: "3.8"

services:

  web:
    build: .                     # লোকাল Dockerfile থেকে ইমেজ বানাবে
    container_name: flask_app
    ports:
      - "5000:5000"              # হোস্ট 5000 → কন্টেইনার 5000
    environment:
      - REDIS_HOST=redis         # Flask অ্যাপ জানবে Redis সার্ভিসের নাম
    depends_on:
      - redis                    # Redis আগে উঠবে

  redis:
    image: redis:alpine          # অফিসিয়াল Redis ইমেজ
    container_name: redis_db
    volumes:
      - redis_data:/data         # ডেটা named volume এ থাকবে

volumes:
  redis_data: {}
```

**Why these lines are needed:**

* `services:` → Where you define container configurations
* `web / redis` → Service names; Compose uses them as DNS names for communication
* `build:` → Build the image from a local Dockerfile
* `image:` → Pull a prebuilt image from Docker Hub
* `ports:` → Map host ↔ container ports
* `environment:` → Send runtime environment variables to the container
* `depends_on`: → Startup order (which service should start first)
* `volumes:` → Share data or code with the container
* `volumes (root-level):` → Declare named volumes

**How to run:**

```bash
docker compose up --build
```

* **Open in browser:** `http://localhost:5000`
* Every refresh will increment the Redis hit counter

## 3️⃣ Frequently Used Keys (Cheat Sheet)

* `version` → Compose file version
* `services` → Configurations for all containers
* `build` → Build image from a local Dockerfile
* `image` → Pull image from Docker Hub
* `container_name` → Optional container name
* `ports` → `Host:Container` port mapping
* `environment` → Runtime environment variables
* `volumes` → Bind mount or named volume
* `depends_on` → Startup order
* `command` → Override default command of the image
* `restart` → Handle crashes `(always, unless-stopped)`
* `networks` → Define which network the service belongs to


## 4️⃣ Common Mistakes & Fixes

* **YAML indentation errors** → Use spaces, not tabs
* **Port mapping reversed** → `8080:80` is correct, not `80:8080`
* **Wrong service name** → DNS connection will fail
* **Incorrect file path** → Bind mount will fail
* Old volumes causing conflicts → Use `docker compose down -v` for a clean start


## 5️⃣ Useful Commands

```bash
docker compose up             # Start all services (logs in foreground)
docker compose up -d          # Start in detached mode (background)
docker compose up --build     # Rebuild images before starting
docker compose ps             # List running services/containers
docker compose logs -f web    # Follow logs of a specific service
docker compose down           # Stop all services and remove containers
docker compose down -v        # Stop and remove containers + volumes (data deleted)
```

## Easy Formula to Write a Compose File

* File name: `docker-compose.yml`

* Start with: `version: "3.8"`

* `services:` → List the service names

* For each service, provide `image` or `build`

* Optionally include `ports` `environment` `volumes` `depends_on`

* For persistent data → declare root-level `volumes:`
