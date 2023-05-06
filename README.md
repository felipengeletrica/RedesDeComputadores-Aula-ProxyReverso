














# Projeto PROXY reverso  (Exercicio troca de subdominio)

## 1° Passo:

Abrir o docker-compose.yaml como ediçao de texto e alterar dentro da tag "LABEL" os subdominios onde fazem referência ao HOST:


![Testando o Apache](doc/dockercompose_subdominios.png) 

 ***

 ## 2° Passo:
 Abrir o terminal e inserir o comando para iniciar os serviços:

 > $ docker-compose up --build

 Caso necessite ou queira parar o serviço:

> $ docker-compose stop

 Caso necessite ou queira remover o serviço:
> $ docker-compose rm
***

 ## 3° Passo:

Utilize o navegador web e digite as seguintes urlscom os subdominios que foram alterados:

> http://ricardolangbecker_apache1.localhost

![Verificando o Apache](doc/subdominio_ricado.png) 



 > http://ricardolangbecker_grafana.localhost


 ![Verificando o Grafana](doc/grafana.png) 


  > http://ricardolangbecker_dashboard.localhost



 ![Verificando o DocuWiki](doc/DocuWiki.png) 



  > http://ricardolangbecker_dashboard.localhost



 ![Verificando o Traefik](doc/traefik.png) 



### E verificando dentro do Routers do Traefikk, podemos ver nosso subdominio:


 ![Verificando o Traefik](doc/dashboard_traefik2.png) 
