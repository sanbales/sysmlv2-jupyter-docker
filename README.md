# Docker image for running SysML v2

Create a docker image for running [SysML v2 Release](https://github.com/Systems-Modeling/SysML-v2-Release) in Jupyter.

The setup is taken from the [Jupyter installation](https://github.com/Systems-Modeling/SysML-v2-Release/tree/master/install/jupyter).

In addition, an [API Server](https://github.com/Systems-Modeling/SysML-v2-API-Services) is also started and everything published in Jupyter will be pushed into this server.

## Remote Services

You can try this out on Binder, via DockerHub or just view the notebooks at nbviewer.

### Binder

You can run this on [Binder](https://mybinder.org) but it will only run the SysMLv2-based Jupyter server, not the API server.

Latest version: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/gorenje/sysmlv2-jupyter-docker/HEAD)

See below for specific release links.

You can also view notebooks via [nbviewer](https://nbviewer.jupyter.org/github/gorenje/sysmlv2-jupyter-docker/tree/master/notebooks) and from there it's possible to start up [Binder](https://mybinder.org).

### Dockerhub

Docker images are also [available](https://hub.docker.com/r/gorenje/sysmlv2-jupyter). These are only of the Jupyter installation not the API server.

See below for specific pull statements.

### nbviewer

Repo can also be viewed using [nbviewer](https://nbviewer.jupyter.org/github/gorenje/sysmlv2-jupyter-docker/tree/main/).

See below for specific release links.

### Dedicated Server

Thanks to [Tim Weilkiens](https://github.com/Weilkiti), there is now a dedicated [server](https://www.sysmlv2lab.com/) running the [latest](https://hub.docker.com/r/gorenje/sysmlv2-jupyter/tags?ordering=last_updated&page=1&name=latest) version of this repo.

### Overview

| [nbviewer](https://nbviewer.jupyter.org/github/gorenje/sysmlv2-jupyter-docker/tree/main/) | [binder](https://mybinder.org/v2/gh/gorenje/sysmlv2-jupyter-docker/HEAD) | [docker hub](https://hub.docker.com/r/gorenje/sysmlv2-jupyter) |
|:--|:--|:--|
| [2020-11](https://nbviewer.jupyter.org/github/gorenje/sysmlv2-jupyter-docker/tree/release-2020-11/)  | [2020-11](https://mybinder.org/v2/gh/gorenje/sysmlv2-jupyter-docker/release-2020-11) |  `docker pull gorenje/sysmlv2-jupyter:2020-11` |
| [2020-10](https://nbviewer.jupyter.org/github/gorenje/sysmlv2-jupyter-docker/tree/release-2020-10/) |  [2020-10](https://mybinder.org/v2/gh/gorenje/sysmlv2-jupyter-docker/release-2020-10) | `docker pull gorenje/sysmlv2-jupyter:2020-10` |

## Local Usage

Be aware, building the docker images will take a while since all the software
packages will be retrieved. Everything is built and run locally.

### Prerequistes

- [Docker](https://www.docker.com/)

Everything else is installed by the build process.

### Makefile

To start up the SysML-Jupyter server, the postgres server and the API server:

    make spin-up

Then point your browser first to ```http://localhost:9000/docs/``` - this will setup
the database for the API server. Once this displays a page, then point your
browswer to the Jupyter page. This is on ```http://localhost:8888```,
don't use the hostname ```sysmljupyter```, that's internal to docker.

```
    To access the notebook, open this file in a browser:
        file:///root/.local/share/jupyter/runtime/nbserver-1-open.html
    Or copy and paste one of these URLs:
        http://sysmljupyter:8888/?token=392e5b7c0e8cde28d6f988862bc7ad81ba6c517e31b63520
     or http://127.0.0.1:8888/?token=392e5b7c0e8cde28d6f988862bc7ad81ba6c517e31b63520
```

The token is unique for each start of the container.

NOTE: If `localhost` does not work in the URLs, try `127.0.0.1` instead.

### Using Docker

If you want to do this using docker only, i.e. no makefile, then have a
look at the Makefile. Basically it's something along the lines of:

    docker build -t sysml.jupyter -f Dockerfile.jupyter .
    docker build -t sysml.api     -f Dockerfile.api     .
    docker network create thenetwork
    docker volume create postgresdbserver
    docker-compose -f docker-compose.yml up

That is the same as doing ```make spin-up```.

### Other Docker Builds

The Makefile also does the following builds for local usage:

1. `make build-mybinder` will build the docker image that is used with mybinder. This image can then be run locally using `make run-mybinder`.

2. `make build-hub` will build the docker hub image. Running this image can be done with `make run-hub`.

These also work for each release that is supported by this repo.

### Checking out other releases

Each release has it's own branch, so for example to test the [SysML v2 Release 2020-11](https://github.com/Systems-Modeling/SysML-v2-Release/releases/tag/2020-11), do the following:

```
git checkout release-2020-11
make run-hub
```

That will locally start DockerHub Jupyter image with the 2020-11 release.

## Production Use?

Don't.

This isn't designed for production use, this is for local or trusted use only.

## Example Notebooks

There are a few example notebooks included in the image, their usefulness
might vary according to your experience level.

## Inspiration

- [MBSE4U.com](https://mbse4u.com/2020/12/21/sysml-v2-release-whats-inside/) is where I found the meta commands.
- Also from MBSE4U.com, the example [notebook](https://nbviewer.jupyter.org/github/MBSE4U/SysMLv2JupyterBook/blob/master/SysMLv2JupyterBook.ipynb) at [nbviewer.jupyter.org](https://nbviewer.jupyter.org).


## Licensing

Both [SysMLv2 API Server](https://github.com/Systems-Modeling/SysML-v2-API-Services/blob/master/LICENSE) and [SysMLv2 Release](https://github.com/Systems-Modeling/SysML-v2-Release/blob/master/LICENSE) are licensed under the LGPL and this continues to be the case.

**This project does not make any changes to the existing licensing of the
referenced projects.**

This project is also licensed under the [LGPL](/LICENSE).
