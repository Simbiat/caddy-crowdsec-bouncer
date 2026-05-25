# Docker Compose example

## Usage

1. In `Caddyfile`, replace the placeholder domains and `reverse_proxy` backends with your own. Protection is wrapped in a reusable `(crowdsec)` snippet, so adding `import crowdsec` to a reverse proxy is all it takes to guard it.

2. Build and start:

   ```bash
   docker compose up -d --build
   ```

3. Register the bouncer and copy the key into the `api_key` field of the `Caddyfile`:

   ```bash
   docker compose exec crowdsec cscli bouncers add caddy
   ```

4. Reload Caddy:

   ```bash
   docker compose restart reverse-proxy
   ```

## AppSec (optional)

To enable [WAF](https://doc.crowdsec.net/docs/next/appsec/intro/), uncomment the `appsec`-related lines in `compose.yml` (the `7422` port and the AppSec `COLLECTIONS`), `acquis.yaml` (the `appsec_configs` block), and `Caddyfile` (`appsec_url` and `#appsec`), then rebuild.
