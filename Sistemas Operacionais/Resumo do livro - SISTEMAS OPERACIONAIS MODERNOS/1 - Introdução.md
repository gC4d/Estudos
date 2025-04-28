Sistemas Operacionais surgem com o intuito de evitar que cada programador necessite possuir conhecimento sobre todas as partes existentes do hardware e a melhor maneira para utilizá-lo, ou seja, de maneira otimizada.

Sistemas como Windows, Distros Linux, Distros BSDs ou macOS são exemplos de sistemas operacionais utilizados. Porém, o meio como o usuário interage com esses SOs não são exatamente parte dele, mas sim interfaces de texto (shells) ou interfaces gráficas (Graphical User Interface), também chamadas de GUI.

## 1.1 - O que é um sistema operacional?

Não possui uma definição clara, porém, além de ser o software que roda em modo de núcleo, também é responsável por exercer duas funções: fornecer interfaces abstratas de comunicação com o hardware, para que possa ser usada por programas aplicativos, e gerenciar os recursos de hardware da máquina em operação.

## 1.1. - O sistema operacional
### 1.1.1  Como máquina estendida

O S.O atua como máquina estendida fornecendo abstrações que simplificam a interação de aplicativos com o hardware. Como um disco rígido moderno, o qual possui diversas interfaces extremamente detalhadas, exigindo drivers para sua operação.

Um bom exemplo para isso é um "Arquivo", o qual permite manipular dados, por mais complexos que sejam, sem se preocupar com detalhes de hardware.

**Abstrações** são fundamentais para lidar com a **Complexidade**.

O papel de um sistema operacionais é esconder a complexidade existente no hardware e oferecer maneiras limpas e simples de se comunicar com o mesmo. Isso faz com que, mesmo que interfaces gráficas variem (Windows, Gnome e KDE) as abstrações serão sempre as mesmas.

### 1.1.2 Como gerenciador de recursos

Além de perspectiva apresentada anteriormente chamada Top-Down, onde o sistema operacional atua como simplificador para que as camadas superiores interajam com as inferiores, também é importante destacar uma abordagem oposta chamada de Down-Top, que define que o sistema operacional atual como gerenciador de recursos da máquina. Máquinas modernas possuem diversos recursos (CPU, memórias, disco, redes, etc.), e o sistema operacional é o responsável por controlar seu uso de forma ordenada, evitando conflitos.

As principais atribuições de um sistema operacional segundo a abordagem Down-Top é os seguintes:
- **Alocações de recursos**
	- Gerencia o acesso concorrente a processadores, memória, dispositivos de E/S, etc.
- **Proteção e controle**
	- Em sistemas multiusuário, evita que programas ou usuários interfiram uns com os outros.
- **Multiplexação (Compartilhamento de Recursos):**
	- **No tempo:** Recursos são alocados alternadamente.
	- **No espaço:** Recursos são divididos em partes alocadas simultaneamente.

## 1.2 - História dos sistemas operacionais

Os sistemas operacionais evoluíram juntamente das arquiteturas dos computadores. Embora isso não tenha ocorrido de maneira linear é possível destacar-se algumas eras dessa evolução.

#### Pré História - Máquina analítica de Babbage 

Está é o primeiro projeto de um computador, projetado pelo matemático **Charles Babbage** no século XIX, porém jamais foi retirada do papel pelo mesmo, devido a tecnologia existente da época.

Além de Babbage também é importante destacar o nome de **Ada Lovelace**, considerada a primeira programadora da história, a qual trabalhava com Babbage escrevendo os algoritmos para a máquina.

Como é de se imaginar, nesse primeiro projeto não existia nenhuma hipótese sobre um sistema operacional.

#### Primeira Geração (1945 - 1955)

##### Válvulas e Programação em Linguagem de Máquina

- **Hardware:** Computadores baseados em **válvulas termiônicas** (ex: ENIAC, UNIVAC).
    - Eram enormes, consumiam muita energia e quebravam frequentemente.
- **Sistemas Operacionais:** **Não existiam**.
    - Programação era feita diretamente em **linguagem de máquina** (binário).
    - Cada programa controlava todo o hardware sozinho.
- **Processamento:**
    - **Modo batch (lote) manual**: Programas eram inseridos um de cada vez por operadores, usando cartões perfurados ou fitas.
    - Sem multiprogramação – a CPU ficava ociosa durante operações de E/S.

#### Segunda Geração (1955–1965)

##### Transistores e Sistemas Batch

- **Hardware:** Surgimento dos **transistores**, substituindo válvulas.
    - Computadores ficaram mais rápidos, menores e confiáveis (ex: IBM 7094).
- **Sistemas Operacionais Primitivos:**
    - **Monitor residente**: Um programa simples que automatizava a troca de jobs (tarefas).
    - **Sistemas batch (lote) automatizados**:
        - Operadores agrupavam jobs semelhantes em lotes.
        - Ex: **FMS (Fortran Monitor System)** e **IBSYS** (IBM).
- **Limitações:**
    - **CPU ainda ociosa** durante E/S (um job por vez).
    - Programadores perdiam horas/dias para corrigir erros devido ao atraso no feedback.

#### Terceira Geração (1965–1980)

##### Circuitos Integrados e Multiprogramação

_(Já resumido anteriormente, mas para completar:)_
- **IBM System/360**: Família de computadores compatíveis com CIs.
- **Multiprogramação**: Vários jobs na memória, reduzindo ociosidade da CPU.
- **Timesharing**: Interação em tempo real via terminais (ex: CTSS, MULTICS).
- **UNIX**: Surgiu como um sistema simplificado e portátil.

#### Quarta Geração (1980–Presente)

##### PCs e Interfaces Gráficas

- **CP/M → MS-DOS → Windows**: Dominância da Microsoft.
- **GUI**: Macintosh (Apple) e Windows popularizaram interfaces visuais.
- **UNIX/Linux**: Alternativas robustas para servidores e desenvolvedores.

#### Quinta Geração (1990–Presente)
##### Dispositivos Móveis

- **Smartphones**: Android e iOS dominam, substituindo Symbian e BlackBerry.
- **Foco**: Portabilidade, conectividade e ecossistema de apps.