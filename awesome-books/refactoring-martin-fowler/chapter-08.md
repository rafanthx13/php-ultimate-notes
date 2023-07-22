# Chapter 08

Move Function (198)
Move Field (207)
Move Statements into Function (213)
Move Statements to Callers (217)
Replace Inline Code with Function Call (222)
Slide Statements (223)
Split Loop (227)
Replace Loop with Pipeline (231)
Remove Dead Code (237)

Até agora, as refatorações estavam relacionadas a criar, remover e renomear
elementos de programa. Outra parte importante da refatoração é mover
elementos entre contextos. Uso Mover função (Move Function) para mover
funções entre classes e outros módulos. Campos também podem ser movidos
com Mover campo (Move Field).

Posso igualmente mover instruções individuais. Uso Mover instruções para
uma função (Move Statements into Function) e Mover instruções para os
pontos de chamada (Move Statements to Callers) para movê-las para dentro
ou para fora de funções, assim como Deslocar instruções (Slide Statements)
para movê-las no interior de uma função. Às vezes, posso tomar algumas
instruções que correspondam a uma função existente e usar Substituir código
internalizado por chamada de função (Replace Inline Code with Function
Call) para remover a duplicação.

Duas refatorações que uso frequentemente com laços são Dividir laço (Split
Loop), para garantir que um laço faça apenas uma tarefa, e Substituir laço por
pipeline (Replace Loop with Pipeline), para me livrar totalmente de um laço.

Por fim, temos a refatoração preferida de muitos bons programadores:
Remover código morto (Remove Dead Code). Não há nada tão satisfatório
quanto aplicar o lança-chamas digital em instruções supérfluas.

## Move Function

**Site Traduzido**
Mova uma funâo de um lugar para outro  para garantir que os elementos de software relacionados sejam agrupados e os links entre eles sejam fáceis de encontrar e entender. Também use isso quando as funções referenciarem elementos em outros contextos além daquele em que residem atualmente. Ou use-o quando precisar tornar alguma função mais fácil de chamar.

**Motivação**
O coração de um bom design de software é a sua modularidade – que é minha
capacidade de fazer a maioria das modificações em um programa tendo de
compreender somente uma pequena parte dele. Para alcançar essa
modularidade, é necessário garantir que elementos de software relacionados
estejam agrupados e as ligações entre eles sejam fáceis de encontrar e de
entender. No entanto, minha compreensão de como fazer isso não é estática –
à medida que entendo melhor o que estou fazendo, aprendo a agrupar melhor
os elementos de software. Para que essa compreensão crescente se reflita no
código, devo mover os elementos.


Todas as funções estão em algum contexto; este pode ser global, mas, em
geral, é alguma espécie de módulo. Em um programa orientado a objetos, o
contexto principal dos módulos é uma classe. Aninhar uma função em outra
cria outro contexto comum. Diferentes linguagens oferecem formas variadas
de modularidade, cada qual criando um contexto para uma função ser
inserida.

Um dos motivos mais óbvios para mover uma função é quando ela
referencia mais elementos de outros contextos do que do contexto em que se
encontra no momento. Movê-la para junto desses elementos com frequência
melhora o encapsulamento, permitindo que outras partes do software sejam
menos dependentes dos detalhes desse módulo.

De modo semelhante, posso mover uma função por causa do local em que
estão suas chamadas, ou de onde devo chamá-la em minha próxima melhoria
do código. Uma função definida como auxiliar dentro de outra função pode
ter valor por si só, portanto valerá a pena movê-la para outro lugar mais
acessível. Um método de uma classe talvez seja mais facilmente usado se for
movido para outra classe.

A decisão de mover uma função raramente é fácil. Para me ajudar a decidir,analiso o contexto atual e o contexto candidato para receber essa função. É
necessário observar as funções que chamam essa função, as que são
chamadas pela função sendo movida e quais dados ela utiliza. Muitas vezes,
percebo que preciso de um novo contexto para um grupo de funções, e crio
um usando Combinar funções em classe (Combine Functions into Class) ou
Extrair classe (Extract Class). Embora seja difícil decidir qual é o melhor
lugar para uma função, quanto mais difícil for essa escolha, em geral menos
importante ela será. Acho relevante tentar trabalhar com funções em um
contexto, sabendo que aprenderei até que ponto elas serão apropriadas a esse
contexto; caso não sejam, é sempre possível movê-las depois.

**Resumo Final**
Mova uma função de um lugar para outro para garantir que os elementos de software relacionados sejam agrupados e os links entre eles sejam fáceis de encontrar e entender. Também use isso quando as funções referenciarem elementos em outros contextos além daquele em que residem atualmente. Ou use-o quando precisar tornar alguma função mais fácil de chamar.


## Move Field

**Site Traduzido**
Use assim que perceber que uma determinada estrutura de dados não está correta. Deixar as estruturas de dados com problemas continuará a confundir os leitores e usuários da estrutura de dados no futuro. Use também quando achar que sempre precisa passar um campo de um registro sempre que passar outro registro para uma função.

**Motivação**

A programação envolve escrever muito código para implementar
comportamentos – mas a força de um programa na verdade se encontra emsuas estruturas de dados. Se eu tiver um bom conjunto de estruturas de dados
apropriadas ao problema, meu código que implementa os comportamentos
será simples e organizado. Contudo, estruturas de dados ruins resultam em
muito código cuja tarefa é apenas lidar com dados ruins. E não é somente um
código confuso que é mais difícil de entender; significa também que as
estruturas de dados encobrirão o que o programa faz.

Desse modo, as estruturas de dados são importantes – mas, como na maioria
dos casos em programação, é difícil criá-las corretamente. Faço uma análise
inicial a fim de determinar as melhores estruturas de dados possíveis, e
percebo que experiência e técnicas como design orientado a domínios têm
melhorado minha habilidade para fazer isso. Todavia, apesar de todas as
minhas habilidades e experiência, ainda noto que, com frequência, cometo
erros nesse design inicial. Durante o processo da programação, aprendo mais
sobre o domínio do problema e minhas estruturas de dados. Uma decisão de
design que seja razoável e correta em uma semana poderá se tornar incorreta
em outra.

Assim que percebo que uma estrutura de dados não está correta, é essencial
alterá-la. Se eu deixar minhas estruturas de dados com defeitos, eles
confundirão meu raciocínio e complicarão meu código muito além no futuro.
Posso procurar mover dados ao perceber que tenho sempre de passar um
campo de um registro quando passo outro registro para uma função. Seria
melhor que porções de dados que são sempre passadas em conjunto
estivessem em um único registro para que seu relacionamento esteja claro. A
mudança também é um fator a ser considerado: se uma mudança em um
registro fizer com que um campo de outro registro também mude, é sinal de
que há um campo no lugar errado. Se eu tiver de atualizar o mesmo campo
em várias estruturas, é sinal de que esse campo deve ser movido para outro
lugar, de modo que precise ser atualizado somente uma vez.

Em geral, executo Mover campo no contexto de um conjunto mais amplo de
mudanças. Depois que movo um campo, percebo que, para muitos usuários
desse campo, seria melhor acessar os dados por meio do objeto final em vez
de usar o código original. Então os altero depois, com refatorações. De modo
semelhante, talvez eu descubra que não é possível executar Mover campo no
momento em virtude do modo como os dados estão sendo usados. É
necessário refatorar alguns padrões de uso antes, e então mover o código.

Em minha descrição até agora, menciono “registro”, mas tudo isso é válido
para classes e objetos também. Uma classe é um tipo de registro com funções
associadas – e elas precisam se manter saudáveis tanto quanto qualquer outro
dado. As funções associadas facilitam mover os dados, pois eles estão
encapsulados por métodos de acesso. Posso mover os dados, modificar os
métodos de acesso, e os clientes desses métodos continuarão funcionando.
Assim, essa é uma refatoração mais fácil de fazer se você tiver classes, e
minha descrição a seguir parte desse pressuposto. Se eu estiver usando
registros comuns, sem suporte para encapsulamento, ainda é possível fazer
uma modificação como essa, porém será mais complicado.

**Resumo Final**


## Move Statements into Function

**Resumo**
Se certas instruções estiverem sempre localizadas no local da chamada de uma função, é hora de mover as instruções para a função. Ao fazer isso, as instruções que se movem para a função devem fazer sentido apenas dentro do contexto da função. Use se isso reduzir a duplicação de código. Procure a oportunidade de usar isso observando os locais de chamada de uma função. Ao fazer isso, as instruções que se movem para a função devem fazer sentido apenas dentro do contexto da função.

**Site Traduzido**
Inverso de instruções de movimento para chamadores (217). Use se isso reduzir a duplicação de código. Procure a oportunidade de usar isso observando os locais de chamada de uma função. Se certas instruções estiverem sempre localizadas no local da chamada, é hora de mover as instruções para a função. Ao fazer isso, as instruções que se movem para a função devem fazer sentido apenas dentro do contexto da função.

**Motivação**
Remover duplicação é uma das melhores regras gerais de um código
saudável. Se eu vir o mesmo código executado sempre que chamar uma
função em particular, procurarei combinar esse código repetido na própria
função. Dessa forma, quaisquer modificações futuras no código repetido
poderão ser feitas em um só lugar e usadas por todos que o chamam. Caso o
código precise variar no futuro, posso facilmente o mover (ou parte dele) de
novo usando Mover instruções para os pontos de chamada (Move Statements
to Callers).

Movo instruções para uma função quando posso compreender melhor essas
instruções como parte da função chamada. Se elas não fizerem sentido comoparte dessa função, mas devam ser chamadas com ela, basta usar Extrair
função (Extract Function) nas instruções e na função chamada. É
essencialmente o mesmo processo que descrevo a seguir, mas sem os passos
para internalizar e renomear. Não é incomum fazer isso, e então, depois de
refletir melhor, executar esses passos finais.

**Resumo Final**


## Move Statements to Callers




**Site Traduzido**
Inverso de Mover Instruções para Função (213). As funções devem ser uma unidade atômica de alguma ação. Quando o comportamento comum usado em vários locais precisa variar ligeiramente em cada um de seus locais de chamada, é hora de mover o código variável de uma função para os locais de chamada.

**Motivação**
As funções são o bloco de construção básico das abstrações que
implementamos como programadores. E como qualquer abstração, nem
sempre definimos as fronteiras corretamente. À medida que as
funcionalidades de uma base de código mudam – como ocorre na maioria dos
softwares úteis –, com frequência percebemos que as fronteiras de nossas
abstrações se deslocam. Para as funções, isso significa que uma unidade de
comportamento que no passado era coesa e atômica se transforma em uma
mistura de duas ou mais funcionalidades distintas.

Um fator que dispara esse processo se dá quando um comportamento
comum usado em vários lugares deve variar em algumas de suas chamadas.Agora temos de mover o comportamento que varia para fora da função, para
os pontos de chamada. Nesse caso, uso Deslocar instruções (Slide
Statements) para levar o comportamento que varia para o início ou para o
final da função, e então utilizo Mover instruções para os pontos de chamada.
Depois que o código variante estiver no ponto de chamada, posso alterá-lo
quando necessário.

Mover instruções para os pontos de chamada funciona bem para pequenas
alterações; às vezes, porém, as fronteiras entre quem chama e quem é
chamado precisam ser totalmente redefinidas. Nesse caso, minha melhor
opção será usar Internalizar função (Inline Function) e então deslocar e
extrair novas funções para definir fronteiras mais apropriadas.

**Resumo**
As funções devem ser uma unidade atômica de alguma ação. Quando o comportamento comum usado em vários locais precisa variar ligeiramente em cada um de seus locais de chamada, é hora de mover o código variável de uma função para os locais de chamada. É o Inverso de Mover Instruções para Função. Você a executa quando há instruções que nem sempre deverão ser chamadas na função.



## Replace Inline Code with Function Call

**Resumo**
Basicamente é reescrever a instrução de uma nova forma. No exemplo do livro está usando includes para buscar se um elemento está no array substituindo a mesma coisa feita com um for. Pois há funções que empacotam comportamentos e assim reduz código e deixa mais simples. Se eu vir um código internalizado que faça o mesmo que uma função existente, em geral vou querer substituir esse código por uma chamada de função.

**Site Traduzido**
Simplesmente, isso é pegar instruções e colocá-las em uma nova função. Isso é muito semelhante em um conceito a Move Statements into Function (213), mas apenas sem o relacionamento entre uma função já existente e seus locais de chamada. Com essa refatoração, você está apenas reempacotando instruções em uma nova função, principalmente para dar um nome à operação para que o local de chamada possa se concentrar no que fazer e a função empacotada possa se concentrar em como está fazendo isso.

**Motivação**
As funções me permitem empacotar comportamentos. Isso é conveniente
para entender o código – uma função nomeada é capaz de explicar o
propósito do código em vez de explicar o seu funcionamento. Também é
importante para remover duplicações: em vez de escrever o mesmo código
duas vezes, basta chamar a função. Então, caso eu precise modificar a
implementação da função, não será necessário procurar códigos semelhantes
para atualizar e fazer todas as mudanças. (Talvez eu tenha de olhar para as
chamadas e ver se todas elas devem usar o novo código, mas isso é menos
comum e mais simples.)

Se eu vir um código internalizado que faça o mesmo que uma função
existente, em geral vou querer substituir esse código por uma chamada de
função. Haverá uma exceção se eu considerar que a semelhança é uma
coincidência – de modo que, se eu alterar o corpo da função, não espero que
o comportamento desse código internalizado mude. Uma orientação a ser
seguida nesse caso é o nome da função. Um bom nome deve fazer sentido no
local em que estiver o código internalizado. Se o nome não fizer sentido,
talvez seja um nome ruim (caso em que uso Renomear função (Rename
Function) para corrigi-lo) ou o propósito da função é diferente daquilo que
quero nesse caso – portanto essa função não deverá ser chamada.

Acho particularmente satisfatório fazer isso com chamadas de funções de
biblioteca – dessa forma, não terei nem mesmo de escrever o corpo da
função.

**Resumo Final**


## Slide Statements

**Site Traduzido**
Use para co-localizar instruções de código que compartilham preocupações semelhantes ou acessam as mesmas estruturas de dados. Use também como uma etapa intermediária para uma refatoração maior. De volta ao topo

**Motivação**

Um código é mais fácil de entender quando elementos relacionados aparecem
juntos. Se várias linhas de código acessam a mesma estrutura de dados, é
melhor que elas estejam juntas, em vez de estarem entrelaçadas com um
código que acesse outras estruturas de dados. No caso mais simples, uso
Deslocar instruções para manter um código como esse junto. Um caso muito
comum está na declaração e no uso de variáveis. Algumas pessoas gostam de
declarar todas as variáveis no início de uma função. Eu prefiro declarar a
variável imediatamente antes de usá-la pela primeira vez.

Em geral, movo o código relacionado como um passo preparatório para
outra refatoração – com frequência, é um Extrair função (Extract Function).
Colocar um código relacionado em uma função claramente distinta é uma
forma de separação melhor do que apenas mover um conjunto de linhas, mas
não é possível executar Extrair função (Extract Function) a menos que o
código esteja junto antes.

**Resumo Final**
Você muda instruções de lugar para aproximar instruções relacionadas. Se várias linhas de código acessam a mesma estrutura de dados, é melhor que elas estejam juntas, em vez de estarem entrelaçadas com um código que acesse outras estruturas de dados.

## Split Loop

**Site Traduzido**
Use quando encontrar um loop que está fazendo várias coisas ao mesmo tempo. Essa refatoração acaba fazendo você repetir o loop na busca por um código mais claro. Isso pode ser desconfortável, mas se a duplicação do loop acabar sendo o gargalo, a refatoração tornará mais fácil combinar o loop novamente depois.

**Motivação**
Muitas vezes, vemos laços que fazem duas tarefas distintas de uma só vez,
somente porque podem fazer isso com uma única passagem por um laço. No
entanto, se você estiver fazendo duas tarefas distintas no mesmo laço, sempre
que for necessário modificar o laço, você terá de entender as duas tarefas. Ao
separar o laço, você garante que precisará entender apenas o comportamento
a ser modificado.

Dividir um laço também pode deixá-lo mais fácil de ser usado. Um laço que
calcule um único valor pode simplesmente devolver esse valor. Laços que
fazem muitas tarefas devem devolver estruturas ou preencher variáveis locais.
Com frequência, executo uma sequência composta de Dividir laço, seguida
de Extrair função (Extract Function).

Muitos programadores se sentem desconfortáveis com essa refatoração, pois
ela força você a executar o laço duas vezes. Como sempre, devo lembrar que
devemos separar a refatoração da otimização (veja a seção Refatoração e
desempenho do Capítulo 2, página 87). Depois que meu código estiver claro,
eu o otimizo; se percorrer o laço for um gargalo, será fácil reunir os laços de
novo. Porém, mesmo uma iteração por uma lista grande raramente representa
um gargalo, e dividir os laços muitas vezes permite outras otimizações mais
eficazes.

**Resumo Final**
(Copy) Use quando encontrar um loop que está fazendo várias coisas ao mesmo tempo. Essa refatoração acaba fazendo você repetir o loop na busca por um código mais claro. Isso pode ser desconfortável, mas se a duplicação do loop acabar sendo o gargalo, a refatoração tornará mais fácil combinar o loop novamente depois.

## Replace Loop with Pipeline

**Site Traduzido**
Pipelines encadeados como filter, map e reduce geralmente são significativamente mais legíveis do que loops for complexos que executam várias instruções. Quando apropriado, converta o loop-for em um pipeline dessas funções.

**Motivação**
Assim como a maioria dos programadores, aprendi a usar laços para iterar
por uma coleção de objetos. Cada vez mais, porém, os ambientes das
linguagens oferecem uma construção mais apropriada: o pipeline de coleção.
Os Pipelines de Coleção (Collection Pipelines) [mf-cp] permitem descrever
meu processamento como uma série de operações, cada uma consumindo e
gerando uma coleção. As mais comuns dessas operações são mapear (map),
que usa uma função para transformar cada elemento da coleção de entrada, e
filtrar (filter), que utiliza uma função para selecionar um subconjunto da
coleção de entrada para passos subsequentes do pipeline. Acho que uma
lógica é muito mais fácil de entender se for expressa como um pipeline –
posso então ler de cima para baixo e ver como os objetos fluem pelo pipeline.

**Resumo Final**

## Remove Dead Code

**Site Traduzido**
Use sempre. Código especialmente comentado. Você sempre pode recuperá-lo com git.

**Motivação**

Quando colocamos um código no ambiente de produção, até mesmo nos
dispositivos das pessoas, não somos cobrados pelo seu peso. Algumas linhas
de código não usadas não deixam nossos sistemas mais lentos nem ocupam
um espaço significativo de memória; na verdade, compiladores decentes as
removerão instintivamente. No entanto, um código não usado continua um
fardo significativo quando tentamos entender como o software funciona. Ele
não porta nenhum sinal de aviso dizendo aos programadores que essa função
pode ser ignorada porque não é mais chamada; assim, eles ainda terão de
gastar tempo para entender o que ela faz e por que a alterar não parece alterar
o resultado conforme esperado.

Quando um código deixa de ser usado, devemos apagá-lo. Não me preocupo
com o fato de poder precisar dele algum dia no futuro; caso isso aconteça,
tenho meu sistema de controle de versões, portanto é sempre possível
recuperá-lo novamente. Se for um código que eu de fato ache que precisarei
algum dia, posso colocar um comentário nele que mencione esse código
perdido e em qual versão ele foi removido – honestamente, porém, sou
incapaz de me lembrar de qual foi a última vez em que fiz isso, ou que tenha
me arrependido por não o fazer.

Comentar um código morto já foi um hábito comum. Era conveniente na
época em que os sistemas de controle de versões não eram amplamente
usados ou quando eram inconvenientes. Atualmente, quando posso colocar
até mesmo a menor das bases de código em um sistema de controle de
versões, isso não é mais necessário.

**Resumo Final**
Quando um código deixa de ser usado, devemos apagá-lo. Apague código morto, que tem um if que nunca entra ou comentários. Você sempre pode recuperá-lo com git.


