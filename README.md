# DockerSwarm

## Paso 1 - Establecer arquitectura

* Ir a la página oficial de **Docker for AWS**: https://docs.docker.com/docker-for-aws/
* Elegir entre la versión Estable, Edge o Test de la Community Edition (CE).
* Lanzar la plantilla Cloud Formation, seleccionando los tipos y números de instancias.

## Paso 2 - Instalar visualizador

```
$ docker service create \  
  --name=viz \  
  --publish=8080:8080/tcp \  
  --constraint=node.role==manager \  
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \  
  dockersamples/visualizer
```

Se podrá acceder al visualizador en la ruta: https://<FQDN_ELB>:8080, donde <FQDN_ELB> es el punto de entrada público del balanceador de carga, creado por CloudFormation en el paso anterior.
