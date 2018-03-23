= docker

with vglrun and ensight:

```
docker build -t novnc:ensight -f Dockerfile-novnc-debian .
docker run --rm -it \
   -v /opt/CEI/license8:/opt/licenses \
   -v $HOME/feel:/home/feelpp/feel \
   -p 8080:8080 novnc:ensight
```

optional build args:
* PLATFORM=debian
* OS=buster
* GRAPHICS=nvidia

with vglrun:
```
docker build -t novnc:virtualgl -f Dockerfile-novnc .
docker run --rm -it -p 8080:8080 novnc:virtualgl
```

open a browser:
```
firefox http://<DOCKER_MACHINE_IP>:8080/vnc.html
```

typiquement localhost ca marche
reste a ajouter ssl... et salome ;)


= docker compose

First you need to build - see in docker/ensight:
```
docker build -t novnc:virtualgl -f Dockerfile-novnc .
docker build -t ensight:virtualgl -f ../ensight/Dockerfile-novnc .
```

```
docker-compose up -d
docker-compose logs -f
docker-compose stop
docker-compose down
```

= Other configurations

To use an alternative working dir `path` and a custom file name `file.yml`:

```
docker-compose up -p path -f file.yml -d 
```

Add these same options for all other operations.
For more options see: `docker-compose --help`

= Issues

Make sure to have `docker` installed and running.

On Debian/Ubuntu platform you can check:
```
sudo systemctl status docker.service
```
If the service is not running, simply restart it.
Otherwise you will need to install `docker`.

= further readings

* [docker](https://docs.docker.com/get-started/)
* [nonc on docker](https://github.com/psharkey/docker/tree/master/novnc)
* [salome on docker](https://github.com/feelpp/hifimagnet/blob/develop/docker/salome/Readme.md)

NB: not working with Alpine since missing packages