# Docker Compose (Portfolio Website)

Docker Compose files for my [portfolio website](https://github.com/Flamov/flamov-portfolio).

## Installation

1. Clone the repository
2. Login with Docker to the GitHub Packages Registry: `docker login docker.pkg.github.com`
3. Run `docker-compose up -d`

## Updating the app container

When a new image for the app has been published, do the following in order to update and restart the app container:

1. Rebuild the image: `docker-compose pull app`
2. Update and restart _just_ the app: `docker-compose up --no-deps -d app`

This can also be done in a single command as:

```docker-compose pull app && docker-compose up --no-deps -d app```
