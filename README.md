# CORS Proxy (Caddy)

Small Caddy-based HTTPS proxy that adds permissive CORS headers while only forwarding requests to explicitly allowed hosts.

Adds permissive CORS headers while proxying only to hosts that match `ALLOWED_HOSTS_REGEX` via the `X-Host` header.

## Run
```bash
cp example.env .env  # set ALLOWED_HOSTS_REGEX
docker compose up -d
curl -i http://localhost:8080/health
```

## Example Usage
```bash
curl -i \
  -H "X-Host: canvas.nus.edu.sg" \
  -H "Authorization: Bearer <TOKEN>" \
  "http://localhost:8080/api/v1/users/self"
```

If `X-Host` matches the regex, the request proxies to `https://<X-Host>:443/...` with CORS headers; otherwise it returns `400`.
