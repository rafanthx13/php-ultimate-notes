# 09 - Organizing Data

SITE: https://gist.github.com/cs-cordero/3799f26699bdecdb286fd719f08122af#extract-function-106

Site de código:

https://carbon.now.sh/

Site com imagme e código

https://refactoring.com/catalog/extractFunction.html

Editor

https://languagetool.org/pt-BR

User o languagetool para corrigir no final;
Recorte e inria o texto e depis insira corrigdo no md


## Split Variable

**Site Traduzido**
Use quando você vir um identificador de variável sendo reutilizado repetidas vezes em instruções separadas. Idealmente, um identificador deve ser declarado e usado uma vez. Haverá exceções notáveis a isso, mas, na maioria das vezes, tente obter um uso único.

**Motivação**
As variáveis têm muitos usos. Alguns desses usos resultam naturalmente em
uma variável receber valores diversas vezes. Variáveis de laço mudam a cada
execução do laço (por exemplo, i em for (let i=0; i10; i++) ). Variáveis
acumuladoras armazenam um valor calculado durante o método.

Muitas outras variáveis são usadas para armazenar o resultado de uma
porção de código extensa a fim de facilitar futuras referências. Esses tipos de
variáveis devem receber valor somente uma vez. Se receberem mais de uma
vez, é sinal de que elas têm mais de uma responsabilidade no método.
Qualquer variável com mais de uma responsabilidade deve ser substituída por
diversas variáveis, uma para cada responsabilidade. Usar uma variável para
duas tarefas distintas é muito confuso para o leitor.

**Resumo Final**
Separe em variaveis diferentes se uma mesma variavel é usada para amarzenar valores com contextos diferentes. Variáveis que servem para armazenar resultado devem receber valor somente uma vez. Se receberem mais de uma
vez, é sinal de que elas têm mais de uma responsabilidade no método.
Qualquer variável com mais de uma responsabilidade deve ser substituída por
diversas variáveis, uma para cada responsabilidade. Usar uma variável para
duas tarefas distintas é muito confuso para o leitor.


## Rename Variable

**Site Traduzido**
Use quando um novo nome transmitir melhor o propósito e o uso de uma variável.

**Motivação**
Nomes são importantes, e nomes de campo em estruturas de registro podem
ser especialmente importantes quando essas estruturas são usadas de forma
ampla em um programa. As estruturas de dados desempenham um papel
particularmente importante para a compreensão. Muitos anos atrás, Fred
Brooks disse: “Mostre-me seus fluxogramas e esconda suas tabelas, e eu
continuarei atônito. Mostre-me suas tabelas e, em geral, não precisarei de
seus fluxogramas; elas serão óbvias”. Embora eu não veja muitas pessoas
desenhando fluxogramas atualmente, a citação permanece válida. As
estruturas de dados são o segredo para entender o que está acontecendo.
Por serem tão importantes, é essencial manter essas estruturas de dados
organizadas. Como tudo, minha compreensão dos dados melhora quanto mais
eu trabalhar com o software, portanto é crucial que essa compreensão
melhorada seja embutida no programa.
Você talvez queira renomear um campo em uma estrutura de registro, mas a
ideia também se aplica a classes. Métodos getter e setter formam um campo
eficaz para os usuários da classe. Renomeá-los é tão importante quanto
renomear campos em estruturas de registro simples.

**Resumo Final**

Renomeie os campos de estruturas de dados e consequentemente seus getters e setters para transmitir melhor o seu propósito.

## Replace Derived Variable with Query

**Site Traduzido**
Use quando o uso de uma variável estiver localizado longe de locais onde essa variável pode sofrer mutação. Se possível, torne a variável derivada computada lentamente ou sob demanda. Isso torna mais fácil raciocinar qual pode ser o valor da variável em um determinado momento.

**Motivação**
Uma das maiores fontes de problemas em software são os dados mutáveis.
Mudanças em dados muitas vezes podem acoplar porções de código de modo
inconveniente, com mudanças em uma parte resultando em efeitos em cascata
difíceis de identificar. Em muitas situações, remover totalmente os dados
mutáveis não é realista – mas defendo minimizar o máximo possível o escopo
desses dados.

Uma maneira de causar um grande impacto é remover qualquer variável que
seja possível calcular facilmente. 

Um cálculo muitas vezes deixa mais claro o
significado dos dados, e estará protegido de ser corrompido se você falhar em
atualizar a variável conforme os dados originais mudarem.

Uma exceção razoável é quando o dado original para o cálculo é imutável e
podemos forçar para que o resultado seja imutável também. Operações de
transformação que criam novas estruturas de dados são, desse modo,
razoáveis de serem mantidas como estão, mesmo se puderem ser substituídas
por cálculos. Com efeito, há uma dualidade, nesse caso, entre objetos que
encapsulam uma estrutura de dados e uma série de propriedades calculadas e
funções que transformam uma estrutura de dados em outra. A alternativa com
um objeto será claramente melhor se os dados originais mudarem e você tiver
de administrar o tempo de vida das estruturas de dados derivadas. Todavia, se
os dados originais forem imutáveis, ou os dados derivados forem muito
transientes, as duas abordagens serão eficazes.

**Resumo Final**
Se uma variável é o resultado de um cálculo de outras, ao invés de calcular quando atribui as variáveis bases, faça com que o getter seja o resultado do cálculo (lazy evaluation) e o setter seja para setar forçadamente ela (pois não precisaria já que é o resultado de outras). Isso passa pelo problema de haver dados mutáveis. Se um dado mudar toda hora e essa variável computada tiver que ser recalculada isso pode gerar muito problema. Usando essa técnica de refatoração ameniza isso. "Um cálculo muitas vezes deixa mais claro o significado dos dados, e estará protegido de ser corrompido se você falhar em atualizar a variável conforme os dados originais mudarem."



## Change Reference to Value

**Site Traduzido**
Armazenar variáveis como valores em vez de referências é vantajoso porque os valores podem ser tratados como imutáveis e, quando são definidos como novos valores, um valor completamente novo pode ser instanciado e substituído. somente se você não precisar que o valor real seja compartilhado. Para isso, você precisaria de uma referência.

**Motivação**
Quando deixo um objeto, ou uma estrutura de dados, aninhado em outro,
posso tratar o objeto interno como uma referência ou como um valor. A
diferença é mais evidentemente visível no modo como trato as atualizações
nas propriedades do objeto interno. Se eu tratar esse objeto interno como uma
referência, atualizarei a sua propriedade, mantendo o mesmo objeto interno.
Se tratá-lo como um valor, substituirei o objeto interno completo por um
novo objeto com a propriedade desejada.

Se eu tratar um campo como um valor, posso mudar a classe do objeto
interno e transformá-lo em um Objeto de Valor (Value Object) [mf-vo]. De
modo geral, é mais fácil raciocinar com objetos de valor, particularmente
porque eles são imutáveis. Em geral, é mais fácil lidar com estruturas de
dados imutáveis. Posso passar um dado imutável para outras partes do
programa e não me preocupar com o fato de ele poder mudar sem que o
objeto que o inclua tenha ciência da mudança. Posso replicar valores em meu
programa sem me preocupar em manter ligações de memória. Objetos de
valor são particularmente convenientes em sistemas distribuídos e
concorrentes.

Isso também sugere quando não devo fazer essa refatoração. Se eu quiser
compartilhar um objeto entre vários objetos de modo que qualquer alteração
no objeto compartilhado seja visível a todos os colaboradores, será necessário
que o objeto compartilhado seja uma referência.

**Resumo Final**
A questão de escolha entre referência e valor influencia muito na questão de atualização. Em referência eu aumento/diminuo a variável. Por valor eu atribuo um novo valor. É PREFERÍVEL USAR POR VALOR. "É mais fácil raciocinar com objetos de valor, particularmente porque eles são imutáveis. Em geral, é mais fácil lidar com estruturas de dados imutáveis. Posso passar um dado imutável para outras partes do programa e não me preocupar com o fato de ele poder mudar sem que o objeto que o inclua tenha ciência da mudança. Posso replicar valores em meu programa sem me preocupar em manter ligações de memória. Objetos de valor são particularmente convenientes em sistemas distribuídos e concorrentes." Obviamente 'Valor' não serve quando quero compartilha um objeto em outros locais.

## Change Value to Reference

**Site Traduzido**
Inverso da referência de mudança para valor (252). Use quando desejar que o valor de alguma variável seja ditado em alguma fonte de verdade que todos os acessadores devem referenciar.

**Motivação**
Uma estrutura de dados pode ter vários registros associados à mesma
estrutura de dados lógica. Posso ler uma lista de pedidos, alguns dos quais
são para o mesmo cliente. Quando tenho um compartilhamento como esse,
posso representá-lo tratando o cliente como um valor ou como uma
referência. Com um valor, os dados do cliente serão copiados em cada
pedido; com uma referência, há apenas uma estrutura de dados à qual vários
pedidos estarão associados.

Se o cliente jamais tiver de ser atualizado, as duas abordagens serão
razoáveis. Talvez seja um pouco confuso ter várias cópias dos mesmos dados,
mas é suficientemente comum a ponto de não ser um problema. Em alguns
casos, pode haver problemas com memória em consequência das várias
cópias – mas, como qualquer problema de desempenho, isso é relativamente
raro.

A maior dificuldade em ter cópias físicas dos mesmos dados lógicos ocorre
quando é necessário atualizar os dados compartilhados. Tenho então de
encontrar todas as cópias e atualizá-las. Se eu me esquecer de uma, terei uma
inconsistência problemática em meus dados. Nesse caso, muitas vezes vale a
pena mudar os dados copiados para uma única referência. Desse modo,
qualquer alteração será visível a todos os pedidos do cliente.
Mudar um valor para uma referência resulta em apenas um objeto presente
para uma entidade, e em geral significa que preciso de algum tipo de
repositório no qual eu acesse esses objetos. Então crio o objeto para uma
entidade somente uma vez, e, em todos os demais lugares, eu o obtenho a
partir do repositório.

**Resumo Final**

Quando desejo que ao editar um valor ele afete em outros lugares, use o acesso da variável por referência. "A maior dificuldade em ter cópias físicas dos mesmos dados lógicos, ocorre quando é necessário atualizar os dados compartilhados. Tenho então de encontrar todas as cópias e atualizá-las. Se eu me esquecer de uma, terei uma inconsistência problemática em meus dados. Nesse caso, muitas vezes vale a pena mudar os dados copiados para uma única referência. Desse modo, qualquer alteração será visível a todos os pedidos do cliente. Mudar um valor para uma referência resulta em apenas um objeto presente para uma entidade, e, em geral, significa que preciso de algum tipo de repositório no qual eu acesse esses objetos. Então crio o objeto para uma entidade somente uma vez, e, nos demais lugares, eu o obtenho a partir do repositório. "
