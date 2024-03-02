# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
A compilação cruzada, ou cross-compiling, é um processo pelo qual o código-fonte de um programa é compilado em um sistema de desenvolvimento que é diferente do sistema de destino no qual o programa será executado. Isso significa que o ambiente de compilação e o ambiente de execução são distintos em termos de arquitetura de hardware, sistema operacional ou ambos. O principal objetivo da compilação cruzada é permitir o desenvolvimento de software para plataformas que não são diretamente compatíveis com o sistema de desenvolvimento utilizado. Por exemplo, você pode desenvolver e compilar um programa em um computador com arquitetura x86 (como um PC) e depois executá-lo em um dispositivo embarcado com uma arquitetura ARM. Isso é especialmente útil em sistemas embarcados, onde os recursos de computação podem ser limitados e não é prático ou viável compilar o código diretamente no dispositivo alvo.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
O código de inicialização, também conhecido como código de startup, é um conjunto de instruções que é executado imediatamente após ligar ou reiniciar um sistema embarcado. Sua finalidade é configurar o ambiente de execução necessário para carregar e executar o restante do software. Isso inclui inicializar e configurar hardware, estabelecer a pilha e heap, configurar o ambiente de execução e carregar o código principal. Em resumo, o código de inicialização garante uma inicialização ordenada e prepara o sistema para a execução do software principal.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
Makefile é um automatizador de processos de compilação que coordena e gerencia diferentes componentes de software para produzir um executável final ou outros artefatos de construção, como bibliotecas compartilhadas. Ele simplifica e automatiza o processo de compilação, garantindo que as dependências entre os arquivos fonte sejam adequadamente gerenciadas e que o software seja construído de forma eficiente e consistente.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
 1. Leitura do Makefile: O utilitário make inicia lendo o arquivo Makefile no diretório atual. Este arquivo contém as regras e instruções para compilar o programa, incluindo as dependências entre os arquivos fonte e os comandos necessários para compilação. 2. Análise das Dependências: make analisa as dependências entre os diferentes arquivos fonte e determina quais partes do código precisam ser recompiladas com base nas datas de modificação dos arquivos e nas regras definidas no Makefile. 3. Execução dos Comandos de Compilação: Para cada parte do programa que precisa ser compilada, make executa os comandos especificados no Makefile. Isso geralmente envolve invocar o compilador (como gcc para C/C++ ou javac para Java) com as opções apropriadas e os arquivos fonte relevantes. 4. Vinculação dos Objetos Compilados: Depois que todas as partes do programa são compiladas com sucesso, make vincula os objetos compilados juntos para formar o executável final. Isso geralmente envolve invocar o linker (como ld para C/C++ ou javac para Java) para combinar os objetos compilados em um único arquivo executável. 5. Conclusão da Compilação: Uma vez que todas as etapas de compilação e vinculação são concluídas sem erros, o utilitário make gera o executável final ou outros artefatos de construção especificados no Makefile.
    
#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
A sintese consiste em:
nome_do_alvo: dependencias
	comandos
#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
As dependências são usadas pelo utilitário make para determinar quando o alvo precisa ser reconstruído.
nome_do_alvo: dependência1 dependência2 ...
	comando1
	comando2
	...
 As dependências representam os arquivos ou outros targets que o target em questão precisa antes de ser construído. Quando o make é executado, ele verifica as datas de modificação dessas dependências em relação ao próprio target. Se alguma dependência tiver uma data de modificação mais recente do que a do target, o make entende que o target precisa ser reconstruído.
 
#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras do Makefile são instruções que especificam o processo para gerar um alvo específico. Dentro desse contexto, as instruções explícitas são aquelas em que os comandos são fornecidos de forma direta para criar um alvo particular. Já as instruções implícitas referem-se às regras padrão integradas ao make, destinadas a compilar e vincular arquivos de tipos específicos.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
O conjunto de diretrizes Thumb representa uma extensão da arquitetura ARM, especialmente otimizada para sistemas embarcados, oferecendo instruções mais condensadas. Essa compactação resulta em economia significativa de espaço de memória e redução do consumo de energia. A arquitetura ARM Cortex-M é compatível tanto com as diretrizes Thumb quanto com as ARM, oferecendo aos desenvolvedores a flexibilidade de escolha da melhor opção conforme as exigências de suas aplicações. O chaveamento entre conjuntos é viabilizado pela instrução "Branch and Link with Exchange" (BLX). Apesar da maior eficiência em termos de compactação das instruções Thumb, em determinados cenários, pode haver uma leve redução no desempenho em comparação com as instruções ARM.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
No modelo de acesso à memória da arquitetura ARM, somente as instruções de carga (LDR) e armazenamento (STR) têm permissão para acessar a memória, enquanto as operações de processamento são exclusivamente conduzidas entre registradores. Já no modelo de registro/memória, as instruções de processamento podem operar diretamente entre registradores, dispensando a necessidade de acessar a memória. As principais discrepâncias entre essas arquiteturas residem no acesso à memória e nas operações dos registradores.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
Os processadores ARM Cortex-M oferecem dois níveis distintos de acesso para a execução de código: o "Thread Mode", utilizado para aplicativos convencionais, e o "Handler Mode", ativado em resposta a exceções e interrupções. Ademais, apresentam diversos modos de operação, como o "User Mode", destinado à execução de aplicativos padrão, e modos privilegiados, tais como o "Handler Mode" e outros, que concedem acesso a recursos específicos para o tratamento de interrupções. Essa arquitetura proporciona uma clara segregação entre a execução de código de aplicativos e as operações do sistema operacional, facilitando o desenvolvimento de sistemas RTOS (Real-Time Operating Systems) mais robustos e responsivos.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
Os processadores ARM Cortex-M gerenciam exceções, como erros ou eventos específicos, e interrupções, como sinais de periféricos, de maneira altamente eficiente. Diversos tipos de exceções são reconhecidos, abrangendo exceções de hardware, sistema e usuário. A priorização é alcançada por meio de um sistema de níveis de prioridade, empregando estratégias de "Group Priority" e "Sub-Priority". A "Group Priority" organiza as exceções em grupos, enquanto a "Sub-Priority" permite uma priorização mais detalhada dentro de cada grupo. Exceções e interrupções de prioridade superior são tratadas com prioridade, e em situações de igualdade, a sub-prioridade determina a sequência de atendimento. Quando uma exceção ou interrupção é acionada, o processador preserva o contexto atual, executa o código associado e, após o tratamento, restaura o contexto e retoma a execução do programa principal. Esse sistema desempenha um papel fundamental na garantia de uma resposta eficiente a eventos críticos em sistemas de tempo real.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
O CPSR (Current Program Status Register) mantém o estado atual do processador durante a execução do programa principal, enquanto o SPSR (Saved Program Status Register) é empregado para temporariamente armazenar o estado do processador durante a ocorrência de exceções. Isso viabiliza uma restauração apropriada do estado anterior do processador após o tratamento das exceções. A presença e o correto funcionamento desses registradores são fundamentais para assegurar uma transição suave entre a execução do código principal e os procedimentos de tratamento de exceções em sistemas embarcados.

### (f) Qual a finalidade do **LR** (***Link Register***)?
O principal propósito do Link Register (LR) é possibilitar que, ao término de uma sub-rotina, o programa retorne à instrução imediatamente subsequente à chamada dessa sub-rotina. Essa funcionalidade é essencial para o controle efetivo do fluxo do programa, particularmente em linguagens que empregam chamadas de função ou procedimentos.

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
O Program Status Register (PSR) em processadores ARM é responsável por armazenar informações críticas sobre o estado atual do processador. Este registro engloba flags de condição, indica o modo de operação, gerencia interrupções, controla o estado Thumb/ARM, e registra a endianness. Tais dados desempenham um papel vital na execução eficiente do código, além de possibilitar respostas apropriadas a diversas condições e eventos durante a execução do programa.

### (h) O que é a tabela de vetores de interrupção?
Trata-se de uma estrutura de dados utilizada em sistemas embarcados conhecida como "tabela de vetores de interrupção". Essa tabela mapeia endereços de memória para os manipuladores de interrupção. Cada entrada na tabela corresponde a um número de interrupção específico, e o conteúdo dessa entrada é o endereço de memória do código responsável por tratar aquela interrupção específica. Essa tabela é essencial para o sistema operacional ou firmware do dispositivo identificar corretamente e direcionar as interrupções para o código apropriado, garantindo uma resposta eficiente e oportuna a eventos externos ou internos.

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
Em aplicações de tempo real, o NVIC (Nested Vectored Interrupt Controller) desempenha uma função crítica ao fornecer um mecanismo eficaz para lidar com eventos assíncronos. A capacidade de aninhar interrupções é especialmente valiosa, permitindo que o sistema responda rapidamente a eventos prioritários sem perder o contexto de execução. Esse recurso é fundamental para garantir o atendimento de requisitos de tempo críticos em sistemas embarcados de tempo real. Ao permitir que interrupções de maior prioridade interrompam o tratamento de interrupções de menor prioridade, o NVIC contribui significativamente para a eficiência e a previsibilidade do sistema em situações onde a resposta rápida é essencial.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
Quando uma exceção, como uma interrupção, ocorre no processador Cortex-M, o registrador LR (Link Register) assume um papel crucial no gerenciamento do retorno dessa exceção. Ao contrário de uma chamada de função convencional, na qual o LR armazena o endereço de retorno, durante uma interrupção, o LR recebe um valor especial denominado EXC_RETURN. Esse valor contém informações essenciais sobre o contexto da pilha, o estado da exceção e outros detalhes relevantes para garantir um retorno adequado. O EXC_RETURN possui um formato específico, e seus diferentes bits indicam aspectos fundamentais, como se a pilha foi ajustada automaticamente durante o tratamento da exceção, se o retorno deve ser realizado para o modo Handler ou Thread, se uma pilha diferente deve ser utilizada no retorno e se o processador deve voltar ao modo Thumb ou ARM. Quando chega o momento de retornar de uma interrupção, o processador utiliza a instrução BX LR, que interpreta o valor armazenado no registrador LR (EXC_RETURN). Com base nos bits relevantes desse valor, o processador executa as ações apropriadas, como ajustar a pilha ou alterar o modo de execução. Esse mecanismo inteligente garante que o Cortex-M retorne eficientemente de uma interrupção, adaptando-se dinamicamente ao contexto no qual a exceção ocorreu, assegurando uma execução consistente e eficiente do programa principal.

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
A principal distinção no salvamento de contexto durante a ocorrência de uma interrupção nos processadores Cortex-M3 e Cortex-M4F reside na presença de registradores de ponto flutuante e no consequente impacto no tempo e no uso da pilha. Nos processadores Cortex-M4F, que possuem suporte a ponto flutuante, há a necessidade de salvar e restaurar os registradores de ponto flutuante adicionais durante o tratamento de interrupções, o que pode resultar em um aumento no tempo de resposta e no consumo de memória da pilha. Uma estratégia configurável conhecida como "lazy stacking" pode ser empregada para otimizar ainda mais o empilhamento dos registradores durante as interrupções. Essa técnica adia o salvamento dos registradores na pilha até que seja realmente necessário, ou seja, até o momento em que ocorra uma alteração nos valores desses registradores. Isso pode reduzir o número de operações de salvamento e restauração realizadas durante o tratamento de interrupções, melhorando assim o desempenho geral do sistema e otimizando o uso da memória da pilha.

## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
