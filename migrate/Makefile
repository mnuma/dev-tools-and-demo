_mysql='mysql://root:@tcp(127.0.0.1)/demodb' -path ./mysql
_spanner='spanner://projects/$(PROJECT_ID)/instances/$(INSTANCE)/databases/mnuma' -path ./spanner

help:
	@echo "Make for migration."

migrate-prepare-go:
	go get -u -d github.com/golang-migrate/migrate/cli
	migrate --version

migrate-prepare-release:
	curl -L https://github.com/golang-migrate/migrate/releases/download/v4.3.1/migrate.darwin-amd64.tar.gz | tar xvz
	mv migrate.darwin-amd64 /usr/local/bin/migrate
	migrate --version

db-start:
	docker-compose -f docker-compose.yml up

migrate-up:
	migrate -database $(_mysql) up

migrate-down:
	migrate -database $(_mysql) down

migrate-version:
	migrate -database $(_mysql) version

migrate-force:
	migrate -database $(_mysql) force

migrate-create: # ex make migrate-create NAME=create_table_projects
	migrate create -ext sql -dir db ${NAME}

migrate-spanner-up:
	migrate -database $(_spanner) up

migrate-spanner-down:
	migrate -database $(_spanner) down

migrate-spanner-version:
	migrate -database $(_spanner) version

migrate-spanner-force:
	migrate -database $(_spanner) force

migrate-spanner-create: # ex make migrate-create NAME=create_table_projects
	migrate create -ext sql -dir spanner ${NAME}
