# Работа с Django

|bonobo| обеспечивает лёгкую интеграцию с Django, чтобы включать ETL-пайплайны в команды управления Django.

## Быстрый старт

Чтобы написать команду управления Django, которая запускает задания |bonobo|, просто расширите :class:`ETLCommand` вместо :class:`django.core.management.base.BaseCommand` и переопределите метод :meth:`ETLCommand.get_graph`:

```python
import bonobo
from bonobo.contrib.django import ETLCommand

class Command(ETLCommand):
    def get_graph(self, **options):
        graph = bonobo.Graph()
        graph.add_chain(...)
        return graph
```

### Сервисы

Вы можете переопределить :meth:`ETLCommand.get_services`, чтобы предоставить свои реализации сервисов.

Один из распространённых рецептов для этого — импортировать его откуда-то ещё и переопределить как :obj:`staticmethod`:

```python
import bonobo
from bonobo.contrib.django import ETLCommand

from myproject.services import get_services

class Command(ETLCommand):
    get_services = staticmethod(get_services)

    def get_graph(...):
        ...
```

### Несколько графов

Метод :meth:`ETLCommand.get_graph` также может быть реализован как генератор. В этом случае каждый выданный элемент должен быть графом, и каждый граф будет выполнен по порядку:

```python
import bonobo
from bonobo.contrib.django import ETLCommand

class Command(ETLCommand):
    def get_graph(self, **options):
        yield bonobo.Graph(...)
        yield bonobo.Graph(...)
        yield bonobo.Graph(...)
```

Это особенно полезно в двух основных случаях:

* Вы должны гарантировать, что одно задание завершено перед запуском следующего, и, таким образом, не можете добавить узлы обоих графов в один и тот же граф.
* Вы хотите изменить, какой граф запускается, в зависимости от аргументов командной строки.

### Аргументы командной строки

Как и с обычными командами управления Django, вы можете добавить аргументы в парсер аргументов, переопределив :meth:`ETLCommand.add_arguments`.

Единственное отличие от Django заключается в том, что предоставленный парсер аргументов уже будет иметь добавленные аргументы для обработки окружения.

## Справочник

### :mod:`bonobo.contrib.django`

.. automodule:: bonobo.contrib.django

## Исходный код

https://github.com/python-bonobo/bonobo/tree/master/bonobo/contrib/django
