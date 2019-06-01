# Docker Compose (Portfolio Website)

Docker Compose files for my [portfolio website](https://github.com/Flamov/flamov-portfolio).

## Installation

1. Clone the repository
2. Create a file in the root of the repository called `app-variables.env` and populate it with the appropriate environment variables ([more information here](https://github.com/Flamov/flamov-portfolio#installation))
    * Initially set `NODE_ENV` to `development` for the app to run only with HTTP in order for certificate verification to work
3. Run `docker-compose up -d` to start all services
4. Start a command shell in the _certbot_ container by running `docker exec -it certbot bash` and run the following to generate a set of SSL certificate files (the same command can be found in [certbot/register](certbot/register)):

    ```/scripts/certbot-auto certonly --webroot -w /webroots/flamov.com -d flamov.com -d www.flamov.com```

5. Exit the command shell (`exit`) and change `NODE_ENV` to `production` in the `app-variables.env` file
6. Recreate and restart the app container by running `docker-compose up --no-deps -d app` so it picks up the new environment variables and runs with HTTPS using the newly created certificate files

## Updating the app container

When a new image for the app has been published, do the following in order to update and restart the app container:

1. Rebuild the image: `docker-compose pull app`
2. Update and restart _just_ the app: `docker-compose up --no-deps -d app`

This can also be done in a single command as:

```docker-compose pull app && docker-compose up --no-deps -d app```

More information [can be found here](https://docs.docker.com/compose/production/#deploying-changes). For the website, the image and container update is done by CircleCI: https://github.com/Flamov/flamov-portfolio/blob/master/.circleci/config.yml#L92-L94
