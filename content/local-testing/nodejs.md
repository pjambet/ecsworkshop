---
title: "Node.js Backend API"
hidden: false
weight: 3
---

## Generate local docker compose file

```
cd ~/environment/ecsdemo-nodejs/
```
```
ecs-cli local create --task-def-remote $(aws ecs list-task-definitions | jq -r '.taskDefinitionArns[] | select(contains ("ecsdemo-nodejs"))')
```

## Modify the port in the generated file to avoid collision when testing with backend services running

```
sed -i 's/published: 3000/published: 4000/g' docker-compose.ecs-local.yml
```

## To follow our service discovery namespace for consistency, let's change the name of the service to use the service domain as we do in ecs

```
sed -i 's/ecsdemo-nodejs:/ecsdemo-nodejs.service:/g' docker-compose.ecs-local.*
```

## Run the service locally

```
ecs-cli local up
```

## Confirm container is running locally

```
ecs-cli local ps --all
```

## You should see your container running on the expected port. Now go ahead and give it a curl!

```
curl localhost:4000
curl localhost:4000/health
```

