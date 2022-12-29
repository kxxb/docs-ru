# Базовая библиотека API Platform

Базовая библиотека API Platform - это простая в использовании и мощная библиотека для создания [управляемых гипермедиа REST API](https://en.wikipedia.org/wiki/HATEOAS).
Это компонент [фрэйворка API Platform](https://api-platform.com).
Его можно использовать как автономно, так и с [фреймворком Symfony](https://symfony.com)(рекомендуется).

It embraces [JSON for Linked Data (JSON-LD)](http://json-ld.org) and [Hydra Core Vocabulary](http://www.hydra-cg.com) web
standards but also supports [HAL](http://stateless.co/hal_specification.html), [Swagger/Open API](https://www.openapis.org/), XML, JSON, CSV and YAML.

Build a working and fully featured CRUD API in minutes. Leverage the awesome features of the tool to develop complex and
high-performance API-first projects.

If you are starting a new project, the easiest way to get API Platform up is to install
the [API Platform Distribution](../distribution/index.md).

Он охватывает такие стандарты как [JSON для связанных данных (JSON-LD)](http://json-ld.org) и [Основной словарь Hydra](http://www.hydra-cg.com),
но также поддерживает [HAL](http://stateless.co/hal_specification.html), [Swagger/Open API](https://www.openapis.org/), XML, JSON, CSV и YAML.

Создавайте работающий и полнофункциональный CRUD API за считанные минуты.
Используйте потрясающие возможности этого инструмента для разработки сложных и
высокопроизводительных проектов, основанных на API.

Если вы начинаете новый проект, самый простой способ запустить платформу API - это установить
[Дистрибутив платформы API](../distribution/index.md).


![Screenshot](../../distribution/images/swagger-ui-1.png)

## Возможности

Вот полнофункциональный REST API, который вы получите за считанные минуты:

* [Автоматический CRUD](operations.md)
* Гипермедиа (JSON-LD и HAL)
* Машиночитаемая документация по API в форматах Hydra и [Swagger/Open API](swagger.md),
  генерируется из метаданных PHPDoc, Serializer, Validator и Doctrine ORM/MongoDB ODM
* Хорошая удобочитаемая документация, созданная с помощью пользовательского интерфейса Swagger (включая песочницу) и/или ReDoc.
* [Разбивка на страницы](pagination.md)
* Куча [фильтров](filters.md)
* [Сортировка](default-order.md)
* [Валидация](validation.md) с использованием компонента Symfony Validator (с поддержкой групп)
* Расширенные правила [аутентификации и авторизации](security.md)
* Сериализация ошибок (поддерживаются Hydra и [RFC 7807](https://tools.ietf.org/html/rfc7807))
* Расширенная [сериализация](serialization.md) благодаря компоненту Symfony Serializer (поддержка групп, встраивание отношений, максимальная глубина...)
* Автоматическая регистрация маршрутов
* Автоматическая генерация точки входа, дающая доступ ко всем ресурсам
* [Пользователь](user.md) поддержка
* Поддержка [JWT](jwt.md) и [OAuth](https://oauth.net/)
* Файлы и `\DateTime`, а также сериализация и десериализация

Все полностью настраивается с помощью мощной [системы событий](events.md) и сильного ООП.

Этот комплект тщательно протестирован (модуль и функционал). Каталог [`Fixtures/`](https://github.com/api-platform/core/tree/main/tests/Fixtures) содержит рабочее приложение, охватывающее все функции библиотеки.

## Скринкасты

<p align="center" class="symfonycasts"><a href="https://symfonycasts.com/tracks/rest?cid=apip#api-platform"><img src="../../distribution/images/symfonycasts-player.png" alt="SymfonyCasts, API Platform screencasts"></a></p>

Самый простой и веселый способ научиться пользоваться API Platform — это посмотреть [более 60 скринкастов, доступных на SymfonyCasts](https://symfonycasts.com/tracks/rest?cid=apip#api-platform)!
