A **Entrada e Saída** é umas das partes mais complexas do sistema operacional devido a grande variedade de dispositivos e as diferentes velocidades e modos de operação.

> **Nota:** Neste documento, os termos **entrada e saída** serão representados como **E/S**, **I/O** ou **IO**.

## Princípios:
### Princípios de Hardware de E/S

Para entender a E/S é essencial conhecer os componentes de hardware envolvidos:
1. **Dispositivos de E/S:** São os periféricos conectados ao computador, como teclados, mouses, impressoras, monitores, HD's, SSD's, placas de rede, etc. Cada dispositivo tem características e modos de operação únicos.
2. **Controladores de Dispositivos:** Para cada tipo de dispositivo de E/S, existe um controlador de dispositivos (ou *adaptador*). Este é um chip ou placa de circuito que interfaceia o dispositivo físico com o barramento do sistema, Ele contém registradores de controle e status para comunicação com a CPU e um buffer de dados para armazenar temporariamente os dadas de E/S.
3. **E/S Mapeada na Memória (Memory-Mapped I/O):** Em muitos sistemas, os registrados dos controladores de E/S e os buffers de dados são mapeados em endereços da memória. Isso significa que a CPU pode acessar e controlar os dispositivos de E/S usando instruções de leitura e escrita de memória comuns, em vez de instruções de E/S especiais.
4. **Acesso Direto à Memória (DMA - Direct Memory Access):** Para operações de E/S de alto volume como leitura de disco, a CPU pode ser ineficiente copiando byte a byte. O DMA permite que um controlador de DMA (*um chip especial*) transfira dados diretamente entre os dispositivos de E/S e a memória principal, sem a intervenção da CPU. A CPU apenas inicia a transferência de DMA e é notificada (*via interrupção*) quando a transferência é concluída. Isso libera a CPU para outras tarefas.
5. **Interrupções:** São sinais de hardware enviados pelos controladores de dispositivos para a CPU para indicar que uma operação de E/S foi concluída, que um evento ocorreu (e.g., tecla pressionada) ou que há um erro. As interrupções são um mecanismo assíncrono que permite a CPU continuar processando enquanto a E/S ocorre em segundo plano, melhorando a eficiência.

### Princípios de Software de E/S

O software de E/S lida com a programação dos dispositivos. Ele pode ser classificado com base em como a CPU interage com os controladores:

1. **E/S Programada (Programmed I/O - PIO)**:
    - A CPU fica em um _loop de polling_, verificando repetidamente o registrador de status de um controlador de dispositivo para ver se uma operação de E/S foi concluída.
    - É simples de implementar para operações pequenas ou em sistemas embarcados simples, mas é muito ineficiente, pois a CPU desperdiça ciclos preciosos esperando pela E/S.        
2. **E/S Orientada a Interrupções (Interrupt-Driven I/O)**:
    - A CPU inicia uma operação de E/S e, em vez de esperar, continua com outras tarefas.
    - Quando a operação de E/S é concluída (ou um evento ocorre), o controlador de dispositivo gera uma interrupção.
    - A CPU suspende a tarefa atual, salva seu estado, e executa um **tratador de interrupção (interrupt handler)**, que é uma rotina de software específica para lidar com aquela interrupção. Após o tratamento, a CPU retorna à tarefa original.
    - É muito mais eficiente que a PIO, pois permite que a CPU e os dispositivos de E/S operem em paralelo.
3. **E/S Usando DMA**:
    - Para transferências de blocos grandes, o DMA é o método mais eficiente.
    - A CPU programa o controlador de DMA com os endereços de origem e destino na memória, o número de bytes a transferir e o modo de operação.        
    - O DMA assume a transferência de dados, e a CPU fica livre.        
    - Uma vez que o DMA completa a transferência, ele gera uma interrupção para notificar a CPU.

## Tipos de E/S

Para entender sobre o funcionamento dos dispositivos de IO primeiramente é preciso saber sobre os tipos de entrada e saída. São eles classificados em 3 taxonomias:

- Tipo de conexão.
- Tipo de transferência de dados.
- Tipo de compartilhamento de conexão

### 1. Tipo de conexão (Como os Dispositivos se Conectam)

Esta taxonomia refere-se a interface física e lógica que os dispositivos de IO utilizam para se comunicar com o restante do sistema computacional, especialmente com a CPU e a memória. 

> Resumo: Refere-se a comunicação do módulo de IO com o periférico.
> (Serial x Paralela)
#### Conexão Serial

Basicamente é uma unica linha de conexão entre o periférico e o módulo IO. Sendo assim, os dados seguem bit atrás de bit até percorrer o seu trajeto.

>Trajeto pode ser em ambos os sentidos:
>- Módulo de IO -> Periférico
>- Periférico -> Módulo de IO
>Porém, não ao mesmo tempo
##### Características:
- Mais barata que a paralela.
- Mais lenda que a paralela.
- Relativamente confiável.
- Usada em dispositivos brados e lentos.
	- Impressoras e terminais.

#### Conexão Paralela

Diferentemente da serial, aqui existem várias linhas de conexão entre os periféricos e o módulo de IO. Consequentemente isso faz com que o fluxo de dados seja feito com muito maior intensidade.
##### Características:
- Mais complexa que a serial.
- Mais cara.
- Mais rápida.
- Altamente confiável.
- Usada em dispositivos velozes.
	- Exemplo: disco.

### 2. Tipo de Transferência de Dados (Como os Dados são Movidos)

Este ponto se refere aos métodos pelos quais os dados são fisicamente movidos entre o dispositivo de IO e a memória principal ou a CPU.
#### Dispositivos de Bloco (block devices):

Aqui a transferência é realizada utilizando bloco de tamanho fixo entre 128 e 1024 bytes, onde cada um desses blocos possui um endereço.

A transferência é feita com um ou mais blocos.
##### Por que utilizar essa tipo de transferência?

R: Para ter melhor referência de localidade, uma vez que carrega um conjunto maior de dados agregados.

> **Exemplo:** Ao carregar a página 10 de um livro, também é carregado as próximas páginas, já que a possibilidade de leitura delas é maior do que a leitura unica da página solicitada.

Isso torna esse processo de transferência mais otimizado, já que não carrega vários dados de uma vez. 
Deve-se sempre considerar que a nível computacional gasto de tempo desnecessário é desperdício, e o processo de E/S toma tempo.

Exemplos de dispositivos de IO que utilizam esse modo de transferência:
- HD
- CD-ROM
- Drive USB
#### Dispositivos de caractere (character devices):

- Acessam um fluxo de caracteres
- Não consideram blocos.
- Não são endereçáveis 
- Não possuem acesso aleatório

Exemplos de dispositivos de IO que utilizam esse modo de transferência:
- Impressoras
- Interfaces de Rede
- Mouses
### 3. Compartilhamento de Conexões

São as abordagens de conexão mais dedicadas e aquelas que permitem múltiplas interações simultâneas ou quase simultâneas
#### Ponto a Ponto

Uma conexão ponto a ponto, no contexto de E/S, refere-se a uma ligação direta e exclusiva entre dois componentes. Isso significa que um dispositivo de E/S ou um controlador está conectado diretamente a um único outro componente, sem que outros dispositivos compartilhem a mesma linha de comunicação específica.

**Características**:
- **Dedicada**: A banda larga da conexão é dedicada apenas à comunicação entre os dois pontos conectados.
- **Simplicidade**: A comunicação é geralmente mais simples, pois não há necessidade de arbitrar acesso a um canal compartilhado.

**Protocolos que utilizam esse modo de conexão:**
- RTS: Request To Send
- CTS: Clear To Send
#### Multipontos

As conexões multipontos, ou multidrop, são muito mais comuns em sistemas de computação modernos e são fundamentais para o compartilhamento de recursos de E/S. Elas envolvem múltiplos dispositivos compartilhando o mesmo canal de comunicação ou barramento.

> **Nota:** Como os dispositivos estão compartilhando o mesmo barramento é incapaz de trabalhar com paralelismo

**Características**:
- **Compartilhada**: Vários dispositivos se conectam ao mesmo meio de comunicação. Isso economiza pinos, fiações e complexidade de porta no sistema principal.
- **Necessidade de Arbitragem**: Como o meio é compartilhado, é essencial ter um mecanismo de arbitragem para determinar qual dispositivo pode usar o barramento em um determinado momento, evitando colisões. Isso é gerenciado por hardware e software (e.g., controladores de barramento, _bus arbiters_).
- **Multiplexação Temporal**: Embora a conexão física seja compartilhada, o acesso é geralmente serializado no tempo. Cada dispositivo tem sua "vez" de usar o barramento, dando a ilusão de acesso simultâneo.
- **Exemplos Comuns**:
	- **Barramentos do Sistema**: O exemplo mais comum é o próprio **barramento do sistema** (e.g., PCIe, USB, SCSI, IDE/ATA, etc.). Múltiplos controladores de dispositivo (e, indiretamente, os dispositivos que eles controlam) se conectam ao mesmo barramento da CPU e da memória. Eles compartilham a largura de banda do barramento.
	- **Dispositivos Encadeados**: Alguns tipos de dispositivos podem ser encadeados em um único controlador (e.g., dispositivos SCSI em um único cabo SCSI).