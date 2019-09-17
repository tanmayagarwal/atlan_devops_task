# Tools and technologies used
Jenkins, docker-compose, Git, Prometheus, nginx

## Ease of clustered enterprise level deployments

I have used jenkins triggering here. As a new push commit is made to github, jenkins triggering will take place and image will be build on jenkins portal running on port no 8080.

We will setup docker-compose.yml file. Then we will pull the image formed by jenkins and make the service up using - 

```bash
docker compose up
```

## Incremental remotely triggered application updates

As and when new update is pushed commit to github, jenkins triggering will take place and new image is built and in docker-compose we will pull the image and make the service up again.`

## Easy remote debugging

For debugging pupose we will access and analyze the logs.
For this purpose we first obtain the container id using 

```bash
docker ps | grep <service name>
```
Using above command we can obtain container-id 

Using this container id we can access logs

```bash
 docker exec -it [container_id] bash
```

## Health Alerts and Monitoring

For this purpose we will use Prometheus as a monitoring tool.

Prometheus collects metrics from monitored targets by scraping metrics HTTP endpoints

Once all the containers are up, Prometheus will now scrape and store the data based on the configuration. Prometheus is configured on port 9090,Go to the dashboard http://localhost:9090 and verify that Prometheus now has information about the time series information on the containers,node.

Use the dropdown next to the “Execute” button to see a list of metrics this server is collecting. In the list we can see a number of metrics prefixed with node_, that have been collected by the Node Exporter. For example, you can see the node’s CPU usage via the node_cpu metric.

## Disaster management

Each service defined in Docker compose configuration can be scaled using below command

```bash
docker-compose scale <service name> = <no of instances>
```
Now we can provide load balancer on top of these containers for disaster recovery.



