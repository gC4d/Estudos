## Introdução

A camada de transporte tem como função básica receber os dados da camada de aplicação, dividi-los caso necessário e repassá-los para a camada de rede. Além disso, também tem a função de isolar as camadas superiores de mudanças no hardware.

- Atua ligando o ponto de origem ao de destino em formato **end-to-end**.
    - Um programa da máquina de origem mantém uma conversa com um programa semelhante na máquina de destino.

A camada de transporte é responsável por multiplexar todas as comunicações em um único canal, determinando a qual conexão uma mensagem pertence.

### Responsabilidades

- **Estabelecer conexões**
- **Encerrar conexões**
- **Controle de fluxo** (quando utilizando TCP)

## Operação

O transporte de dados realizado entre diferentes hosts é feito com base em **TPDUs (Transport Protocol Data Units)**, também chamados de **Segmentos**.

- Um segmento é composto pelo cabeçalho de transporte e os dados da camada de aplicação.

### Protocolos

- **TCP (Confiável)**
    
    - Congestão
    - Controle de fluxo
    - Orientado a conexão
- **UDP (Não Confiável)**
    
    - Melhor esforço:
        - Para redes com grande fluxo, onde pode se dar ao luxo de perder alguns dados.
    - Não possui os serviços de:
        - Tempo real
        - Garantia de banda

### Multiplexação de Aplicações

Reúne os dados de múltiplos processos de aplicação, juntando cabeçalhos com informações para demultiplexação.

- **Segmento**: Unidade de dados trocadas entre entidades da camada de transporte.
- **TPDU**: Transport Protocol Data Units (Unidade de dados de protocolo de transporte).
- **Demultiplexação**: Processo de encaminhamento dos dados multiplexados aos processos de aplicação corretos.
- **Hosts Multiprogramados**: Permitem que muitas conexões entrem e saiam de cada host simultaneamente.

### Endereçamento

Os processos dessa camada utilizam o **TSAP (Transport Service Access Point)**.

- Em redes IP, o TSAP é um número de 16 bits.
- O endereço da camada de transporte é composto por 48 bits, sendo a agregação do endereço IP do host e da porta.
- Os serviços dessa camada são obtidos por meio da comunicação entre **sockets**.
    - Um socket é o ponto final do fluxo de comunicação entre processos através da rede.
    - Exemplo de socket: **PROTOCOLO://IP:PORTA**
- A **IANA (Internet Assigned Numbers Authority)** define algumas portas como **"Well-known ports"**:
    - Abaixo de 1024: "Well-known ports"
    - Acima de 1024: Destinadas para aplicações não padronizadas.

## UDP: User Datagram Protocol [RFC 768]

- Protocolo de transporte simples e leve.
- Serviço **best-effort** (melhor esforço).
- Segmentos UDP podem ser:
    - Perdidos
    - Entregues fora de ordem
- Não orientado a conexão.
- Utilizado em aplicações de multimídia contínua (voz e vídeo), que são tolerantes à perda.
- Outros usos:
    - **DNS**: Utilizado para resolver nomes de domínio antes da comunicação via TCP.
    - **SNMP**: Protocolo de gerenciamento de rede.

### Constituição do Segmento UDP

- **Porta de origem e Porta de destino**: Identificam os pares de portas envolvidos na comunicação.
    
- **Comprimento (tamanho)**: Indica o comprimento total do datagrama (cabeçalho e dados).
    
- **Checksum**: Verifica a integridade do datagrama.
    
    - **Objetivo**:
        - Detectar erros no segmento transmitido.
        - **Transmissor**: Calcula a soma do complemento de 1 do conteúdo do segmento.
        - **Receptor**: Verifica se o checksum recebido corresponde ao calculado:
            - Se sim: Sem erros.
            - Se não: Erro detectado.

## TCP: Transport Control Protocol [RFC 1122]

- Proporciona um fluxo de bytes confiável fim a fim (e2e) em redes não confiáveis.
- **Orientado a conexão**.
- Fragmenta o fluxo de entrada em segmentos e os transmite, remontando-os na recepção.

### Constituição do Segmento TCP

- **Porta de origem e Porta de destino**: Identificam os pares de portas envolvidos na comunicação.
- **Número de sequência**: Identifica o fragmento dentro do fluxo.
- **Número de confirmação**: Indica o próximo byte esperado.
- **Tamanho do cabeçalho**: Indica a quantidade de palavras de 32 bits no cabeçalho TCP.
- **Checksum**: Verifica a integridade do segmento.
- **Sinais de Controle**:
    - **URG**: Indica dados urgentes.
    - **ACK**: Confirma recebimento.
    - **PSH**: Indica prioridade no envio.
    - **RST**: Reinicia a conexão.
    - **SYN**: Solicita conexão.
    - **FIN**: Finaliza a conexão.
- **Tamanho da janela**: Define quantos bytes podem ser enviados sem confirmação.
- **Urgent Pointer**: Indica dados urgentes no fluxo.
- **Opções**: Permite recursos extras ao TCP.

### Estabelecimento de Conexão - Three Way Handshake

- Cliente envia um **SYN** solicitando conexão.
- Servidor responde com **SYN + ACK** confirmando a conexão.
- Cliente responde com **ACK**, estabelecendo a comunicação.

Isso permite a sincronização de números de sequência para garantir a entrega ordenada dos segmentos.

## Well Known Ports

- Lista de algumas das principais portas:
	- HTTP: 80
	- FTP: 20 e 21
	- TELNET: 23
	- DHCP: 67
	- DNS: 53
	- SNMP: 161 e 162
	- NFS: 2049
	- SMB: 137, 138, 139 e 445
	- SMTP: 25
	- POP3: 110

## RESUMO

A camada de transporte é o núcleo da hierarquia de protocolos, responsável por garantir a transferência de dados de forma confiável, eficiente e econômica entre a máquina de origem e a de destino, independentemente da infraestrutura de rede subjacente. Para isso, utiliza diversos serviços fornecidos pela camada de rede.

[[Camada de Aplicação]]