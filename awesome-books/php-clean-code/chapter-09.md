# Organizing PHP Quality Tools - CHapter 9

Nesse capitulo vamos aprende coomo configurar da melhor formas essa ferramenas de qualiade de sofware do PHP no nosso preojeot, iremos ver 3 formas: composer, phar files e pHive

•	 Installing code quality tools using Composer
•	 Installing code quality tools as phar files
•	 Managing phar files using the PHAR Installation and Verification Environment (Phive)

**Só irei lsitar o compsoer**

## Installing code quality tools using Composer

$ composer require phpmetrics/phpmetrics --dev

**Ovce poed baisar o phpmetrics também de forma global**

$ composer global update

$ composer global require phpmetrics/phpmetrics

### COnfigurar composer.json

````json
{
  ...
  "scripts": {
    "analyze": [
      "vendor/bin/php-cs-fixer fix src",
      "vendor/bin/phpstan analyse --level 1 src"
    ]
  }
}
````

If you want to share these Composer commands, you might want to add a short description text as
well, which is displayed when you execute composer list to see a list of available commands.
To do that, you need to add the script-descriptions section to your composer.json file.
For the previously introduced analyze command, it could look like this:

````json
{
  ...
    "scripts": {
        ...
    },
    "scripts-descriptions": {
        "analyze": "Perform code cleanup and analysis"
    }
}
````


## Summary

Composer is an indispensable part of today’s PHP world. The usual approach to adding code quality
tools to your project is by adding them to the require-dev section of the dependencies, which
works fine in many cases.
However, Composer is not the one and only way there is. Therefore, in this chapter, we introduced two
more options to manage your code quality tools: by adding the phar files manually to your project,
or by utilizing Phive to manage the phar files.
You are probably eager to apply all your gained knowledge to your code now. However, relentless
refactoring can do more harm than good, and clicking through all parts of your application after every
change to check if anything broke will cost you a lot of time and can be very frustrating. Thus, in the
next chapter, we will show you how automated testing can help you here.
