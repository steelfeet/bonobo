# Работа с SQLAlchemy

.. include:: _beta.rst

Прочитайте введение: https://www.bonobo-project.org/with/sqlalchemy

## Установка

Чтобы установить расширение, используйте дополнительный пакет `sqlalchemy`:

```shell-session
$ pip install bonobo[sqlalchemy]
```

> **Примечание** Вы можете установить более одного дополнительного пакета одновременно, разделяя имена запятыми.

## Обзор и примеры

Сначала вам понадобится подключение к базе данных (экземпляр :obj:`sqlalchemy.engine.Engine`), которое должно быть предоставлено как сервис.

```python
import sqlalchemy

def get_services():
    return {
        'sqlalchemy.engine': sqlalchemy.create_engine(...)
    }
```

Имя `sqlalchemy.engine` — это имя по умолчанию, используемое предоставленными преобразованиями, но вы можете переопределить его (например, если вам нужно более одного подключения) и указать имя сервиса, используя `engine='myengine'` при создании ваших преобразований.

Давайте создадим несколько таблиц и добавим данные. (Возможно, вам нужно будет отредактировать SQL, если ваш сервер базы данных использует другую версию SQL.)

```sql
CREATE TABLE test_in (
  id INTEGER PRIMARY KEY NOT NULL,
  text TEXT
);

CREATE TABLE test_out (
  id INTEGER PRIMARY KEY NOT NULL,
  text TEXT
);

INSERT INTO test_in (id, text) VALUES (1, 'Cat');
INSERT INTO test_in (id, text) VALUES (2, 'Dog');
```

Это расширение предоставляет два класса преобразований.

Один средство чтения, одно средство записи.

Давайте выберем некоторые данные:

```python
import bonobo
import bonobo_sqlalchemy

def get_graph():
    graph = bonobo.Graph()
    graph.add_chain(
        bonobo_sqlalchemy.Select('SELECT * FROM test_in', limit=100),
        bonobo.PrettyPrinter(),
    )
    return graph
```

Вы должны увидеть:

```shell-session
$ python tutorial.py
┌
│ id[0] = 1
│ text[1] = 'Cat'
└
┌
│ id[0] = 2
│ text[1] = 'Dog'
└
 - Select in=1 out=2 [done]
 - PrettyPrinter in=2 out=2 [done]
```

Теперь давайте вставим некоторые данные:

```python
import bonobo
import bonobo_sqlalchemy


def get_graph(**options):
    graph = bonobo.Graph()
    graph.add_chain(
        bonobo_sqlalchemy.Select('SELECT * FROM test_in', limit=100),
        bonobo_sqlalchemy.InsertOrUpdate('test_out')
    )

    return graph
```

Если вы проверите таблицу `test_out`, в ней теперь должны быть данные.

## Справочник

### :mod:`bonobo_sqlalchemy`

.. automodule:: bonobo_sqlalchemy

## Исходный код

https://github.com/python-bonobo/bonobo-sqlalchemy
