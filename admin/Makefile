NAME=admin
IMAGE=$(USER)/$(NAME)
CONFIG=$(CONTAINER_CONFIG_ROOT)/$(NAME)

all: build

build: 
	sudo docker build --rm -t $(IMAGE) .

create:
	sudo docker run -i -t --privileged=true --restart=always --name $(NAME) -d -h $(NAME) -v /var/run/docker.sock:/run/docker.sock -v $(CONFIG):/config -p 80:80 $(IMAGE):latest /bin/bash

clean:
	sudo docker rm $(NAME)
	sudo docker rmi $(IMAGE)
