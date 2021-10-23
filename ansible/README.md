# Ansible deployment

## Setup

Install Python 3 virtual environment and Ansible

```shell
cd ansible
make clean
make setup
```

## Provision a local Vagrant box

```shell
make vagrant-provision
```

This may take a while to download the Ubuntu 20.04 Vagrant image.

To check if the vagrant box is up and running:

```shell
sudo vagrant status
```

## Configure the server

Now we run an Ansible playbook (`playbook-setup.yml`) that will:

* Install base packages
* Create a user plone
* Configure nginx webserver to listen on port 80 (`files/nginx/default`)
* Copy the docker-compose.yml configuration to the server

First, you need to edit the file `playbook-setup.yml` and replace the line:
```
      - "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDJIwjHxRAM1a8zc1kuTJ0GyzvloaBTz/fO7bGoNOlxY2lnUDop+q3CbHF28IkmVQCk28I+MXCnUXG6ARZgnBcb4LDey9WPVsiy3NRCXOmaZK6NKmKUejdA5Y4ZTHbs6rdIInDLWaFxzoxg5p/LaXUaTrKra2SpGc3kv7xKiZKXyTznFjFSv/u6Wm/vvZopWM6m4k8Z00fTUtxQO0eWKArStF99YFszUDU2w2jhL7n8irLow0UqjNjp0MvkPiic2SueoylQRIlD57XzveMBpGynYdsZWKDa3Czzo5ykHPLYrOByioKKjnpwgruXnXkkN4ov8sK+LqqAXaicxed6ohbOh68IWVB8nssb+RbISmzzpIXUwd1qkAyeiSjt5b9MFcIT56zeRb5B+aWZbYffc+pKy8kAjrYHCWEFl6O3N+M/bI9jgtXcZ9L6FSBN5vWjgRQPn7UwiMXIUssm0lU5AgCxs7q7S0xACj0xVFk5NeUM9vcCzXkY9vAjJmE1hzBWeOVhhQqLKmkbi/scr5hW2rrNwnuPBpyHUu2wTIyGHbnZ9CCwU3u21XDyvvO9ufxDjIH3v2EwEPqpbejKRM8QUH6YuH2goy89yQQijsC0YUE8AlJpbs9ctxSyzsJ6Z3ZwHJA681Ei15omhab2iwmT4KcS+3mC5pSCsFQgA4OsJKy5OQ== ericof@gmail.com"
```
With your ssh public key (probably available in `~/.ssh/id_rsa.pub`)

Then we run the playbook:

```shell
make playbook-setup
```

You can test if the `plone` user setup is correct:

```shell
ssh plone@127.0.0.1 -p 2222
```

## Create a new Docker context

```shell
docker context create vagrant --description "Plone Deployment training" --docker "host=ssh://plone@127.0.0.1:2222"
```

## Pull Docker images

```shell
make compose-pull
```

## Start all services

```shell
make compose-up
```
