### Usando Dockerfile

Além do Source to Image, o Openshift permite realiza o build de `Dockerfile` para você. Basta adicionar o seu `Dockerfile`em um repositório git e informar ao Openshift que iremos utilizar a estratégia de build do tipo docker. Para esse exemplo, iremos **utilizar o mesmo repositório criado no lab anterior **conforme exemplo abaixo**:**

```
https://github.com/<seu-usuario>/workshop-ocp.git
```

#### Criando nosso Dockerfile

Vamos criar um Dockerfile com base na [imagem oficial do PHP para Openshift](https://access.redhat.com/containers/#/registry.access.redhat.com/rhscl/php-70-rhel7). É importante salientar que, existem boas práticas na construção de [imagens Docker](https://docs.openshift.com/container-platform/3.7/creating_images/guidelines.html#general-container-image-guidelines) e também em[ imagens para o Openshift](https://docs.openshift.com/container-platform/3.7/creating_images/guidelines.html#openshift-specific-guidelines).

Abaixo segue o conteúdo do arquivo:

```dockerfile
FROM registry.access.redhat.com/rhscl/php-70-rhel7

RUN echo "<h1>Meu Dockerfile</h1>" > /opt/app-root/src/index.php

CMD ["container-entrypoint", "/usr/libexec/s2i/run"]
```

![](/assets/Selection_240.png)

O conteúdo do arquivo fica assim:

![](/assets/Selection_249.png)E commita ele

![](/assets/Selection_242.png)

Nosso repositório agora tem um novo arquivo:

![](/assets/Selection_250.png)

Também podemos salvar esse arquivo com nome de **Dockerfile** na raiz do nosso git executando:

```bash
git add Dockerfile
git commit -m "Dockerfile adicionado"
git push
```

#### Executando o Dockerfile com Openshift

Para criar uma aplicação com base no Dockerfile, precisamos executar o seguinte comando:

```bash
oc new-app \
 --name=dockerfile-app \
 --strategy=docker \
 https://github.com/<seu-usuario>/workshop-ocp.git \
 -n <nome do seu projeto do openshift>
```

Para saber o nome do seu projeto no Openshift, basta executar:

```
oc get projects
```

O valor default para o parametro **strategy** é **source. **Isso indica que, por padrão, o Openshift irá analisar o repositório git tentando compilar o código fonte da aplicação e usar o source-to-image. No nosso caso, queremos que ele use somente o Dockerfile e ignore o código fonte. Por isso informamos o parametro **--strategy=docker**

Assim que executamos o comando, o Openshift inicia o novo build.

![](/assets/Selection_044.png)Na versão 3.7 do Openshift, o build é mostrado conforme imagem abaixo:

![](/assets/Selection_251.png)

A diferença desse build para o source-to-image executando anteriormente, é que nesse caso o Openshift está construindo nossa imagem Docker usando Dockerfile. Se acessarmos o log do build, podemos ver ae execução do nosso código.

![](/assets/Selection_046.png)Para finalizar, crie uma rota no Openshift para podermos acessar nossa aplicação:

```
oc expose svc dockerfile-app -n <nome do seu projeto>
```

#### Limpando nosso lab

Vamos apagar nossa aplicação criada com base no Dockerfile. Dessa forma, deixaremos nosso Openshift limpo, organizado e pronto para o próximo lab.

```
oc delete all -l app=dockerfile-app -n <nome do seu projeto do openshift>
```



