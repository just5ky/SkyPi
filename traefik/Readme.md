

```yml
      traefik.enable: true
      traefik.http.routers.UNIQUE_APP_NAME.rule: Host(`UNIQUE_APP_NAME.$DOMAINNAME`)
      traefik.http.services.UNIQUE_APP_NAME.loadbalancer.server.port: 6902      # Internal Port of docker servcie
      traefik.http.services.UNIQUE_APP_NAME.loadbalancer.server.scheme: https   # Optional, if your docker service is exposing HTTPS port instead of HTTP
      traefik.http.routers.UNIQUE_APP_NAME.entryPoints: https
```