# cloud-run
Put together some sample codes from https://cloud.google.com/run/docs/quickstarts/build-and-deploy/python

Container runtime contract
- Supported languages and images

    Cloud Run accepts container images in Docker Imanage Manifest V2, Schema 1, and Schema 2 image formats.

- PORT
    Cloud Run injects the PORT environment variable into the container. Default, it is 8080 but possible to be configured.

- TLS
    Should not be implemented

- Responses
    The container must response within a configured time as defined in request timeout setting (1 to 3600 seconds, or from 1 to 60 minutes)

- Environment variables
    - PORT
    - K_SERVICE
    - K_REVISION
    - K_CONFIGURATION: The name of Cloud Run configuration that created the revision

- Filesystem access
    It is an in-memory filesystem

- Container instance lifecycle
    - After being deployed, a service is run with a number of container instances. Each of them runs the deployed container image.
    - If no traffic (incoming requests), the service is scaled down to the minimum number of container instances configured (zero by default).
    - When incoming requests to the service arrive,Cloud Run service scales up the number of container instances.
    - Startup: 
    After startup, a container instance is given 4 minute to serve a request
    - Shutdown
    After its lifetime is reached, the container instance is scheduled to shutdown.
    Upon of receving SIGTERM, it has 10 seconds. Otherwise, CloudRun sends  SIGKILL
- Container instance resrouces
    - CPU: by default a container instance is assigned 1 CPU.
    - Memory: limited to 16GB
    - Concurrency: a container instance can serve more than one request

    All can be configured.
