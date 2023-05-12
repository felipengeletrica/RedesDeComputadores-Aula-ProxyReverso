














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

***

### Resolução de vulnerabilidade


Foi identificado um impasse concernente ao proxy reverso, cuja fragilidade de segurança permitia a intrusão de terceiros não autorizados por meio do perímetro exterior. Nesse sentido, optamos pela adoção de uma medida de isolamento dos serviços em uma rede segregada e, por conseguinte, pela eliminação das portas expostas na máquina, com exceção das que se relacionavam com o traefik. Adicionalmente, procedemos com a eliminação das aplicações web nas tags de rede, com o intuito de superar o impasse identificado.

```yaml
 version: '3'
services:

  traefik:
      image: "traefik:v2.6.6"
      container_name: "traefik-network"
      command:
      - --entrypoints.web.address=:80
      - --entrypoints.websecure.address=:443
      - --providers.docker
      - --api
      - --log.level=DEBUG
      - --certificatesresolvers.letsencrypt.acme.email=felipeng.eletrica@gmail.com
      - --certificatesresolvers.letsencrypt.acme.storage=/acme.json
      - --certificatesresolvers.letsencrypt.acme.tlschallenge=true
      ports:
        - "80:80"
        - "443:443"
      networks:
        - internal
        - web

      volumes:
            - "/var/run/docker.sock:/var/run/docker.sock:ro"
            - "./acme.json:/acme.json"
      labels:
            # Dashboard
            - "traefik.http.routers.traefik.rule=Host(`dashboard.localhost`)"
            - "traefik.http.routers.traefik.service=api@internal"
            - "traefik.http.routers.traefik.tls.certresolver=letsencrypt"
            - "traefik.http.routers.traefik.entrypoints=websecure"
            - "traefik.http.routers.http-catchall.rule=hostregexp(`{host:.+}`)"
            - "traefik.http.routers.http-catchall.entrypoints=web"
            - "traefik.http.routers.http-catchall.middlewares=redirect-to-https"
            - "traefik.http.middlewares.redirect-to-https.redirectscheme.scheme=https"

  apache:
    image: 'bitnami/apache:latest'
    container_name: apache-network

    volumes:
      - ./app:/app
    
    labels:
       - traefik.http.routers.apache.rule=Host(`joaogabriel_apache.localhost`)
       - traefik.http.routers.apache.tls=true
       - traefik.http.routers.apache.tls.certresolver=letsencryp
       - traefik.port=8080
    networks:
      - internal
     
    restart: unless-stopped

  apache1:
    image: 'bitnami/apache:latest'
    container_name: apache-network1
 
    volumes:
      - ./app:/app
    
    labels:
       - traefik.http.routers.apache1.rule=Host(`ricardolangbecker_apache1.localhost`)
       - traefik.http.routers.apache1.tls=true
       - traefik.http.routers.apache1.tls.certresolver=letsencryp
       - traefik.port=8081
    networks:
      - internal

    restart: unless-stopped

  dokuwiki:
    image: docker.io/bitnami/dokuwiki:20200729

    volumes:
      - 'dokuwiki_data:/bitnami/dokuwiki'

    labels:
       - traefik.http.routers.dokuwiki.rule=Host(`ricardolangbecker_dokuwiki.localhost`)
       - traefik.http.routers.dokuwiki.tls=true
       - traefik.http.routers.dokuwiki.tls.certresolver=letsencryp
       - traefik.port=8082
    networks:
      - internal

    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana

    labels:
      - traefik.http.routers.grafana.rule=Host(`ricardolangbecker_grafana.localhost`)
      - traefik.http.routers.grafana.tls=true
      - traefik.http.routers.grafana.tls.certresolver=letsencrypt
      - traefik.port=3000

    networks:
      - internal

```