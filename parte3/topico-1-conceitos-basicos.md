#### LAB01 - Desmistificando docker {#_lab01_desmistificando_docker}

Primeiro passo é entender como Docker funciona e seus principais componentes.

##### 1 - Instalação do Docker {#_1_instala_o_do_docker}

```
yum install docker 

systemctl start docker
```

|  | Instala docker |
| :--- | :--- |
|  | Sobe Docker |

##### 2 - Lista Imagens Docker {#_2_lista_imagens_docker}

```
docker images
```

|  | Lista as imagens locais do Docker |
| :--- | :--- |


##### Criando um Docker file {#_criando_um_docker_file}

```
mkdir helloworld
cd helloworld
echo "FROM php:7.0-apache" >> Dockerfile
```

|  | Fonte:[https://hub.docker.com/\_/php/](https://hub.docker.com/_/php/) |
| :--- | :--- |


##### Construindo Imagem {#_construindo_imagem}

```
docker build -t helloworld .
```

|  | Verifique as camadas da imagem. |
| :--- | :--- |


##### Listando as Imagens {#_listando_as_imagens}

```
docker images
```

##### Subindo o container {#_subindo_o_container}

```
docker run -d --name helloworld helloworld
docker ps
```

##### Entrando no Container {#_entrando_no_container}

```
docker exec -it <id container> /bin/bash
```

 

