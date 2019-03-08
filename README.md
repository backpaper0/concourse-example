# concourse-example

## Run

Run all containers by `docker-compose`.

```
docker-compose up -d
```

Concourse is running at http://localhost:8080 .

|username|password|
|---|---|
|example|password|

Storage is running at http://localhost:9000 .

|username|password|
|---|---|
|example|password|

Nginx is running at http://localhost:8000 .

## Clean

First of all, shutdown all containers.

```
docker-compose down
```

And clear volumes.

```
docker volume rm $(docker volume ls|grep concourse-example|cut -c 6-)
```

