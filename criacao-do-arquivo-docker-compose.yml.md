# Criação do arquivo docker-compose.yml

O docker-compose simplifca a execução de conteiners. Também permite organizar as imagens como um conjunto de serviços. Por exemplo é possível definir uma imagem de banco de dados postgres e criar várias instancias do ambiente, colocando bancos diferentes. Ou definir um arquivo com frontend, backend e banco de dados.

O seguinte exemplo, mostra um arquivo docker-compose.yml para a aplicação de exemplo:

{% code title="docker-compose.yml" %}
```
version: '3.9'
services:
  backend:
    build:
      context: .
      dockerfile: Dockerfile
    image: backend
    ports:
      - '5000:5000'
```
{% endcode %}

Ele está localizado na mesma pasta que o arquivo Dockerfile e define o serviço 'backend', e indica que quando for executado, será construida a imagem a partir do proprio Dockerfile. Também dá o nome 'backend' para imagem e configura que a porta 5000 do conteiner escute a porta 5000 do host.

Para executar o arquivo o comando é o seguinte:

```
docker-compose up --build
```

Tendo esse arquivo funcionando, só falta configurar o repositório para que, quando integrarmos com a plataforma do okteto, ela reconheça que existe um serviço no repositório e que precisa ser implantado. Este arquivo é o okteto-pipeline.yml
