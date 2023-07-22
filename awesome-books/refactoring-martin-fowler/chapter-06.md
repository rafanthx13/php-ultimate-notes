# Chapter 06

SITE: https://gist.github.com/cs-cordero/3799f26699bdecdb286fd719f08122af#extract-function-106

Site de código:

https://carbon.now.sh/

Site com imagme e código

https://refactoring.com/catalog/extractFunction.html

Editor

https://languagetool.org/pt-BR

User o languagetool para corrigir no final;
Recorte e inria o texto e depis insira corrigdo no md


## Extract Function (106)

SITE: https://gist.github.com/cs-cordero/3799f26699bdecdb286fd719f08122af#extract-function-106

SITE: Use quando as funções forem muito longas. Código usado mais de uma vez deve ser colocado em sua própria função. Se você se esforçar olhando para um fragmento de código e descobrindo o que ele está fazendo, transformá-lo em uma função com um nome que descreva isso é uma boa ideia.


Extrair função é uma das refatorações mais comuns

Durante minha carreira, já ouvi vários argumentos sobre quando colocar um código em sua própria função. Algumas dessas diretrizes baseavam-se no tamanho: funções não devem ser maiores que o tamanho de uma tela. Outras eram baseadas em reutilização: qualquer código usado mais de uma vez deve ser colocado em sua própria função, mas um código utilizado somente uma vez deve permanecer interno. O argumento que mais faz sentido para mim, no entanto, é a separação entre intenção e implementação. Se você tiver de dispender esforços para observar um fragmento de código e descobrir o que ele faz, então deve extraí-lo em uma função e atribuir-lhe um nome com base no “o quê”. Então, quando o ler novamente, o propósito da função estará evidente, e, na maioria das vezes, você não terá de se preocupar sobre como a função atende ao seu propósito (que está no corpo da função). Após ter aceitado esse princípio, desenvolvi o hábito de escrever funções muito pequenas – tipicamente, com apenas algumas linhas. Para mim, qualquer função com mais de meia dúzia de linhas de código começa a exalar um cheiro, e não é incomum que eu tenha funções com uma única linha de código.

Muitas vezes, vejo fragmentos de código em uma função maior que
começam com um comentário para dizer o que fazem. O comentário
geralmente é uma boa dica para o nome da função quando extraio esse
fragmento.

Nâo se preocupe em a funçâo ser pequena

**RESUMO**

É uma refatoração muito comum. Use quando a função estiver muito longa. Use em código usados mais de uma vez em locais diferentes (evita duplicação). Se você se esforçar olhando pro código para entender o que ele está fazendo, transforme-o em uma função com um bom nome, que descreva bem a intenção.

## Inline Function (115)

**Site Traduzido**


**Motivação**


**Resumo Final**




**Site Traduzido**
Quando o corpo da função é tão autodescritivo quanto o nome. Também é útil como uma etapa intermediária para uma função de extração posterior (106) para refatorar uma refatoração anterior da maneira que você desejar. Ótimo para quando o código usa muita indireção e você se perde em toda a delegação de uma função para outra.

**Motivação**
Um dos temas deste livro é usar funções pequenas cujos nomes mostrem oseu propósito,
 pois essas funções resultam em um código mais claro e mais
fácil de ler. Às vezes, porém, deparo com uma função cujo corpo é tão claro
quanto o nome. Também posso refatorar o corpo do código para que fique tão
claro quanto o nome. Quando isso acontece, posso me livrar da função. Um
acesso indireto pode ser conveniente, mas um acesso indireto desnecessário é
irritante.
Também uso Internalizar função quando tenho um grupo de funções que
pareça estar fatorado de modo ruim. Posso internalizar todas elas em uma
única função grande e, então, extrair as funções novamente do modo que eu
quiser.
É comum usar Internalizar função quando vejo um código que utilize muito
acesso indireto – quando parece que toda função faz uma simples delegação
para outra função, e me perco com todas essas delegações. Talvez valha a
pena ter alguns desses acessos indiretos, mas não todos. Ao fazer uma
internalização, posso preservar os acessos convenientes e eliminar os demais.

**Resumo Final**
Eu internalizo uma função para dentro de outra quando o seu procedimento é tão claro quanto o seu nome. Serve para retirar muita delegação em uma função.

expressões ode podem se tornar muito complexas e difíceis de ler. Semelhante à extração de uma função, Extrair variável (119) dá a uma expressão um nome que pode ser autodescritivo. Pense no contexto da variável. Se for significativo apenas dentro da função, Extrair Variável (119) é uma boa escolha, mas se for útil de forma mais ampla, você pode usar Extrair Função (106) para torná-la mais amplamente disponível.



## Extract Variable (119)

**Site Traduzido**
As expressões de código podem se tornar muito complexas e difíceis de ler. Semelhante à extração de uma função, Extrair variável (119) dá a uma expressão um nome que pode ser autodescritivo. Pense no contexto da variável. Se for significativo apenas dentro da função, Extrair Variável (119) é uma boa escolha, mas se for útil de forma mais ampla, você pode usar Extrair Função (106) para torná-la mais amplamente disponível.

**Motivação**
As expressões podem se tornar muito complexas e difíceis de ler. Em
situações como essas, as variáveis locais podem ajudar a separar a expressão
em partes mais fáceis de lidar. Particularmente, elas possibilitam nomear uma
parte de uma lógica mais complexa. Com isso, posso entender melhor o
propósito do que está acontecendo.

Variáveis como essas também são convenientes para depuração, pois
oferecem um gancho fácil para um depurador usar ou um valor para uma
instrução print capturar.
Se eu estiver considerando usar Extrair variável, significa que quero
acrescentar um nome a uma expressão em meu código.

Depois de decidir que
quero fazer isso, também penso no contexto desse nome. Se ele for
significativo somente dentro da função na qual estou trabalhando, então
Extrair variável será uma boa opção – porém, se fizer sentido em um
contexto mais amplo, considerarei deixar o nome disponível nesse contexto
maior, em geral como uma função. Se o nome estiver disponível de modo
mais amplo, outros códigos poderão usar essa expressão sem ter de repeti-la,resultando em menos duplicação e melhor demonstração de meu propósito.

**Resumo Final**
Juntar um monte de cálculos numa linha pode tornar a expressão muito complexa e de difícil leitura. Usa-se a extração de variável para dar nome as etapas, facilitar a depuração e deixar tudo mais limpo. É recomendável quando o nome for significativo para dentro da função, agora, se esse variável for acessada de fora, é recomendável extrair a variável para uma função, assim outros locais podem ter acesso.


## Inline Variable (123)

**Site Traduzido**
Use quando o nome da variável não comunicar mais que a própria expressão. Na maioria das vezes, esse refatorador é usado como uma etapa intermediária de um refatorador maior.

**Motivação**
As variáveis fornecem nomes para expressões em uma função e, desse modo,
em geral, são boas. Às vezes, porém, o nome não diz realmente nada além do
que diz a própria expressão. Em outras ocasiões, você talvez note que uma
variável está atrapalhando a refatoração do código ao redor. Nesses casos,
pode ser conveniente internalizar a variável.

**Resumo Final**

Use quando o nome da variável não comunica mais do que a própria expressão.


## Change Function Declaration (124)

**Site Traduzido**
O elemento mais importante de uma função para manutenção é seu nome. Se você encontrar um nome que não esteja claro, é imperativo que você o renomeie assim que entender o que a função faz. O mesmo se aplica aos parâmetros de função, uma vez que os parâmetros determinam a interface com o mundo externo. A alteração dos parâmetros também pode beneficiar a redução do acoplamento entre o código que compartilha os dados, mas tenha cuidado! Às vezes, o código de acoplamento é uma coisa boa ao longo do tempo, à medida que o parâmetro e outro código se desenvolvem.

**Motivação**
As funções representam o modo principal de dividir um programa em partes.
As declarações de funções representam como essas partes se encaixam – elas
efetivamente representam as junções em nossos sistemas de software. E,
como em qualquer construção, muita coisa depende dessas junções. Boas
junções me permitem acrescentar novas partes ao sistema com facilidade,
mas junções ruins são uma fonte constante de problemas, tornando mais
difícil entender o que o software faz e como modificá-lo quando minhas
necessidades mudarem. Felizmente, o software, sendo soft, me permite
modificar essas junções, desde que eu faça isso com cuidado.
O elemento mais importante de uma junção como essa é o nome da função.
Um bom nome me permite entender o que a função faz quando a vejo sendo
chamada, sem que eu veja o código que define a sua implementação. No
entanto, pensar em bons nomes é difícil, e raramente penso nos nomes
corretos na primeira tentativa.

 Quando vejo um nome que me deixa confuso,
sinto-me tentado a deixá-lo como está – afinal de contas, é apenas um nome.
Esse é um feito do maléfico demônio Obfuscatis; pela alma de meu
programa, jamais devo dar ouvidos a ele. Se vejo uma função com um nome
incorreto, é mandatório que eu o altere assim que compreender qual seria um
nome melhor. Dessa forma, da próxima vez que eu ver esse código, não terei
de descobrir novamente o que está acontecendo. (Muitas vezes, uma boa
maneira de ter um nome melhor é escrever um comentário para descrever o
propósito da função e, em seguida, transformar esse comentário em um
nome.)

Uma lógica semelhante se aplica aos parâmetros de uma função. Os
parâmetros de uma função determinam como ela se encaixa no restante de
seu mundo. Os parâmetros definem o contexto no qual posso usar uma
função. Se eu tiver uma função para formatar o número de telefone de uma
pessoa e tal função aceitar uma pessoa como argumento, não poderei usá-la
para formatar o número de telefone de uma empresa. Se eu substituir o
parâmetro pessoa pelo número de telefone propriamente dito, então o código
de formatação será útil de modo mais genérico.
Além de aumentar a aplicabilidade da função, posso também eliminar um
pouco do acoplamento, alterando quais módulos precisam se conectar a
outros. A lógica de formatação de números de telefone pode ficar em um
módulo que não tenha conhecimento algum sobre pessoas. Reduzir o númerode módulos que precise conhecer um ao outro ajuda a reduzir a quantidade de
informações que tenho de colocar em meu cérebro quando modifico um
código – e meu cérebro não é mais tão grande quanto costumava ser (isso,
porém, não diz nada sobre o tamanho de seu contêiner).
Escolher os parâmetros corretos não é algo que seja definido com regras
simples. Posso ter uma função simples para determinar se um pagamento
venceu, verificando se já se passaram mais de 30 dias. O parâmetro dessa
função deve ser o objeto pagamento, ou a data de vencimento do pagamento?
Usar o pagamento acopla a função à interface do objeto pagamento. No
entanto, se uso o pagamento, posso facilmente acessar outras propriedades
dele, caso a lógica evolua, sem ter de modificar todas as porções de código
que chamam essa função – essencialmente, aumentando o encapsulamento da
função.
A única resposta correta para esse problema é que não há uma resposta
correta, especialmente com o passar do tempo. Então acho essencial conhecer
Mudar declaração de função para que o código evolua junto com minha
compreensão sobre quais devem ser as melhores junções no código.
Em geral, somente uso o nome principal de uma refatoração quando me
refiro a ela em outros pontos deste livro. Entretanto, como renomear é um
caso de uso muito importante para Mudar declaração de função, se eu estiver
apenas renomeando algo, vou me referir a essa refatoração como Renomear
função para deixar claro o que estou fazendo. Independentemente de eu estar
apenas renomeando ou se estiver manipulando os parâmetros, usarei o
mesmo procedimento.

**Resumo Final**

Renomeio o nome da função ou os seus parâmetros quando eles forem confusos e não são suficientes para descrever o que o procedimento faz.


## Encapsulate Variable (132)

**Site Traduzido**
Os dados podem ser organizados de forma mais compreensível quando as mutações ocorrem como parte das funções. Acrescenta um ponto claro para monitorar mudanças e uso dos dados. Essa é a base para encapsular dados em um objeto e, em seguida, escrever getters e setters.

**Motivação**
A refatoração tem tudo a ver com a manipulação dos elementos de nossos
programas. É mais complicado manipular dados do que manipular funções.
Como usar uma função em geral significa chamá-la, posso facilmente
renomear ou mover uma função enquanto mantenho a função antiga intacta
como uma função de encaminhamento (desse modo, meu código antigo
chama a função antiga, que chama a função nova). Em geral, não mantenho
essa função de encaminhamento por muito tempo, mas ela simplifica a
refatoração.

Com os dados, torna-se um pouco mais complicado porque não é possível
fazer isso. **Se eu mover os dados, tenho de modificar todas as referências a
eles em um único ciclo para manter o código funcionando. Para dados com
um escopo de acesso bem restrito, por exemplo, uma variável temporária em
uma função pequena não será um problema. Contudo, à medida que o escopo
aumenta, o mesmo acontece com o nível de dificuldade, e é por isso que
dados globais são tão problemáticos.**

Assim, se eu quiser mover dados amplamente acessados, com frequência a
melhor abordagem é encapsulá-los antes, efetuando todos os acessos por
meio de funções. Dessa forma, transformo a difícil tarefa de reorganizar
dados na tarefa mais simples de reorganizar funções.

Encapsular dados é importante em outras situações também.

O encapsulamento oferece um ponto claro para monitorar alterações e o uso dos
dados; posso facilmente acrescentar validações ou uma lógica consequente
nas atualizações. Tenho como hábito deixar todos os dados mutáveis
encapsulados dessa forma, deixando-os acessíveis somente por meio de
funções se o seu escopo for mais amplo que uma única função. Quanto maior
o escopo dos dados, mais importante será encapsulá-los. Em minha
abordagem para um código legado, sempre que eu tiver de alterar ou
acrescentar uma nova referência a uma variável desse tipo, aproveito a
oportunidade para encapsulá-la. Dessa forma, evito que haja mais
acoplamento com dados comumente usados.
Esse princípio explica por que a abordagem de orientação a objetos coloca
tanta ênfase em manter privados os dados de um objeto. Sempre que vejo um
campo público, considero usar Encapsular variável (nesse caso, muitas vezes
chamada de Encapsular campo (Encapsulate Field)) para reduzir sua
visibilidade. Algumas pessoas vão além e argumentam que mesmo referências 
internas a campos dentro de uma classe devem se dar por meio de
funções de acesso – uma abordagem conhecida como autoencapsulamento
(self-encapsulation). De modo geral, acho o autoencapsulamento um exagero
– se uma classe é tão grande a ponto de ser necessário autoencapsular seus
campos, ela deveria ser dividida. Contudo, autoencapsular um campo é um
passo conveniente antes de dividir uma classe.
Manter dados encapsulados é muito menos importante para dados
imutáveis. Quando os dados não mudam, não preciso de um lugar para
colocar uma validação ou outros ganchos de lógica antes das atualizações.
Também posso copiar livremente os dados em vez de movê-los – assim, não
preciso alterar as referências nos locais antigos nem me preocupar se há
seções de código lendo dados desatualizados. A imutabilidade é
extremamente eficaz para preservar dados.

**Resumo Final**
Encapsular variável é acrescentar funções para acessar os valores (como getters e setters). O encapsulamento oferece um ponto claro e unificado para vigiar os dados. Martin Folwer encapsula os dados dessa forma quando o dado pode ser acessado em um escopo maior do que uma única função. Quanto maior o escopo, mais importante é encapsular os dados. Esse princípio explica por que a abordagem de orientação a objetos coloca
tanta ênfase em manter privados os dados de um objeto.

## Rename Variable (137)

**Site Traduzido**
Use quando você errar o nome inicialmente e uma renomeação pode ajudar a tornar o código mais autodescritivo. Em funções minúsculas em que a variável é autoevidente pelo contexto, um nome conciso pode ser aceitável, mas campos persistentes que duram mais de uma chamada de função exigem uma nomenclatura mais cuidadosa.

**Motivação**
Dar bons nomes está no coração de uma programação clara. As variáveis
podem fazer muito para explicar minha intenção – se eu lhes der bons nomes.
No entanto, com frequência, crio nomes incorretos – às vezes porque não
penso com o devido cuidado, outras porque minha compreensão sobre o
problema melhora à medida que aprendo mais, e outras ainda porque o
propósito do programa muda como consequência das mudanças nas
necessidades de meus usuários.
Até mais que a maioria dos elementos de programa, a importância de um
nome depende do quão amplamente ele é usado. Uma variável usada em uma
expressão lambda de uma só linha em geral é fácil de entender –
frequentemente uso uma única letra nesse caso, pois o propósito da variável
será claro em seu contexto. Parâmetros de funções pequenas em geral podem
ser concisos pelo mesmo motivo, embora, em uma linguagem dinamicamente
tipada como JavaScript, eu goste de inserir o tipo no nome (por isso, tenho
nomes de parâmetros como aCustomer ).
Campos persistentes que perdurem além da chamada de uma única função
exigem uma nomenclatura mais cuidadosa. É nesse caso que provavelmente
concentro a maior parte de minha atenção.

**Resumo Final**
Dar bons nomes está no coração do CleanCode. Renomeie a varável para tornar o código mais autodescritivo. É obrigatório que campos persistentes que perdurem além da chamada de uma única função tenham uma boa nomenclatura, porém, em função lambda ou parâmetros de função pequena não precisa de tanto rigor.

## Introduce Parameter Object (140)

**Site Traduzido**

Grupos de dados geralmente viajam juntos, aparecendo em função após função como um agrupamento de dados. Muitas vezes, é uma ótima ideia substituí-lo por uma única estrutura de dados. Esse processo pode simplificar bastante a imagem do código.

**Motivação**

Muitas vezes, vejo grupos de dados que estão regularmente juntos,
aparecendo em uma função após outra. Um grupo como esse forma um
agrupamento de dados, e gosto de substituí-lo por uma única estrutura de
dados.

Agrupar dados em uma estrutura é importante porque torna explícito o
relacionamento entre eles. Com isso, reduzo o tamanho das listas de
parâmetros para qualquer função que use a nova estrutura. A estrutura
contribui para que haja consistência, pois todas as funções que a utilizem
terão os mesmos nomes para acessar seus elementos.

No entanto, a verdadeira eficácia dessa refatoração está no modo como ela
permite modificações mais profundas no código. Quando identifico essas
novas estruturas, posso redirecionar o comportamento do programa a fim de
usá-las. Crio funções que captam o comportamento comum nesses dados –
seja como um conjunto de funções comuns ou como uma classe que combine
a estrutura de dados com essas funções. Esse processo pode alterar o quadro
conceitual do código, elevando essas estruturas a novas abstrações que
podem simplificar bastante a minha compreensão sobre o domínio. Quando
isso funciona, os efeitos podem ser surpreendentemente eficazes – mas nada
disso será possível, a menos que eu use Introduzir objeto de parâmetros para
iniciar o processo.

**Resumo Final**
Há dados que sempre andam juntos, até mesmo em chamadas de função. Nesses casos é uma boa ideia substituí-los por uma estrutura de dados (class, list, dict). Esse processo torna explícito a importância deles esterem juntos podendo tornar obrigação eles existirem. Se for classe, pode-se adicionar métodos para tratar esses dados e deixá-los dentro da classe. Assim há um grande ganho se esses dados forem utilizados em outro lugar. Exemplo (data inicial e data final), posso criar uma classe que além de ter esses dados faça diversas operações com ele, assim, ao invés de espalhar pelo projeto operações com essas datas, eu coloco todas elas na classe.

## Combine Functions into Class (144)

**Site Traduzido**
Use quando um grupo de funções opera em conjunto em um corpo de dados comum. Uma alternativa para esse refator é Combine Functions into Transform (149). Use uma classe se a mutabilidade for aceitável ou importante. Uma segunda alternativa é aninhar as funções umas nas outras, mas isso pode dificultar o teste das funções.

**Motivação**
As classes são uma construção fundamental na maioria das linguagens de
programação modernas. Elas associam dados e funções em um ambiente
compartilhado, expondo alguns desses dados e funções a outros elementos do
programa a fim de que haja colaboração. São a construção principal nas
linguagens orientadas a objetos, mas são também úteis em outras abordagens.

Quando vejo um grupo de funções que atua de forma muito próxima em um
corpo comum de dados (em geral, passados como argumentos da chamada de
função), percebo uma oportunidade para criar uma classe. Usar uma classe
deixa o ambiente comum compartilhado por essas funções mais explícito,
permite simplificar as chamadas de função dentro do objeto por meio da
remoção de vários argumentos, além de fornecer uma referência para a
passagem de um objeto como esse a outras partes do sistema.

Além de organizar funções já criadas, essa refatoração também representa
uma boa oportunidade para identificar outras porções de processamento e
refatorá-las em métodos na nova classe.

Outra maneira de organizar funções juntas é usar Combinar funções em
transformação (Combine Functions into Transform). Qual delas deve ser
usada depende do contexto mais amplo do programa. 

Uma vantagem
significativa de usar uma classe é o fato de ela permitir aos clientes alterar os
dados nucleares do objeto, e as derivações permanecem consistentes.
Assim como em uma classe, funções como essas também podem ser
combinadas em uma função aninhada. Em geral, prefiro uma classe a uma
função aninhada, pois pode ser difícil testar funções aninhadas. As classes
também são necessárias quando há mais de uma função no grupo que eu
queira expor aos colaboradores.
Linguagens que não tenham classes como um elemento de primeira classe,
mas têm funções de primeira classe, em geral usam Função como Objeto
(Function As Object) [mf-fao] para oferecer esse recurso.

**Resumo Final**

Use quando um grupo de funções opera juntas sobre os mesmos dados. A nova classe pode dar uma nova perspectiva de mais coisas que podem ser atribuídas a ela.

## Combine Functions into Transform (149)

**Site Traduzido**

O objetivo dessa refatoração é pegar um monte de funções que operam em um grupo de dados e escrever uma função de transformação pura que pega os dados de origem, os clona, opera neles e adiciona novos atributos ou altera o objeto clonado e os retorna. O benefício é que a transformação de dados ocorre em um único local.

**Motivação**

Um software muitas vezes envolve alimentar dados para programas que
calculam várias informações derivadas a partir deles. Esses valores derivados
podem ser necessários em diversos lugares, e esses cálculos com frequência
se repetem nos pontos em que os dados derivados são usados. Prefiro reunir
todos esses dados derivados de modo a ter um local consistente para
encontrá-los e atualizá-los, evitando qualquer lógica duplicada.

Uma forma de fazer isso é usar uma função de dados que aceite os dados
originais como entrada e calcule todos os dados derivados, colocando cada
um desses valores em um campo nos dados de saída. Então, para analisar os
dados derivados, tudo que preciso fazer é olhar para a função de
transformação.

Uma alternativa para Combinar funções em transformação é usar Combinar
funções em classe (Combine Functions into Class), a qual move a lógica para
os métodos de uma classe criada a partir dos dados originais. Qualquer uma
dessas refatorações é útil, e minha opção muitas vezes dependerá do estilo de
programação que já estiver no software. Contudo, há uma diferença
importante: usar uma classe é muito melhor se os dados originais forem
atualizados no código. Usar uma transformação armazena dados derivados no
novo registro, portanto, se os dados originais mudarem, haverá
inconsistências.

Um dos motivos pelos quais gosto de combinar funções é evitar duplicação
na lógica de derivação. Posso fazer isso apenas usando Extrair função
(Extract Function) na lógica; em geral, porém, é difícil encontrar as funções,
a menos que elas sejam mantidas próximas das estruturas de dados nas quais
atuam. Usar uma transformação (ou uma classe) facilita encontrá-las e usá-
las.

**Resumo Final**

Consiste em juntar funções que editam um mesmo dado para uma mesma classe (ou função) e, além disso, fazer com que a transformação seja por valor e não por referência (clona o valor e opera sobre o valor clonado). O benefício é que a transformação de dados ocorre em um único local.

## Split Phase (154)

**Site Traduzido**
Use quando o código estiver lidando com duas coisas diferentes. Por exemplo, suponha que se você receber JSON e um corpo de código operar no objeto JSON com acesso de chave complexo ou mesmo manipulações de string em diferentes expressões, pode ser benéfico dividir a computação em diferentes fases. Neste exemplo, você poderia ter uma primeira fase que analisa a entrada em uma estrutura de dados intermediária que possui atributos facilmente acessíveis para uma segunda fase.

**Motivação**

Quando deparo com um código que lida com duas tarefas diferentes, procuro
uma forma de separá-las em módulos distintos. Eu me empenho em fazer
essa separação porque, caso precise fazer uma alteração, poderei lidar com
cada assunto separadamente, sem ter de manter ambos em minha mente ao
mesmo tempo. Se estiver com sorte, talvez eu tenha de modificar apenas um
módulo, sem precisar me lembrar de nenhum dos detalhes do outro módulo.

Uma das formas mais organizadas de fazer uma separação como essa é
dividir o comportamento em duas fases sequenciais. Um bom exemplo disso
é quando há um processamento cujas entradas não refletem o modelo
necessário para executar a lógica. Antes de começar, você pode transformar
os dados de entrada em um formato conveniente para o seu processamento
principal. Ou pode tomar a lógica que deve ser executada e separá-la em
passos sequenciais, em que cada passo é significativamente diferente quanto
ao que é feito.

O exemplo mais óbvio disso é um compilador. Sua tarefa básica é tomar um
texto (código em uma linguagem de programação) e transformá-lo em um
formato executável (por exemplo, um código-objeto para um hardware
específico). Com o tempo, percebemos que isso pode ser convenientemente
separado em uma cadeia de fases: transformar o texto em tokens, fazer 
parsedos tokens para gerar uma árvore sintática, executar então vários passos para
transformar a árvore sintática (por exemplo, para otimização) e, por fim,
gerar o código-objeto. Cada passo tem um escopo limitado, e posso pensar
em um passo sem compreender os detalhes dos outros passos.

Separar em fases dessa forma é comum em um software de grande porte;
cada uma das várias fases de um compilador pode conter muitas funções e
classes. No entanto, posso executar a refatoração básica de separação em
fases em qualquer fragmento de código – sempre que vir uma oportunidade
para separar o código em diferentes fases de forma conveniente. A melhor
pista é quando diferentes etapas do fragmento de código usam conjuntos de
dados e funções distintos. Ao transformá-los em módulos separados, posso
deixar essa diferença explícita, revelando a diferença no código.

**Resumo Final**

Separe em fases (funções) tarefas diferentes que antes estavam muito juntas. Isso separar responsabilidades e facilita manutenção.





