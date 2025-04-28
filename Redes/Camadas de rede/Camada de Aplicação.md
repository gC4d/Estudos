## Introdução


## Arquiteturas

Existem 3 principais arquiteturas a serem utilizadas na camada de aplicação

- Client-Server: Cliente-Servidor
- Peer-to-Peer (p2p): Ponta a Ponta
- Hibrido: Client-Server e p2p juntas

### Cliente-Servidor

Nessa arquitetura o servidor permanece sempre ligado e seu endereço IP é fixo, ou seja, nunca muda. Além disso também possui um sistema de escalabilidade com *server farms*

E por outro lado o Cliente é aquele que comunica-se com o servidor. E diferentemente do servidor o Cliente pode ter IP variável, ou dinâmico. Jamais se comunica com outro cliente diretamente

### Peer-to-Peer

==Altamente escalável, porém com difícil gerência==

 Não há a necessidade de um servidor sempre ligado, já que seus sistemas finais são 
 arbitrários se comunicam diretamente.
 Pares estão conectados intermitentemente e mudam de IPs.
 
 Exemplos: Gnutella, Skype, uTorrent.
 
## Processos em comunicação

 **Processo - Programa que executa um hospedeiro**
- Processos no mesmo hospedeiro se comunicam usando **comunicação entre processos** definida pelo SO
- Processos em hospedeiros distintos se comunicam trocando **mensagens através da rede**

**Processo cliente - Processo que inicia a comunicação**
**Processo servidor - Processo que espera ser contatado**

## Sockets

Os processos enviam/recebem mensagens para/dos seus **sockets**

==Um socket é análogo a uma pota==
- Processo transmissor envia mensagem através da porta
- O processo transmissor assumo a existência da infraestrutura de transporte no outro lado da porta que faz com que a mensagem chegue ao *socket* do processo receptor

## Serviços de transporte 

- Perda de dados:
	- Algumas APIs de transmissão de mídia em tempo real (serviços de streaming de videos e músicas) toleram algumas perdas de dados
	- Já outras como APIs que realizam transmissão de arquivos requerem uma transferência 100% confiável
- Temporização:
	- Serviços que necessitam de respostas rápidas, como jogos online multiplayer, requerem baixo retardo para serem "viáveis"
- Largura de banda:
	- Algumas APIs de transmissão multimídia necessitam de uma largura de banda minima para que possam funcionam ser perca de qualidade. Porém existem outras APIs que são elásticas e se adaptam a banda disponível

## WEB

### Formando páginas

- Páginas web consistem de objetos
	- Objetos podem ser um arquivo HTML, imagem JPEG, ou também um arquivo de audio
- Cada objetos é endereçavel por uma URL
	- Exemplo: https://www.tecmundo.com.br/blackfriday/hub/
	- Nome do hospedeiro: https://www.tecmundo.com.br
	- Nome do caminho: **blackfriday/hub/**
### Protocolo HTTP - HyperText Transfer Protocol

É um protocolo da camada de aplicação da WEB que utiliza o modelo cliente-servidor.

- Cliente: **Browser**
	- Pede, recebe e visualiza objetos Web
- Servidor: **Servidor Web**
	- Envia objetos em resposta a pedidos

Versões:
- HTTP 1.0 [RFC 1945]
- HTTP 1.1 [RFC 2068]

- Utiliza o serviço de transporte TCP

==Sem estado: Servidor não armazena informações sobre pedidos anteriores==

#### Formato

- Possui dois tipos de mensagens HTTP:
	- Pedido (==require==)
	- Resposta (==response==)

Mensagens de pedidos (==requests==) HTTP são feitas no formato de ASCII, que é um formato legível por pessoas.

Exemplo: 
`GET /somedir/page.html HTTP/1.0`
`Host: www.someschool.edu` 
`User-agent: Mozilla/4.0 Connection:` 
`close Accept-language:fr`

Onde:
- Linha de pedido: `GET /somedir/page.html HTTP/1.0`
- Linha de cabeçalho: `Host: www.someschool.edu` 
					`User-agent: Mozilla/4.0 Connection:` 
					`close Accept-language:fr`
##### Métodos

- HTTP 1.0:
	- GET
	- POST
	- HEAD
- HTTP 1.1
	- GET
	- POST
	- HEAD
	- PUT
	- DELETE
	
- POST envia os dados no corpo da mensagem
- GET envia os dados na URL

#### Resposta

##### Status

- 200 - OK
- 301 - Moved Permanently
- 400 - Bad Request
- 404 - Not Found
- 505 - HTTP Version Not Supported

#### Cookies

São utilizados para salvar o estado

- Cookies podem obter:
	- Autorização
	- Carrinhos de compra
	- Sugestões
	- Estado da sessão do usuário

## Aplicações

Se trata basicamente do aplicativo que está sendo usado que estabelece comunicações com a rede

- E-mail
- Web
- Jogos online
- Video conferências