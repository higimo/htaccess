# Запрет выдачи листинга каталога

[Директива Options](http://httpd.apache.org/docs/trunk/mod/core.html#options) задаёт: разрешение на выполнение CGI-скриптов, обработку симлинков, демонстрацию списка файлов, если отсутствует индексный файл.

* `All` Все опции, исключая `MultiViews`
* `ExecCGI` Исполнение CGI-скриптов, запущенных через [`mod_cgi`](http://httpd.apache.org/docs/trunk/mod/mod_cgi.html).
* `FollowSymLinks` Использование по симлинками. Установлено по умолчанию.
* `Includes` Использование [`mod_include`](http://httpd.apache.org/docs/trunk/mod/mod_include.html).
* `IncludesNOEXEC` Использование `mod_include`, отключая CMD и CGI. Но разрешается использовать виртуальные CGI-скрипты указанные в `ScriptAliased` директориях.
* `Indexes` если нет индексного файла (указывается в `DirectoryIndex`), то используется [mod_autoindex](http://httpd.apache.org/docs/trunk/mod/mod_autoindex.html), выводящий список файлов в каталоге.
* `MultiViews` исполнение MultiViews, работающего через [mod_negotiation](http://httpd.apache.org/docs/trunk/mod/mod_negotiation.html).
* `SymLinksIfOwnerMatch` Будут использоваться только те симлинки, у которых конечная цель принадлежит тому же создателю.

Параметры записываются через пробел. Предшествующие знаки + или - указывают на наследование

Например:

    # Так записываются комментарии
    # включим только параметр Includes
    Options +Includes 

Чтобы, например, не показывался список файлов в каталоге, если нет индексного файла:

    # запрет выдачи листинга пустого каталога
    Options -Indexes

Наоборот:

    Options Indexes

Включим параметр Includes и выключим параметр Indexes

    Options +Includes -Indexes

Покажем список файлов в каталоге, но скроем часть файлов, фильтруя по формату файла:

    IndexIgnore *.php*  *.pl

Повторим для директории `/web/docs/spec`

    <Directory "/web/docs/spec">
        Options +Includes -Indexes
    </Directory>
