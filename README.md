# FastDNS module for Caddy

This package contains a DNS provider module for [Caddy](https://github.com/caddyserver/caddy). It can be used to manage DNS records with [FastVPS](https://fastvps.ee/) accounts.

## Caddy module name

```
dns.providers.fastdns
```

## Config examples

To use this module for the ACME DNS challenge, [configure the ACME issuer in your Caddy JSON](https://caddyserver.com/docs/json/apps/tls/automation/policies/issuer/acme/) like so:

```json
{
	"module": "acme",
	"challenges": {
		"dns": {
			"provider": {
				"name": "fastdns",
				"api_token": "{env.YOUR_FASTDNS_API_TOKEN}",
				"api_url": "{env.YOUR_FASTDNS_API_URL}"
			}
		}
	}
}
```
* If `api_url` is not defined then used default URL

or with the Caddyfile:

```
your.domain.com {
	respond "Hello World"	# replace with whatever config you need...
	tls {
		dns fastdns {env.YOUR_FASTDNS_API_TOKEN} {env.YOUR_FASTDNS_API_URL}
	}
}
```

You can replace `{env.YOUR_FASTDNS_API_TOKEN}` with the actual auth token if you prefer to put it directly in your config instead of an environment variable.

## Building caddy with this module

install [xcaddy](https://github.com/caddyserver/xcaddy): `go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest`

Then build caddy:

```
xcaddy build \
    --with github.com/nf404/caddy-fastdns@master
```