# Chapter 10 - Simplifying Conditional Logic

Simplifying Conditional Logic

Decompose Conditional (260)
Consolidate Conditional Expression (263)
Replace Nested Conditional with Guard Clauses (266)
Replace Conditional with Polymorphism (272)
Introduce Special Case (289)
Introduce Assertion (302)

## Decompose Conditional

**Site Traduzido**
Em uma função, os condicionais descrevem o que acontece, mas ofuscam o motivo pelo qual isso acontece. Decompor a condição significa pegar a própria condição e reescrevê-la como uma função que retorna algum booleano. O nome da função descreverá a intenção da condição. Este é realmente apenas um caso hiperespecífico da Extract Function, específico para lógica condicional.


**Motivação**
Uma das fontes mais comuns de complexidade em um programa é uma
lógica condicional complexa. À medida que escrevo código para várias
situações que dependam de diversas condições, posso acabar rapidamente
com uma função bem longa. O tamanho de uma função, por si só, é um fator
que dificulta a leitura, mas as condições aumentam a dificuldade. O problema
em geral está no fato de o código, tanto nas verificações das condições
quanto nas ações, me dizer o que acontece, mas facilmente encobrir por que
acontece.

Assim como em qualquer bloco de código grande, posso deixar minha
intenção mais clara decompondo-o e substituindo cada porção de código por
uma chamada de função cujo nome seja atribuído com base na intenção da
respectiva porção. Com as condições, gosto particularmente de fazer isso para
a parte condicional e para cada uma das alternativas. Dessa forma, enfatizo a
condição e deixo claro o código com base no qual se dá a ramificação.
Também enfatizo o motivo para a ramificação.

Na verdade, esse é um caso particular da aplicação de Extrair função
(Extract Function) em meu código, mas gosto de destacá-lo, pois, com
frequência, vejo aí um motivo muito relevante para usar essa refatoração.

**Resumo Final**
Em uma função, os condicionais descrevem o que acontece, mas ofuscam o MOTIVO pelo qual isso acontece. Decompor a condição significa pegar a própria condição e reescrevê-la como uma função que retorna algum booleano. O nome da função descreverá a intenção da condição e assim ficará mais fácil de entender o que está acontecendo. Este é realmente apenas um caso hiperespecífico da Extract Function, específico para lógica condicional.



## Consolidate Conditional Expression

**Site Traduzido**
Use quando encontrar uma série de verificações condicionais, em que cada verificação é diferente, mas o resultado de cada verificação é o mesmo. Usar a lógica and, or and not ajuda a transmitir que você está realmente realizando apenas uma verificação e também configura o código para uma futura Decompose Conditional (260). Este não é um tamanho único, no entanto. Às vezes, mesmo que a série de verificações condicionais deva ser considerada como verificações diferentes, não faça a refatoração.

**Motivação**
Às vezes, deparo com uma série de verificações condicionais em que cada
verificação é diferente, embora a ação resultante seja a mesma. Quando vejo
isso, utilizo os operadores and e or para consolidá-las em uma única
verificação condicional, com um único resultado.

Consolidar o código condicional é importante por dois motivos. Primeiro,
deixa o código mais claro, mostrando que estou realmente fazendo uma única
verificação que combina outras verificações. Usar uma sequência tem o
mesmo efeito, porém passa a impressão de que estou executando uma
sequência de verificações separadas que, somente por acaso, estão próximas.

O segundo motivo pelo qual gosto de consolidar um código condicional é
que, com frequência, isso me deixa preparado para usar Extrair função
(Extract Function). Extrair uma condição é uma das melhores tarefas que
posso fazer para deixar meu código mais claro. Com isso, substituo uma
instrução que mostra o que estou fazendo por outra que informa por que estou
fazendo.

Os motivos a favor de consolidar condicionais também apontam para os
motivos para não o fazer. Se eu considerar que as verificações são de fato
independentes, e que não devem ser pensadas como uma única verificação,
não devo fazer a refatoração.

**Resumo Final**
Você consolida várias verificações em uma função boleana juntando doas as condições com and e or quando a ação de cada uma é a mesma. 



## Replace Nested Conditional with Guard Clauses

**Site Traduzido**
As funções com um condicional vêm em dois tipos: o primeiro é onde a ramificação no código resulta em dois caminhos que podem ser considerados "normais" e talvez até mais ou menos igualmente prováveis. o segundo tipo é onde há um caminho feliz "verdadeiro" e as verificações condicionais para algum estado estranho antes de continuar. Uma cláusula de guarda (definida aqui por Fowler) é uma verificação de if que retorna antecipadamente se for verdadeira.

Retornar antes das cláusulas de guarda ajuda com o deslocamento lateral do código, também conhecido como código que está se tornando cada vez mais aninhado, significa que o código precisa ser cada vez mais recuado para fazer sentido visual.

**Motivação**
De modo geral, vejo que as expressões condicionais se apresentam em dois
estilos. No primeiro, os dois ramos da condicional fazem parte do
comportamento normal, enquanto, no segundo, um ramo é normal e o outro
indica uma condição incomum.
Esses tipos de condicionais têm propósitos diferentes – e esses propósitos
devem estar evidentes no código. Se ambas as condições fizerem parte do
comportamento normal, utilizo uma condição com ramos if e else . Se a
condição for incomum, faço a sua verificação e retorno se ela for verdadeira.

Esse tipo de verificação muitas vezes é chamado de cláusula de guarda
(guard clause).
O ponto principal de Substituir condicional aninhada por cláusulas de
guarda está na ênfase. Se eu usar uma construção if-then-else, estarei dando
pesos iguais aos ramos if e else . Isso diz ao leitor que os ramos são igualmente
prováveis e têm a mesma importância. Em contrapartida, a cláusula de guardadiz que “essa não é a parte essencial desta função; se ela ocorrer, faça algo e
saia”.

Em geral, percebo que uso Substituir condicional aninhada por cláusulas de
guarda quando estou trabalhando com um programador que aprendeu que
deve haver somente um único ponto de entrada e um único ponto de saída em
um método. Ter um único ponto de entrada é garantido pelas linguagens
modernas, mas ter um único ponto de saída não é uma regra realmente útil. A
clareza é o princípio fundamental: se o método for mais claro tendo um único
ponto de saída, use um ponto de saída; caso contrário, não faça isso.

**Resumo Final**
Se os vários ifs que você tem servem só pra retornar um valor específico, ao invéz de fazer um monte de if/else aninhada, faça com que cada if dê um return. Isso reduz o código, deixa mais limpo, e você especifica na hora a saída do método.



## Replace Conditional with Polymorphism

**Site Traduzido**
Use quando você encontrar algum tipo de instrução switch que opera em um conjunto de variáveis de forma diferente com base no tipo da variável. Você pode criar uma classe para cada caso e, em seguida, criar uma função polimórfica que gerencie a si mesma de maneira diferente com base na implementação de caso individual da função. Isso é especialmente útil quando há algum tipo de caso base que deve ser definido, mas alguns casos têm pequenas variações em relação ao caso base.

**Motivação**
Uma lógica condicional complexa é um dos elementos mais difíceis de
entender em programação, portanto sempre procuro maneiras de acrescentar
estrutura em uma lógica condicional. Com frequência, percebo que é possíveldividir a lógica em circunstâncias distintas – casos de alto nível – a fim de
separar as condições. Às vezes é suficiente representar essa separação na
estrutura da própria condicional, mas usar classes e polimorfismo pode deixar
a divisão mais explícita.

Um caso comum é aquele em que é possível criar um conjunto de tipos,
cada qual tratando a lógica condicional de modo distinto. Posso notar que
livros, música e comida variam quanto ao modo como são tratados em razão
de seu tipo. Isso se torna mais evidente quando há várias funções com uma
instrução switch com base em um código de tipo. Nesse caso, removo a
duplicação da lógica comum do switch criando classes para cada caso e
usando polimorfismo para evidenciar o comportamento específico a cada
tipo.

Outra situação é aquela em que posso pensar na lógica como um caso básico
com variantes. O caso básico pode ser o mais comum ou o mais simples.
Posso colocar essa lógica em uma superclasse, o que me permite pensar nela
sem ter de me preocupar com as variantes. Então coloco cada caso variante
em uma subclasse, que expresso com um código que enfatiza a sua diferença
em relação ao caso base.

O polimorfismo é um dos recursos principais da programação orientada a
objetos – e, como qualquer recurso conveniente, ele é suscetível a um uso
exagerado. Já conheci pessoas que argumentam que todos os exemplos de
lógica condicional deveriam ser substituídos por polimorfismo. Não concordo
com essa visão. A maior parte de minhas lógicas condicionais faz uso de
instruções condicionais básicas – if/else e switch/case. Porém, quando vejo
uma lógica condicional complexa que pode ser melhorada conforme
discutimos antes, considero o polimorfismo uma ferramenta eficaz.

**Resumo Final**
Se o switch gera saida que possui muitas instruções, você pode usar  o polimofrismo, definir uma classe abstrata base e por porlimofirmso criar as filhas onde cada uma implementa aquele método de forma específica. Lembra o Design Pattern Strategy.




## Introduce Special Case

**Site Traduzido**
Use quando descobrir algum código em que muitos usuários de uma estrutura de dados verificam um valor específico e, em seguida, fazem a mesma coisa com ele todas as vezes. Um exemplo comum é quando o código é escrito para lidar com nulos. A ideia é ao invés de retornar null, você retorna um objeto literal que representa null e tem seu próprio método de comportamento padrão. Este é, na verdade, um padrão de codificação maior chamado Null Object Pattern, que Fowler chama de um caso especial de "Caso Especial".

**Motivação**
Um caso comum de código duplicado ocorre quando muitos usuários de uma
estrutura de dados verificam um valor específico, e então a maioria deles faz
o mesmo. Se eu encontrar muitas partes na base de código que apresentem a
mesma reação a um valor em particular, gostaria de levar essa reação para um
único lugar.

Um bom procedimento para isso é usar o padrão Caso Especial (Special
Case), no qual crio um elemento para o caso especial que capture todo o
comportamento comum. Isso permite que eu substitua a maior parte das
verificações de casos especiais por chamadas simples.
Um caso especial pode se manifestar de diversas maneiras. Se tudo que eu
estiver fazendo com o objeto é ler dados, posso fornecer um objeto literal
com todos os valores necessários preenchidos. Se eu precisar de outros
comportamentos além de valores simples, posso criar um objeto especial,
com métodos para todos os comportamentos comuns. O objeto de caso
especial pode ser devolvido por uma classe que faça um encapsulamento, ou
pode ser inserido em uma estrutura de dados com uma transformação.

Um valor comum que exige um processamento de caso especial é o valor
nulo (null), e é por isso que esse padrão muitas vezes é chamado de padrão de
Objeto Nulo (Null Object). Porém, a abordagem é a mesma para qualquer
caso especial – gosto de dizer que Objeto Nulo (Null Object) é um caso
especial de Caso Especial (Special Case).

**Resumo Final**

É o Design Pattern Null Object, ou, pode ser usada como 'Default Object Pattern'. Imagine a seguinte situação. Em uma função, se um determinado objeto tiver um determinado estado (pode ser null ou default) ele toma N ações diferentes do normal (principalmente se for o objeto nulo). Nesse cenário, será necessário em vários lugares fazer um `if(objIsNull(obj))` e assim executar uma ação. ACONTECE QUE ISSO GERA IFs DEMAIS. Ao invés de fazer isso você pode usar o NullObject. Você trata essas ações como execuções e um método de um objeto. Aí estende essa classe para um NullObject Class. Ele especifica toas as ações como nulas/falsas conforme a regra de negócio. 

Conclusão: Você trata tudo como classe, se o objeto for nulo, você executa tudo igual, mas usando o NullObject que tem os comportamentos nulos. Assim retira vários  ifs.

````
class UnknownCustomer {

  get isUnknown() {
    return true;
  }
  
  get name() {
    return "occupant";
  }
  
  get billingPlan() {
    return registry.billingPlans.basic;
  }
  
  set billingPlan(arg) {
    /* ignora */ 
  }
  
  get paymentHistory() {
    return new NullPaymentHistory();
  }

}

class NullPaymentHistory {
  
  get weeksDelinquentInLastYear() {
    return 0;
  }
  
}
````


## Introduce Assertion

**Site Traduzido**
Use quando uma seção de código só deve funcionar se certas condições forem verdadeiras. A parte importante é que isso só deve ser feito quando uma falha for causada por um erro do programador. O programa deve estar igualmente correto se todas as declarações de asserção forem removidas.

Asserções (em JS é console.assert(assert_cond, msg)` são um modo valioso de comunicação. Eles indicam o estado esperado em algum ponto do código para o programador.

**Motivação**

Com frequência, seções de código funcionam somente se determinadas
condições forem verdadeiras. Isso pode ser tão simples quanto um cálculo de raiz quadrada funcionar apenas para um valor de entrada positivo. Com um objeto, pode-se exigir que pelo menos um campo de um grupo de campos contenha um valor.

Tais pressupostos muitas vezes não são explícitos e só poderão ser deduzidos analisando um algoritmo. Às vezes, os pressupostos são explicitados com um comentário. Uma técnica melhor consiste em deixar o pressuposto explícito escrevendo uma asserção.

Uma asserção (console.assert() em JS)  é uma instrução condicional que se supõe que seja sempre verdadeira. Uma falha em uma asserção sinaliza um erro do programador. Falhas de asserção jamais devem ser verificadas por outras partes do sistema.

As asserções devem ser escritas de modo que o programa funcione igualmente de modo correto, mesmo que todas sejam removidas; com efeito, algumas linguagens oferecem asserções que podem ser desativadas com uma flag de compilação.

Muitas vezes, vejo pessoas incentivarem o uso de asserções a fim de
encontrar erros. Embora, sem dúvida, seja algo bom, esse não é o único
motivo para usá-las. Acho que as asserções são uma forma importante de
comunicação – elas dizem algo ao leitor sobre o estado em que se supõe que esteja o programa no respectivo ponto de execução. Também as acho
convenientes para depuração, e, em razão de sua importância para a
comunicação, tendo a deixá-las no código depois de ter corrigido o erro que estava procurando. Um código autotestável reduz a importância das asserções na depuração, pois testes de unidade cada vez mais localizados em geral fazem um trabalho melhor, mas continuo gostando das asserções como instrumento de comunicação.

**Resumo Final**

Use quando uma seção de código só deve funcionar se certas condições forem verdadeiras. A parte importante é que isso só deve ser feito quando uma falha for causada por um erro do programador. O programa deve estar igualmente correto se todas as declarações de asserção forem removidas.

Asserções (em JS é `console.assert(assert_cond, msg)` são um modo valioso de comunicação. Eles indicam o estado esperado em algum ponto do código para o programador. Serve mais para indicar erros por conta do if do que um passo de refatoração.



