이따금 docker 의 모든 컨테이너 및 이미지를 삭제하고 싶을 때가 있는데, 아래 커맨드를 수행해 주자.
```bash
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -q)
```
