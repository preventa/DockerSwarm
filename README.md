# DockerSwarm

## Paso 1 - Establecer arquitectura

* Si no se tiene, crear un Key/Pair en la consola de AWS, que se utilizará más adelante para acceder a las máquinas EC2.
* Ir a la página oficial de **Docker for AWS**: https://docs.docker.com/docker-for-aws/
* Elegir entre la versión Estable, Edge o Test de la Community Edition (CE). Tener en cuenta que hay dos tipos de plantilla: Con VPC existente o nueva VPC.
* Revisar la región sobre la que trabajaremos y donde tenemos permisos y la Key/Pair disponible.
* Lanzar la plantilla Cloud Formation, seleccionando los tipos y números de instancias, un Key/Pair existente y demás parámetros.

## Paso 2 - Instalar visualizador

* Desde la consola de AWS, identificar la máquina EC2 que sirve de Manager.
* Realizar conexión SSH al nodo manager, con la Key/Pair indicada en el paso anterior y con el usuario **Docker**
* Ejecutar el siguiente comando desde la conexión SSH:
```
$ docker service create \  
  --name=viz \  
  --publish=8080:8080/tcp \  
  --constraint=node.role==manager \  
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \  
  dockersamples/visualizer
```

Se podrá acceder al visualizador en la ruta: https://<FQDN_ELB>:8080, donde <FQDN_ELB> es el punto de entrada público del balanceador de carga, creado por Cloud Formation en el paso anterior.
