# how to push docker image.

~~~~
docker login
docker build -t dtenpf/minipf_build --no-cache=true --build-arg http_proxy="xxxx" --build-arg https_proxy="xxxx" . 
docker tag <imageid> dtenpf/minipf_build:0.1
docker push denpf/minipf_build:0.1
~~~~

