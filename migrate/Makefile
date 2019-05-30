_database='mysql://root:@tcp(127.0.0.1)/demodb' -path ./db

db-start:
	docker-compose -f db/docker-compose.yml up

migrate-up:
	migrate -database $(_database) up

migrate-down:
	migrate -database $(_database) down

migrate-version:
	migrate -database $(_database) version

migrate-force:
	migrate -database $(_database) force

migrate-create: # ex make migrate-create NAME=create_table_projects
	migrate create -ext sql -dir db ${NAME}

migrate-prepare-go:
	go get -u -d github.com/golang-migrate/migrate/cli
	migrate --version

migrate-prepare-release:
	curl -L https://github.com/golang-migrate/migrate/releases/download/v4.3.1/migrate.darwin-amd64.tar.gz | tar xvz
	mv migrate.darwin-amd64 /usr/local/bin/migrate
	migrate --version
