
# Projeto PROXY reverso

## 1° Etapa:

Alterar os subdominíos:

## 1° Passo:
![Alterando o subdominio do DashBoard](RedesDeComputadores-Aula-ProxyReverso/SubDominio-Dashboard)

## 2° Passo:

![Alterando o subdominio do Apache](RedesDeComputadores-Aula-ProxyReverso/SubDominio-Apache)

## 3° Passo:

![Alterando o subdominio do Apache1](RedesDeComputadores-Aula-ProxyReverso/SubDominio-Apache1)

## 4° Passo:

![Alterando o subdominio do Grafana](RedesDeComputadores-Aula-ProxyReverso/SubDominio-Grafana)

## 5° Passo:

![Alterando o subdominio do Dokuwiki](RedesDeComputadores-Aula-ProxyReverso/SubDominio-Dokuwiki)



## 2° Etapa:

Buildar o docker-compose:

## 1° Passo:

Instalar o docker compose utilizando o comando:

$ sudo apt install docker-compose

Comando para buildar o docker compose:

$ docker-compose --build

Comando para encerrar a build:

$ docker-compose stop:

Comando para remover a build:

$ docker-compose rm

![Buildando o docker compose](RedesDeComputadores-Aula-ProxyReverso/Passo1)

## Passo de verificação:

Links para verificar se o subdominio está funcionando:

>  http://raul_dashboard.localhost

> http://raul_apache.localhost

> http://raul_apache1.localhost

> http://raul_grafana.localhost

>  http://raul_dokuwiki.localhost

## 3° Etapa:

Identificar os subdominios alterados:


![Identificando os subdominios alterados](RedesDeComputadores-Aula-ProxyReverso/SubDominios-Alterados)