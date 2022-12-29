# Начало работы с платформой API: создайте свой API и сайт Jamstack

![Страница приветствия](../../distribution/images/api-platform-2.6-welcome.png)

> *API Platform* — это самая продвинутая платформа API на любой фрэймворке или языке.
>
> — Фабьен Потенсье (создатель Symfony)

[API Platform](https://api-platform.com) — это мощная, но простая в использовании структура **полного стека**, предназначенная для проектов на основе API и реализующая [Jamstack](https://jamstack.org/) архитектура.

## Введение

API Platform содержит [** PHP** library (Core)](../core/index.md) для создания полнофункциональных гипермедиа (или [GraphQL](../core/graphql.md)) веб-API, поддерживающих ведущие отраслевые стандарты: [JSON-LD](https://json-ld.org) с [Hydra](https://www.hydra-cg.com), [OpenAPI](../core/swagger.md)...

API Platform также предоставляет амбициозные инструменты ** JavaScript ** для быстрого создания веб- и мобильных приложений на основе самых популярных интерфейсных технологий. Эти инструменты анализируют документацию API (или любого другого API, поддерживающего Hydra или OpenAPI).

API Platform поставляется с  **[Docker](../deployment/docker-compose.md)** и **[Kubernetes](../deployment/kubernetes.md)** для мгновенной разработки и развертывания в облаке.

Самый простой и мощный способ начать работу - это [загрузить дистрибутив API Platform](https://github.com/api-platform/api-platform/releases).

Он содержит:

* скелет API, включая [основную библиотеку] (../core/index.md), [фреймворк Symfony](https://symfony.com/) ([необязательно](../core/bootstrap.md)) и [Doctrine ORM](https://www.doctrine-project.org/projects/orm.html)([необязательно](../core/extending.md))
* [инструмент построения клиентских каркаса] (../create-client/) для создания [Next.js](../create-client/index.md) веб-приложения из документации API (также поддерживаются [Nuxt.js](https://nuxtjs.org/), [Vue](https://vuejs.org/),
[Создать приложение React](https://reactjs.org), [React Native](https://facebook.github.io/react-native/), [Quasar](https://quasar.dev/) и [Vuetify](https://vuetifyjs.com/))
* [красивая админка] (../admin/), созданная поверх React Admin, путем анализа документации API 
* все, что вам нужно для [создания API-интерфейсов реального времени и асинхронности с использованием протокола Mercure] (../core/mercure.md)
* описанный [Docker](../deployment/docker-compose.md) для запуска рабочей среды разработки с помощью одной команды, предоставляющей контейнеры для API и Next.js
* [Helm](https://helm.sh/) схема развертывания API в любом кластере [Kubernetes](../deployment/kubernetes.md)

## API книжного магазина

Чтобы узнать, как работает фреймворк, мы создадим API для управления книжным магазином.

Для создания полнофункционального API, интерфейса администратора и прогрессивного веб-приложения с использованием Next.js,
все что вам нужно, это спроектировать **общедоступную модель данных нашего API** 
и доработать как *Обычные старые объекты PHP* (Plain Old PHP Objects (POPO)).

API Platform использует эти классы моделей для предоставления и документирования веб-API,
 имеющего множество встроенных функций:

* создание, извлечение, обновление и удаление ресурсов (CRUD)
* проверка данных
* разбивка на страницы
* фильтрация
* сортировка
* гипермедиа/[HATEOAS](https://en.wikipedia.org/wiki/HATEOAS) и поддержка согласования контента ([JSON-LD](https://json-ld.org) и [Hydra](https://www.hydra-cg.com/), [JSON:API](https://jsonapi.org/), [HAL](https://tools.ietf.org/html/draft-kelly-json-hal-08)...)
* [Поддержка GraphQL](../core/graphql.md)
* Приятный пользовательский интерфейс и машиночитаемая документация ([Swagger UI/OpenAPI](https://swagger.io), [GraphiQL](https://github.com/graphql/graphiql)...)
* аутентификация ([Basic HTTP](https://en.wikipedia.org/wiki/Basic_access_authentication), файлы cookie, а также [JWT](../core/jwt.md) и [OAuth](https://oauth.net) через расширения)
* [Заголовки CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)
* проверки безопасности и заголовки (протестированы на соответствие [рекомендациям OWASP](https://www.owasp.org/index.php/REST_Security_Cheat_Sheet))
* [HTTP-кэширование на основе инвалидации](../core/performance.md)
* и все необходимое для создания современных API.

Еще одна вещь, прежде чем мы начнем: поскольку дистрибутив платформы API включает [фреймворк Symfony](https://symfony.com),
он совместим с большинством [бандлов Symfony](https://flex.symfony.com)
(плагинами) которые добавляют функциональности с помощью [многочисленных расширений](../ core/extending.md), 
обеспечивая надежный фундамент (события, контейнер для внедрения зависимостей ...).
Предоставляя возможность легко добавлять в ваши API такие функции, как пользовательские или сервис-ориентированные эндпоинты,
аутентификация JWT или OAuth, кэширование HTTP, отправка почты или асинхронные задания.

## Установка фреймворка

### Использование дистрибутива API Platform (рекомендуется)

Начните с [загрузки дистрибутива API Platform](https://github.com/api-platform/api-platform/releases/latest), или [сгенерируйте репозиторий GitHub из предоставленного нами шаблона](https://github.com/api-platform/api-platform/generate).
Вы добавите свой собственный код и конфигурацию внутри этого скелета.

**Примечание**: Избегайте загрузки архива `.zip`, так как это может привести к потенциальной [проблеме прав доступа к файлам](https://github.com/api-platform/api-platform/issues/319#issuecomment-307037562) [проблемы](https://github.com/api-platform/api-platform/issues/777#issuecomment-412515342), предпочитая `.tar.gz ` архив.

API Platform поставляется с [Docker](https://docker.com) файлом, который упрощает
запуск среды разработки в контенйнере. Если у вас еще нет Docker на вашем компьютере, сейчас самое время [установить его](https://docs.docker.com/get-docker/).

**Примечание**: На Mac поддерживается только [Docker для Mac](https://docs.docker.com/docker-for-mac/).
Аналогично, в Windows, поддерживается только [Docker для Windows](https://docs.docker.com/docker-for-windows/). 
Докер-машина **не поддерживается** из коробки.

Откройте терминал и перейдите в каталог, содержащий скелет вашего проекта. Выполните следующую команду, чтобы запустить все
службы с помощью [Docker Compose](https://docs.docker.com/compose/):

Загружайте и создавайте последние версии образов:

```console
docker compose build --pull --no-cache
```

Запустите Docker Compose в автономном режиме:

```console
docker compose up -d 
```

**Совет:** убедитесь, что порты `80`, `443` и `5432` хоста еще не заняты. Обычно их используют Apache, NGINX и Postgres. Если они запущены, остановите их, и заново запустите "docker compose up -d".

При этом запускаются следующие службы:


| Название    | Описание                                                                                                                                                                                      |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| caddy       | модули [веб-сервер Caddy](caddy.md) с помощью [Mercure](../core/mercure.md) (в режиме реального времени и асинхронно) и [Vulcain](https://vulcain.rocks) (предварительная загрузка отношений) |
| php         | API с PHP 8, Composer и чувствительными конфигурациями                                                                                                                                        |
| pwa         | Next.js проект, совместимый с Create Client и имеющий предустановленного админку                                                                                                              |
| база данных | сервер базы данных PostgreSQL                                                                                                                                                                 |

Доступны следующие компоненты:

| URL                         | Путь                | Язык       | Описание           |
|-----------------------------|---------------------|------------|--------------------|
| `https://localhost/docs /`  | `api/`              | PHP        | API                |
| `https://localhost /`       | `pwa/`              | JavaScript | приложение Next.js |
| `https://localhost/admin /` | `pwa/pages/admin/`  | JavaScript | Админка            |

Чтобы просмотреть журналы контейнера, запустите:

```console
docker compose logs -f
```
Опция `-f` предназначена для отслеживания журналов.

Файлы проекта автоматически распределяются между вашим локальным хост-компьютером и контейнером благодаря предварительно настроенному [Docker
volume](https://docs.docker.com/engine/tutorials/dockervolumes/).
Это означает, что вы можете редактировать файлы вашего проекта локально, используя предпочитаемую вами среду разработки IDE или редактор кода,
эти изменения сразу будут отражены в контейнере.
Говоря об IDE, нашим любимым программным обеспечением для разработки приложений на платформе API Platform [PhpStorm](https://www.jetbrains.com/phpstorm/)
с его потрясающими плагинами для [Symfony](https://confluence.jetbrains.com/display/PhpStorm/Getting+Started+-+Symfony+Development+using+PhpStorm)
и [Инспектором Php](https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-).
Попробуйте их, и вы получите автозавершение кода и потрясающий качественный анализ.

Также хорошо работает [PHP IntelliSense для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=zobo.php-intellisense), является бесплатным и с открытым исходным кодом.

Дистрибутив API Platform поставляется с сущностью  `api/src/Entity/Greeting.php` для тестирования. Мы удалим
ее позже.

Если вы привыкли к экосистеме PHP, вы, вероятно, догадались, что этот тестовый объект использует [Doctrine ORM](https://www.doctrine-project.org/projects/orm.html).
Он поставляется в дистрибутиве платформы API.

Doctrine ORM - это самый простой способ сохранения и получения данных в проекте API Platform через Doctrine Bridge,
поставляемому вместе с дистрибутивом. Но это совершенно необязательно, и [вы можете предпочесть подключить свою собственную систему сохранения](../core/design.md).

Doctrine Bridge оптимизирован для повышения производительности и удобства разработки. Например, при использовании Doctrine API Platform
способна автоматически оптимизировать сгенерированные SQL-запросы, добавляя соответствующие предложения `JOIN`. Он также предоставляет
множество мощных [встроенных фильтров](../core/filters.md).
Doctrine ORM и его мост поддерживают большинство популярных СУБД, включая PostgreSQL, MySQL, MariaDB, SQL Server, Oracle и SQLite.
Существует также [Doctrine MongoDB ODM](https://www.doctrine-project.org/projects/mongodb-odm.html).

При этом имейте в виду, что API Platform на 100% независима от системы сохранения. Вы можете использовать тот(те), который
наилучшим образом соответствует вашим потребностям (включая базы данных NoSQL или удаленные веб-службы), внедрив необходимые интерфейсы.
Платформа API даже поддерживает совместное использование нескольких систем сохранения в одном проекте.

### Используем Symfony CLI

В качестве альтернативы компонент API Platform также может быть установлен непосредственно на локальном компьютере.
**Этот метод рекомендуется только для пользователей, которые хотят получить полный контроль над структурой каталогов и установленными
зависимостями.**

[[Для ознакомления посмотрите, как установить платформу API без дистрибутива на Symphonycast](https://symfonycasts.com/screencast/api-platform/install?cid=apip).

Остальная часть этого руководства предполагает, что вы установили платформу API с использованием официального дистрибутива.
В таком случае, переходите сразу к следующему разделу.

Платформа API имеет официальный рецепт Symfony Flex. Это означает, что вы можете легко установить его из любого
приложения Symfony, используя [Symfony](https://symfony.com/download):

Создайте новый проект Symfony:

```console
symfony new bookshop-api
```

Войдите в каталог проекта:

```console
cd bookshop-api
```

Установите  компонент API Platform в этот скелет:

```console
symfony composer require api
```

Затем создайте базу данных и ее схему:

```console
symfony console doctrine:database:create
symfony console doctrine:schema:create
```

И запустите встроенный сервер PHP:

```console
symfony serve
```

Все JavaScript компоненты доступны как [отдельные библиотеки](https://github.com/api-platform?language=javascript),
и устанавливается с помощью npm (или любого другого менеджера пакетов).

**Примечание:** при установке API Platform таким способом, API будет доступно по пути `/api/`.
Вам нужно открыть `http://localhost:8000/api/`, чтобы увидеть документацию API.
Если вы развертываете API Platform непосредственно на веб-сервере Apache или NGINX и получаете ошибку 404 при открытии этой ссылки,
вам необходимо включить [правила перезаписи](https://symfony.com/doc/current/setup/web_server_configuration.html)
для вашего конкретного веб-сервера.

## Готово

Откройте `https://localhost` в своем любимом веб-браузере:

![Страница приветствия](../../distribution/images/api-platform-2.6-welcome.png)

Вам нужно будет настроить исключение безопасности в своем браузере, чтобы принять созданный самоподписанный сертификат TLS,
для этого контейнера при установке фреймворка.

Вероятно, вы замените, что экран приветствия это приложение Next.js. Если вы не планируете создавать
Progressive Web App, вы можете удалить каталог `pwa/`, а также связанные строки в `docker-compose*.yml` и в `api/docker/caddy/Caddyfile` (не делайте этого
так как мы будем использовать этот контейнер позже в этом руководстве).

Нажмите на кнопку «API» или перейдите на `https://localhost/docs/`:

![API](../../distribution/images/api-platform-2.6-api.png)

API Platform предоставляет описание API в формате [OpenAPI](https://www.openapis.org/)(известном как Swagger).
Он также интегрирует интерфейс [Swagger UI](https://swagger.io/swagger-ui/), отображающий документацию OpenAPI.
Нажмите на операцию, чтобы отобразить ее детали.
Вы также можете отправлять запросы к API прямо из пользовательского интерфейса.
Попробуйте создать новый ресурс *Приветствие* с помощью операции `POST`, затем прочитать его с помощью операции `GET` и, наконец,
удалите его, выполнив операцию `DELETE`.
Если вы обращаетесь к любому URL-адресу API с добавленным расширением `.html`, платформа API отображает
соответствующий запрос API в пользовательском интерфейсе.
Попробуйте сами, зайдя на `https://localhost/greetings.html`.
Если расширения нет, платформа API будет использовать заголовок «Accept» для выбора используемого формата.
По умолчанию отправляется ответ JSON-LD([конфигурация поведения](../core/content-negotiation.md)).

Итак, если вы хотите получить доступ к необработанным данным, у вас есть две альтернативы:

* Добавьте правильный заголовок «Accept» (или вообще не устанавливайте заголовок «Accept», если вас не волнует безопасность) — предпочтительнее при написании клиентов API.
* Добавьте необходимый формат в качестве расширения ресурса - только для целей отладки

Например, перейдите на `https://localhost/greetings.jsonld`, чтобы получить список ресурсов `Greeting` в формате JSON-LD, или
`https://localhost/greetings.json` для получения данных в формате JSON.

Конечно, вы также можете использовать свой любимый HTTP-клиент для запросов к API.
Нам нравится [Postman](https://www.getpostman.com/).
Он отлично работает с API Platform, имеет встроенную поддержку OpenAPI,
позволяет легко писать функциональные тесты и есть хорошие возможности для совместной работы в команде.

## Bringing your Own Model

Your API Platform project is now 100% functional. Let's expose our own data model.
Our bookshop API will start simple. It will be composed of a `Book` resource type and a `Review` one.

Books have an id, an ISBN, a title, a description, an author, a publication date and are related to a list of reviews.
Reviews have an id, a rating (between 0 and 5), a body, an author, a publication date and are related to one book.

Let's describe this data model as a set of Plain Old PHP Objects (POPO):

## Использование собственной модели

Теперь ваш проект API Platform работает на 100%. Давайте представим нашу собственную модель данных.
Наш API книжного магазина начнется с простого. Он будет состоять из типа ресурса `Book` и ресурса `Review`.

Книги имеют идентификатор, ISBN, название, описание, автора, дату публикации и связаны со списком рецензий.
Рецензии имеют идентификатор, рейтинг (от 0 до 5), текст, автора, дату публикации и относятся к одной книге.

Давайте опишем эту модель данных как набор обычных объектов PHP (POPO):

```php
<?php
// api/src/Entity/Book.php
namespace App\Entity;

use ApiPlatform\Metadata\ApiResource;
use Doctrine\Common\Collections\ArrayCollection;

/** Книга. */
#[ApiResource]
class Book
{
    /** Идентификатор этой книги. */
    private ?int $id = null;

    /** ISBN этой книги (или null, если его нет). */
    public ?string $isbn = null;

    /** Название этой книги. */
    public string $title = '';

    /** Описание этой книги. */
    public string $description = '';

    /** Автор этой книги.*/
    public string $author = '';

    /** Дата публикации этой книги. */
    public ?\DateTimeImmutable $publicationDate = null;

    /** @var Review[] Доступные рецензии на эту книгу. */
    public iterable $reviews;

    public function __construct()
    {
        $this->reviews = new ArrayCollection();
    }

    public function getId(): ?int
    {
        return $this->id;
    }
}
```

```php
<?php
// api/src/Entity/Review.php
namespace App\Entity;

use ApiPlatform\Metadata\ApiResource;

/** Рецензия на книгу. */
#[ApiResource]
class Review
{
    /** Идентификатор этого отзыва. */
    private ?int $id = null;

    /** Рейтинг этого обзора (от 0 до 5). */
    public int $rating = 0;

    /** Тело обзора. */
    public string $body = '';

    /** Автор обзора. */
    public string $author = '';

    /** Дата публикации этого обзора.*/
    public ?\DateTimeImmutable $publicationDate = null;

    /** Книга, о которой идет речь. */
    public ?Book $book = null;

    public function getId(): ?int
    {
        return $this->id;
    }
}
```
Мы создали два типичных объекта PHP с соответствующим PHPDoc, оба отмечены атрибутом `#[ApiResource]`.
Для удобства мы также использовали библиотеку Doctrine Collection (независимую от Doctrine ORM), но это не обязательно.

Перезагрузите `https://localhost/docs/`: API Platform использовала эти классы для создания документации OpenAPI (также доступна документация Hydra)
 и зарегистрировала для нас [типовые маршруты REST](../core/operations.md).

![API книжного магазина](../../distribution/images/api-platform-2.6-bookshop-api.png)

Операции, доступные для двух типов ресурсов `Book` и `Review`, отображаются в пользовательском интерфейсе.
 Мы также можем увидеть [Панель инструментов веб-отладки](https://symfonycasts.com/screencast/symfony/profiler?cid=apip).

Обратите внимание, что описания сущностей и свойств в документации API и что API Platform использует типы PHP для создания соответствующих схем JSON.

![Схемы книжного магазина JSON](../../distribution/images/api-platform-2.6-bookshop-json-schemas.png)

Фреймворк также использует эти метаданные для сериализации и десериализации данных из JSON (и других форматов) в объекты PHP (туда и обратно)!

Для простоты, в этом примере мы использовали публичные свойства (кроме id, см. ниже). API Platform (а также
как Symfony и Doctrine) также поддерживает методы доступа (геттеры/сеттеры), используйте их, если хотите.
Мы использовали приватное свойство и геттер для идентификатора, чтобы обеспечить, что он доступен только для чтения (мы позволим СУБД сгенерировать его).
Платформа API также имеет отличную поддержку UUID. [Вероятно, Вам следует использовать их, вместо автоматически инкрементных идентификаторов](https://www.clever-cloud.com/blog/engineering/2015/05/20/why-auto-increment-is-a-terrible-idea/).

Поскольку API Platform предоставляет нам всю инфраструктуру, наш API почти готов!

Единственная оставшаяся задача для работающего API — это иметь возможность запрашивать и сохранять данные.

## Подключение системы хранения (Persistence System)

Для извлечения и сохранения данных API Platform предлагает два основных варианта (и мы можем их смешивать):

1. Написание собственных поставщиков данных и хранилищ данных 
 для извлечения и сохранения данных в любой системе сохранения и использования собственной бизнес-логики. 
 Это то, что мы рекомендуем, как способ отделить общедоступную модель данных, предоставляемую API от внутренней и реализовать многоуровневую архитектуру, такую как чистая архитектура или гексагональная архитектура;
2. Использование одного из существующих провайдеров данных и средств сохранения, позволяющих автоматически извлекать и сохранять данные с использованием популярных библиотек сохранения. По умолчанию провайдеры данных и сохранятели предоставляются [Doctrine ORM](https://www.doctrine-project.org/projects/orm.html) и [Doctrine MongoDB ODM](../core/mongodb.md).
   Провайдер данных (но еще не сохранятель) также доступен для [Elasticsearch](../core/elasticsearch.md). также предоставляют провайдеры и сохранятели для [Pomm](https://github.com/pomm-project/pomm-api-platform) и [PHP Extended SQL](https://github.com/soyuka/esql#api-platform-bridge). Мы рекомендуем этот подход для быстрой разработки приложений.

Обязательно прочтите документ [Общие соображения по проектированию](../core/design.md), чтобы узнать больше об архитектуре API Platform и о том, как выбрать один из этих двух подходов.

В оставшейся части этого руководства мы будем использовать встроенный поставщик данных Doctrine ORM.

Измените классы, чтобы сопоставить их с таблицами базы данных, используя аннотации, предоставляемые Doctrine ORM.

Измените эти файлы, как описано ниже:

`api/src/Entity/Book.php`

```diff
 use ApiPlatform\Metadata\ApiResource;
 use Doctrine\Common\Collections\ArrayCollection;
+use Doctrine\ORM\Mapping as ORM;
 
 /** Книга. */
+#[ORM\Entity]
 #[ApiResource]
 class Book
 {
     /** Идентификатор этой книги. */
+    #[ORM\Id, ORM\Column, ORM\GeneratedValue]
     private ?int $id = null;
 
     /** ISBN этой книги (или null, если его нет). */
+    #[ORM\Column(nullable: true)]
     public ?string $isbn = null;
 
     /** Название этой книги. */
+    #[ORM\Column]
     public string $title = '';
 
     /** Описание этой книги. */
+    #[ORM\Column(type: 'text')]
     public string $description = '';
 
     /** Автор этой книги. */
+    #[ORM\Column]
     public string $author = '';
 
     /** Дата публикации этой книги.*/
+    #[ORM\Column]
     public ?\DateTimeImmutable $publicationDate = null;
 
     /** @var Review[] Доступные рецензии на эту книгу.*/
+    #[ORM\OneToMany(targetEntity: Review::class, mappedBy: 'book', cascade: ['persist', 'remove'])]
     public iterable $reviews;
 
     public function __construct()
```

`api/src/Entity/Review.php`

```diff
 namespace App\Entity;
 
 use ApiPlatform\Metadata\ApiResource;
+use Doctrine\ORM\Mapping as ORM;
 
 /** Рецензия на книгу. */
+#[ORM\Entity]
 #[ApiResource]
 class Review
 {
     /** Идентификатор этого отзыва. */
+    #[ORM\Id, ORM\Column, ORM\GeneratedValue]
     private ?int $id = null;
 
     /** Рейтинг этого обзора (от 0 до 5). */
+    #[ORM\Column(type: 'smallint')]
     public int $rating = 0;
 
     /** Тело обзора. */
+    #[ORM\Column(type: 'text')]
     public string $body = '';
 
     /** Автор обзора. */
+    #[ORM\Column]
     public string $author = '';
 
     /** Дата публикации этого обзора.*/
+    #[ORM\Column]
     public ?\DateTimeImmutable $publicationDate = null;
 
     /** Книга, о которой идет речь. */
+    #[ORM\ManyToOne(inversedBy: 'reviews')]
     public ?Book $book = null;
 
     public function getId(): ?int
```

**Совет**: вы также можете использовать Symfony [MakerBundle](https://symfonycasts.com/screencast/symfony-fundamentals/maker-command?cid=apip) благодаря опции `--api-resource`:

```console
docker compose exec php \
    bin/console make:entity --api-resource
```

[Аннотации Doctrine](https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/annotations-reference.html) сопоставляют эти сущности с таблицами в базе данных.
Также поддерживается сопоставление через [атрибуты](https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/attributes-reference.html), если вы предпочитаете это.
Оба метода удобны тем, что позволяют группировать код и конфигурацию, но если вы хотите отделить классы от их метаданных, вы можете переключиться на сопоставления XML или YAML.
Они также поддерживаются.

Узнайте больше о том, как отображать объекты с помощью Doctrine ORM, в [официальной документации проекта](https://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/association-mapping.html)
или в книге Кевина «[Persistence in PHP with the Doctrine ORM](https://www.amazon.fr/gp/product/B00HEGSKYQ/ref=as_li_tl?ie=UTF8&camp=1642&creative=6746&creativeASIN=B00HEGSKYQ&linkCode=as2&tag=kevidung-21)».

Теперь удалите файл `api/src/Entity/Greeting.php`. Этот демонстрационный объект больше не нужен.
Наконец, сгенерируйте новую миграцию базы данных с помощью [Doctrine Migrations](https://symfony.com/doc/current/doctrine.html#migrations-creating-the-database-tables-schema) и примените ее:

```console
docker compose exec php \
    bin/console doctrine:migrations:diff
docker compose exec php \
    bin/console doctrine:migrations:migrate
```

Контейнер `php` — это место, где находится ваше приложение API. Команда `docker compose exec php` позволяет запустить
 контейнер. Вы можете [создать псевдоним](http://www.linfo.org/alias.html), чтобы облегчить себе жизнь.

**Теперь у нас есть работающий API с возможностью чтения и записи!**

В пользовательском интерфейсе Swagger щелкните операцию POST типа ресурса Book, нажмите "Try it out" и отправьте следующий документ JSON в качестве тела запроса:


```json
{
  "isbn": "9781782164104",
  "title": "Persistence in PHP with the Doctrine ORM",
  "description": "This book is designed for PHP developers and architects who want to modernize their skills through better understanding of Persistence and ORM.",
  "author": "Kévin Dunglas",
  "publicationDate": "2013-12-01"
}
```
Вы только что сохранили новый книжный ресурс через API книжного магазина! API Platform автоматически преобразует документ JSON в
экземпляр соответствующего класса сущностей PHP и использует Doctrine ORM для его сохранения в базе данных.

По умолчанию API поддерживает `GET` (извлечение коллекций и элементов), `POST` (создание), `PUT` (замена), `PATCH` (частичное обновление) и `DELETE` (не требует пояснений).
HTTP-методы. Не забудьте [отключить те, которые вам не нужны](../core/operations.md#enbling-and-disabled-operations)!

Попробуйте выполнить операцию GET для коллекции. Появится добавленная нами книга. Когда коллекция содержит более 30 предметов,
автоматически появится  нумерация страниц [и это полностью настраивается](../core/pagination.md). Вам может быть интересно
как [добавить некоторые фильтры и сортировки в коллекцию](../core/filters.md).

Вы могли заметить, что некоторые ключи начинаются с символа `@` в сгенерированном ответе JSON ("@id`, `@type`, `@context`...)
API Platform поставляется с полной поддержкой формата [JSON-LD](https://json-ld.org/) (и его расширение [Hydra](https://www.hydra-cg.com/)).
Это позволяет создавать смарт клиенты с возможностями автоматического обнаружения, такими как админка API Platform, про  который
мы узнаем ниже.
Это полезно для публичных данных и SEO, особенно когда [используется словари, такие как Schema.org](http://blog.schema.org/2013/06/schemaorg-and-json-ld.html)
и позволяет [предоставить поисковым системам, таким как Google, Yandex доступ к вашим структурированным данным](https://developers.google.com/search/docs/guides/intro-structured-data)
или запросить ваши API в [SPARQL](https://en.wikipedia.org/wiki/SPARQL) с помощью [Apache Jena](https://jena.apache.org/documentation/io/#formats)).

Мы считаем, что JSON-LD — лучший формат по умолчанию для нового API.
Однако API Platform изначально [поддерживает многие другие форматы](../core/content-negotiation.md), включая [GraphQL](https://graphql.org/)
(мы доберемся до этого), [JSON:API](https://jsonapi.org/), [HAL](https://github.com/zircote/Hal), сырой [JSON](https://www.json.org/),
[XML](https://www.w3.org/XML/)(экспериментальный) и даже [YAML](https://yaml.org/) и [CSV](https://en.wikipedia.org/wiki/Comma-separated_values).
Вы также можете легко [добавить поддержку других форматов](../core/content-negotiation.md), и вам решать, какой формат
включить и использовать по умолчанию.

Теперь добавьте обзор этой книги, используя операцию `POST` для ресурса `Review`:


```json
{
    "book": "/books/1",
    "rating": 5,
    "body": "Interesting book!",
    "author": "Kévin",
    "publicationDate": "September 21, 2016"
}
```

**Примечание.** Если вы установили API Platform в существующем проекте с помощью `composer`, содержимое ключа `book` должно быть `"/api/books/1"`

Есть две интересные вещи, которые следует упомянуть об этом запросе:

Во-первых, мы научились работать с отношениями. В API гипермедиа каждый ресурс идентифицируется (уникальным) [IRI](https://en.wikipedia.org/wiki/Internationalized_Resource_Identifier).
URL-адрес — это допустимый IRI, и именно его использует API Platform. Свойство `@id` каждого JSON-LD документа содержит идентификатор IRI.
Вы можете использовать этот IRI для ссылки на этот документ из других документов. В предыдущем запросе мы использовали IRI
книгу, которую мы создали ранее, чтобы связать ее с `Review`, который мы создавали. API Platform достаточно умна, чтобы работать с IRI.
Кстати, вы можете [встроить документы](../core/serialization.md) вместо того, чтобы ссылаться на них
(например, чтобы уменьшить количество HTTP-запросов). Вы даже можете [разрешить клиенту выбирать только те свойства, которые ему нужны](../core/filters.md#property-filter).

Другая интересная вещь заключается в том, как API Platform обрабатывает даты (свойство `publicationDate`). API Platform понимает
[любой формат даты, поддерживаемый PHP](https://www.php.net/manual/en/datetime.formats.date.php). В продакшн мы настоятельно рекомендуем
используя формат, указанный в [RFC 3339](https://tools.ietf.org/html/rfc3339), но, как видите, может использоваться наиболее распространенные форматы
`September 21, 2016`.

Подводя итог, если вы хотите раскрыть какую-либо сущность, вам просто нужно:

1. Поместите его в пространство имен `App\Entity\`
2. Напишите своих поставщиков данных и сохранятелей(персистентов) или, если вы используете Doctrine, сопоставьте их с базой данных.
3. Отметьте его атрибутом `#[ApiResource]`

Что может быть проще?!

## Проверка данных

Теперь попробуйте добавить другую книгу, отправив запрос `POST` к `/books` со следующим JSON:

```json
{
  "isbn": "2815840053",
  "description": "Hello",
  "author": "Me",
  "publicationDate": "today"
}
```

Книга успешно создана, но есть проблема; мы не давали ему названия. Нет смысла создавать запись книги без названия, поэтому нам нужно реализовать некоторые проверки, чтобы предотвратить это.

API Platform поставляется с [компонентом Symfony Validator](https://symfony.com/doc/current/validation.html).
Для проверки данных, отправляемых пользователем, в наших сущностях мы можем использовать [готовые проверки](https://symfony.com/doc/current/validation.html#supported-constraints)
(или [создать собственые](https://symfony.com/doc/current/validation/custom_constraint.html)).
Давайте добавим несколько правил проверки в нашу модель данных.

Измените следующие файлы, как описано в этих исправлениях:

`api/src/Entity/Book.php`

```diff
 use ApiPlatform\Metadata\ApiResource;
 use Doctrine\Common\Collections\ArrayCollection;
 use Doctrine\ORM\Mapping as ORM;
+use Symfony\Component\Validator\Constraints as Assert;

     #[ORM\Column(nullable: true)] 
+    #[Assert\Isbn]
     public ?string $isbn = null;     
 
     #[ORM\Column]
+    #[Assert\NotBlank]
     public string $title = '';
 
     #[ORM\Column(type: 'text')]
+    #[Assert\NotBlank]
     public string $description = '';
 
     #[ORM\Column] 
+    #[Assert\NotBlank]
     public string $author = '';
 
     #[ORM\Column]
+    #[Assert\NotNull]
     public ?\DateTimeImmutable $publicationDate = null;
```

`api/src/Entity/Review.php`

```diff
 use ApiPlatform\Metadata\ApiResource;
 use Doctrine\ORM\Mapping as ORM;
+use Symfony\Component\Validator\Constraints as Assert;

     #[ORM\Column(type: 'smallint')]   
+    #[Assert\Range(min: 0, max: 5)]
     public int $rating = 0;
 
     #[ORM\Column(type: 'text')]
+    #[Assert\NotBlank]
     public string $body = '';
 
     #[ORM\Column]
+    #[Assert\NotBlank]
     public string $author = '';
 
     #[ORM\Column] 
+    #[Assert\NotNull]
     public ?\DateTimeImmutable $publicationDate = null;
 
     #[ORM\ManyToOne(inversedBy: 'reviews')] 
+    #[Assert\NotNull]
     public ?Book $book = null;
 
     public function getId(): ?int
```

После обновления сущностей путем добавления этих атрибутов `#[Assert\*]` (как и в случае с Doctrine, вы также можете использовать XML или YAML), попробуйте
снова предыдущий запрос `POST`.

```json
{
  "@context": "/contexts/ConstraintViolationList",
  "@type": "ConstraintViolationList",
  "hydra:title": "An error occurred",
  "hydra:description": "isbn: This value is neither a valid ISBN-10 nor a valid ISBN-13.\ntitle: This value should not be blank.",
  "violations": [
    {
      "propertyPath": "isbn",
      "message": "This value is neither a valid ISBN-10 nor a valid ISBN-13."
    },
    {
      "propertyPath": "title",
      "message": "This value should not be blank."
    }
  ]
}
```

Теперь вы получаете правильные сообщения об ошибках проверки, всегда сериализованные с использованием формата ошибок Hydra (также поддерживается [RFC 7807](https://tools.ietf.org/html/rfc7807)).
Эти ошибки легко анализировать на стороне клиента. Добавив соответствующие ограничения проверки, мы также заметили, что
ISBN недействителен...


## Добавление поддержки GraphQL

Разве API Platform не является фреймворком только для REST  **но и** GraphQL? Это правда! Поддержка GraphQL не включена по умолчанию. Чтобы добавить его, нам
необходимо установить библиотеку [graphql-php](https://webonyx.github.io/graphql-php/). Выполните следующую команду:

```console
docker compose exec php sh -c '
    composer require webonyx/graphql-php
    bin/console cache:clear
'
````

You now have a GraphQL API! Open `https://localhost/graphql` (or `https://localhost/api/graphql` if you used Symfony Flex to install API Platform) to play with it using the nice [GraphiQL](https://github.com/graphql/graphiql)
UI that is shipped with API Platform:

Теперь у вас есть GraphQL API! Откройте `https://localhost/graphql` (или `https://localhost/api/graphql`, если вы использовали Symfony Flex для установки API Platform),
 чтобы поиграть с ним, используя интерфейс [GraphiQL](https://github.com/graphql/graphiql), поставляемый с API Platform:

![GraphQL endpoint](../../distribution/images/api-platform-2.6-graphql.png)

Try it out by creating a greeting:

```graphql
mutation {
  createGreeting(input: {name: "Test2"}) {
    greeting {
      id
      name
    }
  }
}
```

И, прочитав приветствие:

```graphql
{
  greeting(id: "/greetings/1") {
    id
    name
    _id
  }
}
```

Вы также можете попробовать что-то более сложное:

```graphql
{
  books {
    totalCount
    edges {
      node {
        id
        title
        reviews {
          totalCount
          edges {
            node {
              author
              rating
            }
          }
        }
      }
    }
  }
}
```
Реализация GraphQL поддерживает [запросы](https://graphql.org/learn/queries/), [мутации](https://graphql.org/learn/queries/#mutations),
[100% спецификации сервера ретрансляции](https://facebook.github.io/relay/docs/en/graphql-server-specification.html), нумерация страниц,
[фильтры](../core/filters.md) и [правила контроля доступа](../core/security.md).
Вы можете использовать его с популярными клиентами [RelayJS](https://facebook.github.io/relay/) и [Apollo](https://www.apollographql.com/docs/react/).

## Админка

Было бы неплохо иметь админку для управления данными, предоставляемыми вашим API?
Подождите... У вас уже она есть!

Откройте `https://localhost/admin/` в вашем браузере:

Эта Админка использует [Material Design](https://material.io/guidelines/) и является [прогрессивным веб-приложением](https://developers.google.com/web/progressive-web-apps/)
построен с помощью [API Platform Admin](../admin/index.md) внутри которой ([React Admin](https://marmelab.com/react-admin/)).
 Она полностью настраиваема. Обратитесь к документации, чтобы узнать больше.
Для построения, она использует документацию Hydra, предоставляемую компонентом API.
Это 100% динамичность — **происходит без генерации кода**.

## Приложение Next.js

Платформа API также имеет отличный [генератор клиентов](../create-client/index.md), способный создавать полностью рабочие Next.js, Nuxt.js, React/Redux, Vue.js, Quasar и Vuetify Progressive Web Apps, которые вы можете легко настроить под свои нужды.
Если вы предпочитаете использовать все возможности мобильных устройств, генератор также поддерживает
[React Native](https://facebook.github.io/react-native/).

Дистрибутив поставляется со скелетом [Next.js](https://nextjs.org/). Чтобы загрузить ваше приложение, запустите:

```console
docker compose exec pwa \
    pnpm create @api-platform/client
```

Откройте в браузере `https://localhost/books/`:

![The Next.js Progressive Web App](../../distribution/images/api-platform-2.6-pwa-react.png)


Вы также можете сгенерировать код для определенного ресурса с аргументом `--resource` (пример:
`pnpm create @api-platform/client --resource books`).

Сгенерированный код содержит список (включая разбиение на страницы), кнопку удаления, форму создания и редактирования. Он также включает
разметку [Bootstrap](https://getbootstrap.com) и [роли ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)
чтобы сделать приложение доступным для людей с ограниченными возможностями.

Если вы предпочитаете создавать PWA, построенный поверх другого стека внешнего интерфейса, прочитайте [специальную документацию](../create-client/index.md).

## Подключаем собственную бизнес-логику

Теперь, когда вы изучили основы, обязательно прочитайте [общие соображения по проектированию](../core/design.md) и [как расширить API Platform](../core/extending.md), чтобы понять, как API Platform разработана, и как подключить вашу пользовательскую бизнес-логику!

## Другие преимущества

Во-первых, вы можете узнать [как развернуть свое приложение](../deployment/index.md) в облаке, используя [встроенную интеграцию Kubernetes](../deployment/kubernetes.md).

Есть еще много возможностей в API Platform! Прочтите [полную документацию](../core/index.md), чтобы узнать, как их использовать,
и как расширить API Platform в соответствии с вашими потребностями.
API Platform невероятно эффективна для прототипирования и быстрой разработки приложений (RAD), но в основном эта платформа
предназначена для создания сложных проектов на основе API, выходящих далеко за рамки простых приложений CRUD. Она дает приемущество от [**от возможности расширений**](../core/extending.md)
и она **постоянно оптимизируется для [производительности](../core/performance.md).** Она поддерживает множество веб-сайтов с высоким трафиком.

API Platform имеет встроенную систему инвалидации кеша HTTP, которая позволяет приложениям API Platform работать молниеносно с помощью [Varnish](https://varnish-cache.org/). Подробнее читайте в главе
[Основная библиотека платформы API: включение встроенной системы инвалидации кэша HTTP](../core/performance.md#enbling-the-built-in-http-cache-invalidation-system).

Имейте в виду, что вы можете использовать свою любимую клиентскую технологию: API Platform предоставляет генераторы для популярных фреймворков JavaScript, но вы также можете напрямую использовать предпочитаемую клиентскую технологию, включая Angular, Ionic и Swift.
 Любой язык, способный отправлять HTTP запросы (даже COBOL может это сделать).

Чтобы пойти дальше, команда API Platform поддерживает демо приложение, демонстрирующее более продвинутые варианты использования, такие как использование сериализации,
группы, управление пользователями или аутентификация JWT и OAuth. [Ознакомьтесь с исходным кодом демо-версии на GitHub](https://github.com/api-platform/demo)
и [просмотреть на него в Интернете] (https://demo.api-platform.com).

## Скринкасты

<p align="center" class="symfonycasts"><a href="https://symfonycasts.com/tracks/rest?cid=apip#api-platform"><img src="../../distribution/images/symfonycasts-player.png" alt="SymfonyCasts, скринкасты API Platform"></a></p>

Самый простой способ научиться пользоваться API Platform — это посмотреть [более 60 скринкастов, доступных на SymfonyCasts](https://symfonycasts.com/tracks/rest?cid=apip#api-platform)!
