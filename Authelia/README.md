
# Set up with Nginx Proxy Manager

##

### Put the [Nginx proxy config](https://github.com/Just5KY/SkyPi/blob/main/Authelia/nginx_proxy_configuration) in the additional settings of a proxy setting

### Change the IP:Port, service name, auth URL where mentioned

###

## Follow this tutorial by DBTech if you are stuck somewhere

### [Youtube](https://www.youtube.com/DBTechYT)

### [DBTech Doc](https://dbt3ch.com/books/authelia-for-nginx-proxy-manager)

# How to Bypass certain pages behing authelia to share data and api

## Add these to authelia configuration.yml as required

### **Matomo** tracking links globally in all subdomains

```yml
access_control:
  default_policy: deny # NOTE: all domains added in NPM rules will be denied unless added below
  rules:
    - domain:
        - "*.DOMAIN"   #Allow tracking links
      resources:
        - "/*Matomo*"
      policy: bypass
```

### **Grafana** public endpoints

```yml
access_control:
  rules:
    - domain:
        - "grafana.DOMAIN"   #Grafana
      resources:
        - "/public/"
      policy: bypass
```

### **File Browser** shares

```yml
access_control:
  rules:
    - domain:
        - "file.DOMAIN"     #File Browser
      resources:
        - "^/api/public/dl/*"
        - "/share/*"
        - "/static/js/*"
        - "/static/css/*"
        - "/static/img/*"
        - "/static/themes/*"
        - "/static/fonts/*"
      policy: bypass
```

### **Portainer api**

#### You can access portainer using android apps

```yml
access_control:
  rules:
    - domain:
        - "portainer.DOMAIN"  
      resources:
        - "/api/*"
      policy: bypass
```

### **Paperless-ng api**

#### You can access it from the mobile app, and upload documents

#### Thumbnails will be shown as it can be access by anybody using that link

```yml
access_control:
  rules:
    - domain:
        - "paper.DOMAIN"    
      resources:
        - "/api/tags/"
        - "/api/documents/"
        - "/api/correspondents/"
        - "/fetch/doc/"
      policy: bypass
```

### **Vaultwarden api**

#### You access it from Browser extensions and Mobile apps

```yml
access_control:
  rules:
    - domain:
        - "pswd.DOMAIN"       
      resources:
        - "/identity/connect/"
        - "/api/"
        - "/notifications/"
        - "/duo*"
        - "/favicon*"
        - "/images/"
        - "/icons/"
      policy: bypass
```

#
