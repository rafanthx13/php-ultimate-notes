# Chapter 10 - Automated Testing

## Intro

Through automated testing, you will be able to verify that your improvements to the code did not
break its functionality in a fast and reliable way. This is one of the cornerstones of writing clean code
since it enables you to refactor code with confidence.

The topic of automated testing deserves a whole book or two, so we can only scratch the surface here.
Yet since we are convinced you will greatly benefit from it in your daily work, we hope that this chapter
will make you want to learn more about this exciting topic.
The following sections will give you a good overview:
•	 Why you need automated tests
•	 Types of automated tests
•	 About code coverage

## Techincal Reuqirmenetes

Seŕa instaaldo a extesão debug

## Vantagens do testes automatizados

Velocidade e confiabilidade: Imagine que você precise executar as mesmas etapas de teste repetidamente. Em pouco tempo, você cometeria erros ou simplesmente pularia os testes em algum momento. No entanto, os testes automatizados fazem o trabalho chato para você de uma maneira muito mais rápida e confiável - e eles não reclamam.

Documentação: Com os testes automatizados, você pode documentar indiretamente a funcionalidade do código por meio de asserções, que explicam o que se espera que o código faça. Em comparação com comentários ou artigos em uma wiki, você será imediatamente notificado pelos testes falhados quando algo tiver mudado significativamente. Abordaremos esse tópico novamente no Capítulo 13, Criando Documentação Eficaz, quando falarmos sobre a criação de documentação eficaz.

Integração de novos membros: Um conjunto de testes com boa cobertura do código ajuda novos desenvolvedores a se tornarem produtivos em um projeto mais rapidamente. Os testes não apenas atuam como documentação adicional, mas também permitem que os desenvolvedores façam alterações ou adicionem recursos com confiança. Eles podem verificar se suas alterações não quebram nada antes de serem implantadas em qualquer ambiente de preparação ou produção.

Integração contínua/implantação contínua (CI/CD): Sejam CI ou CD, se seus testes forem automatizados, você pode confiar em seu pipeline de build para garantir que o código que você mescla não esteja quebrado, o que permite que você envie código para produção mais rápido e com mais frequência. No próximo capítulo, daremos uma olhada detalhada nesse tópico.

Melhor código: Você não precisa seguir estritamente a infame abordagem de desenvolvimento orientado a testes (TDD) para se beneficiar de testes já em desenvolvimento. Escrever código testável por unidades melhora ainda mais seu código. Para testar o código isoladamente (por exemplo, sem executar um banco de dados real em segundo plano), é necessário escrever o código com separação em mente. Se as dependências externas forem injetadas usando injeção de dependência (DI), será muito mais fácil substituí-las por objetos de teste do que se elas forem instanciadas nas funções da classe. Dedicaremos um olhar mais atento ao padrão DI no Capítulo 12, Trabalhando em Equipe. Além disso, funções longas e complexas são tão difíceis de testar quanto as curtas (pense, por exemplo, na complexidade do NPath aqui, que discutimos no Capítulo 8), então você logo começará a escrever funções mais curtas para reduzir o número de caminhos de decisão em seu código.

Refatoração mais fácil: Testes automatizados são uma ferramenta inestimável quando você deseja refatorar um projeto com base nos resultados

## O que é TDD

O TDD (Test-Driven Development) é uma forma de desenvolver código que combina escrever testes e o código real ao mesmo tempo. A ideia básica é simples e é chamada de vermelho/verde/refatorar: antes de escrever qualquer código para uma nova funcionalidade ou até mesmo corrigir um erro, o primeiro passo é escrever um teste que verifica o resultado esperado. Como você ainda não escreveu nenhum código real, os testes falharão (indicado pela cor vermelha). No segundo passo, você escreve o código, sem se preocupar muito em deixá-lo perfeito, até que os testes passem (fiquem verdes). Agora que você tem testes funcionando, pode facilmente melhorar (refatorar) o código até ficar satisfeito.

O TDD garante que todo o seu código seja testado e que o código seja escrito de uma forma totalmente testável. No entanto, não leve as coisas muito a sério: há momentos em que você simplesmente quer experimentar sem ter um objetivo claro em mente, por exemplo, quando você está brincando com uma nova interface de programação de aplicativos (API). Nesses casos, você não precisa seguir o TDD.

## Com tests fic amais fácil refatorar

Os testes são importantes para a refatoração, pois ajudam a garantir a integridade do sistema durante as alterações de código. Eles fornecem uma segurança ao desenvolvedor ao detectar possíveis efeitos colaterais indesejados das alterações. Além disso, os testes funcionam como uma documentação do comportamento esperado do código, permitindo que as modificações sejam feitas com confiança e facilitando a justificativa do trabalho de refatoração.

## TIpos de testse automatizados

This concept basically shows three types of tests—namely, end-to-end tests (or E2E tests in short),
integration tests, and unit tests.

### Unit Tests

Os testes unitários são utilizados para testar pequenas unidades de código. É recomendável escrever um teste para cada funcionalidade do objeto, mantendo os testes pequenos e fáceis de entender. É comum ter centenas ou milhares de testes unitários, portanto, é importante que eles sejam executados rapidamente, em alguns microssegundos cada.

Os testes unitários devem ser executados de forma isolada, sem interação com serviços externos, como bancos de dados ou APIs. Isso é feito simulando as dependências externas por meio de objetos simulados, chamados de "mocks". Esses mocks garantem que um teste não falhe por causa de mudanças externas ao código testado.

Os testes unitários são rápidos, independentes e úteis para identificar problemas no código em segundos. Eles formam a base da pirâmide de testes e são recomendados para começar a trabalhar com testes em PHP, usando frameworks como PHPUnit. No entanto, uma limitação dos testes unitários é que eles não interagem entre si, o que pode resultar em testes passando mesmo com erros na aplicação devido a interações não testadas entre as classes.

**Padrão AAA**

O padrão AAA (Arrange-Act-Assert) é uma convenção comum para escrever testes unitários. O "Arrange" refere-se à preparação dos objetos e dos cenários necessários para o teste. O "Act" envolve a execução da funcionalidade ou do código sendo testado. O "Assert" é o momento em que verificamos se os resultados obtidos estão de acordo com as expectativas. Seguir esse padrão ajuda a organizar e estruturar os testes, tornando-os mais legíveis e compreensíveis. Se uma asserção falhar, o teste será considerado um falha.

### Integration tests

É os testes da aplicaçâo real. Nâo usamos mocks, usaremos o sistema em estado normla para testar tanto o sistema quanto as susa dependências externas

**Codeceptions**

O Codeception (https://codeception.com) combina uma variedade de tipos de testes, como testes unitários, de integração e até mesmo de ponta a ponta, em uma única ferramenta. Por baixo dos panos, ele é baseado em ferramentas existentes, como o PHPUnit. O Codeception oferece módulos para todos os principais frameworks e, portanto, se integra bem à maioria dos projetos em PHP.

**Pontos sobre os testse de integraçao**

Testes de integração envolvem a interação com dependências externas, como bancos de dados.

É necessário garantir que as dependências estejam em um estado confiável antes de executar os testes.

A preparação do banco de dados de teste inclui a criação de um banco de dados limpo, execução de migrações e preenchimento com dados de teste.

Os testes de integração tendem a ser mais lentos devido às transações de banco de dados.

A complexidade dos testes de integração aumenta devido à interação com várias dependências, tornando-os mais propensos a quebras.

É importante garantir que os testes de integração façam parte da estratégia geral de testes e sejam a segunda camada na pirâmide de testes.

Os testes de integração são úteis para verificar a integração dos objetos testados dentro do contexto da aplicação.

Além dos testes de integração, é necessário considerar testes de interação entre o PHP e o navegador, que serão abordados nos testes E2E

## Testes E2E

Com testes de ponta a ponta (E2E), queremos garantir que todo o fluxo do servidor para o cliente (por exemplo, o navegador) e de volta para o servidor esteja funcionando corretamente. Basicamente, simulamos um usuário sentado na frente do computador e navegando pela nossa aplicação.

Para conseguir fazer isso presimaos de duas coisa

+ 1. Reproduzir o ambiente que o usuário vai usar, ou seja, os sitsem 
rodadndo nolamnemente, que o banco de dados e as API estejam como um ambiente normal, pelo menos mínimamente.

+ 2.  Automatizar a interaçao do usuário. COMo o PHP é na Web, precisamso de uam ferramenta que navague de forma automatica na web.

Para isso, presiasmo de um geadless browser, uma especie de browser em CLI que nâo necessáriamnete abra uma tela e faça as operaçaoes, pois asism, evitar ter que dependede de abrir uma janela de browser para usar. Imagien por exmeplo executar isso nums erve da azure que nâo tem o browsser la. Hoje, o Chrome possui esse modo Headless, e uma ferramenta muito usada para usar essa interaçâo com o browser é o **Cypress**, um frameork wbeb para Testes E2E.

O uso do CYpress sobre o selenium foi um grande avanço, ele é muito mais fácil de usar.

Apesar disos, nem tudo sao flores. Testes E2E sâo muito mas fáceis de quebrar, pois sao baseados em elementos que podem mudar facilemnte como a DOM do HTML gerado

EXTRA ==> **Page objects**: If you are interested in creating maintainable E2E tests, you should check out the concept of
page objects (https://www.martinfowler.com/bliki/PageObject.html).

## Code covarage: quanto do seu código você realmente precisa testar?

Code coverage mede a proporção do código coberta pelos testes. Quanto maior a cobertura de código, melhor - se houver mais testes, é menos provável que o software contenha bugs e será mais difícil introduzir novos bugs sem serem percebidos. Uma cobertura de código mais alta também pode ser um indicador de melhor qualidade de código, já que o código testado geralmente é escrito de uma maneira que leva a uma melhor qualidade.

Geralmente, o grau de cobertura é expresso simplesmente usando a porcentagem de código testado, ou seja, de 0% (totalmente não testado) a 100% (cobertura de código completa). Mas como podemos medir a cobertura de código? Para isso, usaremos o PHPUnit, pois ele pode gerar um relatório de cobertura de código para nós. No entanto, é necessário uma extensão adicional do PHP para a funcionalidade de cobertura de código.

Será usado para medir essa code-coverage o Xdebug:.

## Configurando o Debug

Outras alternativas Tech: Tideways
(https://tideways.com); Blackfire (https://www.blackfire.io); PCOV (https://github.com/krakjoe/pcov) - par aomente code-coverage e mais nada)

==> Como instalar o Xdebug no Windows 

Para instalar o Xdebug no Windows, siga estas etapas:

1. Verifique a versão do PHP instalada em seu sistema Windows. Certifique-se de baixar a versão correta do Xdebug compatível com sua versão do PHP.
2. Acesse o site oficial do Xdebug (https://xdebug.org/) e navegue até a seção "Downloads".
3. Encontre a versão do Xdebug compatível com sua versão do PHP e sistema operacional Windows. Baixe o arquivo DLL correspondente.
4. Copie o arquivo DLL do Xdebug baixado para a pasta de extensões do PHP. A localização dessa pasta pode variar dependendo da sua instalação do PHP, mas geralmente está em "C:\xampp\php\ext" se você estiver usando o XAMPP.
5. Abra o arquivo php.ini em um editor de texto. Você pode encontrá-lo na pasta de configuração do PHP, geralmente em "C:\xampp\php".
6. Adicione as seguintes linhas ao arquivo php.ini:

```sh
[Xdebug]
zend_extension = "caminho/para/o/arquivo/xdebug.dll"
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
```

Certifique-se de substituir "caminho/para/o/arquivo/xdebug.dll" pelo caminho correto para o arquivo DLL do Xdebug que você copiou anteriormente.

1. Salve o arquivo php.ini e reinicie o servidor web ou o serviço PHP para aplicar as alterações.

Após a instalação, o Xdebug estará pronto para uso no seu ambiente PHP no Windows. Verifique a documentação oficial do Xdebug para obter informações adicionais sobre a configuração e o uso do Xdebug.

## Como gerar code coverage repots

.........
.........
.........
Trecho que explica como usar o Xdebug para code coverage
.........
.........
.........

## O que testar

evemos buscar uma cobertura de código completa, 100%?

Seguido o prncípio de Parreto, já chegar a 80% de code coverage já está bom. COncentre-se na regra de negócio mias importantes.

Há também casos de getters e setters que nâo presisam ser testados, entao, ter 100 de code coverage vai gerar muito trabalho pra pouco ganho.

Outros exemplos são arquivos de configuração, factories ou definições de rotas. É suficiente usar testes E2E ou de integração, que garantem que a aplicação funcione em geral. Eles testam implicitamente (ou seja, sem usar asserções concretas) todo o código de "cola", que é todo o código que mantém sua aplicação unida, mas é tedioso de testar.

Em particular, os testes E2E geralmente não são contabilizados na métrica de cobertura de código porque é tecnicamente difícil fazê-lo. Se você os tiver, no entanto, eles adicionam uma camada extra de cobertura de teste que não pode ser medida. Você não pode se orgulhar de ter 100% de cobertura de código, mas sabe que todos os diferentes tipos de teste estão cobrindo você, e esse deve ser nosso objetivo principal.

## Summary

In this chapter, we discussed why you should use automated testing and how it improves your code
quality. We covered the main three testing types, which are unit testing, integration testing, and E2E
testing, with their pros and cons, potential pitfalls, and our recommendations on how to use them.
Finally, you learned about the concept of code coverage, and how to use it in your own projects.

Together with the knowledge from the previous chapter about code quality tools and how to organize
them, in the next chapter, we can finally start combining all these tools together into a process that
helps to run all of them in structured and reliable ways—build pipelines.

## Further reading

Existem mais tipos de teste do que poderíamos abordar neste capítulo. Se você achar o mundo dos testes automatizados tão fascinante quanto os autores, pode ser interessante explorar outros tipos de teste, como os seguintes:

- Teste de mutação envolve modificar o código a ser testado com pequenas alterações (chamadas de mutantes). Se seus testes conseguem capturar esses mutantes, geralmente estão bem escritos; caso contrário, permitirão que o mutante escape. A ferramenta mais conhecida para esse tipo de teste no mundo do PHP é o Infection ([https://infection.github.io](https://infection.github.io/)).

- Teste de regressão visual compara literalmente capturas de tela da aplicação feitas durante os testes com capturas de tela originais para identificar problemas em Cascading Style Sheets (CSS). Embora não seja diretamente relacionado ao PHP, pode ser interessante se você quiser manter a aparência do seu projeto web perfeita. Uma boa opção para verificar é o BackstopJS (https://github.com/garris/BackstopJS).

- Teste de API pode ser considerado um teste E2E, mas apenas para a API que sua aplicação pode fornecer. Como os testes são baseados em solicitações HTTP, um navegador sem interface gráfica não é necessário, o que facilita a configuração. Uma boa escolha para começar com testes de API é o Codeception ([https://codeception.com](https://codeception.com/)).

- Desenvolvimento orientado a comportamento (BDD) é uma abordagem muito interessante, pois se concentra na comunicação entre as partes interessadas (por exemplo, o gerente de projeto), QA (se houver) e os desenvolvedores. Isso é feito por meio de uma forma especial de escrever testes em uma linguagem chamada Gherkin, que basicamente permite que pessoas não técnicas escrevam conjuntos de testes. A ferramenta de BDD para PHP é chamada Behat (https://github.com/Behat/Behat).

Resumo: Existem outros tipos de teste além dos abordados neste capítulo. Alguns exemplos incluem teste de mutação, teste de regressão visual, teste de API e desenvolvimento orientado a comportamento (BDD). Cada um tem suas características e ferramentas específicas, e podem ser explorados para complementar as estratégias de teste.
























