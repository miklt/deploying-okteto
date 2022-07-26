---
description: Como pré-requisito é preciso ter uma conta no https://okteto.com/
---

# Criação arquivo okteto-pipeline.yml

A plataforma Okteto consegue carregar um arquivo docker-compose.yml e criar um ambiente de execução para o conteiner. Para isso, é preciso configurar o repositório para que, quando façamos a integração, a implantação seja automática.

{% code title="okteto-pipeline.yml" %}
```
deploy:  
  - okteto build -t okteto.dev/backend:${OKTETO_GIT_COMMIT} backend
  - okteto stack deploy -f backend/docker-compose.yml --wait
  
devs:  
  - backend/docker-compose.yml
```
{% endcode %}

Ao colocar  o arquivo oketo-pipeline.yml na raiz do repositório, a plataforma ira:

* construir a imagem&#x20;
* implantar os serviços definidos em docker-compose.yml

Preste atenção que no repositório de exemplo, ambos arquivos estão na pasta 'backend'

Uma vez colocado o arquivo no repositório, vamos a seguir o seguinte passo a passo:

1. Logar na plataforma Okteto.
2. Clicar em Deploy
3. ![](.gitbook/assets/image.png)
4. Escolher Git e configurar a importação do repositório github
5. ![](<.gitbook/assets/image (8).png>)
6. Aparecerá outra tela para autorização do github. Clique em Configurar.
7. ![](<.gitbook/assets/image (3).png>)
8. Na nova tela, digite suas credenciais de acesso para o github
9. Depois, aparecerá uma tela do github e, embaixo, uma lista dos seus repositórios. Escolha o repositório que será importado. Em nosso caso é 'cautious-system'. Clique em Salvar.
10. ![](<.gitbook/assets/image (1).png>)
11. Uma vez configurado, ele aparecerá na tela de seleção de repositórios. Selecione o repositório e clique em Deploy:
12. ![](<.gitbook/assets/image (5).png>)
13. ![](<.gitbook/assets/image (7).png>)
14. Na interface do okteto, aparecerá o estado da implantação
15. ![](<.gitbook/assets/image (4).png>)
16. Eventualmente, se tudo der certo, o estado será o seguinte:
17. ![](<.gitbook/assets/image (6).png>)

Na interface aparecerá o link onde o endpoint será visível: [https://backend-miklt.cloud.okteto.net/](https://backend-miklt.cloud.okteto.net/). Perceba que o okteto apresenta o link como https , ou seja ele roda na porta 443, mesmo que nosso serviço rode internamente na porta 5000. Esse é o funcionamento padrão.
