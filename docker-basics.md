# Install Docker

# Install Docker-Compose

# Always mention container name in docker-compose.yml

Docker will create container with name <<container_name>>_<<service>>

# To start docker container
`
sudo docker-compose up -d
`
'-d' is for detached mode so that container can run on background independent on terminal


# To stop docker container
`
sudo docker-compose down
`

# To build a container for updation after configurational changes (like changes in RUN commands) without pulling whole Image all over again
`
sudo docker-compose up -d --build
`

# To get into running docker container bash
`
sudo docker exec -it <<container_name>> bash
`

# In case of use of ReWriteRule/Engine/Base in .htaccess in Apache Container mention following command in Dockerfile
`
RUN a2enmod rewrite
`