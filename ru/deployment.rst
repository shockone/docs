Развертывание
#############

Как только ваше приложение готово, или даже до того, вы захотите развернуть его
на production-сервере. Есть несколько вещей, которые вы должны сделать при
развертывании CakePHP приложения.

Установите document root
========================

Правильная установка document root для вашего приложения - это важный шаг для
обеспечения безопасности вашего кода. Используя приложения, написанные с помощью CakePHP, 
убедитесь, что document root вашего виртуального хоста ведет в ``app/webroot``.
В этом случае файлы содержащие логику или настройки не будут доступны через URL.
Настройка document root различается для разных серверов. Смотрите :doc:`/installation/advanced-installation` для конкретных серверов.

Настройте core.php
==================

Очень важным моментом для production-сервера является настройка core.php, особенно значение ``debug``. Установка debug = 0 отключает большое количество 
функций, необходимых при разработке, которые ни в коем случае не должны 
попасть на production-сервер. Отключение отладки меняет следующее:

* Отладочные сообщения, созданные с помощью :php:func:`pr()` и :php:func:`debug()`
  отключаются и не выводятся на экран.
* Кеш ядра CakePHP обновляется каждые 99 лет, вместо 10 секунд, как для разработки 
  (эти числа настраиваются в core.php).
* Представления для ошибок менее информативны и содержат только обобщенные сообщения об
  ошибках.
* Ошибки не выводятся.
* Трассирование стека исключений отключается.

В добавок к вышеперечисленному, многие плагины и приложения при разном 
значении ``debug`` ведут себя по-разному.


Несколько CakePHP приложений, использующих одно ядро
====================================================

Есть несколько способов конфигурации приложений для совместного 
использования одного ядра CakePHP. Можно либо использовать PHP ``include_path``,
либо изменить константу ``CAKE_CORE_INCLUDE_PATH`` (``webroot/index.php``) во всех приложениях. Как правило использование ``include_path`` проще и надежнее. 
CakePHP устроен таким образом, чтобы учитывать ``include_path``, потому его 
просто использовать.

В файле ``php.ini`` установите директиву, или добавьте в ней путь к ядру::

    include_path = '.:/usr/share/php:/usr/share/cakephp-2.0/lib'

В этом примере подразумевается, что приложение работает на \*nix сервере, а
CakePHP находится в ``/usr/share/cakephp-2.0``.
