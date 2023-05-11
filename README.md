## Mudando o subdominio

    Mudar o endereço mudando o host que fica dentro de "Label", mudando assim o subdominio
    
### Exemplo:
![Mudando o endereço](doc/Apache_edicao.png)

 ## Usando o Docker   
    Para executar os comandos utilize o comando "sudo" na frente

Rode o Docker usando o comando(para cancelar CTRL + C):

> $ docker-compose up --build

Se não rodar, pode ser que não tenha um docker construido, o comando para consertar se encontra no erro.

Se a porta já estiver em uso, desinstale o apache2 usando o comando:

> $ sudo apt remove apache2

![Removendo Apache](doc/RemoverApache.png)

 Quando fizer tudo, deve rodar e exibir a seguinte tela:

    
![Done](doc/Done.png)

Se quiser parar o serviço utilize:

> $ docker-compose stop

ou se quiser remover utilize o comando:

> $ docker-compose rm


## Testando

    Quando mudar o dominio lembrar de mudar o endereço
### Exemplo:
![Exemplo Endereco](doc/Endereco.png)

Pelo navegador podemos acessar o endereço

>http://apache.localhost

    Pode aparecer uma tela de aviso de segurança, só clicar em avançar

Se estiver rodando, deve aparecer uma tela com a palavra it works

![It works](doc/ItWorks.png)

    Caso não funcione aparecerá uma tela de erro 404

Para testar o grafana, se utiliza o seguinte link

>http://grafana.localhost

e assim aparecerá essa tela

![Tela Grafana](doc/Grafana.png)

Fazendo o login entramos nele
![Tela Dentro do Grafana](doc/DentroGrafana.png)

Podemos ver os subdominios, as rotas e portas usando o site do DashBoard

>http://dashboard.localhost

![Tela DashBoard](doc/TelaDashBoard.png)

    O 80 representa o HTTP e o 443 o HTTPS
    Os gŕaficos mostram que tem 6 rotas e 8 serviços e 1 middleware

Lá na parte superior, mudando para http podemos ver todas as rotas

![Rotas](doc/Dominio.png)

## Removendo vulnerabilidade
Removemos a possibilidade de entrar utilizando o ip, fazendo ser obrigado a entrar com o dominio, e impossilitando entrar com o ip. Para fazer isso se remove as portas expostas e a network WEB de quase todas as tags, menos do traefik, assim isolando ela.