# GitLab with HTTPS on Docker
This repository contains custom Docker files for GitLab CE. Everything is setup to run on HTTPS using a self-signed certificate (this needs to be created) and includes commonly used features specified as environment variables in the included Docker Compose file.

## Tools requirement
- Git
- OpenSSH client and SSH Keys for passwordless authentication between ansible host and servers
- Docker engine

## Usage
### Step 1: Clone the repo
```sh
git clone https://github.com/m-adnan8080/gitlab-docker.git
cd gitlab-docker
```
## Step 2: Create a self-signed certificate
To create a silf-signed certificate use below command
```sh
openssl req -newkey rsa:4096 -x509 -sha256 -days 3650 -nodes -out server-cert.pem -keyout server-key.pem -subj "/C=PK/ST=ISB/L=ISB/O=Home-DC/OU=IT Department/CN=gitlab.example.com"
```
## Step 3: Run gitlab in docker container
```sh
docker-compose up -d
```
This command will start gitlab in docker container and expose port 8443 (HTTPS for browser access)
