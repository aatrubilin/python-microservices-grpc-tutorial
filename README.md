# python-microservices-grpc-tutorial
https://realpython.com/python-microservices-grpc/


## Generate protobufs

```shell
cd recommendations
python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto
```

```shell
cd marketplace
python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto
```

## Run flask app

```shell
set FLASK_APP=marketplace.py flask run
```

## Run in docker

### Build images

```shell
docker build . -f recommendations/Dockerfile -t recommendations
docker build . -f marketplace/Dockerfile -t marketplace
```

### Create network

```shell
docker network create microservices
```

### Run containers

```shell
docker run -p 127.0.0.1:50051:50051/tcp --network microservices --name recommendations recommendations
```

```shell
docker run -p 127.0.0.1:5000:5000/tcp --network microservices -e RECOMMENDATIONS_HOST=recommendations marketplace
```
