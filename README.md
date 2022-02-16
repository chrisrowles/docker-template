# docker-template

This is a simple docker template to get started with a standard LAMP stack for projects that have:

- `.env` files
- composer dependencies

If your project doesn't use [vlucas/phpdotenv](https://github.com/vlucas/phpdotenv), or doesn't have a
`vendor/` directory, then you'll need to modify the startup script `./bin/up` to suit your needs...

Also, I built my dev-web service into an image, so don't forget to either build your image first (The Dockerfile's
in the `build/` directory), or modify `docker-compose.yml`, it's up to you...

## Getting Started

1. Clone this repository
   ```sh
   git clone https://github.com/chrisrowles/docker-template
   ```

2. Create `.env`:
   ```sh
   PROJECT_WORKSPACE=/home/chris/workspace
   PROJECT=/home/chris/workspace/rowles.ch
   GIT_URL=git@github.com:chrisrowles/rowles.ch.git

   DATABASE=mysql8
   MYSQL_ROOT_PASSWORD=******
   MYSQL_EPHEMERAL_STORAGE=./tmp/mysql 

   NETWORK_NAME=dev
   NETWORK_SUBNET=192.168.32.0/24
   NETWORK_GATEWAY=192.168.32.1

   HTTP_LOCAL_PORT=80
   HTTP_CONTAINER_PORT=80
   HTTP_CONTAINER_IP=192.168.32.10
   HTTP_CONTAINER_NAME=dev-web

   DATABASE_LOCAL_PORT=3306
   DATABASE_CONTAINER_PORT=3306
   DATABASE_CONTAINER_IP=192.168.32.11
   DATABASE_CONTAINER_NAME=dev-database
   ```

3. Create your vhost for local development, put it in the `vhosts` directory.

4. Run `./bin/up`:
    ```sh
    ./bin/up
    ```

5. You should see something like the following:
   ```sh
   Project directory already exists.
   Project vendor directory already exists.
   Project .env file already exists.
   MySQL storage already exists.
   Checking whether the dev network has been created.
   Creating dev network.
   d17ee4a50f8af7bda8b5695948388471ab4be83c31be3b1f1c136f9d7a0aa565
   dev network created successfully.
   Spinning up containers.
   [+] Running 2/2
    ⠿ Container dev-database  Started                                                                                                                                                                                      1.4s
    ⠿ Container dev-web       Started
   ```
