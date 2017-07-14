# How to run docker
~~~~
docker pull dtenpf/minipf_build:0.1
docker run --name my_build  -v <path to share dir>:/root/share -i -t dtenpf/minipf_build:0.1
~~~~
# How to reconnect docker

~~~~
docker start my_build
docker exec -it my_build /bin/bash
~~~~
# How to remove docker 
~~~~
docker rm my_build
~~~~
