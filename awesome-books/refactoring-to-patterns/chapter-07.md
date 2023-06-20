# Chapter 7. Simplification

Much of the code we write doesn't start out being simple. To
make it simple, we must reflect on what isn't simple about it
and continually ask, "How could it be simpler?" We can often
simplify code by considering a completely different solution.
The refactorings in this chapter present different solutions for
simplifying methods, state transitions, and tree structures.

Compose Method (123) is about producing methods that
efficiently communicate what they do and how they do what
they do. A Composed Method [Beck, SBPP] consists of calls to
well-named methods that are all at the same level of detail. If
you want to keep your system simple, endeavor to apply
Compose Method (123) everywhere.

Algorithms often become complex as they begin to support
many variations. Replace Conditional Logic with Strategy (129)
shows how to simplify algorithms by breaking them up into
separate classes. Of course, if your algorithm isn't sufficiently
complicated to justify a Strategy [DP], refactoring to one will
only complicate your design.

You probably won't refactor to a Decorator [DP] frequently. Yet
it is a great simplification tool for a certain situation: when you
have too much special-case or embellishment logic in a class.
Move Embellishment to Decorator (144) describes how to
identify when you really need a Decorator and then shows how
to separate embellishments from the core responsibility of a
class.

Logic for controlling state transitions is notorious for becoming
complex. This is especially true as you add more and more
state transitions to a class. The refactoring Replace State-Altering Conditionals with State (166) describes how to
drastically simplify complex state transition logic and helps you
determine whether your logic is complex enough to require a
State [DP] implementation.

Replace Implicit Tree with Composite (178) is a refactoring that
targets the complexity of building and working with tree
structures. It shows how a Composite [DP] can simplify a
client's creation and interaction with a tree structure.
The Command pattern [DP] is useful for simplifying certain
types of code. The refactoring Replace Conditional Dispatcher
with Command (191) shows how this pattern can completely
simplify a switch statement that controls which chunk of
behavior to execute.

## Compose Method

## Motivação

A Composed Method is a small, simple method that you can
understand in seconds. Do you write a lot of Composed
Methods?

Kent Beck once said that some of his best patterns are those
that he thought someone would laugh at him for writing. Composed Method [Beck, SBPP - Beck, Kent. Smalltalk Best Practice Patterns.
Upper Saddle River, NJ: Prentice Hall, 1997.] may be such a pattern.

A Composed Method is composed of calls to other methods.
Good Composed Methods have code at the same level of detail.

Most refactorings to Composed Method involve applying Extract
Method [F] several times until the Composed Method does most
(if not all) of its work via calls to other methods. The most difficult
part is deciding what code to include or not include in an
extracted method.

If you extract too much code into a method,
you'll have a hard time naming the method to adequately
describe what it does. In that case, just apply Inline Method [F] to
get the code back into the original method, and then explore
other ways to break it up.

O que você tem no final:
Once you finish this refactoring, you will likely have numerous
small, private methods that are called by your Composed
Method. Some may consider such small methods to be a
performance problem. They are only a performance problem
when a profiler says they are. I rarely find that my worst
performance problems relate to Composed Methods; they almost
always relate to other coding problems.

If you apply this refactoring on numerous methods within the
same class, you may find that the class has an overabundance
of small, private methods. In that case, you may see an
opportunity to apply Extract Class [F].

Another possible downside of this refactoring involves
debugging. If you debug a Composed Method, it can become
difficult to find where the actual work gets done because the logic
is spread out across many small methods.

A Composed Method's name communicates what it does, while
its body communicates how it does what it does. This allows you
to rapidly comprehend the code in a Composed Method. When
you add up all the time you and your team spend trying to
understand a system's code, you can just imagine how much
more efficient and effective you'll be if the system is composed of
many Composed Methods.

## Prós e COntras

Benefits and Liabilities

+ Efficiently communicates what a method does and
how it does what it does.
+ Simplifies a method by breaking it up into well-
named chunks of behavior at the same level of
detail.


– Can lead to an overabundance of small methods.
– Can make debugging difficult because logic is spread
out across many small methods.

## Mecânica

Mechanics
This is one of the most important refactorings I know.
Conceptually, it is also one of the simplest—so you'd think that
this refactoring would lead to a simple set of mechanics. In
fact, it's just the opposite. While the steps themselves aren't
complex, there is no simple, repeatable set of steps. Instead,there are guidelines for refactoring to Composed Method,
some of which include the following.

+ Think small: Composed Methods are rarely more than ten
lines of code and are usually about five lines.

+ Remove duplication and dead code: Reduce the amount
of code in the method by getting rid of blatant and/or
subtle code duplication or code that isn't being used.

+ Communicate intention: Name your variables, methods,
and parameters clearly so they communicate their
purposes (e.g., public void addChildTo(Node
parent)).

+ Simplify: Transform your code so it's as simple as
possible. Do this by questioning how you've coded
something and by experimenting with alternatives.

+ Use the same level of detail: When you break up one
method into chunks of behavior, make the chunks operate
at similar levels of detail. For example, if you have a piece
of detailed conditional logic mixed in with some high-level
method calls, you have code at different levels of detail.
Push the detail down into a well-named method, at the
same level of detail as the other methods in the
Composed Method.

## Exemmplo

Foi usado os seguintas refact-actions:
+ Extract Method [F]




## Replace Conditional Logic with Strategy

Conditional logic in a method controls which of several
variants of a calculation are executed.

Create a Strategy for each variant and make the method
delegate the calculation to a Strategy instance.

## Motivação

"Simplifying Conditional Expressions" is a chapter in
Refactoring [F] that contains over a half-dozen highly useful
refactorings devoted to cleaning up conditional complexity.

Replace Conditional Logic with Strategy (129) envolve composição de objetos: você produz uma família de classes para cada variação do algoritmo e equipa a classe hospedeira (quem vai fazer a chamada) com uma instância de Estratégia para a qual a classe hospedeira delega em tempo de execução.
+ Uma solução baseada em herança pode ser alcançada aplicando a Replace Conditional with Polymorphism [F]. O pré-requisito para essa refatoração é uma estrutura de herança (ou seja, a classe hospedeira do algoritmo deve ter subclasses). Se as subclasses existirem e cada variação do algoritmo for facilmente mapeada para subclasses específicas, esta é provavelmente a refatoração preferida. Se você precisar primeiro criar as subclasses, terá que decidir se seria mais fácil usar uma abordagem de composição de objetos, como refatoração para Strategy. 
+ Se as condicionais no algoritmo forem controladas por um código de tipo, pode ser fácil criar subclasses da classe hospedeira do algoritmo, uma para cada código de tipo (consulte Replace Type Code with Subclasses [F]). Se não houver tal código de tipo, provavelmente será melhor refatorar para Strategy. Por fim, se os clientes precisarem trocar um tipo de cálculo por outro em tempo de execução, é melhor evitar uma abordagem baseada em herança, porque isso significa alterar o tipo de objeto com o qual um cliente está trabalhando em vez de simplesmente substituir uma instância de Estratégia por outra.

Ao decidir se deve refatorar para ou em direção a uma Strategy, você precisa considerar como o algoritmo incorporado em cada Strategy acessará os dados de que precisa para realizar seu trabalho. Como a seção Mecânica destaca, existem duas maneiras de fazer isso: passar a classe hospedeira (chamada de contexto) para a Strategy, para que ela possa chamar métodos de retorno para obter seus dados, ou passar os dados diretamente para a Strategy por meio de parâmetros. Ambas as abordagens têm vantagens e desvantagens, que são discutidas na seção Mecânica.

Os padrões Strategy e Decorator oferecem maneiras alternativas de eliminar a lógica condicional associada a comportamentos especiais ou alternativos. A seção lateral Decorator vs. Strategy na seção Motivação de Move Embellishment to Decorator(144) oferece uma visão de como esses dois padrões diferem.

Ao implementar um design baseado em Strategy, você deve considerar como sua classe de contexto obterá sua Strategy. Se você não tiver muitas combinações de Strategies e classes de contexto, é uma boa prática proteger o código do cliente de ter que se preocupar tanto em instanciar uma instância de Estratégia quanto em equipar um contexto com uma instância de Strategy. Encapsulate Classes with
Factory (80) ca (80) pode ajudar com isso: basta definir um ou mais métodos que retornem uma instância de contexto, devidamente equipada com a instância apropriada de Estratégia.


### Prós e COntras

Benefícios
+ Esclarece algoritmos ao diminuir ou remover lógica condicional.
+ Simplifica uma classe ao mover variações de um algoritmo para uma hierarquia.
+ Permite que um algoritmo seja trocado por outro em tempo de execução.

Responsabilidades
- Complica um design quando uma solução baseada em herança ou uma refatoração de "Simplificar Expressões Condicionais" [F] é mais simples.
- Complica como os algoritmos obtêm ou recebem dados de sua classe de contexto.

## COmo fazer



## Exemplo



Temos a clsse LOan (emprstimo) que calcula emprestimos. Hoje, ela tem 4 formas de fazer (4 possiveis campinhos) que envolve chamar outras funçẽs



```java
public class Loan {

    // Metodo princiapl que queremos aplicar o Strategy
    public double capital() { 
        if (expiry == null && maturity != null) // 1
            return commitment * duration() * riskFactor(); 
        if (expiry != null && maturity == null) {
            if (getUnusedPercentage() != 1.0) // 2
                return commitment * getUnusedPercentage() * duration() * riskFactor();         
            else // 3
                return (outstandingRiskAmount() * duration() * riskFactor()) + (unusedRiskAmount() * duration() * unusedRiskFactor()); 
        } 
        return 0.0; // 4
    }
    
    /* *** FUNÇÕES ADICIONAIS  de capital() **/
    
    private double outstandingRiskAmount() { 
        return outstanding; 
    } 
    
    private double unusedRiskAmount() { 
        return (commitment - outstanding); 
    }
    
    public double duration() { 
        if (expiry == null && maturity != null) 
            return weightedAverageDuration(); 
        else if (expiry != null && maturity == null) 
            return yearsTo(expiry); 
        return 0.0; 
    }
    
    private double weightedAverageDuration() { 
        double duration = 0.0; 
        double weightedAverage = 0.0;
        double sumOfPayments = 0.0;
        Iterator loanPayments = payments.iterator(); 
        while (loanPayments.hasNext()) { 
            Payment payment = (Payment)loanPayments.next(); 
            sumOfPayments += payment.amount(); 
            weightedAverage += yearsTo(payment.date()) * payment.amount();
        } 
        if (commitment != 0.0) 
            duration = weightedAverage / sumOfPayments;
         return duration; 
    }
    
    private double yearsTo(Date endDate) {
        Date beginDate = (today == null ? start : today); 
        return ((endDate.getTime() - beginDate.getTime()) / MILLIS_PER_DAY) /  DAYS_PER_YEAR;
    }
    
    private double riskFactor() { 
        return RiskFactor.getFactors().forRating(riskRating);
    }
    
    private double unusedRiskFactor() { 
        return UnusedRiskFactors.getFactors().forRating( riskRating); 
    }
    
    
}
```



Como vai ficar as Strategy

```java
public abstract class CapitalStrategy { 
    
    	// Variaveis usadas no processo
    private static final int MILLIS_PER_DAY = 86400000; 
    private static final int DAYS_PER_YEAR = 365;
    public abstract double capital(Loan loan); 
    
    protected double riskFactorFor(Loan loan) { 
        return RiskFactor.getFactors().forRating(loan.getRiskRating()); 
    } 
    
    public double duration(Loan loan) { 
        return yearsTo(loan.getExpiry(), loan); 
    } 
    
    protected double yearsTo(Date endDate, Loan loan) { 
        Date beginDate = (loan.getToday() == null ? loan.getStart() : loan.getToday()); 
        return ((endDate.getTime() - beginDate.getTime()) / MILLIS_PER_DAY) / DAYS_PER_YEAR; 
    } 
    
}
```



..

```java
public class CapitalStrategyTermLoan extends CapitalStrategy { 
    
    public double capital(Loan loan) { 
        return loan.getCommitment() * duration(loan) * riskFactorFor(loan); 
    } 

    public double duration(Loan loan) { 
        return weightedAverageDuration(loan); 
    }

    private double weightedAverageDuration(Loan loan) { 
        double duration = 0.0; 
        double weightedAverage = 0.0; 
        double sumOfPayments = 0.0; 
        Iterator loanPayments = loan.getPayments().iterator(); 
        
        while (loanPayments.hasNext()) { 
            Payment payment = (Payment)loanPayments.next(); 
            sumOfPayments += payment.amount(); 
            weightedAverage += yearsTo(payment.date(), loan) * payment.amount(); 
        } 
        
        if (loan.getCommitment() != 0.0) 
            duration = weightedAverage / sumOfPayments; 
        
        return duration; 
    }
}
```

Classe principal

```java
public class Loan { 
    
    	private CapitalStrategy capitalStrategy; 
    
    private Loan(..., CapitalStrategy capitalStrategy ) { 
        // ... 
        this.capitalStrategy = capitalStrategy; 
    }
    
     public static Loan newTermLoan( double commitment, Date start, Date maturity, int riskRating) { 
        return new Loan( commitment, commitment, start, null, maturity, riskRating, new CapitalStrategyTermLoan() );
    }
    
    public static Loan newRevolver( double commitment, Date start, Date expiry, int riskRating) { 
        return new Loan( commitment, 0, start, expiry, null, riskRating, new CapitalStrategyRevolver() ); 
    } 
    public static Loan newAdvisedLine( double commitment, Date start, Date expiry, int riskRating) { 
        if (riskRating > 3) 
            return null; 
        
        Loan advisedLine = new Loan( commitment, 0, start, expiry, null, riskRating, new CapitalStrategyAdvisedLine());
        advisedLine.setUnusedPercentage(0.1); 
        return advisedLine;
    }
    
    public double capital() { 
        return capitalStrategy.capital(this); 
    }
    public double duration() {
        return capitalStrategy.duration(this); 
    }

    
}
```

O que fiz:

+ Ao criar Loan, a depender de qual MethodFactory eu escolher, eu especifico diferntes objetos CaptiralStrategy e asism posso realizad o cálculo sem me preocupar com a lógica
+ 

7-2-1-schema-no-final

**Como ficaria o tetes disso**

```java
public class CapitalCalculationTests extends TestCase { 

    public void testTermLoanSamePayments() { 
        Date start = november(20, 2003); 
        Date maturity = november(20, 2006); 
        // Cria a classe
        Loan termLoan = Loan.newTermLoan(
            LOAN_AMOUNT, start, maturity, HIGH_RISK_RATING); 
        termLoan.payment(1000.00, november(20, 2004)); 
        termLoan.payment(1000.00, november(20, 2005)); 
        termLoan.payment(1000.00, november(20, 2006)); 
        // Testa os metodos capital e duraction
        assertEquals("duration", 2.0, termLoan.duration(), TWO_DIGIT_PRECISION); 
        assertEquals("capital", 210.00, termLoan.capital(), TWO_DIGIT_PRECISION); 
    }
    
}
```

7-2-1-schema-no-final.png

## Move Embellishment to Decorator

### Explicação com ChatGPT

"Move Embellishment to Decorator" é um padrão de refatoração que envolve mover a lógica de embelezamento de um objeto para um decorator separado. O objetivo é separar a funcionalidade de embelezamento da lógica principal do objeto, tornando o código mais modular, reutilizável e seguindo o princípio de responsabilidade única.

Aqui está um exemplo em PHP para ilustrar o processo de "Move Embellishment to Decorator" passo a passo:

Passo 1: Identificar o embellishment
Identifique a funcionalidade específica que deseja mover para o decorator. Neste exemplo, vamos supor que temos uma classe `Texto` que possui um método `gerarTexto()` e queremos adicionar um comportamento adicional de adicionar um cabeçalho ao texto.

```php
class Texto {
    public function gerarTexto() {
        return "Conteúdo do texto";
    }
}
```

Passo 2: Criar o decorator
Crie uma classe decorator separada que irá encapsular a funcionalidade de embelezamento. Neste exemplo, vamos criar a classe `TextoDecorator` que adicionará um cabeçalho ao texto.

```php
class TextoDecorator {
    protected $texto;

    public function __construct(Texto $texto) {
        $this->texto = $texto;
    }

    public function gerarTexto() {
        $cabeçalho = "Cabeçalho do Texto\n";
        $conteúdo = $this->texto->gerarTexto();
        return $cabeçalho . $conteúdo;
    }
}
```

Passo 3: Mover a lógica de embelezamento para o decorator
Mova a lógica de embelezamento do objeto original para o decorator. No exemplo, movemos a lógica de adicionar o cabeçalho para o método `gerarTexto()` da classe `TextoDecorator`.

Passo 4: Aplicar o decorator
Aplique o decorator ao objeto original. No exemplo, vamos criar uma instância da classe `Texto` e, em seguida, criar uma instância da classe `TextoDecorator`, passando o objeto `Texto` como parâmetro.

```php
$textoOriginal = new Texto();
$textoDecorado = new TextoDecorator($textoOriginal);
```

Passo 5: Utilizar o objeto decorado
Utilize o objeto decorado como se fosse o objeto original. No exemplo, chamamos o método `gerarTexto()` no objeto `TextoDecorator`, que agora inclui o comportamento de adicionar um cabeçalho.

```php
echo $textoDecorado->gerarTexto();
```

A saída resultante será:

```
Cabeçalho do Texto
Conteúdo do texto
```

Ao seguir esses passos, movemos a lógica de embelezamento para um decorator separado, separando as responsabilidades e tornando o código mais modular e reutilizável. O objeto decorado pode ser facilmente personalizado com diferentes decoradores para adicionar ou remover funcionalidades extras de forma flexível.

**Minhas Consideraçôes**:

+ Decorator é recusao, onde você tem o objeto base (que fica no final e é o ultimo a ser executado) e vai vai empilhando chamaos sobre eles (cada chamada é um decorator).
  + A ideia é que cada decorator faça algo independente e assim um nao atrapalhe o outro e que nem a odem deles altere as coisa  (ou, pode até mesmo alterar, dando mais funcionaldaide por essa questão de ordenação)
  + A vantagem é, se quiser adicionar mais alguma coisa, é só criar uma classe decorator e jogar na stack
+ No final, esse exemplo do ChatGPT explica bem o decorator mas não explica o exemplo dado no livro

## Mecanism do livro

1 - Antes de começar esta refatoração, você deve identificar umclasse embelezada, uma classe que contém um embelezamento para sua responsabilidade principal.

+ Será a calsse base, no cal vai ser a ultima a ser executarda. é nela que ficara na base da stack de chaamdas

2 - .Identifique ou crie um tipo de exosure, uma interface ou classe que declara todos os métodos públicos necessários aos clientes da classe embelezada. Um tipo de gabinete é conhecido como Decorador:

+ Joque tudo no guardachuva d euma só interface

3 - Encontre a lógica condicional (umatrocarousedeclaração) que adiciona o embelezamento à sua classe embelezada e remove essa lógica aplicando Substituir condicional por polimorfismo

4 - A etapa anterior produziu uma ou mais subclasses da classe embelezada. Transforme essas subclasses em delegar classes aplicandoSubstituir Herança por Delegação[F ]. Ao implementar essa refatoração, certifique-se de fazer o seguinte.

+ Faça com que cada classe delegante implemente o tipo de gabinete.
+ Faça com que o tipo do campo delegado da classe delegante seja o tipo de inclusão. 
+ Decida se seu código de embelezamento será executado antes ou depois que sua classe delegante fizer sua chamada para o delegado.

5 - Cada classe delegante agora atribui seu campo delegado a uma nova instância da classe embelezada. Certifique-se de que essa lógica de atribuição exista em um construtor de classe de delegação. Em seguida, extraia a parte da instrução de atribuição que instancia a classe embelezada em um parâmetro aplicandoExtrair Parâmetro (346). Se possível, remova quaisquer parâmetros de construtor desnecessários aplicando repetidamenteRemover Parâmetro[F ].

**É extramamente confuso, ele passa 1/3 para chegar na hora em que vê a chance de colocar o decortaor, e no 1/3 final refatoranadno mais ainda. No final nem sei se dá certo ou não**

## Replace State-Altering Conditionals with State

## Replace Implicit Tree with Composite

Envolve árvore o qu quqsse nunca se usa

## Replace Conditional Dispatcher with Command
