
type of docker images : 

- python 
FROM ${REPO_LOCATION}amazon/aws-sam-cli-build-image-python3.7:${BASE_VERSION}

- haproxy-alpine 
FROM ${REPO_LOCATION}haproxytech/haproxy-alpine:${BASE_VERSION}

- aws-cli + python 
FROM ${REPO_LOCATION}amazon/aws-cli:latest as installer
FROM ${REPO_LOCATION}python:3.10

- nginx 

https://github.com/nginx/nginx-prometheus-exporter#running-the-exporter-in-a-docker-container
https://docs.nginx.com/nginx-ingress-controller/logging-and-monitoring/prometheus/
nginx-prometheus-exporter



- as-tomcat



- nodejs
FROM ${REPO_LOCATION}airbus/airbus-nodejs-22-ubi10:latest






https://instaclustr.medium.com/hosting-prometheus-on-amazon-elastic-container-service-ecs-to-monitor-metrics-for-your-8d9e82ac8f32

