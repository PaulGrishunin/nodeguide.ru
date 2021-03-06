==============================================
Руководство по стилю кода в Node.js от Felix'a
==============================================

В настоящий момент не существует официального документа, который бы
регламентировал **стиль кода в Node.js**-приложениях. Это руководство - моя
попытка донести до читателя набор подходов, позволяющих создавать
прекрасное и целостное ПО.

Руководство предполагает, что читатель работает исключительно в Node.js.
Если предполагается запуск кода в браузере или каком-либо другом окружении,
то некоторые пункты текста можно игнорировать.

Также следует обратить внимание, что и Node.js, и многие пакеты для него,
имеют свои собственные соглашения о стиле кода, которые не всегда совпадают.
Таким образом, если Вы собираетесь вносить вклад в код какого-либо пакета, то
следуйте соглашению о стиле этого пакета.

Табуляция vs Пробелы
====================

Начнем с религиозных проблем. Наш :ref:`великодушный диктатор <community-ryan-dahl>`
выбрал при разработке ядра Node.js отступ в 2 пробела. Таким образом, было бы
хорошо, если бы вы так же последовали его примеру.

Точка с запятой
===============

Есть :ref:`мятежные силы <community-isaac-schlueter>`, которые пытаются
украсть у вас точки с запятой. Но не совершайте ошибок! Наша традиционная
культура все еще `живет`_. Так что следуйте за сообществом
и пользуйтесь точками с запятыми!

.. _живет: http://news.ycombinator.com/item?id=1547647

Редакторы
=========

Вы можете использовать любой редактор. Однако было бы удобно, чтобы он умел
подсвечивать синтаксис JavaScript'a и выполнять в среде Node.js редактируемый
файл. `Vim`_, конечно, не поможет вам впечатлить девушку, но зато он угодит
нашему `великодушному пожизненному диктатору`_ и ваш дедушка его тоже одобрит.

Я пишу этот документ в Notes на моем iPad'e, но это все потому, что я сейчас 
нахожусь на пляже в Таиланде. Так что, вполне вероятно, что ваше собственное
рабочее окружение повлияет на ваш выбор редактора.

.. _vim: http://www.vim.org/
.. _великодушному пожизненному диктатору: http://ru.wikipedia.org/wiki/Великодушный_пожизненный_диктатор

Концевые пробелы
================

Точно так же, как вы чистите зубы после еды, вы должны подчищать конечные 
пробелы в своих JavaScript файлах перед тем, как сделать коммит. Иначе гнилой
запах небрежности и пренебрежения разгонит в итоге авторов и/или коллег.

Длина строки
============

Следует ограничивать строки 80-ю символами. Да, экраны за последние несколько
лет стали больше, но ваш мозг не стал. Используйте дополнительное место для 
разбиения экрана. Ваш же редактор это позволяет, не так ли?

Кавычки
=======

Используйте одиночные кавычки везде, кроме случаев редактирования JSON.

*Хорошо*:

.. code-block:: javascript

    var foo = 'bar';

*Плохо*:

.. code-block:: javascript

    var foo = "bar";

Фигурные скобки
===============

Располагайте открывающую скобку на той же линии, что и выражение.

*Хорошо*:

.. code-block:: javascript

    if (true) {
      console.log('winning');
    }

*Плохо*:

.. code-block:: javascript

    if (true)
    {
      console.log('losing');
    }

Также обратите внимание на использование пробела перед и после условного
выражения.

Объявление переменных
=====================

Объявляйте по одной переменной с каждым ключевым словом var. Такой подход
облегчает переупорядочивание строк. Не обращайте внимания на `Crockford`_'a
по этому поводу и размещайте объявления там, где они имеют смысл.

.. _Crockford: http://javascript.crockford.com/code.html

*Хорошо*:

.. code-block:: javascript

    var keys = ['foo', 'bar'];
    var values = [23, 42];

    var object = {};
    while (items.length) {
      var key = keys.pop();
      object[key] = values.pop();
    }

*Плохо*:

.. code-block:: javascript

    var keys = ['foo', 'bar'],
        values = [23, 42],
        object = {},
        key;

    while (items.length) {
      key = keys.pop();
      object[key] = values.pop();
    }


Имена переменных и свойств
==========================

Переменные и свойства должны использовать **нижний** `верблюжий регистр`_.
Кроме того, они должны быть наглядными. Одиночных символов и необычных
аббревиатур следует избегать.

.. _верблюжий регистр: http://ru.wikipedia.org/wiki/CamelCase

*Хорошо*:

.. code-block:: javascript

    var adminUser = db.query('SELECT * FROM users ...');

*Плохо*:

.. code-block:: javascript

    var admin_user = d.query('SELECT * FROM users ...');

Имена классов
=============

Имена классов должны использовать **верхний** `верблюжий регистр`_.

*Хорошо*:

.. code-block:: javascript

    function BankAccount() {
    }

*Плохо*:

.. code-block:: javascript

    function bank_Account() {
    }

Константы
=========

Константы должны объявляться как обычные переменные или статические свойства
классов. Все буквы должны быть в верхнем регистре.

Node.js / V8 поддерживает расширение const_ от mozilla, но, к сожалению,
оно не применимо к членам класса, равно как и часть любого стандарта ECMA.

.. _const: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

*Хорошо*:

.. code-block:: javascript

    var SECOND = 1 * 1000;

    function File() {
    }
    File.FULL_PERMISSIONS = 0777;

*Плохо*:

.. code-block:: javascript

    const SECOND = 1 * 1000;

    function File() {
    }
    File.fullPermissions = 0777; 

Создание Объекта / Массива
==========================

Используйте завершающие запятые и *короткие* объявления на одной строке. 
Ключи помещайте в кавычки только тогда, когда интерпретатор может не
понять код (составные ключи и т.п.). 

*Хорошо*:

.. code-block:: javascript

    var a = ['hello', 'world'];
    var b = {
      good: 'code',
      'is generally': 'pretty',
    };

*Плохо*:

.. code-block:: javascript

    var a = [
      'hello', 'world'
    ];
    var b = {"good": 'code'
            , is generally: 'pretty'
            };


Оператор равенства
==================

Программирование - это вам не запоминание `глупых правил`_. Используйте
тройной оператор равенства, так как только он будет работать так, как
ожидается.

.. _глупых правил: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

*Хорошо*:

.. code-block:: javascript

    var a = 0;
    if (a === '') {
      console.log('winning');
    }

*Плохо*:

.. code-block:: javascript

    var a = 0;
    if (a == '') {
      console.log('losing');
    }

Расширение прототипов
=====================

Не расширяйте прототипы всех подряд объектов, особенно встроенных. В аду есть
специальное место, в котором вас будут ждать, если вы не будете следовать этому
правилу.

*Хорошо*:

.. code-block:: javascript

    var a = [];
    if (!a.length) {
      console.log('winning');
    }

*Плохо*:

.. code-block:: javascript

    Array.prototype.empty = function() {
      return !this.length;
    }

    var a = [];
    if (a.empty()) {
      console.log('losing');
    }

Условия
=======

Все нетривиальные условия должны присваиваться переменной.

*Хорошо*:

.. code-block:: javascript

    var isAuthorized = (user.isAdmin() || user.isModerator());
    if (isAuthorized) {
      console.log('winning');
    }

*Плохо*:

.. code-block:: javascript

    if (user.isAdmin() || user.isModerator()) {
      console.log('losing');
    }

Размер функций
==============

Функции должны быть короткими. Хорошая функция должна помещаться на слайд,
который будет хорошо читаться людьми, сидящими на последнем ряду в большой
комнате.

Оператор return
===============

Возвращайте значение из функции как можно раньше. Тем самым будет исключаться
большая вложенность if-else конструкций.

*Хорошо*:

.. code-block:: javascript

    function isPercentage(val) {
      if (val < 0) {
        return false;
      }

      if (val > 100) {
        return false;
      }

      return true;
    }

*Плохо*:

.. code-block:: javascript

    function isPercentage(val) {
      if (val >= 0) {
        if (val < 100) {
          return true;
        } else {
          return false;
        }
      } else {
        return false;
      }
    }

Или для этого конкретного примера этот подход также применим:

.. code-block:: javascript

    function isPercentage(val) {
      var isInRange = (val >= 0 && val <= 100);
      return isInRange;
    }

Именованные замыкания
=====================

Не бойтесь давать замыканиям имена. Это показывает, что вы заботитесь о них.
Результатом этой заботы будет более полная трассировка стека:

*Хорошо*:

.. code-block:: javascript

    req.on('end', function onEnd() {
      console.log('winning');
    });

*Плохо*:

.. code-block:: javascript

    req.on('end', function() {
      console.log('losing');
    });

Вложенные замыкания
===================

Не используйте вложенные замыкания. Иначе ваш код превратится в кашу

*Хорошо*:

.. code-block:: javascript

    setTimeout(function() {
      client.connect(afterConnect);
    }, 1000);

    function afterConnect() {
      console.log('winning');
    }

*Плохо*:

.. code-block:: javascript

    setTimeout(function() {
      client.connect(function() {
        console.log('losing');
      });
    }, 1000);

Функции обратного вызова (callbacks)
====================================

Так как Node.js прежде всего сосредоточен на неблокирующем вводе/выводе, то
функции в основном возвращают свой результат, используя callback'и. В ядре 
Node.js принято соглашение, что первый параметр любого callback'а всегда 
является необязательным объектом-ошибкой (error object).

Вам также следует пользоваться этим подходом для своих callback'ов.

Object.freeze, Object.preventExtensions, Object.seal, with, eval
================================================================

Абсолютное безумие, которое, вероятно, никогда вами не будет использовано.
Держитесь от этого дела подальше.

Getter'ы и setter'ы
===================

Не используйте setter'ы. У людей, которые будут пытаться использовать ваш
код, они обязательно вызовут массу проблем.

Getter'ы же, напротив, можно совершенно спокойно использовать в своем коде.
Так как они являются чистыми функциями и свободны от `побочных эффектов`_.
Типовым примером является предоставление свойства длины для класса коллекции.

.. _побочных эффектов: http://ru.wikipedia.org/wiki/Побочный_эффект_(программирование) 

EventEmitter'ы
==============

Node.js включает в себя, среди прочего, простой класс EventEmitter, который 
может быть подключен из модуля 'events':

.. code-block:: javascript

    var EventEmitter = require('events').EventEmitter;

При создании классов, которые должны поддерживать события, их обычно наследуют
от этого класса EventEmitter. В основном, это простая реализация `шаблона 
Observer`_

.. _шаблона Observer: http://ru.wikipedia.org/wiki/Наблюдатель_(шаблон_проектирования) 

Однако, я настоятельно не рекомендую слушать события объекта изнутри самого 
объекта. Это не естественно - слушать самого себя. Зачастую, это ведет к
нежелательному открытию деталей реализации и усложнению сопровождения кода.

Наследование / Объектно-ориентированное программирование
========================================================

Наследование и объектно-ориентированное программирование являются обширными
темами. Если вы интересуетесь этими популярными подходами программирования,
то почитайте, пожалуйста, мое :doc:`Руководство по объектно-ориентированному 
программированию <object_oriented_programming>`.

