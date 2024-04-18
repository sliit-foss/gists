---

## Running MySQL Server Using Docker

### Prerequisites:
- Install Docker on your machine. You can download it from [Docker Hub](https://hub.docker.com/).

### Steps to Setup:

1. **Pull the MySQL Docker Image:**

    Open your terminal or command prompt and execute the following command to download the MySQL image from Docker Hub:

    ```bash
    docker pull mysql
    ```

    This command pulls the latest MySQL server image.

2. **Create a MySQL Container:**

    Run the following command to create and start a MySQL server container. Replace `[your_password]` with your desired root password.

    ```bash
    docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=[your_password] -d mysql:latest
    ```

    - `--name some-mysql` gives your container a name.
    - `-e MYSQL_ROOT_PASSWORD=[your_password]` sets the MySQL root user's password.
    - `-d` runs the container in detached mode, meaning the container runs in the background.
    - `mysql:latest` specifies which image to use (in this case, the latest version of MySQL).

3. **Access MySQL Server:**

    You can connect to the MySQL server using the following command:

    ```bash
    docker exec -it some-mysql mysql -uroot -p
    ```

    This will prompt you for the password you set earlier.

### Usage:

1. **Managing the MySQL Container:**

   - **Start Container:**

     If your container is stopped, start it with:

     ```bash
     docker start some-mysql
     ```

   - **Stop Container:**

     To stop the running container, use:

     ```bash
     docker stop some-mysql
     ```

   - **Remove Container:**

     If you no longer need the container, you can remove it:

     ```bash
     docker rm some-mysql
     ```

   - **View Logs:**

     To see the logs for your MySQL container, use:

     ```bash
     docker logs some-mysql
     ```

### Advanced Configuration:

- **Setting up Persistent Storage:**

  To ensure that your MySQL data persists even after the container is removed, use the `-v` option to mount a directory from your host to the container:

  ```bash
  docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=[your_password] -d -v /my/own/datadir:/var/lib/mysql mysql
