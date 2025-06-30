Sua principal função é fornecer uma abstração conveniente para o armazenamento físico, permitindo que os usuário manipulem informações de forma lógica, sem precisar se preocupar com os detalhes de baixo nível do hardware.

Além disso, o sistema de arquivos também oferecem mecanismos para organizar esses dados em estruturas hierárquicas, garantir a proteção e segurança e otimizar o desempenho do acesso.

## Arquivos

Um arquivo é uma abstração do sistema operacional para armazenar informações em dispositivos de armazenamento secundário.

Para o usuário, um arquivo é menor unidade de armazenamento de dados. Tende eles, uma série de características e operações que tornam uma entidade fundamental em qualquer S.O.

### Nomeação de arquivos

#### Convenções de nomenclatura:

Arquivos são identificados por nomes que devem ser únicos dentro de um diretório. As regras de nomes de arquivos variam entre os sistemas operacionais, mas geralmente envolvem uma sequência de caracteres.

Alguns S.Os distinguem letras maiúsculas de minúsculas, já outros não. Em sistemas UNIX podemos ter 3 arquivos: maria, Maria MARIA. Cada um deles representando um arquivo diferentes (primeiro caso), já o MS-DOS ambos representam o mesmo arquivo (segundo caso)

#### Extensões de arquivos:

Muitos sistemas operacionais permitem o uso de extensões (e.g., `.txt`, `.pdf`, `.exe`) para indicar o tipo ou formato do arquivo. Essas extensões são convenções para os usuários e para o próprio sistema operacional, que pode associar programas específicos a determinados tipos de arquivos.

- MS-DOS:
	- 1-3 caracteres; suporta apenas uma extensão.
	- 8 caracteres para o nome + 3 para a extensão.
- UNIX:
	- Mais de 3 caracteres.
	- suporta mais de uma extensão (Ex: exemplo.c.Z).
	- suporta arquivos sem extensão.
	- Nome do arquivo + extensões (não maior que 255 caracteres).

Extensões geralmente são associadas a algum aplicativo.
- \*.doc - Microsoft Word.
- \*.c - Compilador C.

Se diz que *GERALMENTE* são associadas com aplicativos, devido ao fato que, a depender do sistema operacional ele pode, ou não, fazer essa associação.

- Sistemas operacionais base UNIX não associam.
	- Linux faz essa associação, porém só no GUI para maior facilidade de uso.
- Windows associa.

**Figura 4.1**

| Extensão | Significado                                              |
| -------- | -------------------------------------------------------- |
| `.bak`   | Cópia de segurança                                       |
| `.c`     | Código-fonte de programa em C                            |
| `.gif`   | Imagem no formato Graphical Interchange Format           |
| `.hlp`   | Arquivo de ajuda                                         |
| `.html`  | Documento em HTML                                        |
| `.jpg`   | Imagem codificada segundo padrões JPEG                   |
| `.mp3`   | Música codificada no formato MPEG (camada 3)             |
| `.mpg`   | Filme codificado no padrão MPEG                          |
| `.o`     | Arquivo objeto (gerado por compilador, ainda não ligado) |
| `.pdf`   | Arquivo no formato PDF (Portable Document Format)        |
| `.ps`    | Arquivo PostScript                                       |
| `.tex`   | Entrada para o programa de formatação TEX                |
| `.txt`   | Arquivo de texto                                         |
| `.zip`   | Arquivo compactado                                       |

### Estruturas de arquivos

#### Estrutura 1 - Sequência não estruturada de bytes.

S.O não se importa com o conteúdo do arquivo, já que é visto apenas um amontoado de bytes. Sendo assim, o significado deve ser dado pelas aplicações.

Quais as vantagens dessa abordagem?
- Flexibilidade
	- Os usuários colocam o que quiserem
	- Nomeiam arquivos como quiserem
Já que independente do que for feito pelo usuário, para o S.O permanece igual.

Sistemas operacionais que adotam: UNIX, Windows
#### Estrutura 2 - Sequência de registros de tamanho fixo.

Cada arquivos é separado em registros, onde cada registro ocupa a mesma quantidade de bytes no arquivo. Isso significa que mesmo que o conteúdo real seja menor, o espaço é sempre reservado com o mesmo tamanho.

Exemplo:
- Se cada registro tem 100 bytes
	- E são armazenados 10 registro - 1 arquivo de 1000 bytes
	- Isso ocorre mesmo que cada registro só tenha 50 bytes uteis, realmente sendo usados

Leitura/Escrita são realizadas em registros. Então se lê, sobrescreve ou adiciona um registro.

Estrutura de arquivos usadas em S.Os antigos -> mainframes.

- De 80 a 132 caracteres cada registro.
	- 80 caracteres do cartão perfurado.

#### Estrutura 3 - Árvores de registros

Baseado na arquitetura anterior, porém aqui, o tamanho dos registro não é fixo, mas sim variado.

Cada registro possui 1 campo de dados e um de chave, que indica o próximo registro, formando assim uma arquitetura de arvore.

Utilizada em S.Os de mainframes modernos.

### Tipos de arquivos

- Arquivos regulares -> Informações dos usuários.
- Diretórios -> Arquivos para estruturar o sistema de arquivos.
- Arquivos do sistema -> informações do sistema.

###### 1 - ASCII:

*Também podem ser chamados de arquivos de texto.*

- Consistem de linhas de texto com CR+LF.
- Facilitam a integração de programas.
- Podem ser exibidos e impressos como são.
- Podem ser editados em qualquer editor de texto.
- Mais portável e interoperável.

###### 2 - Binário:

*Tudo aquilo que não é um arquivo ASCII*

- Sua estrutura interna é conhecida apenas pelos aplicativos que os usam.
	- Ex: Arquivos executáveis

### Atributos de um arquivo

Além do nome e dos dados os arquivos possuem outras informações, são elas seus atributos (metadados).

O que seriam os atributos?

- Atributos são os metadados mais específicos de cada arquivo como:
	- Quem criou
	- Informações de segurança
		- Permissões de acesso
	- Etc.

| Tipo de Atributo       | Descrição                                                                 |
|------------------------|---------------------------------------------------------------------------|
| 📛 Nome                | Nome do arquivo, incluindo extensão (ex: `documento.txt`)                 |
| 📦 Tamanho             | Quantidade de bytes ocupados pelo arquivo                                 |
| 📅 Data de criação     | Data e hora em que o arquivo foi criado                                   |
| ✏️ Data de modificação | Data e hora da última modificação no conteúdo do arquivo                   |
| 👁️ Data de acesso      | Data e hora do último acesso (leitura) ao arquivo                         |
| 🔐 Permissões          | Indicam quem pode ler, escrever ou executar o arquivo (ex: `rwx`)         |
| 👤 Proprietário        | Usuário que é dono do arquivo                                              |
| 👥 Grupo               | Grupo de usuários associado ao arquivo                                    |
| 🧩 Tipo                | Tipo de arquivo (texto, binário, diretório, link simbólico, etc.)         |
| 📍 Localização         | Caminho no sistema de arquivos (ex: `/home/user/docs/arquivo.txt`)        |
| 🧾 Sistema de arquivos | Tipo de sistema (ex: NTFS, FAT32, ext4, etc.) onde o arquivo está armazenado |
| ⛓️ Link count         | Número de links (hard links) apontando para o mesmo conteúdo               |
| 📄 Atributos especiais | Flags como "somente leitura", "oculto", "sistema", "arquivado" etc.       |

Esses lista de atributos varia de S.O para S.O