# Production Calendar

Предоставляет возможность проверить является ли день выходным|праздничным|рабочим.
Данные предоставлены [basicdata.ru], однако, библиотека позволяет подключить любой источник данных.

# Установка

```bash
composer require maximaster/production-calendar
```

# Использование

## isFree($day)
Проверяет, является ли день "свободным", т.е. либо праздником, либо рядовым выходным
```php
use Maximaster\ProductionCalendar\Calendar;
use Maximaster\ProductionCalendar\RulesProvider\BasicdataProvider;

$calendar = Calendar::fromProvider(new BasicdataProvider);
if ($calendar->isFreeDay('01.01.2017')) {
```

## isDay($day, $types)
Проверяет, относится ли день к определённому типу (или одному из типов, если передан массив). Доступные типы см. константы класса Rules
```php
use Maximaster\ProductionCalendar\Rules;
if ($calendar->isDay('01.01.2017', [Rules::HOLIDAY, Rules::PRE_HOLIDAY])) {
```

## getDayType($day)
Возвращает тип дня
```php
$calendar->getDayType('01.01.2017'); // Rules::REGULAR_REST
```

# Кеширование
Позволяет кешировать результаты любого источника с помощью CacheProvider, в том числе встроенного. Пример:
```php
Calendar::fromProvider(new CacheProvider(new BasicdataProvider));
```
Для использования необходимо подключить пакет desarrolla2/cache

[basicdata.ru]:basicdata.ru