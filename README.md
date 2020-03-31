Code Style for Symfony 4.x - 5.x
================================
Code Style for Symfony 4.x - 5.x

##### Описание рекомендаций по оформлению кода можно прочитать тут: 

- [PSR-2](https://www.php-fig.org/psr/psr-2/)
- [PSR-12](https://www.php-fig.org/psr/psr-12/)
- https://github.com/index0h/php-conventions#91-inspections-%D0%B8-code-style

Файлы
------
**settings.zip** - настройки code style для IDE PhpShtorm

**.php_cs** - файл настроек для [PHP CS Fixer](https://cs.symfony.com/) (в нашем случаи для Symfony).

Кратко о настройки [PHP CS Fixer](https://cs.symfony.com/):

Установка
---------
Установить php-cs-fixer можно глобально или локально. При локальной установке библиотека будет сохранена в папке vendor вашего проекта.

Cкачать программу можно напрямую из репозитория, но мы для удобства воспользуемся менеджером пакетов [Composer](http://getcomposer.org/download/).

Мы расмотрим лакольную установку:
```
composer require friendsofphp/php-cs-fixer
```

Далее переносим файл **.php_cs** в корень нашего проекта.

Фыйл настроект **.php_cs**:

```php
<?php

return PhpCsFixer\Config::create()
    ->setRules([
        '@PSR2'        => true,
        'array_syntax' => ['syntax' => 'short'],
        /*...*/
        ])
        ->setUsingCache(false)
        ->setFinder(
            PhpCsFixer\Finder::create()
                ->exclude(['var', 'public', 'vendor', 'bin', 'ci'])
                ->notPath('*')
                ->in(__DIR__)
        );

```
**setRules** - задает набор правил оформления. Список доступных правил можно посмотреть [тут](https://mlocati.github.io/php-cs-fixer-configurator/#version:2.16)

**setUsingCache** - ускоряет выполнение программы, запоминая время и список файлов, чтобы в следующий раз при запуске исправлять только те файлы, которые менялись. 

**setFinder** - определяет папку, в которой будут исправлены файлы. Если нужно исключить папку, то для этого добавляется параметр **exclude('somedir')**.

Запуск
------
Для запуска выполните комманду в консоли из корня прокта:
```
php vendor/bin/php-cs-fixer fix
```