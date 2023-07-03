# Chapter 06

SITE: https://gist.github.com/cs-cordero/3799f26699bdecdb286fd719f08122af#extract-function-106

Site de código:

https://carbon.now.sh/

Site com imagme e código

https://refactoring.com/catalog/extractFunction.html

Editor

https://languagetool.org/pt-BR

User o languagetool para corrigir no final;
Recorte e inria o texto e depis insira corrigdo no md


## Extract Function (106)

SITE: https://gist.github.com/cs-cordero/3799f26699bdecdb286fd719f08122af#extract-function-106

SITE: Use quando as funções forem muito longas. Código usado mais de uma vez deve ser colocado em sua própria função. Se você se esforçar olhando para um fragmento de código e descobrindo o que ele está fazendo, transformá-lo em uma função com um nome que descreva isso é uma boa ideia.


Extrair função é uma das refatorações mais comuns

Durante minha carreira, já ouvi vários argumentos sobre quando colocar um código em sua própria função. Algumas dessas diretrizes baseavam-se no tamanho: funções não devem ser maiores que o tamanho de uma tela. Outras eram baseadas em reutilização: qualquer código usado mais de uma vez deve ser colocado em sua própria função, mas um código utilizado somente uma vez deve permanecer interno. O argumento que mais faz sentido para mim, no entanto, é a separação entre intenção e implementação. Se você tiver de dispender esforços para observar um fragmento de código e descobrir o que ele faz, então deve extraí-lo em uma função e atribuir-lhe um nome com base no “o quê”. Então, quando o ler novamente, o propósito da função estará evidente, e, na maioria das vezes, você não terá de se preocupar sobre como a função atende ao seu propósito (que está no corpo da função). Após ter aceitado esse princípio, desenvolvi o hábito de escrever funções muito pequenas – tipicamente, com apenas algumas linhas. Para mim, qualquer função com mais de meia dúzia de linhas de código começa a exalar um cheiro, e não é incomum que eu tenha funções com uma única linha de código.

Muitas vezes, vejo fragmentos de código em uma função maior que
começam com um comentário para dizer o que fazem. O comentário
geralmente é uma boa dica para o nome da função quando extraio esse
fragmento.

Nâo se preocupe em a funçâo ser pequena

**RESUMO**

É uma refatoração muito comum. Use quando a função estiver muito longa. Use em código usados mais de uma vez em locais diferentes (evita duplicação). Se você se esforçar olhando pro código para entender o que ele está fazendo, transforme-o em uma função com um bom nome, que descreva bem a intenção.

## Inline Function (115)

## Extract Variable (119)

## Inline Variable (123)

## Change Function Declaration (124)

## Encapsulate Variable (132)

## Rename Variable (137)

## Introduce Parameter Object (140)

## Combine Functions into Class (144)

## Combine Functions into Transform (149)

## Split Phase (154)


Use quando as funções forem muito longas. Código usado mais de uma vez deve ser colocado em sua própria função. Se você se esforçar olhando para um fragmento de código e descobrindo o que ele está fazendo, transformá-lo em uma função com um nome que descreva isso é uma boa ideia.
