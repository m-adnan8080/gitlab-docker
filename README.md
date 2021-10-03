# GitLab with HTTPS on Docker
This repository contains custom Docker files for GitLab CE. Everything is setup to run on HTTPS using a self-signed certificate (this needs to be created) and includes commonly used features specified as environment variables in the included Docker Compose file.

## Tools requirement
- Git
- OpenSSL to generate self-signed certificate
- Docker engine to run docker containers
- Docker-compose to start gitlab docker container with custom settings

## Usage
### Step 1: Clone the repo
```sh
git clone https://github.com/m-adnan8080/gitlab-docker.git
cd gitlab-docker
```
### Step 2: Create a self-signed certificate
To create a silf-signed certificate use below command. Create volume_data directory in current folder and copy generated pem file to it. Also change permission to 400 (readonly)
```sh
openssl req -newkey rsa:4096 -x509 -sha256 -days 3650 -nodes -out server-cert.pem -keyout server-key.pem -subj "/C=PK/ST=ISB/L=ISB/O=Home-DC/OU=IT Department/CN=gitlab.example.com"

mkdir -p volume_data/ssl
cp *.pem volume_data/ssl
chmod 400 volume_data/ssl
```
### Step 3: Run gitlab in docker container
```sh
docker-compose up -d
```
This command will start gitlab in docker container and expose port 8443 (HTTPS for browser access)

### Local DNS resolution
As in openssl and docker-compose.yml file gitlab.example.com is configured as FQDN, for local dns resolution and below line to `/etc/hosts` file.
```sh
cat '127.0.2.1 gitlab.example.com' | sudo tee -a /etc/hosts
```
After adding this line then visit below URL to access gitlab [https://gitlab.example.com](https://gitlab.example.com)
