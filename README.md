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

# Written a blog post to explain project steps
For more details please use below link to implement and understand the project by yourself.

https://neerajsomani.medium.com/openweathermap-dashboard-using-terraform-project-f1b09ac2ede4


### Some useful terraform commands

```
terraform workspace new prod # if workspace not already created
terraform workspace select prod # if workspace already created and want to use it
terraform plan # test everything before deployment
terraform apply --auto-approve #to create and deploy resources
terraform destroy --auto-approve #to destroy resources once done
```

## Mapped Ports

```
Host    Container   Service

3000    3000      grafana
8086    8086      influxdb
1880    1880      Node-red
```
