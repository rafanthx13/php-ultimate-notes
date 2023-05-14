# 06 - PHP is Evolving – Deprecations and Revolutions

## O que vai falar

Coisas novas do PHP 8

## Match Synxtax

Forma condensado do switch/case

````php
$foo = match($var) {
    ‹value 1› => Bar::myMethod1(),
    ‹value 2› => Bar::myMethod2(),
};
````

## Named arguments

Ao chamar uma funçâo, voc epode passar os nomes dos arqugmentos, asism, voce pode até mesmo mudar a odem deles

Quando usar:
+ Se , por exmeplo, o metodo tem 11 arguemtnos, tudo com valor default, e s'queremos alterar o 5 e 11. Aí, named  arguments será o ideal
+ Passar nomes para deixar mais claro

## Read-only classes and properties


````php
<?php
namespace App\Model;
class MyValueObject
{
protected readonly string $foo;
    public function __construct(string $foo)
    {
        $this->foo = $foo; // First assignment, all good
        // Any further assignment of $this->foo will result
          in a fatal error
    }
}
````

## Protecting your sensitive arguments from leaking

coloando um argumento/atributo entre #[] você impede que ele seja mostrado ao dar um vr_dump ou print_r

````php
<?php
namespace App\Controller;
class SecurityController
{
    public function authenticate(string $username,
      #[SensitiveParameter] string $password)
    {
        // In case of any exception occurring or var_dump
          being called in here, the value of $password will
          be hidden in the different outputs
    }
}
````

## Summary 

O PHP tem evoluido bastante não pode mais ser considerdo uma linguagem morta, só as suas versões anteiores
