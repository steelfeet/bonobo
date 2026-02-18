# Модуль `Bonobo <bonobo>`

**Модуль:** `bonobo`

## Графы

* `bonobo.structs.graphs.Graph`

## Узлы

* `bonobo.nodes.CsvReader`
* `bonobo.nodes.CsvWriter`
* `bonobo.nodes.FileReader`
* `bonobo.nodes.FileWriter`
* `bonobo.nodes.Filter`
* `bonobo.nodes.FixedWindow`
* `bonobo.nodes.Format`
* `bonobo.nodes.JsonReader`
* `bonobo.nodes.JsonWriter`
* `bonobo.nodes.LdjsonReader`
* `bonobo.nodes.LdjsonWriter`
* `bonobo.nodes.Limit`
* `bonobo.nodes.MapFields`
* `bonobo.nodes.OrderFields`
* `bonobo.nodes.PickleReader`
* `bonobo.nodes.PickleWriter`
* `bonobo.nodes.PrettyPrinter`
* `bonobo.nodes.RateLimited`
* `bonobo.nodes.Rename`
* `bonobo.nodes.SetFields`
* `bonobo.nodes.Tee`
* `bonobo.nodes.UnpackItems`
* `bonobo.nodes.count`
* `bonobo.nodes.identity`
* `bonobo.nodes.noop`

## Другие API верхнего уровня

* `bonobo.create_reader`
* `bonobo.create_strategy`
* `bonobo.create_writer`
* `bonobo.get_argument_parser`
* `bonobo.get_examples_path`
* `bonobo.inspect`
* `bonobo.open_examples_fs`
* `bonobo.open_fs`
* `bonobo.parse_args`
* `bonobo.run`

### create_reader

Создаёт средство чтения.

### create_strategy

Создаёт стратегию выполнения.

### create_writer

Создаёт средство записи.

### get_argument_parser

Возвращает парсер аргументов для командной строки.

### get_examples_path

Возвращает путь к примерам.

### inspect

Инспектирует граф или задание.

### open_examples_fs

Открывает файловую систему примеров.

### open_fs

Открывает файловую систему.

### parse_args

Разбирает аргументы командной строки.

### run

Запускает выполнение графа.
