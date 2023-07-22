# Encapsulation

Encapsulate Record (162)
Encapsulate Collection (170)
Replace Primitive with Object (174)
Replace Temp with Query (178)
Extract Class (182)
Inline Class (186)
Hide Delegate (189)
Remove Middle Man (192)
Substitute Algorithm (195)

Talvez os critérios mais importantes a serem usados na decomposição de
módulos seja identificar os segredos que os módulos devem ocultar do
restante do sistema [Parnas]. As estruturas de dados são os segredos mais
comuns, e posso ocultá-las encapsulando-as com Encapsular registro
(Encapsulate Record) e Encapsular coleção (Encapsulate Collection). Até
mesmo valores primitivos podem ser encapsulados com Substituir primitivo
por objeto (Replace Primitive with Object) – a dimensão das vantagens
secundárias consequentes disso muitas vezes surpreende as pessoas. Com
frequência, as variáveis temporárias atrapalham a refatoração – devo garantir
que elas sejam calculadas na ordem correta e que seus valores estejam
disponíveis a outras partes do código que precisem delas. Usar Substituir
variável temporária por consulta (Replace Temp with Query) constitui uma
ótima ajuda nesse caso, particularmente quando dividimos uma função que
seja muito longa.
As classes foram concebidas para ocultar informações. No capítulo anterior,
descrevi uma forma de criá-las com Combinar funções em classe (Combine
Functions into Class). As operações comuns de extração/internalização
também se aplicam às classes com Extrair classe (Extract Class) e
Internalizar classe (Inline Class).
Além de ocultar informações internas, em geral as classes são convenientes
para ocultar conexões entre elas, e isso pode ser feito com Ocultar delegação
(Hide Delegate). Entretanto, ocultar demais resulta em interfaces inchadas,
portanto preciso também de sua inversa: Remover intermediário (Remove
Middle Man).
Classes e módulos são as formas mais amplas de encapsulamento, mas
funções também encapsulam a sua implementação. Às vezes, posso precisar
de uma mudança completa em um algoritmo, e isso pode ser feito
encapsulando-o em uma função usando Extrair função (Extract Function) eaplicando Substituir algoritmo (Substitute Algorithm).


## Encapsulate Record

**Site Traduzido**
Fowler gosta de encapsular registros em um objeto quando os próprios dados são mutáveis. Com um objeto, os acessos aos dados e as mutações são mais facilmente abstraídos e controlados. A estrutura de dados subjacente pode ser refatorada sem preocupação com efeitos colaterais. Se os dados forem imutáveis, você terá duas opções: usar uma estrutura que tenha todos os seus campos explicitamente definidos ou usar uma estrutura com campos dinâmicos.

**Resumo**
Para armazenar registros é preferível usar classe ao invés de dict/json. Com classe, os acessos aos dados e as mutações são mais facilmente abstraídos e controlados. Além disso, olhando seus métodos eu sei o que tem na classe enquanto usar um array associativo não é tão intuitivo nem para IDE.


**Motivação**

Estruturas de registro são um recurso comum nas linguagens de programação.
Elas oferecem um modo intuitivo para agrupar dados relacionados,
permitindo que eu passe unidades de dados significativas, em vez de
conjuntos desconectados. No entanto, estruturas de registro simples têm
desvantagens. A mais irritante delas é o fato de me forçarem a separar
claramente o que está armazenado no registro dos valores calculados.
Considere a noção de um intervalo inclusivo de inteiros. Posso armazenaresse intervalo como {start: 1, end:5} ou {start: 1, length:5} (ou até mesmo {end: 5,
length:5} , se eu quiser evidenciar o meu antagonismo). No entanto,
independentemente do que eu armazenar, quero saber o início (start), o fim
(end) e o tamanho (length).

É por isso que, em geral, prefiro objetos aos registros para dados mutáveis.
Com os objetos, posso ocultar o que é armazenado e disponibilizar métodos
para todos os três valores. O usuário do objeto não precisa saber nem se
importar com o que é armazenado e o que é calculado. Esse encapsulamento
também ajuda caso eu queira renomear itens: posso renomear o campo
enquanto disponibilizo métodos tanto para o nome antigo quanto para o nome
novo, atualizando gradualmente as chamadas até que todas estejam
atualizadas.

Acabei de dizer que prefiro objetos para dados mutáveis. Se eu tiver um
valor imutável, posso ter simplesmente os três valores em meu registro,
usando um passo de enriquecimento, se for necessário. De modo semelhante,
é fácil copiar o campo ao renomear.

Posso ter dois tipos de estruturas de registro: aquelas em que declaro os
nomes oficiais dos campos e aquelas que me permitem usar o que eu quiser.

As últimas em geral são implementadas com uma classe de biblioteca cujo
nome é algo como hash, mapa (map), hashmap, dicionário (dictionary) ou
array associativo (associative array). Muitas linguagens oferecem uma
sintaxe apropriada para criar hashmaps, o que os torna convenientes em
muitos cenários de programação. A desvantagem de usá-los é que eles não
são explícitos quanto a seus campos. O único modo pelo qual posso saber se
usam início/fim ou início/tamanho é observando o local em que são criados e
usados. Isso não será um problema se eles forem usados somente em uma
pequena seção de um programa; porém, quanto mais amplo for seu escopo de
uso, mais problemas terei em consequência de sua estrutura implícita. Eu
poderia refatorar esses registros implícitos e transformá-los em explícitos –
mas, se tiver de fazer isso, prefiro transformá-los em classes.

É comum passar estruturas aninhadas de listas e hashmaps, as quais, com
frequência, são serializadas em formatos como JSON e XML. Estruturas
como essas também podem ser encapsuladas; isso ajudará se seus formatos
mudarem depois ou se eu estiver preocupado com atualizações nos dados que
sejam difíceis de monitorar.

**Resumo Final**



## Encapsulate Collection

**Site Traduzido**
Este é um caso especial de Encapsulate Record (162) que toma cuidado especial com as coleções. Se uma lista for encapsulada em um objeto e algum método getter retornar a própria lista, a lista poderá sofrer mutação inadvertidamente, o que remove todos os benefícios do encapsulamento. Em vez disso, você pode fornecer métodos de adicionar/remover/acessar que interagem em uma coleção e, se uma lista precisar ser retornada, você pode retornar uma cópia ou, se o idioma permitir, um ponteiro somente leitura.

**Resumo**
Se sua classe tem como variável uma lista, ofereça métodos de acesso a essa lista e de preferência não faça com que o aceso seja direto, para isso use sempre por valor, passando e recebendo clones da lista. A grande questão é tentar se preocupar com o acesso à lista.

**Motivação**
Gosto de encapsular qualquer dado mutável em meus programas. Isso facilita
ver quando e como as estruturas de dados são modificadas, o que, por sua
vez, facilita modificar essas estruturas de dados quando necessário. Com
frequência, o encapsulamento é incentivado, particularmente por
desenvolvedores que usam orientação a objetos, mas um erro comum ocorre
quando trabalhamos com coleções. O acesso a uma variável de coleção pode
estar encapsulado, mas, se o getter devolver a própria coleção, os membros
dessa coleção poderão ser alterados sem que a classe que faz o
encapsulamento possa intervir.

Para evitar isso, disponibilizo métodos para modificar a coleção – em geral,
add e remove – na própria classe. Desse modo, as alterações na coleção passam
pela classe responsável, dando-me a oportunidade de alterar essas modificações à medida que o programa evoluir.

Se a equipe tiver o hábito de não modificar coleções fora do módulo
original, somente disponibilizar esses métodos pode ser suficiente. Todavia,
contar com esses hábitos, em geral, não é uma atitude sábia; um erro pode
resultar em bugs difíceis de identificar no futuro. Uma abordagem mais
conveniente é garantir que o getter da coleção não devolva a coleção bruta, de
modo que os clientes não possam alterá-la acidentalmente.

Uma maneira de impedir a modificação da coleção subjacente é jamais
devolver um valor de coleção. Nessa abordagem, qualquer uso de um campo
de coleção é feito com métodos específicos da classe responsável,
substituindo aCustomer.orders.size por aCustomer.numberOfOrders . Não concordo com
essa abordagem. As linguagens modernas têm classes de coleção ricas, com
interfaces padronizadas, que podem ser combinadas de formas convenientes,
como Pipelines de Coleções (Collection Pipelines) [mf-cp]. Criar métodos
especiais para lidar com esse tipo de funcionalidade implica a adição de
muito código extra e dificulta usar facilmente o recurso de composição das
operações de coleção.

Outra forma é permitir algum tipo de acesso apenas de leitura a uma
coleção. Java, por exemplo, facilita devolver um proxy somente de leitura
para a coleção. Um proxy como esse encaminha todas as leituras para a
coleção subjacente, porém bloqueia todas as escritas – no caso de Java,
lançando uma exceção. Uma alternativa semelhante é usada por bibliotecas
que baseiam sua composição de coleções em algum tipo de iterador ou objeto
enumerável – desde que esse iterador não modifique a coleção subjacente.

Provavelmente a abordagem mais comum é disponibilizar um método de
leitura para a coleção, mas fazê-la devolver uma cópia da coleção subjacente.
Desse modo, qualquer modificação na cópia não afetará a coleção
encapsulada. Isso pode causar certa confusão caso os programadores esperem
que a coleção devolvida modifique o campo original – porém, em muitas
bases de código, eles estão acostumados com o fato de os getters de coleção
devolverem cópias. Se a coleção for enorme, pode haver problema de
desempenho – a maioria das listas, porém, não é tão grande assim, portanto
as regras gerais sobre desempenho devem se aplicar (veja a seção
Refatoração e desempenho do Capítulo 2 na página 87).

Outra diferença entre usar um proxy e uma cópia é o fato de uma
modificação nos dados originais ser visível no proxy, mas não em uma cópia.
Isso não será um problema na maioria das vezes porque as listas acessadasdessa forma em geral são mantidas somente por pouco tempo.

O que importa nesse caso é a consistência em uma base de código. Use
apenas um procedimento para que todos se acostumem com o seu
comportamento e esperem por ele quando chamarem qualquer função de
acesso a uma coleção.

**Resumo Final**



## Replace Primitive with Object

**Site Traduzido**
Eventualmente, as necessidades de alguma variável armazenada como primitiva crescem além de sua utilidade. Por exemplo, um número de telefone pode ter sido suficiente inicialmente como uma string, mas eventualmente você pode precisar de funcionalidades mais detalhadas, como lidar com códigos de área, códigos de país, lidar com diferentes formatos de exibição, autoverificação, etc. Outro exemplo é um intervalo de datas.

**Motivação**
Com frequência, nas etapas iniciais do desenvolvimento, você toma decisões
sobre representar fatos simples como dados simples, por exemplo, como
números ou strings. À medida que o desenvolvimento avança, esses itens
simples não serão mais tão simples. Um número de telefone pode ser
representado como uma string por um tempo; mais tarde, porém, poderá
exigir um comportamento especial para formatação, extração do código de
área, e tarefas afins. Esse tipo de lógica pode acabar rapidamente sendo
duplicado na base de código, exigindo mais esforços sempre que precisar ser
utilizado.

Assim que percebo que quero fazer algo além de uma simples exibição da
porção de dados, gosto de criar uma nova classe para ela. Em um primeiro
momento, uma classe como essa faz somente pouco mais do que encapsular o
primitivo – mas, depois que eu tiver essa classe, terei um local para colocar
comportamentos específicos às suas necessidades. Esses pequenos valores
começam muito humildemente, mas, depois de nutridos, poderão crescer e se
transformar em ferramentas úteis. Embora não pareçam muito, acho que seus efeitos em uma base de código podem ser surpreendentemente grandes. De
fato, muitos desenvolvedores experientes consideram essa refatoração uma
das mais importantes do kit de ferramentas – mesmo que, muitas vezes, ela
pareça contraintuitiva para um novo programador.

**Resumo Final**
Muitas vezes, um campo definido no início como string ou numeric pode hoje apresentar muito mais complexidade do que imaginávamos. Por exemplo, um número de telefone pode ter sido suficiente inicialmente como uma string, mas eventualmente você pode precisar de funcionalidades mais detalhadas, como lidar com códigos de área, códigos de país, lidar com diferentes formatos de exibição, autoverificação, etc. Outro exemplo é um intervalo de datas. Se você tiver que criar n funções para atender isso em cada lugar será complicado. Nesse cenário em que o campo tem um escopo maior e mais complexo do que um simples valor primitivo, é recomendável então por ele como uma classe e usar métodos de manipulação que encapsulam suas funcionalidades.






## Replace Temp with Query

**Resumo**
Ao invés de usar variáveis temporárias, você pode usar funções curtas que fazem o cálculo. Isso também é útil ao dividir uma função grande. Nas classes python, o equivalente é basicamente transformar variáveis temporárias em métodos @property ou campos calculados.


**Site Traduzido**
Use quando desejar fornecer ainda mais código autoexplicativo para uma variável instanciada com uma expressão complexa. Isso também é útil ao dividir uma função grande. Nas classes python, o equivalente é basicamente transformar variáveis temporárias em métodos @property ou campos calculados.

**Motivação**
Um uso para as variáveis temporárias é capturar o valor de um código a fim
de referenciá-lo mais tarde em uma função. Usar uma variável temporária me
permite referenciar o valor, ao mesmo tempo que explica seu significado e
evita repetir o código que a calcula. No entanto, embora usar uma variável
seja prático, muitas vezes pode valer a pena dar um passo além e usar uma
função em seu lugar.

Se eu estiver trabalhando para dividir uma função grande, transformar
variáveis em funções próprias facilita extrair partes da função, pois não
precisarei mais passar variáveis para as funções extraídas. Colocar essa lógica
em funções muitas vezes define uma fronteira mais clara entre a lógica
extraída e a função original, ajudando-me a identificar e a evitar
dependências inconvenientes e efeitos colaterais.

Usar funções no lugar de variáveis também me permite evitar duplicação da
lógica de cálculo em funções semelhantes. Sempre que vejo variáveis
calculadas do mesmo modo em lugares diferentes, procuro transformá-las em
uma única função.

Essa refatoração funciona melhor se eu estiver dentro de uma classe, pois a
classe oferece um contexto compartilhado para os métodos que estou
extraindo. Fora de uma classe, estou sujeito a ter muitos parâmetros em uma
função de nível mais alto, o que anulará boa parte das vantagens de usar uma
função. Funções aninhadas podem evitar isso, mas limitam minha capacidade
de compartilhar a lógica entre funções relacionadas.

Somente algumas variáveis temporárias são apropriadas para o uso de
Substituir variável temporária por consulta. A variável deve ser calculada
uma vez, e então deve ser apenas lida depois. No caso mais simples, isso
significa que a variável recebe valor uma vez, mas também é possível haver
várias atribuições em uma porção de código mais complicada – todas elas
devem ser extraídas e colocadas na consulta. Além do mais, a lógica usada
para calcular a variável deve gerar o mesmo resultado quando a variável for
usada mais tarde – o que exclui as variáveis usadas como snapshots (imagens
instantâneas) com nomes como oldAddress .

**Resumo Final**



## Extract Class

**Site Traduzido**
As classes devem ser uma abstração nítida que lida com algumas responsabilidades claras. Na prática, as classes crescem e crescem e assumem responsabilidades que a princípio não pareciam merecer uma aula própria. Mas, eventualmente, quando uma classe fica muito inchada, é hora de dividir a classe em duas (ou mais).

**Motivação**
Você provavelmente já viu orientações dizendo que uma classe deve ser uma
abstração nítida, deve lidar somente com algumas responsabilidades claras, e assim por diante. Na prática, as classes crescem. Você acrescenta algumas
operações aqui, um pouco de dados ali. Adiciona uma responsabilidade em
uma classe achando que não vale a pena ter uma classe separada – mas, à
medida que essa responsabilidade aumenta, a classe se torna complicada
demais. Em breve, sua classe não será mais tão clara assim.

Pense em uma classe com muitos métodos e uma grande quantidade de
dados. Uma classe grande demais para ser facilmente compreendida. Você
deve considerar em que ponto ela pode ser separada – e separá-la. Um bom
sinal é quando um subconjunto dos dados e um subconjunto dos métodos
parecem formar um conjunto. Outros bons sinais são subconjuntos de dados
que geralmente mudam juntos ou são particularmente dependentes uns dos
outros. Um teste conveniente é perguntar a si mesmo o que aconteceria se
você removesse uma porção dos dados ou um método. Quais outros campos e
métodos deixariam de fazer sentido?

Um sinal que muitas vezes surge mais tarde no desenvolvimento é o modo
como a classe é subtipada. Você poderá perceber que a subtipagem afeta
somente alguns recursos ou que alguns recursos devem ser subtipados de uma
forma, enquanto outros, de forma diferente.

**Resumo Final**
Uma classe, pelo seu nome, deveria ter bem delimitado as suas responsabilidades. Mas as veze, programamos e criamos classes muito grandes. Então, se chegar a esse ponto, é ideal extrair dados de uma classe para formar uma nova classe separada.



## Inline Class

**Site Traduzido**
O inverso de Extract Class (182). Se uma classe estiver fazendo muito pouco, podemos reduzir a indireção dobrando a classe em outra. Isso também pode ser um trampolim para uma refatoração maior. Por exemplo, se você tiver duas classes que deseja refatorar em outras duas classes com alocação diferente de recursos, convém Inline Class (186) e, em seguida, primeiro em uma superclasse e, subsequentemente, Extract Class (182).

**Resumo**
O inverso de Extract Class. Se uma classe estiver fazendo muito pouco, podemos reduzir colocando seus dados dentro em outra.



**Motivação**
Internalizar classe é o inverso de Extrair classe (Extract Class). Uso
Internalizar classe se constatar que não vale mais a pena tê-la, isto é, ela não
deveria mais estar presente. Com frequência, isso é resultado de uma
refatoração que move responsabilidades para fora da classe, restando pouca
coisa nela. A essa altura, desdobro a classe em outra – em uma que faça mais
uso da classe pequena.

Outro motivo para usar Internalizar classe é quando tenho duas classes que
quero refatorar em um par de classes com uma alocação diferente de
recursos. Posso achar mais fácil usar Internalizar classe antes de modo a
combiná-las em uma única classe, e então usar Extrair classe (Extract Class)
para fazer a nova separação. Esta é a abordagem genérica para reorganizar o
código: às vezes, é mais fácil mover elementos, um de cada vez, de umcontexto para outro; outras vezes, porém, é melhor usar uma refatoração de
internalização para reunir os contextos e depois usar uma refatoração de
extração para separá-los em elementos diferentes.

**Resumo Final**



## Hide Delegate

**Site Traduzido**
O inverso de Remove Middle Man (192). Use quando você tiver uma situação em que A chama um método definido em C, mas C é mantido dentro de B. Neste exemplo, C é o delegado com as informações reais com as quais A se preocupa. B pode ocultar o delegado implementando funções que basicamente encapsulam as chamadas para C. Dessa forma, se uma alteração precisar ocorrer em C, o impacto irá apenas para B para garantir que os wrappers permaneçam sincronizados com quaisquer alterações de interface de C. A não precisa se preocupar com a mudança.

**Motivação**
Um dos segredos – se não o segredo – de um bom design modular é o
encapsulamento. Um encapsulamento significa que os módulos precisam
saber menos sobre outras partes do sistema. Então, quando houver mudanças,
menos módulos precisarão ter conhecimento delas – facilitando fazer a
mudança.

Quando começamos a aprender sobre orientação a objetos, nos ensinam que
encapsulamento significa ocultar nossos campos. À medida que nos tornamos
mais sofisticados, percebemos que há outros itens que podemos encapsular.

Se eu tiver um código de cliente que chame um método definido em um
objeto que está um campo de um objeto servidor, o cliente deverá conhecer
esse objeto delegado. Se esse objeto mudar a sua interface, as mudanças se
propagarão para todos os clientes do servidor que usam o objeto delegado.
Posso eliminar essa dependência colocando um método simples de delegação
no servidor que oculte o objeto delegado. Então, qualquer modificação que eu
fizer no objeto delegado se propagará somente até o servidor, e não aos clientes.

**Resumo Final**



## Remove Middle Man

**Site Traduzido**
O inverso de Hide Delegate (189). Ocultar delegados pode se tornar irritante quanto mais o chamador precisar acessar o delegado. Para cada novo ponto de interação, um novo método precisa ser definido apenas para expor uma maneira de o chamador alcançar o delegado. Eventualmente, o acoplamento entre o chamador e o delegado fica grande o suficiente para que seja hora de remover o intermediário e fazer com que o chamador ligue diretamente para o delegado.

**Motivação**
Na motivação de Ocultar delegação (Hide Delegate), falei das vantagens de
encapsular o uso de um objeto delegado. Há um preço para isso. Sempre que
o cliente quiser usar um novo recurso do objeto delegado, tenho de adicionar
um método simples de delegação no servidor. Depois de adicionar recursos
por um tempo, fico irritado com todo esse encaminhamento. A classe de
servidor é apenas um intermediário (middle man) (ver a seção Intermediário
do Capítulo 3 na página 106), e talvez seja hora de o cliente chamar
diretamente o objeto delegado. (Esse cheiro com frequência aparece quando
as pessoas se entusiasmam demais em seguir a Lei de Demeter, que eu
acharia muito melhor se fosse chamada de Sugestão de Demeter
Ocasionalmente Útil.)

É difícil determinar o nível correto para ocultar itens. Felizmente, com
Ocultar delegação (Hide Delegate) e Remover intermediário (Remove
Middle Man), isso não importa tanto. Posso adaptar meu código com o passar
do tempo. À medida que o sistema mudar, o critério para determinar quanto
devo ocultar também mudará. Um bom encapsulamento seis meses atrás
poderá ser inconveniente agora. Refatoração significa jamais ter de lamentar
– eu apenas faço a correção.

**Resumo Final**



## Substitute Algorithm

**Site Traduzido**
Use quando descobrir maneiras novas e melhores de implementar a mesma coisa. Por exemplo, se você começar a usar uma biblioteca que fornece recursos que duplicam seu código, comece a usar os recursos da biblioteca (por exemplo, lodash). Use também se a nova e melhor maneira de implementar o código for mais clara do que a implementação original. Mais simples é melhor que complexo.

**Motivação**
Nunca tentei escalpelar um gato. Já me disseram que há várias maneiras defazer isso. Tenho certeza de que algumas são mais fáceis que outras. O
mesmo vale para os algoritmos. Se eu achar uma maneira mais clara de fazer
algo, substituirei o modo complicado pelo modo mais claro. A refatoração
pode separar algo complexo em partes mais simples; às vezes, porém, atinjo
o ponto em que tenho de remover o algoritmo completo e substituí-lo por
algo mais simples. Isso ocorre à medida que aprendo mais sobre o problema e
percebo que há um modo mais fácil de fazer uma tarefa. Também ocorre
quando começo a usar uma biblioteca que ofereça recursos que dupliquem
meu código.

Às vezes, quando quero modificar o algoritmo para que funcione de modo
um pouco diferente, é mais fácil começar substituindo-o por algo que deixe
minha modificação mais simples de ser feita.

Quando for necessário executar esse passo, tenho de me certificar de que
decompus o método o máximo possível. Substituir um algoritmo grande e
complexo é muito difícil: somente o deixando mais simples posso deixar a
substituição mais controlada.

**Resumo Final**


