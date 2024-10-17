IMAGE=nginx
TAG_DEV=dev
TAG_PROD=prod
NGINX_VERSION=1.27.2-alpine
#PORT_DEV=8081:80 -p ${PORT_DEV} 
#PORT_PROD=8082:80 -p ${PORT_PROD} 
NGX_CONF=$(PWD)/nginx
NETWORK=internal


net:
	@docker network create --driver bridge ${NETWORK}

build-dev:
	@docker build --target ${TAG_DEV} -t ${IMAGE}:${TAG_DEV} .

build-prod:
	@docker build --target ${TAG_PROD} -t ${IMAGE}:${TAG_PROD} .

run-dev: build-dev
	@docker run -d --network ${NETWORK} --network-alias ${IMAGE}-${TAG_DEV} --name ${IMAGE}-${TAG_DEV} ${IMAGE}:${TAG_DEV}
	@echo ${TAG_DEV} started

run-prod: build-prod
	@docker run -d --network ${NETWORK} --network-alias ${IMAGE}-${TAG_PROD} --name ${IMAGE}-${TAG_PROD} ${IMAGE}:${TAG_PROD}
	@echo ${TAG_PROD} started

nginx-proxy:
	@docker run -d --name proxy --mount type=bind,source=.\nginx\nginx.conf,target=/etc/nginx/nginx.conf --network ${NETWORK} -p 8080:80 nginx:1.27.2
	@echo proxy started

stop:
	@docker container rm -f ${IMAGE}-${TAG_DEV} ${IMAGE}-${TAG_PROD} proxy
	@echo everything removed

stop-dev: 
	@docker container rm -f ${IMAGE}-${TAG_DEV}
	@echo ${TAG_DEV} container removed

stop-prod:
	@docker container rm -f ${IMAGE}-${TAG_PROD}
	@echo ${TAG_PROD} container removed

prune:
	@docker image prune

prune-extreme:
	@docker image prune -f -a