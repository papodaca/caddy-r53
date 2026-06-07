# caddy-r53

Caddy Docker image with the [Route53 DNS plugin](https://github.com/caddy-dns/route53) for ACME DNS-01 challenges.

## Usage

```bash
docker pull ghcr.io/papodaca/caddy-r53:main
```

### Caddyfile Example

```caddyfile
example.com {
    tls {
        dns route53 {
            access_key_id {env.AWS_ACCESS_KEY_ID}
            secret_access_key {env.AWS_SECRET_ACCESS_KEY}
            region {env.AWS_REGION}
        }
    }
}
```

### Docker Compose

```yaml
services:
  caddy:
    image: ghcr.io/papodaca/caddy-r53:latest
    ports:
      - "80:80"
      - "443:443"
    environment:
      AWS_ACCESS_KEY_ID: ${AWS_ACCESS_KEY_ID}
      AWS_SECRET_ACCESS_KEY: ${AWS_SECRET_ACCESS_KEY}
      AWS_REGION: ${AWS_REGION}
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
      - caddy_config:/config

volumes:
  caddy_data:
  caddy_config:
```

## Building Locally

```bash
docker build -t caddy-r53 .
```

## Tags

| Tag | Description |
|-----|-------------|
| `latest` | Latest build from `main` |
| `vX.Y.Z` | Semantic version release |
| `sha-<hash>` | Specific commit |

## License

MIT
