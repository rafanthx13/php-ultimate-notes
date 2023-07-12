# 12 - Dealing with Inheritance

01 - Pull Up Method
02 - Pull Up Field
03 - Pull Up Constructor Body
04 - Push Down Method
05 - Push Down Field
06 - Replace Type Code with Subclasses
07 - Remove Subclass
08 - Extract Superclass
09 - Collapse Hierarchy
10 - Replace Subclass with Delegate
11 - Replace Superclass with Delegate

Print de area da tela no windos: Windos + shift + S

Neste último capítulo, voltarei minha atenção a um dos recursos mais
conhecidos da programação orientada a objetos: a herança. Como qualquer
mecanismo eficaz, a herança é muito útil, mas também fácil de ser usada
indevidamente, e, com frequência, é difícil ver esse uso indevido antes que
seja tarde demais.

Muitas vezes, é necessário mover funcionalidades para cima ou para baixo
na hierarquia de herança. Várias refatorações lidam com isso: Subir método
(Pull Up Method), Subir campo (Pull Up Field), Subir corpo do construtor
(Pull Up Constructor Body), Descer método (Push Down Method) e Descer
campo (Push Down Field). Posso adicionar e remover classes da hierarquia
com Extrair superclasse (Extract Superclass), Remover subclasse (Remove
Subclass) e Condensar Hierarquia (Collapse Hierarchy). Posso acrescentar
uma subclasse a fim de substituir um campo que estou usando para acionar
um comportamento distinto com base em seu valor; faço isso com Substituir
código de tipos por subclasses (Replace Type Code with Subclasses).

A herança é uma ferramenta eficaz: às vezes, porém, ela acaba sendo usada
no lugar errado – ou o local em que ela é usada torna-se inapropriado. Nesse
caso, uso Substituir subclasse por delegação (Replace Subclass with
Delegate) ou Substituir superclasse por delegação (Replace Superclass with
Delegate) para transformar a herança em delegação.


**Traduzido**

**Motivação**

**Resumo**


## 01 - Pull Up Method

**Traduzido**

Inverso do Método Push Down (359). Use para reduzir qualquer duplicação de código entre classes "irmãs". Aumentar o método para um pai comum, por definição, removerá a duplicação. Normalmente, para fazer esta refatoração, você terá que fazer outras refatorações também.

Como uma palavra de advertência, Fowler observa que a versão mais complicada disso é quando o corpo de um dos métodos se refere a atributos que estão em uma subclasse, mas não na superclasse. Quando isso acontecer, ele alcançará primeiro o campo Pull Up (353).

**Motivação**

Eliminar código duplicado é importante. Dois métodos duplicados podem
funcionar bem como estão, mas nada mais serão além de um terreno fértil
para bugs no futuro. Sempre que houver duplicação, haverá risco de uma
alteração em uma cópia não ser feita na outra. Em geral, é difícil encontrar as
duplicatas.

É mais fácil usar Subir método quando os métodos têm o mesmo corpo, o
que implica que houve uma operação de copiar e colar. É claro que nem
sempre a situação é assim tão evidente. Eu poderia apenas fazer a refatoração
e ver se os testes acusam erro – mas isso significa depositar muita confiança
em meus testes. Em geral, acho importante procurar as diferenças – muitas
vezes elas exibem comportamentos para os quais esqueci de criar testes.
Frequentemente, Subir método é aplicada depois de outros passos. Vejo dois
métodos em classes diferentes, que podem ser parametrizados de tal modo
que acabam sendo, essencialmente, o mesmo método. Nesse caso, o passo
mais rápido será aplicar Parametrizar função (Parameterize Function)
separadamente e, em seguida, Subir método.

A pior das complicações com Subir método ocorre se o corpo do método
referenciar recursos que estão na subclasse, mas não na superclasse. Se isso
acontecer, tenho de usar Subir campo (Pull Up Field) e Subir método nesses
elementos antes.

Se eu tiver dois métodos com um fluxo geral semelhante, mas que diferem
quanto a detalhes, considerarei o uso de Formar método de template (Form
Template Method) [mf-ft].

**Resumo**

Faça Pull Up (suba o método da classe filho para o pai) quando os irmãos tem o mesmo método e assinatura.  Isso reduz a duplicação, pois basta chamar o do pai. Só não dá para fazer isso quando cada subclasse usa um atributo próprio no método. Se eu tiver dois métodos com um fluxo geral semelhante, mas que diferem quanto a detalhes, posso considerar usar Template Method.

## 02 - Pull Up Field

**Traduzido**

Inverso do Campo Push Down (361). Use pelas mesmas razões que o Método Pull Up (350): para reduzir a duplicação de código entre as classes "irmãos".

**Motivação**

Se as subclasses forem desenvolvidas de forma independente, ou se forem
combinadas por meio de refatoração, muitas vezes percebo que há duplicação
de funcionalidades. Em particular, determinados campos podem estar
duplicados. Campos como esses às vezes têm nomes semelhantes – mas nem
sempre. A única maneira pela qual posso dizer o que está acontecendo é
observar os campos e analisar como estão sendo usados. Se forem usados de
modo semelhante, posso subi-los para a superclasse.

Ao fazer isso, reduzo a duplicação de duas formas. Removo a declaração de
dados duplicada e posso, então, mover comportamentos que usem o campo,
das subclasses para a superclasse.

Muitas linguagens dinâmicas não precisam definir campos como parte da
definição de suas classes – em vez disso, os campos passam a existir quando
recebem valor pela primeira vez. Nesse caso, subir um campo é
essencialmente uma consequência de Subir corpo do construtor (Pull Up
Constructor Body).


**Resumo**
Use pelas mesmas razões que o Método Pull Up: para reduzir a duplicação de código entre as classes "irmãos".

## 03 - Pull Up Constructor Body

**Traduzido**

Este é basicamente um caso especial do Método Pull Up (350), específico para métodos construtores já que para muitas linguagens o construtor é muito importante. O que isso parece é mover o comportamento comum para uma superclasse e, em seguida, fazer com que as subclasses chamem super() ou alguma linguagem equivalente.

**Motivação**

Construtores são elementos ardilosos. Eles não são métodos muito comuns –
portanto há mais restrições quanto ao que posso fazer com eles.

Se vejo métodos com um comportamento comum nas subclasses, minha
primeira ideia é usar Extrair função (Extract Function), seguida de Subir
método (Pull Up Method), movendo o código tranquilamente para a
superclasse. Os construtores complicam isso – porque eles têm regras
especiais sobre o que pode ser feito e em qual ordem, portanto uma
abordagem um pouco diferente é necessária.

Se essa refatoração começar a ficar confusa, lanço mão de Substituir
construtor por função de factory (Replace Constructor with Factory
Function).

**Resumo**

Este é basicamente um caso especial do Método Pull Up (350), específico para métodos construtores já que para muitas linguagens o construtor é muito importante. O que isso parece é mover o comportamento comum para uma superclasse e, em seguida, fazer com que as subclasses chamem super() ou alguma linguagem equivalente.


## 04 - Push Down Method

**Traduzido**

Método inverso do pull up (350). Use isso quando um determinado comportamento for específico para uma das subclasses e não para todas as subclasses. Como advertência, essa refatoração só se aplica se o chamador souber que está trabalhando com a subclasse relevante. Se ele não souber ou não puder saber disso, você deve procurar Substituir condicional por polimorfismo (272).

**Motivação**

Se um método for relevante somente para uma subclasse (ou para uma
pequena parcela das subclasses), removê-lo da superclasse e colocá-lo apenas
na(s) subclasse(s) deixará esse código mais claro. Só será possível fazer essa
refatoração se quem fizer a chamada souber que está trabalhando com uma
subclasse em particular – caso contrário, será necessário usar Substituir
condicional por polimorfismo (Replace Conditional with Polymorphism),
com algum comportamento placebo na superclasse.

**Resumo**

Se um método for relevante somente para uma subclasse (ou para uma
pequena parcela das subclasses), removê-lo da superclasse e colocá-lo apenas
na(s) subclasse(s) deixará esse código mais claro. Só será possível fazer essa
refatoração se quem fizer a chamada souber que está trabalhando com uma
subclasse em particular – caso contrário, será necessário usar Substituir
condicional por polimorfismo (Replace Conditional with Polymorphism),
com algum comportamento placebo na superclasse.

## 05 - Push Down Field

**Traduzido**

Inverso do Campo Push Up (353). Use pela mesma razão que o Método Push Down (359). Se uma subclasse específica se preocupa com um campo e mais de seus "irmãos" não, mova o campo para essa subclasse.

**Motivação**

Se um campo for usado somente por uma subclasse (ou por uma pequena
parcela das subclasses), posso mover esse campo para essa(s) subclasse(s).

**Resumo**
Se uma subclasse específica se preocupa com um campo e mais de seus "irmãos" não, mova o campo para essa subclasse.

## 06 - Replace Type Code with Subclasses

**Traduzido**

Inverso de Remover subclasse (369). Use quando você tem uma classe que possui um atributo especial que indica algum tipo de "tipo" enumerado e muitos de seus outros comportamentos dependem do valor dessa variável de tipo.

**Motivação**

Sistemas de software muitas vezes precisam representar diferentes tipos de
itens parecidos. Posso classificar funcionários (employees) de acordo com
seu tipo de emprego (engenheiro [engineer], gerente [manager], vendedor
[salesman]), ou pedidos conforme a sua prioridade (rápida [rush], comum
[regular]). Minha primeira ferramenta para lidar com isso é ter algum tipo de
campo com um código de tipo – dependendo da linguagem, pode ser um
enumerado, um símbolo, uma string ou um número. Com frequência, esse
código de tipo será proveniente de um serviço externo que disponibilize os
dados com os quais estou trabalhando.

Na maioria das vezes, um código de tipo como esse é o necessário. No
entanto, há duas situações em que eu poderia ter algo a mais, e esse algo a
mais são as subclasses. Dois aspectos são particularmente atraentes no que
diz respeito às subclasses. Em primeiro lugar, elas me permitem usar
polimorfismo para lidar com lógicas condicionais. Acho isso muito
conveniente quando tenho diversas funções que chamam diferentes
comportamentos, de acordo com o valor do código de tipo. Com subclasses,
posso aplicar Substituir condicional por polimorfismo (Replace Conditional
with Polymorphism) nessas funções.

O segundo caso é aquele em que tenho campos ou métodos válidos somente
para valores específicos de um código de tipo, por exemplo, uma quota de
vendas que é aplicável somente ao código de tipo “salesman” (vendedor).
Posso então criar a subclasse e aplicar Descer campo (Push Down Field).
Embora eu possa incluir uma lógica de validação para garantir que um campo
seja usado somente quando o código de tipo tiver o valor correto, usar uma
subclasse deixa o relacionamento mais explícito.

Ao usar Substituir código de tipos por subclasses, devo considerar se vou
aplicá-la diretamente na classe que estou considerando, ou no próprio código
de tipo. Faço com que engenheiro (engineer) seja um subtipo de funcionário
(employee), ou devo criar uma propriedade para tipo de funcionário na classe
funcionário, que poderá ter subtipos para engenheiro e para gerente
(manager)? Usar subclasses diretas é mais simples, mas não poderei usá-las
para o tipo de trabalho caso eu precise delas para outras tarefas. Também não
posso usar subclasses diretas se o tipo for mutável. Se for necessário mover
as subclasses para uma propriedade associada ao tipo do funcionário, poderei
fazer isso usando Substituir primitivo por objeto (Replace Primitive with
Object) no código de tipo, de modo a criar uma classe para o tipo do
funcionário, e então usar Substituir código de tipos por subclasses nessa nova
classe.

**Resumo**
Use quando você tem uma classe que possui um atributo especial que indica algum tipo de "tipo" enumerado e muitos de seus outros comportamentos dependem do valor dessa variável de tipo. Ao invés de passar por parâmetro, crie classes para cada tipo.

## 07 - Remove Subclass


**Traduzido**

Inverso de Substituir Código de Tipo por Subclasses (362). As subclasses perdem seu valor à medida que as variações que suportam são movidas para outros lugares ou removidas completamente. Às vezes, as subclasses foram criadas antecipando recursos que nunca acabam sendo construídos ou construídos de forma que não precisem da subclasse.

Uma subclasse que faz muito pouco é dispendiosa e, portanto, é melhor remover a subclasse, substituindo-a por um campo na superclasse.

**Motivação**

As subclasses são úteis. Elas oferecem suporte para variações em estruturas
de dados e para um comportamento polimórfico. São uma ótima maneira de
programar com base na diferença. Contudo, um sistema de software evolui e
as subclasses podem perder seu valor à medida que as variações tratadas por
elas são movidas para outros lugares ou são totalmente removidas. Às vezes,
subclasses são acrescentadas em antecipação a funcionalidades que jamais
chegam a ser implementadas ou que acabam sendo construídas de modo que
não precisam das subclasses.

Há um custo para compreender uma subclasse, e, se ela fizer muito pouco,
não valerá mais a pena tê-la. Quando esse momento chegar, é melhor
remover a subclasse, substituindo-a por um campo em sua superclasse.

**Resumo**

Uma subclasse que faz muito pouco é dispendiosa e, portanto, é melhor remover a subclasse, substituindo-a por um campo na superclasse. Isso pode acontecer porque às vezes, as subclasses foram criadas antecipando recursos que nunca acabam sendo construídos ou construídos de forma que não precisem da subclasse.

## 08 - Extract Superclass

**Traduzido**

Use quando notar duas classes fazendo coisas semelhantes para extrair o comportamento comum para uma superclasse.

**Motivação**

Se eu vir duas classes fazendo tarefas parecidas, posso tirar proveito do
mecanismo básico de herança para extrair suas semelhanças e inseri-las em
uma superclasse. Posso usar Subir campo (Pull Up Field) para mover dados
comuns para a superclasse, e Subir método (Pull Up Method) para mover
comportamentos comuns.

Muitos que escrevem sobre orientação a objetos tratam a herança como algo
que deve ser cuidadosamente planejado com antecedência, com base em
algum tipo de estrutura de classificação do “mundo real”. Estruturas de
classificação como essas podem ser uma pista para usar herança – porém,
com a mesma frequência, a herança é algo que percebo durante a evolução de
um programa, à medida que identifico elementos comuns que eu gostaria de
manter juntos.

Uma alternativa a Extrair superclasse é Extrair classe (Extract Class).
Nesse caso, você tem essencialmente uma escolha entre usar herança ou
delegação como uma forma de unificar comportamentos duplicados. Em
geral, Extrair superclasse é a abordagem mais simples, portanto farei isso
antes, sabendo que poderei usar Substituir superclasse por delegação
(Replace Superclass with Delegate) caso seja necessário no futuro.

**Resumo**

Use quando notar duas classes fazendo coisas semelhantes para extrair o comportamento comum para uma superclasse que seja pai das duas.

## 09 - Collapse Hierarchy

**Traduzido**

Use quando você determinar que uma classe e seu pai não são mais diferentes o suficiente para mantê-los diferentes.

**Motivação**

Quando estiver refatorando uma hierarquia de classes, com frequência subo e
desço recursos. À medida que a hierarquia evolui, às vezes percebo que uma
classe e sua classe-pai já não são mais tão diferentes para justificar mantê-las
separadas. Nesse ponto, eu as combinarei.

**Resumo**

Use quando você determinar que uma classe e seu pai não são mais diferentes o suficiente para mantê-los diferentes. Nesse caso, una os dois.

## 10 - Replace Subclass with Delegate

**Traduzido**

Às vezes, você deseja abortar o uso de herança. A herança permite apenas um único eixo de variação. Se você quiser variar uma classe de pessoas com base em se eles são jovens ou velhos e também se eles são pobres ou ricos, você não pode fazer isso apenas com herança. A herança também apresenta um relacionamento muito próximo entre as classes. Qualquer alteração em uma classe pai pode facilmente interromper os filhos.

Essa refatoração está muito próxima de dar suporte ao mantra "Favorecer a composição de objetos em detrimento da herança de classes". Fowler chama de "composição de objeto" o mesmo que ele chama de delegado.

**Motivação**

Se houver alguns objetos cujos comportamentos variem conforme a categoria
do objeto, o mecanismo natural para expressar isso será a herança. Coloco
todos os dados e comportamentos comuns na superclasse e deixo que cada
subclasse adicione e sobrescreva os recursos à medida que for necessário.
Linguagens orientadas a objetos simplificam essa implementação e, portanto,
esse é um mecanismo conhecido.

Apesar disso, a herança tem suas desvantagens. A mais óbvia é que ela é
uma cartada que só pode ser usada uma única vez. Se houver mais de um
motivo para variar algo, a herança poderá ser usada somente em um único
eixo de variação. Desse modo, se eu quiser variar o comportamento das
pessoas de acordo com a categoria idade e o seu nível de renda, poderei ter
subclasses para jovens e idosos, ou para ricos e pobres – mas não para ambos.
Outro problema é que a herança introduz um relacionamento muito íntimo
entre as classes. Qualquer mudança que eu quiser fazer na classe-pai poderá
facilmente causar erros nas classes-filhas, portanto tenho de ser cuidadoso e
entender como as filhas derivam da superclasse. Esse problema piora quando
a lógica das duas classes estiver em módulos distintos e houver equipes
diferentes responsáveis por esses módulos.

A delegação cuida desses dois problemas. Posso delegar para várias classes
diferentes por diferentes motivos. A delegação é um relacionamento comum
entre objetos – assim, é possível ter uma interface clara com a qual trabalhar,
o que significa muito menos acoplamento do que haveria com subclasses.
Desse modo, é comum deparar com os problemas consequentes do uso de
subclasses e aplicar Substituir subclasse por delegação.

Há um princípio conhecido que diz: “Prefira composição de objetos à
herança de classe” (em que composição é efetivamente o mesmo que
delegação). Muitas pessoas entendem isso como “herança deve ser
considerada prejudicial”, e argumentam que a herança não deve ser jamais
usada. Eu uso herança frequentemente, em parte porque sei que sempre posso
usar Substituir subclasse por delegação caso tenha de fazer uma mudança
depois. A herança é um mecanismo importante, e é apropriada à tarefa na
maioria das vezes, sem que apresente problemas. Assim, lanço mão dela
antes, e passo para a delegação se ela começar a mostrar problemas. Esse uso,
na verdade, é consistente com o princípio – extraído do livro da Gangue dos
Quatro (Gang of Four) [gof], que explica como a herança e a composição
funcionam juntas. O princípio foi uma reação ao uso excessivo da herança.

Aqueles que têm familiaridade com o livro da Gangue dos Quatro podem
achar conveniente pensar nessa refatoração como uma substituição de
subclasses pelos padrões State (Estado) e Strategy (Estratégia). Esses dois
padrões são estruturalmente iguais, contando com um host fazendo a
delegação para uma hierarquia separada. Nem todos os casos de Substituir
subclasse por delegação envolvem uma hierarquia de herança para a
delegação (como mostra o primeiro exemplo a seguir), mas definir uma
hierarquia para os estados ou as estratégias muitas vezes será conveniente.

**Resumo**

Se você quer ou precise que uma classe tenha uma alta variabilidade, ao invés de criar uma classe para cada variação você coloca toda essa variabilidade em atributos ou até mesmo em composição. Lembre-se: prefira composição de objetos à herança de classe.

## 11 - Replace Superclass with Delegate

**Traduzido**

Use quando alguns, mas não todos os métodos da superclasse não fizerem sentido na subclasse. Por exemplo, no início da história da Ciência da Computação, eles costumavam herdar List em um objeto Stack. O problema era que o objeto Stack tinha todos os métodos que uma List teria, e muitos desses métodos não são aplicáveis a uma Stack.

**Motivação**

Em programas orientados a objetos, a herança é uma forma simples e eficaz
de reutilizar funcionalidades. Herdo de alguma classe existente, e então
sobrescrevo e acrescento outros recursos. Porém, a criação de subclasses
pode ser feita de um modo que resulte em confusão e em complicações.
Um dos exemplos clássicos de uso indevido de herança no início da era dos
objetos era fazer com que uma pilha (stack) fosse uma subclasse de lista
(list). A ideia que levava a isso era a reutilização da armazenagem de dados e
das operações para manipular a lista. Embora fosse bom reutilizar código,
essa herança apresentava um problema: todas as operações de lista estavam
presentes na interface da pilha, embora a maioria delas não lhe fosse
aplicável. Uma abordagem melhor é fazer com que a lista seja um campo da
pilha e delegar as operações necessárias a ela.

Esse é um exemplo de um dos motivos para usar Substituir superclasse por
delegação – se as funções da superclasse não fizerem sentido na subclasse, é
sinal de que eu não deveria estar usando herança para ter as funcionalidades
da superclasse.

Além de usar todas as funções da superclasse, também deve ser verdade que
toda instância da subclasse é uma instância da superclasse, e ela deve ser um
objeto válido em todos os casos em que estivermos usando a superclasse. Se
eu tiver uma classe para o modelo de um carro, com informações como nome
e capacidade do motor, posso pensar que seria possível reutilizar esses
recursos para representar um carro físico, adicionando funções para o
Número de Identificação do Veículo (VIN number) e para a data de
fabricação. Esse é um erro de modelagem comum, muitas vezes sutil, que
chamo de homônimo entre tipo e instância (type-instance homonym) [mftih].

Ambos são exemplos de problemas que resultam em confusão e em erros –
esses podem ser facilmente evitados substituindo a herança por delegação
para um objeto distinto. Usar delegação deixa claro que o objeto é diferente –
um objeto para o qual somente algumas das funções se aplicam.
Mesmo nos casos em que a subclasse seja uma opção razoável de
modelagem, uso Substituir superclasse por delegação porque o
relacionamento entre uma subclasse e uma superclasse é altamente acoplado,
com a subclasse apresentando falhas facilmente como consequência de
mudanças na superclasse. A desvantagem é a necessidade de escrever um
método de encaminhamento para qualquer função que seja igual no host e na
classe de delegação – felizmente, porém, apesar de ser tedioso escrever essas
funções de encaminhamento, elas são muito simples, e será muito difícil
cometer erros aí.

Como consequência disso tudo, algumas pessoas aconselham a evitar
totalmente a herança – mas não concordo. Desde que as condições
semânticas apropriadas se apliquem (todo método do supertipo se aplica ao
subtipo, toda instância do subtipo é uma instância do supertipo), a herança é
um mecanismo simples e eficaz. Posso facilmente aplicar Substituir
superclasse por delegação caso a situação mude e a herança deixe de ser a
melhor opção. Assim, meu conselho é usar herança (na maioria das vezes)
antes, e aplicar Substituir superclasse por delegação quando (e se) ela se
tornar um problema

**Resumo**

???. Use quando alguns, mas não todos os métodos da superclasse não fizerem sentido na subclasse. Por exemplo, no início da história da Ciência da Computação, eles costumavam herdar List em um objeto Stack. O problema era que o objeto Stack tinha todos os métodos que uma List teria, e muitos desses métodos não são aplicáveis a uma Stack.
