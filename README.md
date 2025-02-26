# Local VAMA traefik environment

This repo contains default VAMA traefik configuration for local dev environment.

## Usage

Before first setup, make sure you have the required dependencies:

    sudo apt install make libnss3-tools

Also note that `:80` port has to be unoccupied.

To initialize the environment:

    make init

This will:

- create an `.env` file (if none exists) 
- set up a docker network

To actually run the environment:

    make run

This will start a preconfigured traefik docker container. The container will occupy your `:80` port. It will also automatically start with the system but you can manage it with: `make stop` and `make restart`.

Traefik dashboard will be available here:

- http: http://traefik.vama.localhost

## Sample app

You can verify the environment is working with an included sample app `whoami`. Just run (in the same directory as this file): 

    docker compose up -d

The sample app should be available here:

- http: http://whoami.vama.localhost

## Local domains

Everything with `*.localhost` will be resolved to `127.0.0.1` so there's no need to edit `/etc/hosts` file.

The environment uses domain names matching: `*.vama.localhost`.

## Docker

A docker network `traefik-proxy-vama-local` will be created if it does not exist.

# Using the environment with your project

Detailed instructions on how to use this environment with your project are available
[here](project_usage.md).

# Troubleshooting

- Traefik requires `:80` port and the container will refuse to start if something is blocking any of these.
    - to see what's listening on port 80, you can use this command: `ss -peanut | grep ":80" | grep LISTEN`
