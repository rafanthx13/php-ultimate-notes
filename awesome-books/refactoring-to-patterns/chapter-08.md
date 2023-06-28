# Chapter 8. Generalization

A generalização é a transformação de um código específico em um código de uso geral. A produção de código generalizado freqüentemente ocorre como resultado da refatoração. Todas as sete refatorações neste capítulo produzem código generalizado. A motivação mais comum para aplicá-los é remover código duplicado. Uma motivação secundária é simplificar ou esclarecer o código.

*Form Template Method* (205)ajuda a remover a duplicação em métodos semelhantes de subclasses em uma hierarquia. Se os métodos executam aproximadamente as mesmas etapas, na mesma ordem, mas as etapas são ligeiramente diferentes, você pode separar o que varia do que é genérico produzindo um método de superclasse conhecido como Template Method [DP ].

Extrair composto (214)é uma aplicação da refatoração Extrair superclasse[F ]. É aplicável quando um composto [DP ] foi implementado em várias subclasses de uma hierarquia sem um bom motivo. Ao extrair um Composite para uma superclasse, as subclasses compartilham uma implementação genérica do Composite.

Se você tiver algum código para lidar com um objeto e código separado para lidar com um grupo dos mesmos objetos (geralmente em alguma coleção),Substitua uma/muitas distinções por composição (224)irá ajudá-lo a produzir uma solução genérica que manipule um ou vários objetos sem distinguir entre os dois.

Substitua as notificações codificadas pelo Observer (236)é um exemplo clássico de substituição de uma solução específica por uma geral. Nesse caso, há um acoplamento estreito entre os objetos que notificam e os objetos que são notificados. Para permitir instâncias de outrosclasses a serem notificadas, o código pode ser refatorado para usar um Observer [DP ].

Um adaptador [DP ] fornece outra maneira de unificar interfaces. Quando os clientes se comunicam com classes semelhantes usando interfaces diferentes, tende a haver uma lógica de processamento duplicada. aplicandoUnificar interfaces com adaptador (247), os clientes podem interagir com classes semelhantes usando uma interface genérica. Isso tende a abrir caminho para outras refatorações para remover a lógica de processo duplicada no código do cliente.

Quando uma classe atua como um adaptador para várias versões de um componente, biblioteca, API ou outra entidade, a classe geralmente contém duplicação e geralmente não possui um design simples. Aplicando Extrair Adaptador (258)produz classes que implementam uma interface comum e adaptam uma única versão de algum código.

A refatoração final neste capítulo,Substituir linguagem implícita por intérprete (269), visa o código que seria melhor projetado se usasse uma linguagem explícita. Esse código geralmente usa vários métodos para realizar o que uma linguagem pode fazer, apenas de uma maneira muito mais primitiva e repetitiva. Refatorar tal código para um interpretador [DP ] pode produzir uma solução de propósito geral que é mais compacta, simples e flexível.

## Form Template Method

### O que é

**Se**

Two methods in subclasses perform similar steps in the same order, yet the steps are different.

**Refatore para**

Generalize the methods by extracting their steps into methods with identical signatures, then pull up the generalized methods to form a Template Method.

### Simplificando em uma imagem

### Schema

### Motivação

Métodos de modelo "implementam as partes invariantes de um
algoritmo uma vez e deixam para as subclasses implementarem o
comportamento que pode variar" [DP , 326]. Quando comportamentos
invariantes e variantes são misturados nas implementações de subclasse
de um método, o comportamento invariante é duplicado nasubclasses. A refatoração para um método de modelo ajuda a livrar as
subclasses de seu comportamento invariante duplicado, movendo o
comportamento para um lugar: um algoritmo generalizado em um método de
superclasse.
O comportamento invariante de um Template Method consiste no
seguinte:

+ Métodos chamados e a ordem desses métodos
+ Métodos abstratos que subclasses deve sobrepor
+ Métodos de gancho (ou seja, métodos concretos) que subclasses
  poderia sobrepor

Por exemplo, considere o seguinte código:

```java
public abstract class Game... 
    
    public void initialize() { 
        deck = createDeck(); 
        shuffle(deck); 
        drawGameBoard(); 
        dealCardsFrom(deck); 
    } 

    protected abstract Deck createDeck(); 

    protected void shuffle(Deck deck) { 
        /// ...shuffle implementation 
    } 

    protected abstract void drawGameBoard();

    protected abstract void dealCardsFrom(Deck deck);




```

A lista de métodos chamados por e ordenados dentro inicializar()é
invariante. O fato de que as subclasses devem
substituir oabstratométodos também é invariante. O embaralhar()
implementação fornecida porJogonão é invariável: é um método de gancho
que permite que as subclasses herdem o comportamento ou variem
substituindoembaralhar().

Como é muito tedioso implementar muitos métodos apenas para
desenvolver um Template Method em uma subclasse, os autores de
Padrões de design[DP ] sugerem que um Template Method deve
minimizar o número de classes de métodos abstratosdeve sobrepor.
Também não há uma maneira simples de os programadores saberem
quais métodos podem ser substituídos (ou seja, métodos de gancho) sem
estudar o conteúdo de um Método de modelo.

Métodos de modelo geralmente chamam métodos de fábrica [DP ],
como criarDeck()no código acima. A refatoraçãoIntroduzir
Criação polimórfica com método de fábrica (88)fornece um
exemplo do mundo real disso.

Linguagens como Java permitem que você declare um método de
modelo final, o que evita a substituição acidental do modelo
Método por subclasses. Em geral, isso é feito apenas se o código do cliente em um
sistema ou estrutura depender totalmente do comportamento invariável em um
Método de modelo e se permitir a reinterpretação desse comportamento invariável
puder fazer com que o código do cliente funcione incorretamente.

Martin Fowler's*Form Template Method*[F ] e minha versão
cobrem muito do mesmo terreno e podem ser consideradas como a
mesma refatoração. Minha mecânica usa uma terminologia diferente
e tem uma etapa final diferente da de Martin. Além disso, o código
que discuti na seção Exemplo ilustra um caso em que o
comportamento invariável duplicado em subclasses é sutil, enquanto
o exemplo de Martin trata de um caso em que essa duplicação é
explícita. Se você não está familiarizado com o modeloMethod pattern, você faria bem em estudar ambas as versões desta
refatoração.

### Prós e Contras

**Prós**

+ Remove código duplicado em subclasses movendo o
comportamento invariável para uma superclasse.
+ Simplifica e comunica efetivamente as etapas de um
algoritmo geral.
+ Permite que as subclasses personalizem facilmente um algoritmo.

**Contras**

+ Complica um projeto quando as subclasses devem implementar
  muitos métodos para desenvolver o algoritmo.

### Mecânica da Refatoração

1 - Em uma hierarquia, encontre ummétodo semelhante(um método em uma
subclasse que executa etapas semelhantes em uma ordem semelhante a um
método em outra subclasse). AplicarMétodo de composição
(123)no método semelhante (em ambas as subclasses), extraindo
métodos idênticos(métodos que possuem a mesma assinatura e
corpo em cada subclasse) emétodos únicos (métodos que
possuem assinatura e corpo diferentes em cadasubclasse).
Ao decidir se deseja extrair o código como um método exclusivo ou
um método idêntico, considere o seguinte: Se você extrair o código
como um método exclusivo, eventualmente (durante a etapa 5)
precisará produzir uma versão abstrata ou concreta desse método
exclusivo em a superclasse. Fará sentido que as subclasses herdem
ou sobrescrevam o método exclusivo? Caso contrário, extraia o
código em um método idêntico.

2 - Puxe os métodos idênticos para a superclasse aplicando
Método de puxar para cima[F ].

3 - Para produzir um corpo idêntico para cada versão do método
semelhante, aplique Renomear método[F ] em cada método exclusivo
até que o método semelhante seja idêntico em cada subclasse.

+ Compile e teste após cada aplicação de Renomear método[F ].

4 - Se o método semelhante ainda não tiver uma assinatura
idêntica em cada subclasse, aplique Renomear método[F ] para
produzir uma assinatura idêntica.

5 - Aplicar Método de puxar para cima[F ] no método semelhante (em
qualquer subclasse), definindo métodos abstratos na superclasse para
cada método exclusivo. O método semelhante puxado para cima agora é
um método de modelo.

+ Compilar e testar.

### Exemplo

No final do exemplo utilizado neste catálogo para a refatoração
Substitua a lógica condicional pela estratégia (129)existem três
subclasses da classe abstrata,
 `CapitalStrategy` :

img

Essas três subclasses contêm uma pequena quantidade de
duplicação, que, como veremos nesta seção, pode ser removida
aplicando *Form Template Method* . É relativamente
comum combinar os padrões Strategy e Template Method para
produzir classes Strategy concretas que tenham pouco ou nenhum
código duplicado.
O `CapitalStrategy` class define um método abstrato para o
cálculo do capital:

```java
public abstract class CapitalStrategy... 
    public abstract double capital(Loan loan);

```

Subclasses de `CapitalStrategy` calcular o capital de forma semelhante:

```jva
public class  `CapitalStrategyAdvisedLine`  {
    public double capital(Loan loan) { 
        return loan.getCommitment() * loan.getUnusedPercentage() * duration(loan) * riskFactorFor(loan); 
    }
}

public class CapitalStrategyRevolver {
    // ...
    public double capital(Loan loan) { 
        return (loan.outstandingRiskAmount() * duration(loan) * riskFactorFor(loan)) + (loan.unusedRiskAmount() * duration(loan) * unusedRiskFactor(loan)); 
    }
}

public class CapitalStrategyTermLoan {
    // ...
    public double capital(Loan loan) { 
        return loan.getCommitment() * duration(loan) * riskFactorFor(loan); 
    }

    protected double duration(Loan loan) { 
        return weightedAverageDuration(loan); 
    }
    private double weightedAverageDuration(Loan loan) {
        // ...
    }
}
```

Observe que  cálculo de  ` `CapitalStrategyAdvisedLine` `  é idêntico ao
 `CapitalStrategyTermLoan`  do, exceto por uma etapa
que multiplica o resultado pelo percentual não utilizado do
empréstimo (`loan.getUnusedPercentage()`). Identificar essa
sequência semelhante de etapas com uma ligeira variação significa
que posso generalizar o algoritmo refatorando para o Template
Method. Farei isso nas etapas a seguir e, em seguida, lidarei com a
terceira classe, `CapitalStrategyRevolver`, no final desta seção de
Exemplo.

1 - O ` `capital(...)` ` método implementado por
` `CapitalStrategyAdvisedLine` ` e `CapitalStrategyTermLoan` é o método similar
neste exemplo.

Os mecânicos me orientam a aplicarMétodo de composição
(123) no `capital()` implementações extraindo idênticos
métodos ou métodos únicos. Como as fórmulas em
 `capital()` são idênticos exceto por
 `CapitalStrategyAdvisedLine` passo de multiplicar por
 `loan.getUnusedPercentage()` , devo escolher se deseja extrair
essa etapa em seu próprio método exclusivo ou extraí-la como parte
de um método que inclui outro código. A mecânica funciona de
qualquer maneira. Nesse caso, vários anos programando
calculadoras de empréstimo para um banco me ajudam a tomar uma
decisão. O valor do risco para uma linha aconselhada é calculado
multiplicando o valor do compromisso do empréstimo por sua
porcentagem não utilizada (ou seja,empréstimo.getCommitment() *
 `loan.getUnusedPercentage()` ). Além disso, conheço a fórmula
padrão para capital ajustado ao risco:

Valor do Risco x Duração x Fator de Risco

Esse conhecimento me leva a extrair o código de
` `CapitalStrategyAdvisedLine` ` ,
`loan.getCommitment() *  `loan.getUnusedPercentage()` `, em seu próprio método,
`riskAmountFor()`, ao executar uma etapa semelhante para
`CapitalStrategyTermLoan`:

```java
public class  `CapitalStrategyAdvisedLine`  {
    public double capital(Loan loan) { 
        return riskAmountFor(loan) * duration(loan) * riskFactorFor(loan); 
    }
    private double riskAmountFor(Loan loan) { 
        return loan.getCommitment() * loan.getUnusedPercentage(); 
    }
}
public class CapitalStrategyTermLoan {
    public double capital(Loan loan) { 
        return riskAmountFor(loan) * duration(loan) * riskFactorFor(loan); 
    } 
    private double riskAmountFor(Loan loan) { 
        return loan.getCommitment(); 
    }
}
```

```java
public class  `CapitalStrategyAdvisedLine`  {
    public double capital(Loan loan) { 
        return riskAmountFor(loan) * duration(loan) * riskFactorFor(loan); 
    }
    private double riskAmountFor(Loan loan) { 
        return loan.getCommitment() * loan.getUnusedPercentage(); 
    }
}
public class CapitalStrategyTermLoan {
    public double capital(Loan loan) { 
        return riskAmountFor(loan) * duration(loan) * riskFactorFor(loan); 
    } 
    private double riskAmountFor(Loan loan) { 
        return loan.getCommitment(); 
    }
}
```

conhecimento do domínio claramente influenciou minhas decisões de
refatoração durante esta etapa. Em seu livro Design Orientado ao Domínio[
Evans ], Eric Evans descreve como o conhecimento de domínio geralmente
direciona o que escolhemos refatorar ou como escolhemos refatorá-lo.

2 - Esta etapa me pede para puxar métodos idênticos para
a superclasse, `CapitalStrategy` . Neste caso, o
 `RiskAmountFor(...)`  não é um método idêntico porque o
código em cada implementação dele varia, então eupode passar para a próxima etapa.

3 - Agora devo garantir que todos os métodos exclusivos
tenham a mesma assinatura em cada subclasse. O único
método único, `RiskAmountFor(...)` , já tem o mesmo
assinatura em cada subclasse, para que eu possa prosseguir para a próxima
etapa.
4 - Devo agora garantir que o método semelhante,  `capital(...)` , tem
a mesma assinatura em ambas as subclasses.
Ele faz, então eu prossigo para a próxima etapa.

5 - Porque o `capital(...)` método em cada subclasse agora tem a
mesma assinatura e corpo, posso puxá-lo para
 `CapitalStrategy` aplicandoMétodo de puxar para cima[F ].
Isso envolve declarar um método abstrato para o método
único, `RiskAmountFor(...)` :

```java
public abstract class CapitalStrategy {
    // public abstract double capital(Loan loan); 
    public double capital(Loan loan) { 
        return riskAmountFor(loan) * duration(loan) * riskFactorFor(loan); 
    } 
    public abstract double riskAmountFor(Loan loan);
}

```

 `capital()` agora é um método de modelo. Isso completa a
refatoração para o
 `CapitalStrategyAdvisedLine` e
 `CapitalStrategyTermLoan` subclasses.

Antes de lidar com o cálculo de capital em
`CapitalStrategyRevolver`, gostaria de mostrar o que seria
teria acontecido se eu não tivesse criado um
 `RiskAmountFor(...)`  durante a etapa 1 da refatoração. Nesse
caso, eu teria criado um método único para
 `CapitalStrategyAdvisedLine` passo de multiplicar por
 `loan.getUnusedPercentage()` . Eu teria chamado tal passo
não utilizado PercentageFor(...) e o implementou como um método
de gancho em `CapitalStrategy` :

```java
public abstract class CapitalStrategy {
    public double capital(Loan loan) { 
        return loan.getCommitment() * unusedPercentageFor(loan) * duration(loan) * riskFactorFor(loan); 
    } 
    public abstract double riskAmountFor(Loan loan); 
    protected double unusedPercentageFor(Loan loan) { // hook method 
        return 1.0;
    };
}
```

Como esse método de gancho retorna 1,0, não tem efeito nos
cálculos, a menos que o método seja substituído, como acontece
com  `CapitalStrategyAdvisedLine` :

```java
public class  `CapitalStrategyAdvisedLine`  {
    protected double unusedPercentageFor(Loan loan) {
        return loan.getUnusedPercentage(); 
    };
}
```

O método hook permite `CapitalStrategyTermLoan` 
herdar seu `capital(...)` cálculo, em vez de implementar um
 `riskAmount(...)`  método:

```java
public class CapitalStrategyTermLoan {
    // public double capital(Loan loan) { 
    //     return loan.getCommitment() * duration(loan) * riskFactorFor(loan); 
    // } 
    protected double duration(Loan loan) { 
        return weightedAverageDuration(loan); 
    } 
    private double weightedAverageDuration(Loan loan) {
        // ...
    }
}
```

Essa é outra maneira de produzir um método de modelo
para o  `capital()` Cálculo. No entanto, sofre de alguns
desvantagens:

+ O código resultante comunica mal a fórmula de capital
  ajustado ao risco (Valor do risco x Duração x Fator de risco).
+ Dois dos três `CapitalStrategy` subclasses,
   `CapitalStrategyTermLoan`  e, como veremos,
  `CapitalStrategyRevolver`, herdam o comportamento de não
  fazer nada do método hook, que, por ser uma etapa única em
   `CapitalStrategyAdvisedLine` , realmente pertence
  exclusivamente a essa classe.

Agora vamos ver como `CapitalStrategyRevolvera` proveitaria o
novo `capital()` Método de modelo. é original `capital()` método se
parece com isso:

```java
public class CapitalStrategyRevolver {
    public double capital(Loan loan) { 
        return (loan.outstandingRiskAmount() * duration(loan) * riskFactorFor(loan)) + (loan.unusedRiskAmount() * duration(loan) * unusedRiskFactor(loan)); 
    }
}
```

A primeira metade da fórmula se assemelha à fórmula geral, Valor do Risco
x Duração x Fator de Risco. A segunda metade da fórmula é semelhante,
mas trata da parte não utilizada de um empréstimo. Podemos refatorar
esse código para aproveitar as vantagens do Template Method da seguinte
maneira:

```java
public class CapitalStrategyRevolver {
    public double capital(Loan loan) { 
        return super.capital(loan) + (loan.unusedRiskAmount() * duration(loan) * unusedRiskFactor(loan)); 
    } 
    protected double riskAmountFor(Loan loan) { 
        return loan.outstandingRiskAmount(); 
    }
}
```

Você poderia argumentar se esta nova implementação é mais fácil
de entender do que a anterior. Certamente alguma duplicação na
fórmula foi removida. No entanto, a fórmula resultante é mais fácil
de seguir? Acho que sim, porque comunica que o capital é
calculado de acordo com a fórmula geral com a adição de capital
não utilizado. A adição de capital não utilizado pode ser tornada
mais clara aplicando Extrair método[F ] sobre  `capital()` :

```java
public class CapitalStrategyRevolver {
    public double capital(Loan loan) { 
        return super.capital(loan) + unusedCapital(loan); 
    } 
    public double unusedCapital(Loan loan) { 
        return loan.unusedRiskAmount() * duration(loan) * unusedRiskFactor(loan); 
    }
} 
```



## Extract Composite

## Replace One/Many Distinctions with Composite

## Replace Hard-Coded Notifications with Observer

## Unify Interfaces with Adapter

## Extract Adapter

## Replace Implicit Language with Interpreter

### O que é

### Simplificando em uma imagem

### Schema

### Motivação

### Prós e Contras

### Mecânica da Refatoração

### Exemplo