# 01 - What Is Clean Code and Why Should You Care?

## Pontos que esse capítulo vai discuritr

•	 What this book will cover
•	 Understanding what clean code is
•	 The importance of clean code in teams
•	 The importance of clean code in personal projects

11:18 = 11:40 = 21min (8 páginas)

Significado de PHP: Hypertext PreProcessor

Clean Code: É um midset. E quanto mais cedo você pensar nele melhor. É como um haábito
+ Muita gente nsao se preocupa com clean code ou pir faze rprojtos sozinhos ou por mexer em código legado

## What this book will cover

That is why this book focuses on clean code in PHP especially.

Only basic knowledge of PHP is required to fully
understand what will be exposed.
This book is a compilation of years of experience—years of practice in the field, faced with real
problems that had to be solved according to technical constraints, functional constraints, and time
and money constraints. This will not be yet another book full of utopian principles that cannot be
applied in real life.

### Divisao me partes deste livro

It is divided into two distinct parts:

**PART 1**

 The first one (which you are currently reading)
will expose a bit of theory about what is clean code and what are basic principles of it, directly applied
to the PHP language up to version 8.2, and so on. 

**PART 2**

The second part will be focused on practical tools
you can use to ensure you are following the right rules the correct way, setting up an environment and
your integrated development environment (IDE) in order to be as efficient and clean as possible,
and getting metrics on your code, automated testing, writing documentation, and more. 

This means
you can skip parts, take them in the order you want, and learn at the speed you want.

## Understanding what clean code is

O QUE É CLEAN CODE

Clean code is the act of writing code by thinking of the future—that is, thinking of the people who
will collaborate with you or on the project without you. And when we are talking about “the people
who will collaborate with you”, this may even be yourself. If you never did, you should try to read
and maintain the source code you wrote a few months (or years) ago. Isn’t it challenging? Well, do
not worry—it is hard for everyone. You will surely find this complicated for many years, and there is
no quick fix to this. It is the same process for everyone.

## The importance of clean code in teams

Quando você chega em um projeto que ja'está sendo tocado,  você precisa aprender muita coisa para entedlo, arquitetura, dependencias, libs e isso pode demorar semans ou meses a epender do projeot e sua complexidade

Being able to write clean code is like speaking fluently in the same language as the other people in
the team: it makes it easier to communicate and write code in the same way without noticing who
has written which part.

Clean code will help you with code longevity. When working as a team on a project, there are great
chances the source code will be maintained for at least a few years. The code will continue to be
maintained years after your departure. It is important to do things right because you will not be here
forever to explain everything you did to the person still working on the project.

Escrever Clean code garante que se evite SPOFs (single points of failure) que são o pesadelo em sistemas legados. É uma entidade que, se falha, falha todo o projeto

==> Exemplo de SPOF: Um desenvolvedor que sabe tudo

A concrete example of an entity failing is the departure of a developer. If they are the only person to
utterly understand how the project works and is considered the “superhero” of the project, then it
is a big problem. This means the project will not be able to continue without them, and it will be an
absolute pain to maintain the project after their departure.

==> Como evitar isso: Clena COde

One of the numerous ways to avoid this problem is by writing clear, concise, and understandable
code—writing code in a way everybody can easily understand what is happening. After getting into
this book, you may have a better idea of how to achieve this.

==> COde REview

Talking about teamwork, another critical point is code reviews. Even if we will be getting into the
details of these later in this book, let’s talk about them quickly here. If you have never heard of a
code review, it is simply a process where other developers of the projects are reviewing, reading, and
commenting on the changes you want to bring to the code base. This process is mandatory in most
open source projects and highly recommended for any project, given the benefits it brings. You can
now easily imagine that if everyone has their own way to write code, those reviews are going to take
way longer. This goes from the way you format your code or how you separate files, classes, and so
on. If we all speak the same language, then we can focus on things that really matter during the code
review: if the functional need is respected, whether there are any bugs, and so on.

## The importance of clean code in personal projects

You may think that clean code is less important for personal projects, even just a tiny bit. You would
be wrong if you think like this for many reasons, as set out here:

+ QUe garantia alguem nao pode pegar o seu código para desenvolver algo no futuro?
+ Se você faz um projeto OpenSource, você não gostaria que o mundo visse que você usa celan-code
+ You will probably want to improve your project repeatedly. If you write bad foundations, it
will be a nightmare to maintain and add new things without the fear of breaking anything.
Sometimes, it is impossible to add new features because of bad code writing. In the worst cases,
you will have to entirely rewrite your application. You do not want to do that.


...

As the saying goes, “write code as if the next developer to run it knows your address”. And this should
also apply to personal projects because you are that very next developer.

## Summary

Are we done yet with the theory? Well, kind of. We defined together what clean code consists of. We
gave a mutual definition of clean code. By having the same definition of clean code, we are one step
deeper into it, and ready to dive into more advanced principles in the next section.

But of course, we are not done yet. Even if you agree with the definition we presented, you may of
course have a lot of questions already. And the most important questions should be the following:
Who decides these rules for you? Who has the power to impose this vision? This is what we are going
to see together in the next chapter.
