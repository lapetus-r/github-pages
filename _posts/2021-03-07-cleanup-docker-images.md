이따금 docker 의 모든 컨테이너 및 이미지를 삭제하고 싶을 때가 있다. 아래 커맨드를 수행하자.
```bash
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -q)
```

{% lapetus-r/585bb4e5a47e8be4b4af7cc57e621975 }
