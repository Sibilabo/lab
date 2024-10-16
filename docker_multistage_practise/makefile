
IMAGE=nginx
TAG-DEV=dev
TAG-PRDO=prod
PORT-DEV=8081
PORT-PROD=8082

build-dev:
	@docker build --build-arg STAGE=dev -t ${IMAGE}:${TAG-DEV} .

build-prod:
	@docker build --build-arg STAGE=prod -t ${IMAGE}:${TAG-PRDO} .

run-dev: build-dev
	@docker run -d -p ${PORT-DEV}:80 --name ${IMAGE}-${TAG-DEV} ${IMAGE}:${TAG-DEV}
	@echo "DEV app is running at ${PORT-DEV} port"

run-prod: build-prod
	@docker run -d -p ${PORT-PROD}:80 --name ${IMAGE}-${TAG-PROD} ${IMAGE}:${TAG-PRDO}
	@echo "PROD app is running at ${PORT-PROD} port"

stop-dev: 
	@docker container rm -f ${IMAGE}-${TAG-DEV}
	@echo ${TAG-DEV} container removed

stop-prod:
	@docker container rm -f ${IMAGE}-${TAG-PROD}
	@echo ${TAG-PROD} container removed

prune:
	@docker image prune

prune-extreme:
	@docker image prune -f -a