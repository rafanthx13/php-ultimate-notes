# Best - PHP Clean Code

## 01 - What Is Clean Code and Why Should You Care?

**O QUE É CLEAN CODE**

+ Clean Code: Escrever código pensando no outro e no futuro
  - Da mesma forma que pensamos em limpar a casa para a chegada de uma visita, para não passar vergonha, assim deve ser a escrita de código.
  - Mas também, você deve aplicar clean code em projetos pessoais pois se você cria um projeto com fundametos ruins poderá pegar depois e achar melhor reescrevelo todo denovo. Além dioss, oda mesma orma que gostamos de mostrasa coisas bem feitas, nos gostaiamos de msotrar que fizemos um bomt rabalho com o código.

## 02 - Who Gets to Decide What “Good Practices” Are?

+ DRY: Duas calsses não dvem fazer a mesma coisa
+ KISS: Escreva de forma estupidaemnte simples
+ YAGNI: Faça somente o uqe é petido, nada masis nem menos. Nâo banque o vidente e começe e a projtear coisa pra seresm usadas no futuo, iisso pode casusar problema e nâo ter valor nenhum.
+ SOLID
  - S: Uma classe, uma tarefa única. Ex: MVC
  - O: Aberto ara extensao, fechado para alteração. É prefereivel usar polimofrismoa para, casa surgir uma nova features, simplesmisntes criar uma classe que implemtana/é filha de outra. Isso evita que você tenha que mexer em cosias que já estão dando cerot par apoder inserir ruma nova funcionalidede no sistema.
  - L: Faça com que possa ser possivel trocar pai/filha , variaçoes de interfaces sem prejjudicar o sistesma
  - I: Segrege bem as intefaecs, na faça uma classe ter que implentar uma interface que nâo vai suar.
  - D: Nos parametors de metosos, use interfaçce/herança ao invez e especificar a classe real. Isso garante polimofirmos
+ Scout Princplie: deixe o código melhor do que o encontrou
+ TDD: Escerve o tetes primeiro, e depois implemente pra fazer ele passar.

## 03 - Code, Don't Do Stunts

CHATO

## 04 - It is about More Than Just Code

Fala sobre o poder do PHP e sobre seu ecossistema. Chato.

## 05 - Optimizing Your Time and Separating Responsibilities

O principal desse capítulo é: Fala sobre padronizar como nomear  as coisas em projetos PHP.

+ Classes: são escritas em PascalCase, e, tanto seu nome quanto seu arquivo (PascalCse.php);
+ Script php executáveis: kebab-case
+ Web asserts e resources: kebab-case (bom para ler em url)
+ Classes abstratas: prefixo "Abstract"
+ Interfaces: sufixo Interface, exemplo: MailerINtercace
+ Atributos e métodos camelCase
+ Nomes de pasta, primeira letra maiúsculas

## 06 - PHP is Evolving – Deprecations and Revolutions

Fala de algumas novas features do PHP8. Não é interressante

## 09 - Organizing PHP Quality Tools

Esse cap apresenta outras formas de usar as ferramentas de qualidades: arquivos phar e phive.

## 10 - Automated Testing

Teste Automatizados:
+ Vantagens: Confiabilidade para fazer mudanças; Documentar; Integrar ferramentas de CI/CD e garantir um deploy sem bugs

TDD:

+ Desenvolvimento baseado em teste

+ 1- Cria testes para avaliar o input e output da funcionalidade; Ele não passa; 2. Crie a funcionalidade; 3. Termina quando conseguir fazer passar o teste

+ Vantagem: Garante que tudo o que você fez seja testável e torna o seu pensamento mais modularizado; Ter ele permite que você refatore sem quebrar em outros locais, pois os testes automatizados são rápidos

Tipos de Testes automatizados

+ Testes unitários: 
    + Testa pequenas unidades de código. Usa mocks se necessário, pois devem ser executados de forma isolada
    + Padrão AAA: Arrange-Act-Asset

+ Teste de Integração
    + Testa a comunicação entre sistemas/módulos. N
    + Não usa mocks e usa as dependências/serviços externos reais (BD)

+ Testes E2E
  - Testa toda a experiência do usuário usando o sistema, feita por um usuário: Selenium ou Cypress


Codeceptions: Teste de integração no PHP
+ O Codeception (https://codeception.com) combina uma variedade de tipos de testes, como testes unitários, de integração e até mesmo de ponta a ponta, em uma única ferramenta
+ Muito usado na comunidade PHP. É OpenSource, Free, MIT

Code Coverage:
- Seguindo a regra de pareto, faça pelo meno chega a 80%, considerando as principais partes


Ferramenta de Testes e Debug: XDebug. Outras alternativas:
  - Tech: Tideways (https://tideways.com); 
  - Blackfire (https://www.blackfire.io); 
  - PCOV (https://github.com/krakjoe/pcov) - para somente code-coverage e mais nada)

**Further reading** - Outros tipos de testes:

+ Teste de mutação:
  + É um teste que teste os testes. Ele altera o código em algumas partes e verifica se seus testes captam essas alterações. Servem para avaliar os testes automatizados
  + A ferramenta mais conhecida para esse tipo de teste no mundo do PHP é o Infection ([https://infection.github.io](https://infection.github.io/)).

+ Teste de regressão visual
  + Testa a captura das telas, serve para testar o CSS
  + Embora não seja diretamente relacionado ao PHP, pode ser interessante se você quiser manter a aparência do seu projeto web perfeita. Uma boa opção para verificar é o BackstopJS (https://github.com/garris/BackstopJS).

+ Teste de API
  + Como os testes são baseados em solicitações HTTP, um navegador sem interface gráfica não é necessário, o que facilita a configuração. Uma boa escolha para começar com testes de API é o Codeception ([https://codeception.com](https://codeception.com/)).

+ BDD: Outra metodologia para escrever código com testes
  + Desenvolvimento orientado a comportamento
  + Usando uma linguagem chamada Gherkin basicamente permite que pessoas não técnicas (gerente, cliente) escrevam conjuntos de testes. A ferramenta de BDD para PHP é chamada Behat (https://github.com/Behat/Behat).

## 11 - Continuous Integation

O que é CI:
+  Processo automatizado de reunir todos os componentes necessários de sua aplicação em um pacote entregável para poder ser implantado nos ambientes desejados. Durante o processo, verificações automatizadas garantirão a qualidade geral do código. É importante ter em mente que, se uma das verificações falhar, toda a construção será considerada falha.
+ Exemplo de etapas:
1.  Usar o PHPlinter para garantir a corretude sintática do código.
2.  Executar um code style checker para manter a formatação do código alinhada.
3.  Encontrar possíveis problemas usando análise de código estático.
4.  Executar todos os conjuntos de testes automatizados para garantir que seu código ainda funcione.
5.  Criar relatórios para as métricas de qualidade de código usadas.
6.  Limpar a pasta de compilação e criar um arquivo compactado do código para implantar.

Ferramentas de CI:
+ Existem muitas ferramentas de CI disponíveis, como o Jenkins, que geralmente é auto-hospedado (ou seja, operado por você ou alguém da sua equipe ou empresa). Ou você pode escolher serviços pagos, como GitHub Actions, GitLab CI, Bitbucket Pipelines ou CircleCI.

Neste capítulo ensina fazer CI com GitActions além de falar muita coisa sobre esse processo.

O que é CD:
+ Após passar pelo CI, já sabemos que está tudo correto, então, podemos mandar numa esteira para implantar o pacote

**Further reading** Outras leituras:

If you wish to know more, have a look at the following resources:
+ Additional information about GitHub Actions:
  + The official GitHub Actions documentation with lots of examples: 
    + https://docs.github.com/en/actions
  + `setup-php` is not only very useful for PHP developers, but also offers a lot of useful
    information—for example, about the matrix setup (how to test code against several PHP versions) or caching Composer dependencies to speed up the build:
    + https://github.com/marketplace/actions/setup-php-action
+ More information about CD and related topics can be found here:
  + A good overview of CD: https://www.atlassian.com/continuous-delivery
  + Logging and monitoring explained:
    + https://www.vaadata.com/blog/logging-monitoring-definitions-and-best-practices/
  + A great introduction to advanced deployment methods:
    +  https://www.techtarget.com/searchitoperations/answer/When-to-use-canary-vs-blue-green-vs-rolling-deployment
+ Tools and links regarding your local pipeline:
  + More insights on Git hooks: 
    + https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks
    + GrumPHP is a local CI pipeline “out of the box”: https://github.com/phpro/grumphp

## 12 - Working in a Team

Padronização do PHP = PSR
+ PER Coding Style 1.0.0 (PER é a sigla de PHP Extended Recommendation)baseada na PSR-12 (de 2019): Link: https://www.php-fig.org/per/coding-style
+ O PSR não define padronização de nomenclatura. Em questão de nomenclatura, pose-se usar, por exemplo, a da Symfony: https://symfony.com/doc/current/contributing/code/standards.html.

Guide Lines para o PHP
+ Como escrever classes: UpperCamelCase
+ Eventos UpperCamelCase
+ Propriedade, variáveis e métodos: lowerCamelCase
+ Testes: lowerCamelCase.
+ Traits: UpperCamelCase.
+ Interfaces:  UpperCamelCase.

DocBlocks

````php
/**
* @param int $property
* @return void
*/
public function setProperty(int $property): void {
    // ...
}
````

+ O capítulo fala sobre como fazer e a importância do Code Review

Design Patterns
+ Creational: Exemplifica o Factory Method`
+ Dependency Injection (DI) e Container Dependency Injection (CDI)
+ Behavorial - Observer
+ Anti-Patterns:
  - Singleton
  - Service Locator

**Futher Reading**

+ https://google.github.io/eng-practices/review provides you with more information about the code review process at Google
+ Links úteis sobre design patterns em php
  + https://refactoring.guru/design-patterns/adapter/php/example
  +  https://sourcemaking.com/design_patterns/adapter/php
  + https://designpatternsphp.readthedocs.io/en/latest/README.html

## 13 - Creating Effective Documentation

Documentar:
+ Porque fazer: Facilitar o trabalho de quem pegar o código
+ O que documentar:
  - Configurações
  - Regras de Negócio
  - Arquitetura do Sistema
  - Diretrizes e padrões usados
  - Documentar API

Formas de documentar 
+ Texto: Via Markdown
+ Diagrama: Há as seguintes opções
  - Uma ferramenta versátil é https://www.diagrams.net
  - Existe a linguagem UML que define documentação mais específica
  - Outra ferramenta é o MermaidJS no seguinte link: Mermaid.js (https://mermaid-js.github.io)
  - PlantUML: https://plantuml.com
  - Diagrams-MinGrammer: https://diagrams.mingrammer.com

Quando comentários no código são bons:
+ Quando forem DocBlocks
+ Quando o comentário evita confusão
+ Para descrever algoritmos complexos
+ Para referenciar algum outro link

Documentar API: Através do Swagger
+ Alternativas ao Swagger: Existem outros formatos, como a Linguagem de Modelagem de API RESTful (RAML) ([https://raml.org](https://raml.org/)) ou API Blueprint ([https://apiblueprint.org](https://apiblueprint.org/)), que você pode usar, e não temos preferência por nenhuma solução em particular.

**Further reading**

Se você deseja aprender mais sobre o Mermaid.js, recomendamos o livro "The Official Guide to Mermaid.js" de Knut Sveidqvist e Ashish Jain, publicado pela Packt em 2021.

