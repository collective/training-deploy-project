# Plone Deployment Training Example Repo

## Initial Setup

* Fork this repo into your Github account
* `git clone git@github.com:MYUSER/training-deploy-project.git`
* Open in your favorite text editor. ie: `cd training-deploy-project && code ./`
* Find all occurences of **DOCKER_HUB_USER_CHANGE_ME** and replace it with your Docker Hub user name

## Setup backend

Create a Python virtual environment, install Plone 6.0.0a1 and one addon.

```shell
cd backend
make setup
```

Run the Plone Backend instance
```shell
make start
```

In a browser, go to [http://localhost:8080/@@plone-addsite?site_id=Plone&advanced=1](http://localhost:8080/@@plone-addsite?site_id=Plone&advanced=1 and create a new site:

![Plone site creation](./docs/plone-setup.png "Plone site creation")

Stop the process

## Setup a new frontend project

On the root of this project

```shell
npm init yo @plone/volto
```

Answer the questions:
```
Project name (e.g. my-volto-project) frontend
Would you like to add addons? True
Addon name, plus extra loaders, like: volto-addon:loadExtra,loadAnotherExtra volto-slate:asDefault
Would you like to add another addon? false
```

Edit ```frontend/package.json``` and change ```"@plone/volto": "13.15.1",``` to ```"@plone/volto": "14.0.0-alpha.23",```

And run ```cd frontend && yarn```

Start it with

```yarn start```

## Running everything with docker

```shell
make start-images
```
