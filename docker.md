```
 docker exec -i mariadb mysql -uroot --password=***** frontend < frontend.sql
 docker system prune -a --volumes, docker network prune,
```

```
docker system prune
```

```
docker run --name local-redis -d redis
docker exec -it local-redis redis-cli
```
