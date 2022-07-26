---
description: >-
  Para a implantação na nuvem do serviço de backend iremos usar tecnologias de
  containers e um ambiente de execução kubernetes por embaixo dos panos (okteto)
---

# Roteiro

O arquivo Dockerfile é um descritor de um ambiente de execução, esse ambiente pode ser chamado também de imagem ou imagem de um conteiner. Por exemplo, a imagem do ambiente de python está baseada numa imagem do sistema operacional debian.&#x20;

O gerenciador de conteiners (Docker) cria na memoria do computador um ambiente de execução fiel a partir da imagem do conteiner. Este ambiente, chamado de conteiner, é isolado e possui por exemplo, endereço de rede, alocação de processamento, de memória RAM e sockets de IO compartilhados com o sistema operacional hospedeiro.

Dentro desse ambiente, a sua aplicação será executada.

A plataforma Okteto fornece esse ambiente de execução na nuvem, de forma gratuita, mas com certas limitações de memória que não vão atrapalhar o desenvolvimento.&#x20;

No final da implantação, é esperado que sua aplicação esteja rodando na internet, com endpoints públicos e acessíveis a partir do frontend.

Para continuar o tutorial, usaremos o seguinte repositório:

[https://github.com/miklt/cautious-system](https://github.com/miklt/cautious-system)

