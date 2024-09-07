**Steps to Install Elasticsearch Using Docker Compose**

**Definition:**

1. **Create the `docker-compose.yml` file:**
   - Define the service name as `elasticsearch` and specify the build context path where your Dockerfile is located.
   - Set the `container_name` as `elastic_search`.
   - Define the ports to expose: `9200` for API calls over HTTP and `9300` for communication between nodes in a cluster.
   - Configure a health check, specifying the interval for status checks.
   - Use the default bridge network, and set up a volume to ensure data persistence in case the container restarts. All data will be restored on local storage.

2. **Dockerfile explanation:**
   - Use `ubuntu` as the base image.
   - Define environment variables for the Elasticsearch version (`7.17.5`) and Elasticsearch home path.
   - Install Java and Elasticsearch.
   - Copy the `log.yml` (for defining the logging pattern) and `elasticsearch.yml` (which contains node roles, discovery settings, and cluster-level configurations) from the local machine to `/usr/share/elasticsearch/config`.
   - Define the exposed ports, and specify the command that the container should execute upon startup in the `CMD` section.

**Steps to Install:**

1. **Pre-requisites:**
   Ensure that Docker and Minikube are installed locally.

2. **Build the Docker image:**
   - Run the following command to create the Docker image using the Docker Compose file:
     ```bash
     docker-compose build
     ```
     This will build the Elasticsearch image.
   - You can check the available Docker images with:
     ```bash
     docker images
     ```

3. **Run the container:**
   - Start the Elasticsearch container using the following command:
     ```bash
     docker run -itd --name elastic_search -p 9200:9200 elastic_search:v1
     ```
     - `-itd`: Interactive terminal detached mode (runs in the background).
     - `-p`: Defines the port mapping (e.g., 9200 for HTTP).

4. **Check the status of the container:**
   - To verify if the Elasticsearch container is running, use:
     ```bash
     curl -XGET http://localhost:9200
     ```

5. **Debugging:**
   - If the container is not working as expected, check the container logs:
     ```bash
     docker logs container_name_or_id
     ```
   - If the container doesn’t start at all, list all containers:
     ```bash
     docker ps -a
     ```
   - Inspect the container for further troubleshooting:
     ```bash
     docker inspect container_id
     ```
**Attached Screenshot For reference**


**Elasticsearch Status**
         ![image](https://github.com/user-attachments/assets/a37f24e7-db4c-4a3e-9d86-7ae0636c6ca2)
  
**Cluster Health**
        ![image](https://github.com/user-attachments/assets/2201c83a-7f42-4754-be2c-7ce7ff8dbcf0)


