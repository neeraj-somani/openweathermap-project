## Openweathermap-project

### Weather analytics Dashboard project

  ![Dashboard](photos/Grafana_Dashboard.png?raw=true "Dashboard")

It's a weather monitoring system. This is a simple Data Pipeline (ETL) project that collects (E-extract) weather data from OpenWeatherMap using there RestAPI and make necessary Data Transformations (T) and Load (L) it into InfluxDB. Is it really worth just dump some data to a DB and not showing a meaningful purpose of it. Thats where Grafana comes into picture. We are going to use Grafana to build an insightful dashboard. Below picture depicts the same, this is the container architecture and the different layers of abstraction for analytics.

## Services and tools used for the project

* Terraform
* AWS Cloud9
* Docker Images      
* InfluxDB         
* Grafana          
* Node-red           

![Architecture](photos/weatherappArchitecture.jpeg?raw=true "Architecture")

  
This is the container architecture and the different layers of abstraction for analytics.

# Analytics in IoT using Lambda architecture
Lambda architecture is a data-processing architecture designed to handle massive quantities of data by taking advantage of both batch and stream-processing methods. This approach to architecture attempts to balance latency, throughput, and fault-tolerance. The two view outputs may be joined before the presentation. 
The rise of lambda architecture is correlated with the growth of big data, real-time analytics, and the drive to mitigate the latencies of map-reduce. All of the IoT platforms use this approach to provide comprehensive and accurate views of batch data, while simultaneously using real-time stream processing.


![image](https://user-images.githubusercontent.com/27162948/59328285-49cf3e80-8cec-11e9-979e-c1ff905a8de9.png)


### Differences in the two paths

* “hot” path where latency-sensitive data (e.g., the results need to be ready in seconds or less) flows for rapid consumption by analytics clients.
* “cold” path where all data goes and is processed in batches that can tolerate greater latencies (e.g., the results can take minutes or even hours) until results are ready.

## Quick Start 

To start the container the first time launch:

```sh
docker run --ulimit nofile=66000:66000 \
  -d \
  --name docker-cronograf-influxdb-grafana-node-red \
  -p 3003:3003 \
  -p 3004:8888 \
  -p 8086:8086 \
  -p 8125:8125/udp \
  -p 1880:1880 \
  25987908/hotpathanalytic-it-informatik:v2
```

To stop the container launch:

```sh
docker stop docker-cronograf-influxdb-grafana-node-red
```

To start the container again launch:

```sh
docker start docker-cronograf-influxdb-grafana-node-red
```

## Mapped Ports

```
Host    Container   Service

3003    3003      grafana
3004    8888      influxdb-admin (chronograf)
8086    8086      influxdb
8125    8125      statsd
1880    1880      Node-red
```

## Grafana

Open <http://localhost:3003>

```
Username: root
Password: root
```

### Add the DB on Grafana

1. Using the wizard click on `Add data source`
2. Choose a `name` for the source and flag it as `Default`
3. Choose `InfluxDB` as `type`
4. Choose `direct` as `access`
5. Fill remaining fields as follows and click on `Add` without user and password

```
Url: http://localhost:8086
Database: telegraf
User: telegraf
Password: telegraf
```

Basic auth and credentials must be left unflagged. Proxy is not required.

Now you are ready to add your first dashboard and launch some query on database. Out of the box the container provide a dashboard with information of the resources consume by the container in the host machine.

## InfluxDB

### Web Interface for administration

Open <http://localhost:3004>

```
1 - Get started
2 - Add a connection, use by default "telegraf" no pass no user
3 - Add a "System" dashboard, press "Create 1 dashboard"
4 - Kapacitor, this step skip it.
5 - Done, go to view all connections
```
Only use in case of administration of the databases. Is not use in a normal operation, every new message sent to the DB with a new topic creates automatically a new database with new measurements. In the dashboard tap of grafana main menu should be already a dashboard showing status of the host system. 

### InfluxDB Shell (CLI)

1. Attach to docker container, run shell `/bin/bash`
2. Launch `influx` to open InfluxDB Shell (CLI)

## Node-red

Open <http://localhost:1880>

``` 
No username or password 
```
You can create a user and assing privileges.
