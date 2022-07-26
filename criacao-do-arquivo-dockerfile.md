---
description: >-
  Como pre-requisito é necessário ter instalado e funcionando o Docker no seu
  computador.
---

# Criação do arquivo Dockerfile

O arquivo dockerfile é um descritor de uma imagem de um conteiner,  normalmente ele está baseado em outra imagem, que é pública, em cima da qual a gente executa comandos para deixar nossa imagem adequada para nossa aplicação.

Para nosso exemplo, vamos criar uma imagem que suporte python, flask e a nossa aplicação, que está na pasta backend.

O arquivo Dockerfile para uma aplicação Flask, usando pipenv como gerenciador de pacotes tem o seguinte formato:

{% code title="Dockerfile" %}
```
FROM python:3.9-slim as base

# Setup env
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1


FROM base AS python-deps

# Install pipenv and compilation dependencies
RUN pip install pipenv
RUN apt-get update && apt-get install -y --no-install-recommends gcc

# Install python dependencies in /.venv
COPY ./app/Pipfile .
COPY ./app/Pipfile.lock .
RUN PIPENV_VENV_IN_PROJECT=1 pipenv install --deploy


FROM base AS runtime

# Copy virtual env from python-deps stage
COPY --from=python-deps /.venv /.venv
ENV PATH="/.venv/bin:$PATH"

# Create and switch to a new user
RUN useradd --create-home appuser
WORKDIR /home/appuser
USER appuser

# Install application into container
COPY . .

# Run the application
ENTRYPOINT ["python", "-m", "app.monolito_flask"]
```
{% endcode %}

Neste exemplo,o arquivo está numa pasta acima da pasta com o código fonte python, isto ajuda na organização.&#x20;

Para construir a imagem a partir do arquivo Dockerfile, execute o seguinte comando:



```
docker build -t backend:latest .
```

Onde -t é a flag para nomear a sua imagem. O nome que dei para a imagem é 'backend' o ':' serve para adicionar uma versão na imagem, neste caso é 'latest'

Para executar o conteiner, é preciso usar seguinte comando:

```
docker run -p 5000:5000 backend:latest
```

As flag -p indica que a porta 5000 do conteiner escutará a porta 5000 do host.

Como referência, podem olhar estes tutoriais:

{% embed url="https://runnable.com/docker/python/dockerize-your-flask-application" %}

{% embed url="https://docs.docker.com/language/python/build-images#create-a-dockerfile-for-python" %}
