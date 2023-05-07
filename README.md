# Load balancing with Nginx

Simple example to show how to config Nginx load balancer.

## Description

Node JS, Nginx, Docker

## Getting Started

### Dependencies

* Docker

### Installing

1. Build Node application Docker image
```
 docker build -t node_js_backend:1.0 .
```
2. Verify Node JS image
```
 docker images
```
3. Run 3 container based same image
```
docker run -d -p 4001:4000 --name backend1 -e server=backend_1 node_js_backend:1.0
docker run -d -p 4002:4000 --name backend2 -e server=backend_2 node_js_backend:1.0
docker run -d -p 4003:4000 --name backend3 -e server=backend_3 node_js_backend:1.0
```
4. Verify backend containers
```
 docker ps
```
5. Edit Nginx configuration file: /gateway/nginx.conf.
You should inspect IP address of localhost after that you must write into the "nginx.conf" file. Just copy the first IP address.
```
hostname -I
```
6. Build Nginx image
```
docker build -t api_gateway:1.0 .
```
7. Verify Nginx image
```
 docker images
```
8. Run Nginx container
```
docker run -d -p 87:80 --name load_balancer api_gateway:1.0
```

### Executing program

* You can paste the following command to check how to work load balancing.
```
curl http://<your_ip_address>:87
```
* You can se which backend instance generated the response
```
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_1
This Request redirect to the server backend_2
This Request redirect to the server backend_3
This Request redirect to the server backend_1
...
```


## Author

Kenyeres Géza
https://hu.linkedin.com/in/g%C3%A9za-kenyeres-17341631

