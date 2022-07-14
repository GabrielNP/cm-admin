SHELL=/bin/bash

setup: requirements.txt
	test -d .venv || python3 -m venv .venv
	. .venv/bin/activate; pip install -U pip; pip install -r requirements.txt

include .env
export
run: .venv
	. .venv/bin/activate; FLASK_APP=app FLASK_ENV=development flask run

add_dep: .venv
	. .venv/bin/activate; pip install $(dep) && pip freeze | grep -v "pkg-resources" > requirements.txt

rm_dep: .venv
	. .venv/bin/activate; pip uninstall -y $(dep) && pip freeze | grep -v "pkg-resources" > requirements.txt


include .env
export
makemigration:
	migrate command=create --driver=pgsql --migration=$(migration)

include .env
export
migrate:
	migrate execute --driver=pgsql

generate_rsa:
	openssl genrsa -out private.pem 4096
	openssl rsa -in private.pem -outform PEM -pubout -out public.pem
