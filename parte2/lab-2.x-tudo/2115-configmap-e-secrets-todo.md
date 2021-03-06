### ConfigMap e Secrets

ConfigMap e Secrets são recursos disponíveis no Openshift que permitem que configurações sensíveis e informações de ambiente possam ser externalizadas em relação ao container.

Exemplo de secrets e configmaps:

* Arquivo de properties da aplicação
* Configurações de usuário e senha do banco de dados
* Certificados
* Etc

A grande diferença entre um ConfigMap e uma Secret é que o segundo é obsfucado e focado em guardar informações sensíveis ao passo que o primeiro não. A obsfucação do Secret é feita usando Base64.

#### Criando nosso primeiro ConfigMap

Vamos criar um arquivo de properties contendo algumas informações importantes para nossa aplicação.

`config.properties`

```
ambiente=dev
debug=false
```

Para criar um ConfigMap baseado nesse arquivo, executamos:

```
oc create configmap config --from-file=config.properties
```

Podemos ver o conteúdo do nosso configmap executando:

```
oc describe configmap config
```

#### ![](/assets/configmap.gif)

#### Usando nosso configmap

```bash
oc volumes dc/workshop-ocp \
 --add --mount-path=/tmp/config \
 --configmap-name=config \
 --type=configmap
```

Se acessarmos o container, veremos que na pasta `/tmp/config` existe o nosso arquivo properties.

![](/assets/volume-configmap.gif)

