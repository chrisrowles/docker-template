# docker-template

This is a simple docker template to get started with a standard LAMP stack for projects that have:

- `.env` files
- composer dependencies

If your project doesn't use [vlucas/phpdotenv](https://github.com/vlucas/phpdotenv), or doesn't have a
`vendor/` directory, then you'll need to modify the startup script `./bin/up` to suit your needs.

## Getting Started

1. Clone this repository
   ```sh
   git clone https://github.com/chrisrowles/docker-template
   ```

2. Create `.env`:
   ```sh
   PHP_VERSION=8.1 # OR 7.4
   
   PROJECT_WORKSPACE=/home/chris/workspace
   PROJECT=/home/chris/workspace/my-project
   GIT_URL=git@github.com:me/my-project.git

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
   
- `PHP_VERSION`: Sets the PHP version to use for the web service. Go to line 6 in `docker-compose.yml`, you'll see this environment value is appended to the web service's build context path.
- `PROJECT_WORKSPACE`: Project folder(s) to mount, you can mount as many as you like provided you configure virtual hosts for each of them.
- `PROJECT` (deprecated): If you're working with a single project, use this, it simplifies setup.
- `GIT_URL`: If your project is hosted on git, you can use this to clone it locally to `PROJECT_WORKSPACE`.
- `MYSQL_ROOT_PASSWORD`: Choose a password for the root MySQL user.
- `MYSQL_EPHEMERAL_STORAGE`: Storage for MySQL (despite the name, it's currently left intact when running `./bin/down`).
- `NETWORK_NAME`: Name for the [docker network](https://docs.docker.com/network/).
- `NETWORK_SUBNET`: Subnet for the docker network (CIDR format).
- `NETWORK_GATEWAY`: Gateway for the subnet.
- `HTTP_LOCAL_PORT`: Local port to connect to the web service.
- `HTTP_CONTAINER_PORT`: Container port mapping for the web service.
- `HTTP_CONTAINER_IP`: Container IP address for the web service.
- `HTTP_CONTAINER_NAME`: Container name for the web service.
- `DATABASE_LOCAL_PORT`: Local port to connect to the database service.
- `DATABASE_CONTAINER_PORT`: Container port mapping for the database.
- `DATABASE_CONTAINER_IP`: Container IP address for the database.
- `DATABASE_CONTAINER_NAME`: Container name for the database

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
   
   Creating MySQL storage.
   
   Checking whether the dev network has been created.
   Creating dev network.
   d17ee4a50f8af7bda8b5695948388471ab4be83c31be3b1f1c136f9d7a0aa565
   dev network created successfully.
   ...
   ...
   Spinning up containers.
   [+] Running 2/2
    ⠿ Container dev-database  Started                                                                                                                                                                                      1.4s
    ⠿ Container dev-web       Started
   ```
