# docker-cloud-example
Sample Python Flask application used to demonstrate how to deploy applications to cloud environments using Docker

### Required Software
  -[Docker](https://docs.docker.com/engine/installation/)
  -[Docker Compose](https://docs.docker.com/compose/install/)

### Running Locally

To run the Nginx/Python Flask web application container locally on port 80:
```
sudo docker-compose up -d
```

To then stop and remove the container:
```
sudo docker-compose stop
sudo docker-compose rm -f
```
