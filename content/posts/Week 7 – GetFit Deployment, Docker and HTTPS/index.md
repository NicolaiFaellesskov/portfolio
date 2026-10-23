+++
date = '2026-10-23T12:00:00+02:00'
draft = false
title = 'Week 7 – GetFit Deployment, Docker and HTTPS'
+++

## What I have been working on

This week, I worked on deploying the GetFit Fitness API to a DigitalOcean Droplet. The main focus was setting up the deployment pipeline, running the application and database in Docker containers, configuring a domain, and securing the API with HTTPS.

I also worked on automating Docker image updates and testing the deployed API to make sure that authentication and protected endpoints work correctly over HTTPS.

## GitHub Actions and Docker Hub

I configured a GitHub Actions workflow to build and publish the GetFit API as a Docker image.

The workflow runs when changes are pushed to the `main` or `hibernate` branches. It builds the application using Maven, creates a Docker image, and pushes it to Docker Hub.

The image is published as:

`nicolaifaellesskov/get_fit:latest`

To authenticate with Docker Hub, I configured GitHub Actions repository secrets:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

I also configured a `JWT_SECRET_KEY` secret for the application's JWT configuration.

Using GitHub Actions means that I do not have to build and upload the Docker image manually every time I make changes to the application. The workflow handles the build and publishing process automatically.

## DigitalOcean Droplet

I deployed the API to a DigitalOcean Droplet running Linux.

The server runs the GetFit API in a Docker container named `getfit`. The Java application listens on port `7070`, which allows the server to receive requests and forward them to the application.

I also configured the server to use Docker Compose to manage the API and its supporting services.

This makes it easier to start, stop, and maintain the deployment using a single configuration file instead of manually managing each container.

## PostgreSQL and Docker Networking

The GetFit API uses PostgreSQL as its database.

I kept PostgreSQL in a separate Docker container named `db`, managed through its own Docker Compose configuration. The database uses a Docker volume mapping to `/opt/postgres/data` so that the database files persist outside the container.

I also configured a Docker network named `backend`. This allows the API, database, and other supporting containers to communicate over the internal Docker network.

The API receives its database connection settings through environment variables stored in an `.env` file. This includes the database name, username, password, and connection string.

Keeping the database in a separate container makes the deployment easier to manage and allows the API and database to have separate configurations and lifecycles.

## Environment Variables and Secrets

I configured the environment variables required by the deployed application.

These include:

- `DB_PASSWORD`
- `DB_NAME`
- `DB_USERNAME`
- `CONNECTION_STR`
- `JWT_SECRET_KEY`
- `DEPLOYED`

The server-side environment variables are stored in `/opt/getfit/.env`, with restricted file permissions.

This separates configuration and sensitive values from the application code and Docker image. It also allows the same application image to be used in different environments without hardcoding database credentials or JWT signing keys.

## Watchtower and Automatic Updates

I configured Watchtower to monitor the deployed API container for updated Docker images.

Watchtower checks for new images every 300 seconds and is configured to monitor the `getfit` container.

When GitHub Actions publishes a new version of the image to Docker Hub, Watchtower can detect the update and replace the running API container with the newer version.

This connects the image publishing workflow with the server deployment process. GitHub Actions builds and publishes the image, while Watchtower handles the container update on the server.

The PostgreSQL container is managed separately, so the API image can be updated without deliberately replacing the database container.

## Domain Registration and DNS Configuration

I registered the domain `getfitter.dk` through Simply.com and configured the domain to use DigitalOcean's nameservers:

- `ns1.digitalocean.com`
- `ns2.digitalocean.com`
- `ns3.digitalocean.com`

I then configured a DNS A record in DigitalOcean that points `api.getfitter.dk` to the Droplet's public IP address.

This allows the API to be accessed through a domain name instead of requiring clients to use the server's IP address and application port directly.

During the configuration, I encountered a DNS resolution problem caused by an outdated DNSSEC configuration. The domain initially returned `SERVFAIL` through a public DNS resolver, even though the DNS records were correct on DigitalOcean's nameservers.

I investigated the issue by querying the authoritative nameservers and comparing the results with a public DNS resolver. I then disabled the outdated DNSSEC configuration at Simply.com.

After this change, the public DNS lookup returned the correct IP address, and the API domain could resolve successfully.

## Caddy and HTTPS

I configured Caddy as a reverse proxy in front of the GetFit API.

Caddy runs in its own Docker container and listens on ports `80` and `443`. It forwards requests for `api.getfitter.dk` to the API container on port `7070` through the internal Docker network.

The Caddy configuration is:

```caddyfile
api.getfitter.dk {
    reverse_proxy getfit:7070
}
```

This allows clients to access the API over HTTPS without connecting directly to the application's internal port.

I also configured persistent storage for Caddy's data and configuration. This allows its certificate data to survive container restarts.

Caddy automatically obtained a TLS certificate from Let's Encrypt. I verified the certificate issuance in the container logs, including the successful ACME challenge validation.

Once the certificate was issued, I tested the domain using `curl`. The API returned an HTTP response through Caddy, confirming that HTTPS and the reverse proxy were working.

The root path `/` returned `404 Not Found` because the API does not expose a route at that path. This was not a certificate or reverse proxy failure.

## Testing the Deployed API with Hoppscotch

After configuring the domain and HTTPS, I used Hoppscotch to test the deployed API.

I tested the login endpoint:

`POST https://api.getfitter.dk/api/auth/login`

I sent a JSON request containing the test user's username and password. The login request succeeded and returned a JWT that could be used to access protected endpoints.

I then tested:

`GET https://api.getfitter.dk/api/users`

When I sent the request without an authorization token, the API returned `401 Unauthorized` with the message:

`Missing or invalid Authorization header`

This confirmed that the deployed API was enforcing JWT authentication.

After including the Bearer token returned by the login endpoint, the protected request succeeded.

This verified that the authentication flow worked through the public domain and HTTPS, rather than only when testing the application locally.

## What I learned

This week, I gained experience with deploying a Java API to a cloud server and connecting several services into one working setup.

I learned how GitHub Actions can automate building and publishing Docker images, how Docker Compose can manage application services, and how Watchtower can automate container updates.

I also worked with DNS configuration, nameserver delegation, DNSSEC troubleshooting, reverse proxies, TLS certificates, and HTTPS.

The deployment required more than just running the application on a server. The domain, DNS records, firewall, Docker networking, environment variables, and certificate configuration all had to work together.

I also learned the importance of separating application configuration and secrets from source code, as well as keeping the database's persistent storage separate from the API container.

Overall, I deployed the GetFit Fitness API to DigitalOcean and made it accessible through `https://api.getfitter.dk`. The deployed API successfully handles login requests and protects endpoints using JWT authentication. GitHub Actions publishes new Docker images, and Watchtower checks for updates to the running API container.
+++