# docker-cloud-example
Sample Python Flask application used to demonstrate how to deploy applications to cloud environments using Docker

### Required Software
  * [Docker](https://docs.docker.com/engine/installation/)
  * [Docker Compose](https://docs.docker.com/compose/install/)
  * [Docker Machine](https://docs.docker.com/machine/install-machine/)

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

### Remote Deployment to AWS

To remotely deploy the application to AWS, use the Docker Machine library to setup a remote Docker host
on an AWS instance. Obviously use the AWS Access and secret keys for your account. Also, note that the
```--amazonec2-vpc-id``` field is required and can be found in your account's EC2 management console:
```
docker-machine -D create --driver amazonec2 --amazonec2-access-key $AWS_ACCESS_KEY_ID
--amazonec2-secret-key $AWS_SECRET_KEY --amazonec2-vpc-id vpc-******** [Docker hostname]
```

For additional configuration options, see the Docker Machine [AWS driver docs](https://docs.docker.com/machine/drivers/aws/).
Note that Docker Machine has support for pretty much all of the other cloud service providers that support
containers as well.

The ```docker-machine env [Docker hostname]``` command will give you all of the details for the host that has
been created. To connect to the host to launch the application, run the following command:
```
eval "$(docker-machine env [Docker hostname])"
```

This command simply sets up some necessary environment variables for the Docker Compose library to use.

Finally, run the following command to launch the application on the AWS cloud instance (without sudo):
```
docker-compose up -d
```

To connect to the web application, you will need to make sure that your AWS security group for the instance
has port 80 open.

To shutdown the remote Docker machine host, run the following commands:
```
docker-machine stop [Docker hostname]
docker-machine rm [Docker hostname]
```

This will shutdown the containers and terminate the EC2 instance.