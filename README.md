# Docker Compose (Portfolio Website)

Docker Compose files for my [portfolio website](https://github.com/Flamov/flamov-portfolio).

## Installation

1. Clone the repository
2. Create a file in the root of the repository called `app-variables.env` and populate it with the appropriate environment variables ([more information here](https://github.com/Flamov/flamov-portfolio#installation))
3. Run `chmod +x init-certbot.sh` then `sudo ./init-certbot.sh` to generate mock certificates (for nginx), start the services, then generate a new set of Let's Encrypt certificates (more info [here](https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71))

## Updating the app container

When a new image for the app has been published, do the following in order to update and restart the app container:

1. Rebuild the image: `docker-compose pull app`
2. Update and restart _just_ the app: `docker-compose up --no-deps -d app`

This can also be done in a single command as:

```docker-compose pull app && docker-compose up --no-deps -d app```

More information [can be found here](https://docs.docker.com/compose/production/#deploying-changes). For the website, the image and container update is done with CircleCI: https://github.com/Flamov/flamov-portfolio/blob/master/.circleci/config.yml#L92-L94
