
# Container running without compose with Redis

`docker build -t course-app .`
`docker run --rm -p 8080:8080 course-app`

![](no-redis-logs.png)
![](no-redis-live.png)

# Compose + Redis

`docker compose up`

![](compose+redis-logs.png)
![](compose+redis-live.png)

