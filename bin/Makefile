env:
	cp ../.env.example ../.env
build:
	docker-compose up -d --build
restart:
	docker-compose restart
start:
	docker-compose up -d
exec:
	docker exec -it $(service) bash
stop:
	docker-compose stop

