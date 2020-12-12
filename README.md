## Premise

This is a general spark stack for experimenting with spark.  The stack is supported by several docker images that need to be built (see docker folder).  The current images consist of a base image, a master node image, a worker node image, and a submit node image.  The base image can be changed to support things such as using AWS S3 buckets or Azure object store rather than hadoop.  A good example of such a base image is the getty image base image which rolls up spark without hadoop and loads in all the Azure object store jars.  There are many other examples of base images that can be used.  The docker-compose file can be used to deploy the stack and scale the nodes.  Typically you will have 1 submit node, 1 master node, and n worker nodes.  Jobs can be submitted via the submit node (exec into the node to work on the command line or IDE).  The submit node could be swapped out for jupyter notebook etc, depending on what you want to do.  Currently it is just a vanilla linux box with pyspark, sbt etc.

Note also that for distributed environsments and data to work they must be in a volume that can be shared by all nodes.  The docker stack contains the volumes but they must be manually crated prior to launch.  Images must also be built prior to deploy.

## Helpful Resources
- https://towardsdatascience.com/diy-apache-spark-docker-bb4f11c10d24  The docker compose stack and images are based on this article, though they have been adapted and can be further adapted for different use cases.
- https://github.com/ammnlab/docker
- https://github.com/DIYBigData/personal-compute-cluster/tree/master/simple-spark-swarm
- https://towardsdatascience.com/getting-started-with-data-analytics-using-jupyter-notebooks-pyspark-and-docker-57c1aaab2408 I have a stack similar to this, behind a reverse proxy, completely dockerized, and may place it in this repo at some point.
- https://www.kdnuggets.com/2020/07/apache-spark-cluster-docker.html


### Helpful Commands
- image build: docker build -f .\Dockerfile_worker -t spark_worker .
- create a volume: docker volume create control_node
- launch stack: docker stack deploy -c docker-compose.yml sparkdemo
- Teardown: docker stack rm sparkdemo