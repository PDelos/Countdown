# Countdown

A modern countdown timer web app built with SvelteKit, Bun, and Caddy. Features a responsive UI, Dockerized deployment, and easy configuration for local or production environments.

## Features
- Countdown timer with a clean, modern interface
- Built using SvelteKit for fast, reactive UI
- Bun for fast JavaScript runtime and package management
- Caddy for automatic HTTPS and reverse proxy
- Dockerized for easy deployment

## Getting Started

### Prerequisites
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Bun](https://bun.sh/) (for local development)

### Local Development
1. Install dependencies:
	```bash
	bun install
	```
2. Start the development server:
	```bash
	bun run dev
	```
3. Open your browser at [http://localhost:3000](http://localhost:3000)

### Docker Deployment
1. Build and start the containers:
	```bash
	docker-compose up --build
	```
2. Access the app at [https://localhost](https://localhost) (Caddy provides HTTPS by default)

### Production Deployment
1. Buy a domain and point it to your server's public IP.
2. Update the `Caddyfile` with your domain name.
3. Deploy using Docker Compose as above. Caddy will automatically obtain a trusted TLS certificate.

## Project Structure

- `app/` - SvelteKit app source code
- `Caddyfile` - Caddy web server configuration
- `docker-compose.yml` - Multi-container setup for app and Caddy

## Customization

- **Colors:**
	- You can easily change the app's color scheme by editing `app/src/app.css`.
- **Favicon & Icon:**
	- Replace the favicon and app icon by updating the files in `app/src/lib/assets/` and editing the relevant references in `app/src/routes/+layout.svelte`.

---
