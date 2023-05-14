# 13 - Creating Effective Documentation

## Intro

We are convinced that documentation is too important to abandon it. If done right, it will be a valuable
addition and an important building block for writing clean code, especially when Working in a Team.

We are going to cover the following main topics in this chapter:
•	 Why documentation matters
•	 Creating documentation
•	 Inline documentation

## Why documentation matters

### Why documentation is important

We create documentation because we can make it easier for other people to work with our software.
It is about context, which cannot be easily extracted from reading the code of a couple of classes.

**Documentation is often not only about the what or how, but also about the why.**

### Developer documentation

Vamos ueremos focar na documentação que o auxilia no processo de desenvolvimento e permite que você escreva um código limpo, conforme descrito na seguinte lista não exaustiva:

O que devemos documentar

+ •	 Administration and configuration guides: Besides the obvious need to describe how to install
and configure the software, make sure to include a section about code quality. This should
contain information about which tools are used locally, and how they are configured.

•	 System architecture documentation: As soon as your project becomes big enough that the
basic server setup (usually a web server and database on one physical machine) becomes a
bottleneck, and you start scaling it, you should think about documenting your infrastructure
as well. Eventually, this will save you and others a lot of time searching for the correct Uniform
Resource Locators (URLs) or server accesses, especially in critical situations. It might be a
good place to add information about the continuous integration (CI) pipeline as well.

•	 Software architecture documentation: How is your software built internally? Does it use events
to communicate between the modules? Are there any queues that should be used? Questions
such as these should be answered in the software architecture documentation. This makes it
easier for other developers to follow the principles.

•	 Coding guidelines: In addition to the software architecture documentation, coding guidelines
offer advice on how to write the code. We discussed this topic in depth in Chapter 12, Working
in a Team.

•	 API documentation: If your PHP: Hypertext Preprocessor (PHP) application has an API
that is used by other developers or even customers, you need to provide a good overview of the
API functionality. This makes theirs and your life easier, as you will have fewer interruptions
from people who want to know how the API works. You can also give good examples of how
to build additional API endpoints.

## Creating documentation

**Textos**

Para projetos pequenos, É recomendável fazer a documentaçâo como uma subpasta do projeto, colcando a documentaçâo num formato fácil de ser lido, como o Markdown. 

**Diagramas**

+ Uma ferramenta versáil é https://www.diagrams.net
+ Existe a linguagem UML que define documentaçâo mais específica
+ Outra ferramenta é o MermaidJS no seuginte link: Mermaid.js (https://mermaid-js.github.io)
+ PlantUML: https://plantuml.com
+ Diagrams-MinGrammer: https://diagrams.mingrammer.com

**DOcumentando API**

Um formato muito popular é o de OpenAPi pela ferremnta **Swagger** que describe os aspctos das API, seus end-points usando artuivo YAML (Ain't Markup Language) como  trehco a seguir

````yaml
openapi: 3.0.0
info:
  title: 'Product API'
  version: '0.1'
paths:
  /product:
    get:
      operationId: getProductsUsingAnnotations
      parameters:
        -
          name: limit
          in: query
          description: 'How many products to return'
          required: false
          schema:
            type: integer
      responses:
        '200':
          description: 'Returns the product data'
````

Apartir dess epequeno trehco o swagger consegue gera ruma página que descrive o endpoint e a emesmo pode consumí-lo.

Ao invés de escrver todo o arquivo, você pode usar ferramentas que gerarm o swagger, em  https://github.com/zircote/swagger-php

Ele vai gerar a documentaçao de acrodo com as ANnotation e comentários no método. Infelismente é necessário criar um comentário mutio grande.

**Swagger UI : Swagger UI**

(https://github.com/swagger-api/swagger-ui), which is a visual and interactive
documentation of your API.

**OpenAPI alternatives - RAML e API Blueprint**

There are other formats such as RESTful API Modeling Language (RAML) (https://
raml.org) or API Blueprint (https://apiblueprint.org) that you could use, and
we are not opinionated toward any solution.

## Inline documentation

**DockBLocks**

Anotações em comentários que usam `@`. Tanto IDES quanto outros progrmaa conseguem ler essa anotações e gerar documntação com informação.

Algumas ferramentas de qualdiade de código usam anotações para alterar o seu comportamento.

**Useless comments**

vite comentários inúteis como o a seguir:

````php
// write the string to the log file
file_put_contents($logFileName, $someString)
````
Useless comments

**When commenting is useful**

•	 To avoid confusion: If you can anticipate that other developers might wonder why you chose
that implementation, you should add more context by adding a comment.
•	 When implementing complex algorithms: Even if we try to avoid it, we sometimes have to
write code that is hard to understand—for example, if we need to implement a certain algorithm
or some unknown business logic. In these cases, a brief comment can be a lifesaver.
•	 For reference purposes: If your code implements some logic that is already explained
elsewhere—for example, in a wiki or a ticket—you can add a link to the corresponding source
to make it easier for others to find more information about it. This should only be an exception
and not the rule.

## Summary

Writing clean code is not only knowing how to do it yourself but also about making sure that other
developers will follow this path too. To be able to do this, they need to know the rules that apply to
the project.

In this chapter, we discussed how to create documentation that can help you to achieve this goal. We
discussed best practices for manually writing documentation, as well as creating informative and at
the same time maintainable diagrams. Lastly, we introduced ways to generate documentation from
the code and elaborated on the pros and cons of inline documentation.

## Further reading
If you want to learn more about Mermaid.js, we recommend the book The Official Guide to Mermaid.
js by Knut Sveidqvist and Ashish Jain, published by Packt in 2021.


