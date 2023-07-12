# 11 - Refactoring APIs

1 - Separate Query from Modifier (306)
2 - Parametrize Function (310)
3 - Remove Flag Argument (314)
4 - Preserve Whole Object (319)
5 - Replace Parameter with Query (324)
6 - Replace Query with Parameter (327)
7 - Remove Setting Method (331)
8 - Replace Constructor with Factory Function (334)
9 - Replace Function with Command (337)
10 - Replace Command with Function (344)

Print de area da tela no windos: Windos + shift + S

**Traduzido**

**Motivação**

**Resumo**


## Separate Query from Modifier

**Traduzido**
Em geral e na maioria dos casos, fazer distinções claras entre funções com efeitos colaterais observáveis e aquelas sem efeitos colaterais é uma ótima ideia.

**Motivação**
Quando tenho uma função que me forneça um valor e não gere efeitos
colaterais observáveis, tenho algo muito valioso. Posso chamar essa função
com a frequência que eu quiser; posso mover a chamada dessa função para
outros lugares dentro de uma função e é mais fácil de testar. Em suma, tenho
muito menos com que me preocupar.

É uma boa ideia sinalizar claramente a diferença entre funções com efeitos
colaterais e funções sem eles. Uma boa regra a ser seguida determina que
qualquer função que devolva um valor não deve ter efeitos colaterais
observáveis – é a separação entre comando-consulta (command-query
separation) [mf-cqs]. Alguns programadores tratam essa regra como absoluta.
Não defendo uma pureza de 100% quanto a isso (assim como para tudo
mais), mas tento segui-la na maioria das vezes, e ela tem me servido bem.

Se eu deparar com um método que devolva um valor, mas que também
tenha efeitos colaterais, sempre tento separar a consulta do modificador.
Note que uso a expressão efeitos colaterais observáveis. Uma otimização
comum é fazer cache do valor de uma consulta em um campo para agilizar as
chamadas repetidas. Embora isso altere o estado do objeto com o cache, a
mudança não é observável. Qualquer sequência de consultas sempre
devolverá o mesmo resultado para cada consulta.

**Resumo**
Deixe separado funções que buscam valores das que modificam valores. É uma boa ideia sinalizar claramente a diferença entre funções com efeitos colaterais e funções sem eles. Uma boa regra a ser seguida determina que qualquer função que devolva um valor ( que faz uma consulta, um find/search/filter não deve ter efeitos colaterais observáveis. Se eu deparar com um método que devolva um valor, mas que também tenha efeitos colaterais, sempre separe a consulta do modificador.



## Parametrize Function

**Traduzido**
Use quando houver duas funções muito semelhantes que fazem quase a mesma coisa, mas diferem em alguma constante codificada. A constante pode ser transformada em um parâmetro para uma função comum.

**Motivação**
Se vejo duas funções executando uma lógica muito parecida com valores
literais distintos, posso remover a duplicação usando uma única função com
parâmetros para os diferentes valores. Com isso, a função se torna mais útil,
pois poderá ser aplicada em outros lugares com valores diferentes.

**Resumo**
Refatore quando houver duas funções muito semelhantes que fazem quase o mesmo, mas diferem em um valor interno. A constante pode ser transformada em um parâmetro para uma função que sirva para as duas.

## Remove Flag Argument

**Traduzido**
Use quando um parâmetro para uma função serve como um argumento sinalizador que leva a algum caminho de ramificação dentro da função. Deve haver duas funções separadas para os diferentes casos do sinalizador.

**Motivação**

**Resumo**
Se numa função há uma flag que serve para escolher qual if entrar, ao invés de manter desa forma, separe em funções distintas.

## Preserve Whole Object

**Traduzido**
Use quando um callsite desconstrói um objeto ou registro em valores individuais e, em seguida, passa esses valores desconstruídos para outra função. A função deve apenas aceitar todo o registro e desconstruir o que precisa dele.

"Puxar vários valores de um objeto para fazer alguma lógica neles sozinho é um cheiro e geralmente um sinal de que essa lógica deve ser movida para o todo em si."

**Motivação**

Um argumento de flag é um argumento utilizado por quem chama uma
função a fim de indicar a lógica que a função chamada deve executar. Posso
chamar uma função como esta:

````
function bookConcert(aCustomer, isPremium) {
if (isPremium) {
// lógica para reserva premium
} else {
// lógica para reserva comum
}
}
````

Para reservar (book) um concerto premium, faço a chamada assim:
````
bookConcert(aCustomer, true);
````
Argumentos de flag também podem estar na forma de enumerados:
````
bookConcert(aCustomer, CustomerType.PREMIUM);
````
ou como strings (ou símbolos, em linguagens que os usem):
````
bookConcert(aCustomer, "premium");
````

Não gosto de argumentos de flag porque eles complicam o processo para
entender quais são as chamadas de função disponíveis e como chamá-las. Em
minha primeira incursão por uma API, em geral analiso a lista de funções
disponíveis, e os argumentos de flag ocultam as diferenças nas chamadas
dessas funções. Após selecionar uma função, é necessário descobrir quais são
os valores disponíveis para os argumentos de flag. Flags booleanas são piores
ainda, pois elas não informam seu significado para o leitor – em uma
chamada de função, não é possível descobrir o que true significa.
Disponibilizar uma função explícita para a tarefa que quero executar é uma
opção mais clara.
````
premiumBookConcert(aCustomer);
````
Nem todos os argumentos como esses são argumentos de flag. Para ser um
argumento de flag, quem faz as chamadas deve definir o valor booleano com
um valor literal, e não com dados que fluam pelo programa. Além disso, a
função de implementação deve usar o argumento para influenciar o seu
controle de fluxo, e não como um dado a ser passado para outras funções.
Remover argumentos de flag não só deixa o código mais claro como
também auxilia minhas ferramentas. Ferramentas de análise de código agora
poderão ver mais facilmente a diferença entre chamar a lógica premium e
chamar a lógica comum.

Argumentos de flag podem ter sua utilidade caso haja mais de um deles na
função, pois, do contrário, seria necessário ter funções explícitas para cada
combinação de seus valores. Contudo, isso também é um sinal de que uma
função está fazendo tarefas demais, e eu deveria procurar uma maneira de
criar funções mais simples, que possam ser compostas para implementar essa
lógica.

**Resumo**
Se você tem um objeto, e tiver que extrair valores dele para executar algo, isso é bad smell.  A função deve apenas aceitar todo o registro e desconstruir o que precisa dele internamente. "Puxar vários valores de um objeto para fazer alguma lógica neles sozinho é um cheiro e geralmente um sinal de que essa lógica deve ser movida para o todo em si."

## Replace Parameter with Quer

**Traduzido**
Inverso de Substituir Consulta por Parâmetro (327). A lista de parâmetros para uma função deve resumir os pontos de variabilidade dessa função, indicando as principais maneiras pelas quais essa função pode se comportar de maneira diferente.

Se uma chamada passa um valor que a função pode facilmente determinar por si mesma, isso é uma forma de duplicação - uma que complica desnecessariamente o chamador, que precisa determinar o valor de um parâmetro quando poderia ter sido liberado desse trabalho.

Não deve ser usado se remover o parâmetro e mover sua derivação para a função adicionaria uma dependência indesejada ao corpo da função.

**Motivação**

Ao observar o corpo de uma função, às vezes vejo referências a algo no
escopo dela com as quais não me sinto satisfeito. Pode ser uma referência a
uma variável global ou a um elemento do mesmo módulo que pretendo
mover para outro lugar. Para resolver esse problema, é necessário substituir a
referência interna por um parâmetro, transferindo a responsabilidade de
resolver a referência para quem chama a função.

A maioria desses casos se deve ao meu desejo de alterar os relacionamentos
de dependência no código – para que a função final não seja mais dependente
do elemento que quero parametrizar. Há uma tensão, nesse caso, entre
converter tudo para parâmetros, o que resultaria em listas de parâmetros
longas e repetitivas, e compartilhar bastante escopo, resultando em alto nível
de acoplamento entre funções. Como em muitas decisões complicadas, não é
algo sobre o qual eu tenha absoluta certeza, portanto é importante que seja
possível modificar o código de forma confiável para que o programa tire
proveito de minha compreensão cada vez maior.

É mais fácil pensar em uma função que sempre dará o mesmo resultado
quando for chamada com os mesmos valores de parâmetros – isso se chama
transparência referencial. Se uma função acessar um elemento que não seja
referencialmente transparente em seu escopo, a função que a contém também
não terá transparência referencial. Posso corrigir isso fazendo com que esse
elemento seja um parâmetro. Embora uma ação como essa transfira a
responsabilidade para quem faz a chamada, em geral há muitas vantagens em
criar módulos claros, com transparência referencial. Um padrão comum é ter
módulos que consistem de funções puras, encapsuladas por uma lógica que
cuide da E/S e de outros elementos variáveis de um programa. Posso usar
Substituir consulta por parâmetro para deixar partes de um programa mais
puras, facilitando os testes e a compreensão dessas partes.

Contudo, Substituir consulta por parâmetro não representa somente
vantagens. Ao mover uma consulta para um parâmetro, estarei forçando
quem faz a chamada a descobrir como fornecer esse valor. Isso complica a
vida de quem chama as funções, e minha tendência habitual é projetar
interfaces que facilitem a vida de seus clientes. No final, tudo se reduz à
alocação de responsabilidades pelo programa, e essa decisão não é fácil nem
imutável – por isso, é necessário conhecer bem essa refatoração (e a sua
inversa).


**Resumo**
De preferência, não passe a mesma informação nos parêmtros de uma funçâo. É o contrário de 'Replace Query with Parameter'.

## Replace Query with Parameter

**Traduzido**

Inverso de Substituir Parâmetro por Consulta (324). Use quando a consulta dentro da função fizer parte de alguma dependência indesejada que você não deseja mais que a função se importe ou esteja ciente. Por exemplo, em JavaScript, se a função tiver encerramento sobre alguma variável que está usando e você quiser desacoplá-la de seu site de declaração, convém parametrizar a consulta para facilitar a movimentação da função.

**Motivação**

Se eu vir um código que faça a derivação de alguns valores de um registro e
então passe esses valores para uma função, gostaria de substituí-los pelo
próprio registro completo, deixando o corpo da função fazer a derivação dos
valores necessários.

Passar o registro completo é melhor para lidar com alterações caso a função
chamada necessite de mais dados desse registro no futuro – essa alteração
não exigirá que eu altere a lista de parâmetros. Com isso, o tamanho da lista
de parâmetros também será reduzido, em geral deixando a chamada da
função mais fácil de entender. Se muitas funções forem chamadas com os
dados parciais, com frequência elas duplicarão a lógica que manipula esses
dados – uma lógica que em geral poderá ser movida para o objeto completo.

O principal motivo para não fazer essa refatoração seria não querer que a
função chamada estabeleça uma dependência com o objeto completo –
ocorrerá tipicamente se eles estiverem em módulos distintos.

Extrair diversos valores de um objeto somente para executar uma lógica
neles é um mau cheiro no código (veja a seção Inveja de recursos no
Capítulo 3, página 101), e em geral é um sinal de que essa lógica deve ser
movida para o próprio objeto completo. Preservar objeto inteiro é
particularmente comum após ter usado Introduzir objeto de parâmetros
(Introduce Parameter Object), quando busco quaisquer ocorrências do
conjunto de dados originais a fim de substituí-los pelo novo objeto.

Se várias porções de código usarem somente o mesmo subconjunto dos
recursos de um objeto, isso pode sinalizar uma boa oportunidade para o uso
de Extrair classe (Extract Class).

Um caso que muitas pessoas podem não perceber é aquele em que um
objeto chama outro com vários de seus próprios dados. Se vejo isso, posso
substituir esses valores por uma autorreferência (this em JavaScript).

**Resumo**
Inverso de Substituir Parâmetro por Consulta (324). Use quando a consulta dentro da função fizer parte de alguma dependência indesejada que você não deseja mais que a função se importe ou esteja ciente. Por exemplo, em JavaScript, se a função tiver encerramento sobre alguma variável que está usando e você quiser desacoplá-la de seu site de declaração, convém parametrizar a consulta para facilitar a movimentação da função.

## Remove Setting Method

**Traduzido**
No contexto de getters e setters, a remoção do método de setter transmitirá que a atualização dos valores de algum objeto não faz sentido após a inicialização. Isso reduz as áreas no código que podem modificar o objeto. Se o chamador quiser um objeto diferente, ele pode instanciar um novo.

**Motivação**
Disponibilizar um método de escrita indica que um campo pode ser alterado.
Se eu não quiser que esse campo mude depois que o objeto for criado, não
disponibilizarei um método de escrita (e tornarei o campo imutável). Desse
modo, o campo recebe valor somente no construtor, minha intenção de não
modificar esse campo estará clara e, geralmente, eliminarei a própria
possibilidade de que o campo mude.

Há alguns casos comuns em que essa situação pode surgir. Um deles é
aquele em que as pessoas sempre usam um método de acesso para manipular
um campo, mesmo nos construtores. Isso resulta em uma única chamada a
um método de escrita sendo feita no construtor. Prefiro remover o método de
escrita para deixar claro que as atualizações não fazem sentido após a
construção.

Outro caso é aquele em que o objeto é criado por clientes usando um script
de criação no lugar de uma simples chamada de construtor. Um script de
criação como esse começa com a chamada do construtor, seguida de uma
sequência de chamadas de métodos de escrita para criar o novo objeto.
Depois que o script termina, não se espera que o novo objeto altere certos
campos (ou todos). É esperado que os setters sejam chamados somente
durante essa criação inicial. Nesse caso, eu me livraria deles para deixar
minhas intenções mais claras.

**Resumo**

Disponibilizar um setter indica que um campo pode ser alterado. Se eu não quiser que esse campo mude depois que o objeto for criado, não devo disponibilizar o setter (e tornarei o campo imutável). Desse modo, o campo recebe valor somente no construtor, minha intenção de não modificar esse campo estará clara e, geralmente, eliminarei a própria possibilidade de que o campo mude.

## Replace Constructor with Factory Function

**Traduzido**

Use quando quiser que o código crie objetos diferentes condicionalmente com base em algum parâmetro. Muitas linguagens têm limitações quanto ao que você pode fazer com um construtor, mas uma função que retorna um objeto instanciado não terá tais limitações.

**Motivação**

Muitas linguagens orientadas a objetos têm uma função especial de
construtor, chamada para inicializar um objeto. Os clientes geralmente
chamam esse construtor quando querem criar um novo objeto. Entretanto,
esses construtores muitas vezes apresentam limitações inconvenientes, que
não estão presentes em funções mais genéricas. Um construtor Java deve
devolver uma instância da classe com a qual foi chamado, o que significa que
não poderei substituí-lo por uma subclasse ou um proxy, dependendo do
ambiente ou dos parâmetros. A nomenclatura do construtor é fixa, tornando
impossível para mim usar um nome que seja mais claro que o nome default.
Com frequência, os construtores exigem um operador especial para serem
chamados (“new” em muitas linguagens), o que dificulta usá-los em
contextos que esperem funções comuns.

Uma função de factory não está sujeita a essas limitações. Provavelmente
ela chamará o construtor como parte de sua implementação, mas posso
substituí-lo livremente por outro código.

**Resumo**

Com frequência, os construtores exigem um operador especial para serem chamados (“new” em muitas linguagens), o que dificulta usá-los em contextos em que seria mais fácil esperar por uma função.  Uma função de factory não está sujeita a essas limitações. Provavelmente ela chamará o construtor como parte de sua implementação, mas posso substituí-lo livremente por outro código. Por isso use factory ao invés do new quando quiser que o código crie objetos diferentes condicionalmente com base em algum parâmetro. 

## Replace Function with Command

**Traduzido**
Inverso de Substituir Comando por Função (344). Às vezes, pode ser uma boa ideia pegar uma função e movê-la para algum objeto de classe que deve primeiro ser instanciado e subsequentemente ter a função chamada. Fowler chama esse objeto de conteúdo de Comando. Os comandos oferecem um estilo de vida muito mais rico para a função. Por exemplo, como está em uma classe que pode ter estado, você pode ter uma função de desfazer. Você também pode aproveitar a natureza da classe usando herança, garantindo maior flexibilidade.

A desvantagem acima é a complexidade adicional, que, com base na circunstância, você pode querer evitar.

**Motivação**
As funções – sejam elas independentes ou associadas a objetos na forma de
métodos – são um dos blocos de construção fundamentais da programação.
Há ocasiões, porém, em que é conveniente encapsular uma função em seu
próprio objeto, ao qual me refiro como um “objeto de comando”, ou
simplesmente um comando. Um objeto como esse, na maioria dos casos, é
construído em torno de um único método, cuja requisição e execução são o
propósito do objeto.

Um comando oferece mais flexibilidade para o controle e a expressão de
uma função, em comparação com o mecanismo simples de função. Os
comandos podem ter operações complementares, por exemplo, uma operação
de desfazer (undo). Posso disponibilizar métodos para construir seus
parâmetros a fim de oferecer um suporte para um ciclo de vida mais rico,
além de incluir personalizações usando herança e ganchos (hooks). Se eu
estiver trabalhando em uma linguagem com objetos, mas sem funções de
primeira classe, posso oferecer boa parte dessas funcionalidades usando
comandos em seu lugar. De modo semelhante, posso usar métodos e campos
para ajudar a dividir uma função complexa, mesmo em uma linguagem que
não tenha funções aninhadas, e posso chamar esses métodos diretamente
enquanto faço testes e depuração.

Tudo isso são bons motivos para usar comandos, e tenho de estar preparado
para refatorar funções e transformá-las em comandos quando necessário.
Entretanto, não devemos esquecer que essa flexibilidade, como sempre, tem
um preço a ser pago em termos de complexidade. Assim, dada a opção de
escolher entre uma função de primeira classe e um comando, optarei pela
função em 95% das vezes. Uso um comando apenas se precisar
especificamente de um recurso que abordagens mais simples não são capazes
de oferecer.

Como muitas palavras em desenvolvimento de software, “comando” tem
vários significados. No contexto em que estou usando aqui, o comando é um
objeto que encapsula uma requisição, seguindo o padrão de comando dos
Padrões de Projeto (Design Patterns) [gof]. Quando uso “comando” nesse
sentido, utilizo “objeto de comando” para definir o contexto, e “comando”
depois. A palavra “comando” também é usada no princípio da separação
entre comando-consulta [mf-cqs], em que um comando é um método de
objeto que modifica um estado observável. Sempre procuro evitar usar
comando nesse sentido, preferindo “modificador” ou “mutator”.

**Resumo**
Às vezes, pode ser uma boa ideia pegar uma função e movê-la para uma classe que deve primeiro ser instanciado e somente depois executaar a funçâo que queria chamar antes. Fowler chama essa classe de Command (tendo uma funcionalidade semelahnte ao COmmand do GoF). Os Commands oferecem um estilo de vida muito mais rico para a função. Por exemplo, como está em uma classe que pode ter estado, você pode ter uma função aletrar e desfazer. Você também pode aproveitar a natureza da classe usando herança, garantindo maior flexibilidade. A desvantagem acima é a complexidade adicional, que, com base na circunstância, você pode querer evitar.

## Replace Command with Function

**Traduzido**

Inverso da Função Substituir por Comando (337). Use quando um comando for um exagero para o que você está tentando fazer ou deseja que a função faça.

**Motivação**

Objetos de comando oferecem um mecanismo eficaz para lidar com
processamentos complexos. Esses podem ser facilmente divididos em
métodos separados que compartilhem um estado comum por meio de
campos; podem ser chamados por métodos diferentes para ter efeitos
diferentes; podem ter seus dados construídos em etapas. Contudo, essa
eficácia tem um custo. Na maioria das vezes, quero apenas chamar uma
função para que ela faça o que tenha de ser feito. Se for esse o caso, e a
função não for muito complexa, não valerá a pena ter um objeto de comando,
pois ele representará mais problemas, e a função deverá ser transformada em
uma função comum.

**Resumo**

Inverso da Função Substituir por Command. Use quando um comando for um exagero para o que você está tentando fazer ou deseja que a função faça.


