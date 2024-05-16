# service.template

service for TEMPLATE

[Documentation of service core](https://github.com/Vereine-Vereint/service.core)

[Documentation of borg](https://github.com/Vereine-Vereint/service.borg)

## Requires Authentik outpost!

put this configuration in your traefik configuration folder. Only works if authentik is running on the same traefik instance or a proxy outpost named "authentik-server" is hosted on the same traefik instance.

```yaml
http:
  middlewares:
    authentik:
      forwardAuth:
        address: http://authentik-server:9000/outpost.goauthentik.io/auth/traefik
        trustForwardHeader: true
        authResponseHeaders:
          - X-authentik-username
          - X-authentik-groups
          - X-authentik-email
          - X-authentik-name
          - X-authentik-uid
          - X-authentik-jwt
          - X-authentik-meta-jwks
          - X-authentik-meta-outpost
          - X-authentik-meta-provider
          - X-authentik-meta-app
          - X-authentik-meta-version
```

In Authentik, create Application a d Proxy provider with "Forward auth (single application)" with external host of https://$UPTIMEKUMA_DOMAIN and set the following unauthenticated paths:

```
^/$
^/status
^/assets/
^/assets
^/icon.svg
^/api/.*
^/upload/.*
^/metrics
```
