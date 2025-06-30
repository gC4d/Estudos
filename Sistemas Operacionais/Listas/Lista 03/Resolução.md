### Lista de Exercícios 03

#### Entrada e Saída

1. **Considere as seguintes abordagens para realizar E/S: programada, por interrupção e por DMA e responda:**
    
    I. Quais as etapas envolvidas com E/S programada? Qual o overhead apresentado por essa forma de E/S?
    
    * Etapas envolvidas com E/S programada:
    
    1. A CPU inicia a operação de E/S emitindo um comando para o controlador do dispositivo.
    
    2. A CPU entra em um loop de espera contínuo (polling), verificando o status do controlador do dispositivo repetidamente até que a operação de E/S seja concluída.
    
    3. Quando o dispositivo de E/S sinaliza que está pronto, a CPU transfere os dados.
    
    * Overhead apresentado: O principal overhead é o alto consumo de CPU. A CPU fica ocupada em um loop de espera, verificando constantemente o status do dispositivo, o que a impede de realizar outras tarefas úteis. Isso é particularmente ineficiente para dispositivos lentos.
    
    II. Quais as etapas envolvidas com E/S orientada à interrupção? Qual o overhead apresentado por essa forma de E/S?
    
    * Etapas envolvidas com E/S orientada à interrupção:
    
    1. A CPU inicia a operação de E/S emitindo um comando para o controlador do dispositivo.
    
    2. A CPU continua executando outras tarefas.
    
    3. Quando a operação de E/S é concluída, o controlador do dispositivo gera uma interrupção para a CPU.
    
    4. A CPU suspende sua tarefa atual, salva seu contexto e transfere o controle para o handler de interrupção apropriado.
    
    5. O handler de interrupção lida com a transferência de dados e/ou conclui a operação de E/S.
    
    6. A CPU restaura seu contexto e retoma a tarefa que estava executando.
    
    * Overhead apresentado: O overhead é menor do que na E/S programada, pois a CPU não precisa ficar em um loop de espera. No entanto, ainda há um overhead associado ao processamento das interrupções: salvar e restaurar o contexto da CPU, e a execução do handler de interrupção. Para transferências de dados muito grandes, o número de interrupções pode se tornar um gargalo, pois cada interrupção requer uma intervenção da CPU.
    
    III. Quais as etapas envolvidas com E/S utilizando DMA? Qual o overhead apresentado por essa forma de E/S?
    
    * Etapas envolvidas com E/S utilizando DMA:
    
    1. A CPU programa o controlador DMA, fornecendo o endereço de memória de origem/destino, o número de bytes a serem transferidos e a direção da transferência (E/S).
    
    2. A CPU continua executando outras tarefas.
    
    3. O controlador DMA gerencia a transferência de dados diretamente entre o dispositivo de E/S e a memória, sem a intervenção da CPU para cada byte ou palavra.
    
    4. Somente quando a transferência de todo o bloco de dados é concluída, o controlador DMA gera uma única interrupção para a CPU.
    
    5. A CPU, via handler de interrupção, finaliza a operação de E/S.
    
    * Overhead apresentado: O overhead é o menor entre as três abordagens para grandes blocos de dados. A CPU é liberada para realizar outras tarefas durante a maior parte da transferência de dados. O único overhead significativo para a CPU é a programação inicial do controlador DMA e o tratamento da única interrupção ao final da transferência. Há um pequeno overhead conhecido como "roubo de ciclo" (cycle stealing), onde o DMA compete com a CPU pelo acesso à memória, mas isso geralmente é insignificante.
    
2. **Considerando o software gerenciador de E/S de um sistema operacional, observa-se que se procura atingir um alto grau de independência ao dispositivo. Isto é, em se tratando de acesso a disco, por exemplo, procura-se implementar o sistema de modo a se ter o mesmo tratamento uniforme para o acesso a arquivos, quer estejam eles em um disquete, disco rígido, disco ótico, etc. Explique como essa independência é alcançada e como se faz quando um novo tipo de dispositivo deve ser introduzido no sistema.**
    
    A independência de dispositivo é alcançada através de uma arquitetura em camadas do software de E/S e do uso de interfaces padronizadas. O sistema operacional implementa uma camada superior de E/S que interage com os aplicativos usando chamadas de sistema genéricas (por exemplo, `abrir()`, `ler()`, `escrever()`, `fechar()`) que não especificam o tipo de dispositivo. Abaixo dessa camada, existem as camadas de software de E/S específicas do dispositivo, incluindo _drivers_ de dispositivo.
    
    - **Como é alcançada:**
        
        - **Camadas de abstração:** O software de E/S é organizado em camadas hierárquicas, onde as camadas superiores oferecem uma interface genérica para as aplicações, independentemente do dispositivo físico.
            
        - **Drivers de dispositivo:** A camada mais baixa contém os _drivers_ de dispositivo, que são módulos de software específicos para cada tipo de hardware. Eles traduzem as requisições genéricas das camadas superiores em comandos específicos que o hardware do dispositivo entende.
            
        - **Interface padronizada:** As camadas superiores se comunicam com os _drivers_ de dispositivo através de uma interface bem definida e padronizada. Isso significa que, enquanto o _driver_ adere a essa interface, o resto do sistema operacional não precisa saber os detalhes internos de como o dispositivo funciona.
            
    - Como se faz quando um novo tipo de dispositivo deve ser introduzido no sistema:
        
        Quando um novo tipo de dispositivo deve ser introduzido no sistema, o processo geralmente envolve:
        
        1. **Desenvolvimento de um novo _driver_:** Um _driver_ de dispositivo específico para o novo hardware é desenvolvido. Este _driver_ é responsável por entender os comandos e o comportamento do novo dispositivo.
            
        2. **Adesão à interface do SO:** O _driver_ deve ser escrito de forma a aderir à interface padrão que o sistema operacional espera para _drivers_ de dispositivo.
            
        3. **Instalação do _driver_:** O _driver_ é então instalado no sistema operacional. Em sistemas modernos, isso muitas vezes é plug-and-play, onde o SO detecta o novo hardware e instala o _driver_ automaticamente (se disponível). Caso contrário, o usuário precisa instalar o _driver_ manualmente.
            
        4. **Integração:** Uma vez que o _driver_ está instalado e funcionando, as camadas superiores do software de E/S podem interagir com o novo dispositivo de forma transparente, usando as mesmas chamadas de sistema genéricas que usariam para qualquer outro dispositivo similar. As aplicações não precisam ser modificadas para usar o novo hardware.
            
3. **Considere que um arquivo está em um disco rígido e deva ser transferido para uma impressora. Descreva os passos necessários para a realização desta operação, discutindo o que ocorre em cada camada do software que gerencia operações de E/S. Deixe claro em que camada de E/S cada passo é executado.**
    
    A transferência de um arquivo de um disco rígido para uma impressora envolve múltiplas camadas do software de E/S:
    
    1. **Camada de Aplicação:**
        
        - **Passo:** O usuário ou um programa de aplicação (por exemplo, um editor de texto, navegador) inicia a operação de impressão, chamando uma função como "Imprimir" ou "Print". A aplicação faz uma chamada de sistema de alto nível ao sistema operacional para abrir o arquivo e enviá-lo para a impressora.
            
        - **Ocorre:** A aplicação formata os dados para a impressora (por exemplo, PostScript, PCL, PDF) e solicita o serviço de impressão ao sistema operacional.
            
    2. **Camada de Software Básico do Sistema de Arquivos (Sistema de Arquivos Lógico):**
        
        - **Passo:** O sistema operacional, através de sua camada de sistema de arquivos, recebe a requisição de ler o arquivo do disco. Ele verifica as permissões de acesso ao arquivo para o usuário que fez a requisição.
            
        - **Ocorre:** O sistema de arquivos abre o arquivo, localiza seus metadados (como o i-node em sistemas Unix ou entradas na FAT em sistemas Windows) para saber onde os blocos de dados do arquivo estão localizados no disco. Traduz a requisição de leitura do arquivo em blocos lógicos de disco.
            
    3. **Camada de Software Básico do Sistema de E/S (Controle de Dispositivo Genérico / Camada de Agendamento):**
        
        - **Passo:** As requisições de leitura dos blocos lógicos são passadas para a camada de E/S de disco. Se houver várias requisições de leitura/escrita pendentes para o disco, esta camada as enfileira e pode aplicar um algoritmo de escalonamento de disco (por exemplo, FIFO, SSTF, SCAN) para otimizar o movimento da cabeça do disco.
            
        - **Ocorre:** O agendador de disco decide a ordem em que os blocos serão lidos do disco físico.
            
    4. **Camada de Driver de Dispositivo (para o Disco Rígido):**
        
        - **Passo:** O _driver_ do disco rígido recebe as requisições de blocos do agendador. Ele traduz os números de blocos lógicos em endereços físicos de cilindro, cabeça e setor (CHS) ou endereços LBA (Logical Block Addressing).
            
        - **Ocorre:** O _driver_ emite comandos específicos para o controlador do disco rígido (por exemplo, via interface SATA ou NVMe) para ler os dados. O controlador DMA é programado para transferir os dados lidos do disco diretamente para um buffer na memória principal. Uma interrupção é gerada quando a leitura do bloco é concluída.
            
    5. **Camada de Armazenamento em Buffer (Buffer Cache):**
        
        - **Passo:** Conforme os dados são lidos do disco pelo DMA, eles são colocados em um buffer de memória (cache de disco).
            
        - **Ocorre:** O sistema operacional gerencia esse buffer, permitindo que os dados sejam lidos da memória de forma mais rápida pela próxima camada.
            
    6. **Camada de Software Básico do Sistema de E/S (Controle de Dispositivo Genérico / Spooling e Agendamento para Impressora):**
        
        - **Passo:** Os dados do arquivo que foram lidos para a memória são agora direcionados para a impressora. Geralmente, esta operação é feita via _spooling_. Os dados formatados para impressão são colocados em uma fila (buffer de _spool_) no disco ou em memória, para que a aplicação possa continuar sem esperar a impressão física ser concluída.
            
        - **Ocorre:** O subsistema de _spooling_ da impressora gerencia a fila de impressão.
            
    7. **Camada de Driver de Dispositivo (para a Impressora):**
        
        - **Passo:** O _driver_ da impressora retira os dados da fila de _spool_ (ou diretamente do buffer de memória, se não houver _spooling_). Ele então traduz esses dados formatados para comandos específicos que a impressora entende (por exemplo, comandos de impressão de caracteres, comandos de controle de página).
            
        - **Ocorre:** O _driver_ da impressora envia esses comandos e os dados para o controlador da impressora (via USB, Ethernet, etc.). O controlador da impressora gerencia a saída física dos dados (imprimindo na folha). O DMA também pode ser usado aqui para transferir dados da memória para o controlador da impressora.
            
    8. **Hardware da Impressora:**
        
        - **Passo:** A impressora recebe os comandos e dados, e fisicamente imprime o arquivo.
            
        - **Ocorre:** O hardware da impressora executa as operações de impressão (movimento da cabeça, deposição de tinta/toner, alimentação de papel).
            
4. **Discuta em que situação (ou situações) cada um dos seguintes algoritmos para escalonamento de disco é mais adequado: Comente as vantagens/desvantagens/dificuldades de cada um desses algoritmos de escalonamento.**
    
    - **Algoritmos de Escalonamento de Disco (assumindo FIFO, SSTF, SCAN/Elevador, C-SCAN):**
        
        1. **FIFO (First-In, First-Out):**
            
            - **Situação mais adequada:** Ambientes com poucas requisições de E/S e onde a justiça entre as requisições é prioritária, ou quando a localização da cabeça do disco é irrelevante para o desempenho. Também é adequado para sistemas de arquivo que realizam E/S sequencial intensiva.
                
            - **Vantagens:** Simples de implementar e garante a justiça (nenhuma requisição fica "starving").
                
            - **Desvantagens/Dificuldades:** Não otimiza o movimento da cabeça do disco, podendo resultar em um grande número de movimentos e baixo desempenho (tempo de busca e latência rotacional). Pode ser ineficiente se as requisições estiverem espalhadas aleatoriamente no disco.
                
        2. **SSTF (Shortest Seek Time First):**
            
            - **Situação mais adequada:** Ambientes onde a otimização do tempo de busca é crucial e o objetivo é maximizar o _throughput_ do disco.
                
            - **Vantagens:** Reduz o tempo médio de busca e aumenta o _throughput_ do disco, pois sempre escolhe a requisição mais próxima da posição atual da cabeça.
                
            - **Desvantagens/Dificuldades:** Pode levar à "starvation" (inanição) de requisições que estão muito longe da posição atual da cabeça, especialmente se houver um fluxo constante de novas requisições próximas à cabeça. É mais complexo de implementar do que FIFO.
                
        3. **SCAN (Elevador / Elevator Algorithm):**
            
            - **Situação mais adequada:** Sistemas com carga de E/S moderada a alta, onde é necessário um bom equilíbrio entre _throughput_ e tempo de resposta, e onde a inanição deve ser evitada. É bom para cargas de trabalho que acessam dados espalhados.
                
            - **Vantagens:** Oferece um bom desempenho médio, minimiza a inanição e tem um comportamento mais previsível do que SSTF. A cabeça se move em uma direção, atendendo todas as requisições em seu caminho, e então reverte.
                
            - **Desvantagens/Dificuldades:** Requisições recém-chegadas na direção inversa da cabeça podem ter que esperar um ciclo completo do disco. O desempenho pode ser menos ideal do que SSTF para cargas de trabalho muito localizadas.
                
        4. **C-SCAN (Circular SCAN):**
            
            - **Situação mais adequada:** Ambientes com alta carga de E/S, onde se deseja uma distribuição mais uniforme do tempo de resposta e evitar a inanição de requisições em uma das extremidades do disco. É frequentemente preferido em sistemas modernos por sua previsibilidade.
                
            - **Vantagens:** Garante um tempo de resposta mais uniforme para todas as requisições do que SCAN, pois a cabeça sempre varre em uma única direção. Isso evita que as requisições na "extremidade" do disco tenham que esperar por um ciclo completo de reversão.
                
            - **Desvantagens/Dificuldades:** O tempo de busca total é ligeiramente maior do que o SCAN porque a cabeça "salta" de uma extremidade à outra sem atender requisições durante o retorno.