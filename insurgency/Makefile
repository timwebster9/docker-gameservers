.DEFAULT=build

build:
	docker build -t mars:5000/timw/insurgency-server .

push:
	docker push mars:5000/timw/insurgency-server

all: build push

up:
	docker-compose up -d && docker-compose logs -f

down:
	docker-compose down