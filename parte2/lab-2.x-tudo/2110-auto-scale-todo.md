### AutoScale

O Openshift suporta scale-out e scale-in da sua aplicação. Dessa forma, é possível que sejam criadas novas instâncias da sua aplicação sob demanda. Assim que o pico de acesso diminuir da sua aplicação, o Openshift realiza o scale-in e volta as instâncias para a quantidade inicial.

Vamos preparar nossa aplicação para o autoscale.

#### Preparando a aplicação

O Openshift suporte autoscale por CPU ou memória. Na console, temos somente a opção por CPU e portanto usaremos ela nessa etapa.

1. Selecione no menu vertical esquerdo a opção **Applications** -&gt; **Deployments**
2. Na tabela a seguir, clique em **workshop-ocp**
3. No menu lateral superior, clique em **Actions** -&gt; **Add Autoscaler**

![](/assets/autoscale.gif)

#### Estressando a aplicação

Para utilizar o nosso próximo comando, precisamos instalar uma nova ferramenta.

```
yum install httpd-tools -y
```

Vamos gerar uma carga agora na aplicação para ver como ela se comporta. Utilizaremo o [ab \(Apache Benchmark\)](https://httpd.apache.org/docs/2.4/programs/ab.html).

```bash
ab -n 10000 -c 50 <url da aplicação>
```

Para ver a url da sua aplicação, basta executar o comando abaixo ou copiar da Web Console

```
oc get route -n <nome do projeto>
```

O Autoscale pode demorar um pouco para acontecer. Openshift demora aproximadamente 1 minuto para coletar as métricas necessárias para tomar uma decisão de escalar a aplicação.

