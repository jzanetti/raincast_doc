Dockerize RainCast
============================
The user can dockerize RainCast package following the steps:

1. check the env.yml

2. build the RainCast package::

    conda build . --no-test

   *The built package is required to be copied to the same directory holding Dockerfile*

3. check the Dockerfile

4. Create the Docker image::

    sudo docker build -t raincast_docker_img . --rm=true
