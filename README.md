# Student Management API

This project is a simple Student Management API built using FastAPI. It allows for basic CRUD operations on student data. The API supports creating, reading, updating, and deleting student information.



## Features

- Create Student: Add a new student.
- Get All Students: Retrieve a list of all students.
- Get Student by ID: Retrieve a specific student by their ID.
- Update Student: Update a student's information.
- Delete Student: Delete a student by their ID.


## Requirments
- Python 3.11+
- PIP
- Docker & Docker Compose
- Make
- Vagrant
- Oracle virual Box
- 8gb Memory Space

## Installation
1) Clone the repository:

```bash
  git clone https://github.com/venk404/Deploy-to-Bare-metal.git
```

2) Change the Directory to Restapi Directory

```bash
  cd Deploy-to-Bare-metal
```

3) For Setting up a Vagrant box with all necessary dependencies pre-installed.

```bash
  make Spin-vm
```

4) ## "Rename the .env file from the Schema folder and also in the root directory"

5) ## "SSH into the Vagrant box after setting it up"

6) Navigate to the Restapi directory within the vagrant folder in root folder.
```bash
  cd ..
  cd ..
  cd vagrant/Restapi
```

7) Navigate to the respective directory and run all services using Docker Compose(Inside vagrant box).

```bash
  make all
```
8) ## You can access the application from outside the Vagrant box.

```bash
  http://127.0.0.1:8080/docs
```


## Documentation(API Documentation)

- Refer to the API documentation for the endpoints listed below
```bash
  http://127.0.0.1:8080/docs
```