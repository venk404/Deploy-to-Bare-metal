.ONESHELL:

# Variables
VENV := venv
DB_SERVICE := postgres
MIGRATION_DIR := ./DB/Schemas
MIGRATION_IMAGE := migrations_img
MIGRATION_CONTAINER := migrations_container
NETWORK_NAME := dem
API_IMAGE := restapi
API_CONTAINER := restapi
API_PORT := 8000

# Determine OS-specific command prefix
ifeq ($(OS),Windows_NT)
    CMD_PREFIX :=
else
    CMD_PREFIX := 
endif

all: Run_all_containers


Code_linting:
	python -m flake8 .

Run_all_containers:
	docker-compose up

Build_api:
	$(CMD_PREFIX) echo "API build successful"

Start_DB:
	$(CMD_PREFIX) docker-compose up $(DB_SERVICE)

run-migrations:
	$(CMD_PREFIX) docker build -t $(MIGRATION_IMAGE) $(MIGRATION_DIR)
	$(CMD_PREFIX) docker run --rm --name $(MIGRATION_CONTAINER) --network $(NETWORK_NAME) $(MIGRATION_IMAGE)

docker_build-api:
	$(CMD_PREFIX) docker build -t $(API_IMAGE) .

docker_run-api:
	$(CMD_PREFIX) docker run -d \
		--name $(API_CONTAINER) \
		--network $(NETWORK_NAME) \
		-p $(API_PORT):$(API_PORT) \
		$(API_IMAGE)


install: $(VENV)/Scripts/activate

$(VENV)/Scripts/activate: requirements.txt
	python -m venv $(VENV)

ifeq ($(OS),Windows_NT)
	$(VENV)\Scripts\activate.ps1
	$(VENV)\Scripts\python -m pip install --upgrade pip
	$(VENV)\Scripts\pip install -r requirements.txt
else
	chmod +x $(VENV)/bin/activate
	$(VENV)/bin/activate
	$(VENV)/bin/python -m pip install --upgrade pip
	$(VENV)/bin/pip install -r requirements.txt
endif


# Define a clean step
clean:
ifeq ($(OS),Windows_NT)
	@powershell -Command "Get-ChildItem -Recurse -Directory -Filter '__pycache__' | Remove-Item -Recurse -Force"
	@powershell -Command "Get-ChildItem -Recurse -Directory -Filter 'data' | Remove-Item -Recurse -Force"
else
	find . -type d -name "__pycache__" -exec rm -rf {} +
	find . -type d -name "data" -exec rm -rf {} +
endif

test:
ifeq ($(OS),Windows_NT)
	python ./test/test.py
else
	python ./test/test.py
endif

.PHONY: all test clean Code_linting Run_all_containers Start_DB run-migrations Build-api docker_build-api docker_run-api