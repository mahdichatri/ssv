version: '3.8'

services:
  traefik:
    image: traefik:latest
    container_name: traefik
    command:
      # Global configuration
      - --api.dashboard=true
      - --api.insecure=true
      - --providers.docker=true
      - --providers.docker.exposedbydefault=false
      
      # Entry points
      - --entrypoints.web.address=:80
      - --entrypoints.websecure.address=:443
      
      # CORRECTED: Configure default certificate using tls stores
      - --tls.stores.default.defaultCertificate.certFile=/certs/certificate.pem
      - --tls.stores.default.defaultCertificate.keyFile=/certs/privatekey.pem
      
      # Optional: Fallback ACME resolver
      - --certificatesresolvers.myresolver.acme.tlschallenge=true
      - --certificatesresolvers.myresolver.acme.email=your-email@example.com
      - --certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json
      
    ports:
      - "80:80"
      - "443:443"
      - "8080:8080"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./letsencrypt:/letsencrypt
      - ./certs:/certs
