# Jetstrap

[![Последняя стабильная версия](https://poser.pugx.org/nascent-africa/jetstrap/v)](//packagist.org/packages/nascent-africa/jetstrap)
[![Всего скачиваний](https://poser.pugx.org/nascent-africa/jetstrap/downloads)](//packagist.org/packages/nascent-africa/jetstrap)
[![Лицензия](https://poser.pugx.org/nascent-africa/jetstrap/license)](//packagist.org/packages/nascent-africa/jetstrap)

## Описание

Jetstrap - это легкий пакет laravel 8, который фокусируется на `VIEW` стороне пакета [Jetstream](https://github.com/laravel/jetstream) / [Breeze](https://github.com/laravel/breeze), установленного в вашем приложении Laravel, так что, когда происходит обмен `Action`, `MODEL`, `CONTROLLER`, `Component` и `Action` классов вашего проекта по-прежнему на 100% обрабатывается командой разработчиков Laravel без дополнительного уровня сложности.

## Содержание

* [Установка](#установка)
  + [Установка Jetstream](#установка-jetstream)
    - [Установите Jetstream с помощью Livewire](#установите-jetstream-с-помощью-livewire)
    - [Или установите Jetstream с помощью Inertia](#или-установите-jetstream-с-помощью-inertia)
  + [Установите Jetstrap](#установите-jetstrap)
  + [Завершение установки](#завершение-установки)
  + [Дополнительно](#дополнительно)
    - [Пагинация](#пагинация)
* [Предустановки](#предустановки)
  + [Core Ui](#core-ui)
  + [AdminLTE](#adminlte)
* [Breeze](#breeze)
  + [Замена ресурсов Breeze](#замена-ресурсов-breeze)
  + [Замена ресурсов Breeze inertia](#замена-ресурсов-breeze-inertia)
* [Тестирование](#тестирование)
* [Лицензия](#лицензия)

## Установка

### Установка Jetstream

Вы можете использовать Composer для установки Jetstream в свой новый проект Laravel:

```
composer require laravel/jetstream
```

Если вы выбрали установку Jetstream через Composer, вам следует запустить Artisan-команду `jetstream:install`. Эта команда принимает имя стека, которое вы предпочитаете (livewire или inertia). Мы настоятельно рекомендуем вам прочитать всю документацию Livewire или Inertia перед тем, как начать свой проект Jetstream. Кроме того, вы можете использовать переключатель --teams, чтобы включить поддержку команды:

#### Установите Jetstream с помощью Livewire

```
php artisan jetstream:install livewire --teams
```

#### Или установите Jetstream с помощью Inertia

```
php artisan jetstream:install inertia --teams
```

### Установите Jetstrap

Используйте Composer для установки Jetstream в ваш новый проект Laravel в качестве зависимости разработчика:

```
composer require nascent-africa/jetstrap --dev
```

Независимо от того, как вы устанавливаете Jetstream, команды Jetstrap очень похожи на команды Jetstream, поскольку они принимают имя стека, который вы хотите поменять местами (livewire или inertia).

> Перед выполнением смены важно установить и настроить [Laravel Jetstream](https://github.com/laravel/jetstream).

Мы настоятельно рекомендуем вам прочитать всю документацию [Jetstream](https://jetstream.getlaravel.ru/2.x/introduction.html) перед тем, как начать свой проект Jetstrap. Кроме того, вы можете использовать переключатель `--teams` для обмена ассетами команды точно так же, как в Jetstream:

```bash

php artisan jetstrap:swap livewire

или

php artisan jetstrap:swap livewire --teams

php artisan jetstrap:swap inertia --teams
```

Это опубликует переопределения для включения Bootstrap, как в старые добрые времена!

### Завершение установки

После установки Jetsrtap и замены ресурсов Jetstream удалите tailwindCSS и его зависимости, если они есть, из вашего package.json, а затем установите и создайте зависимости NPM и перенесите свою базу данных:

```
npm install && npm run dev

php artisan migrate
```

### Дополнительно

#### Пагинация

Также важно отметить, что Laravel 8 по-прежнему включает представления разбивки на страницы, созданные с использованием Bootstrap CSS. Чтобы использовать эти представления вместо представлений Tailwind по умолчанию, вы можете вызвать метод `useBootstrap` пагинатора в вашем `AppServiceProvider`:

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Pagination\Paginator;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Зарегистрируйте любые сервисы приложения.
     *
     * @return void
     */
    public function register()
    {
        //
    }

    /**
     * Загрузите любые сервисы приложений.
     *
     * @return void
     */
    public function boot()
    {
        Paginator::useBootstrap();
    }
}
```

## Предустановки

Пресеты - это настраиваемые сторонние шаблоны, созданные с использованием начальной загрузки. Мы подумали, каковы шансы, что вы собираетесь использовать шаблон по умолчанию, предоставленный Laravel или Laravel Jetstream.

Исходя из предположения, что вы уже знаете, какой путь вы хотите пойти перед запуском любого типа каркаса, поэтому, если вы хотите использовать предустановки CoreUi или AdminLte, выбор должен быть указан в вашем сервис-провайдере (`JetstrapFacade::useCoreUi3()` или `JetstrapFacade::useAdminLte3()`) при первом запуске любой команды `swap`.

И если вы передумали после того, как запустили команду swap и решили использовать предустановку, то запустите команду `jetstrap:swap` еще раз.

### Core Ui

[Core Ui](https://coreui.io/) позволяет сэкономить тысячи бесценных часов, поскольку предлагает все необходимое для создания современных, красивых и отзывчивых приложений, как указано на их веб-сайте.

> Посетите [документацию](https://coreui.io/docs/getting-started/introduction/) для получения дополнительных сведений о том, как его использовать.

Чтобы использовать пресеты Core Ui, просто вызовите метод `useCoreUi3` в своем `AppServiceProvider`:

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use NascentAfrica\Jetstrap\JetstrapFacade;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Зарегистрируйте любые сервисы приложения.
     *
     * @return void
     */
    public function register()
    {
        //
    }

    /**
     * Загрузите любые сервисы приложений.
     *
     * @return void
     */
    public function boot()
    {
        JetstrapFacade::useCoreUi3();
    }
}
```

### AdminLTE

[AdminLTE](https://adminlte.io/) - тема панели управления и панели управления с открытым исходным кодом. AdminLTE, построенный на основе Bootstrap, предоставляет ряд адаптивных, многоразовых и часто используемых компонентов.

> Посетите [документацию](https://adminlte.io/themes/v3/) AdminLTE для получения дополнительных сведений о том, как его использовать.

Чтобы использовать пресеты AdminLte, просто вызовите метод `useAdminLte3` в своем `AppServiceProvider`:

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use NascentAfrica\Jetstrap\JetstrapFacade;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Зарегистрируйте любые сервисы приложения.
     *
     * @return void
     */
    public function register()
    {
        //
    }

    /**
     * Загрузите любые сервисы приложений.
     *
     * @return void
     */
    public function boot()
    {
        JetstrapFacade::useAdminLte3();
    }
}
```

## Breeze

Согласно документации, "Breeze обеспечивает минимальную и простую отправную точку для создания приложения Laravel с аутентификацией.", но лично я бы хотел думать о нем как о Laravel Ui без Vue и Bootstrap.

Недавно я работал над проектом, который не использовал Vue и не требовал сложной системы аутентификации, поэтому Breeze показался мне хорошей идеей, но я снова столкнулся с проблемой TailwindCSS, поэтому я подумал, почему бы не включить его в пакет Jetstrap.

> Before proceeding please familiarize yourself with the Breeze via the official documentation [documentation](https://github.com/laravel/breeze/blob/1.x/README.md).

Опять же, Jetstrap не влияет на часть модели / контроллера Breeze, а только на представление.

### Замена ресурсов Breeze

Чтобы поменять tailwind ресурс yf bootstrap в breeze, настроенном на Laravel, просто запустите:

```bash

php artisan jetstrap:swap breeze
```

### Замена ресурсов Breeze inertia

Laravel Breeze теперь поставляется с заглушками для inertia и, таким образом, с Jetstrap. Чтобы использовать каркас Bootstrap для вашего проекта laravel, работающего на Breeze вместе с inertia, просто запустите приведенный ниже код:

```bash

php artisan jetstrap:swap breeze-inertia
```

Затем вам нужно очистить файл `package.json`, чтобы убедиться, что мы не устанавливаем ненужные пакеты.

После этого запустите:

```
npm install && npm run dev
```

...и вы сделали!

Используйте `JetstrapFacade::useCoreUi3()` или `JetstrapFacade::useAdminLte3();` в вашем сервис-провайдере при замене простых ассетов будет работать должным образом.

## Тестирование

Запустите тесты с помощью:

```bash
vendor/bin/phpunit
```

или

```bash
composer tests
```

## Лицензия

Jetstrap - это программное обеспечение с открытым исходным кодом, лицензируемое по [MIT лицензии](https://github.com/nascent-africa/jetstrap/blob/master/LICENSE).
