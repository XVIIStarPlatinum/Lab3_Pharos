# Отчёт по лабораторной работе №3
___
 - Выполнил: Болорболд Аригуун
 - Группа: P3211
 - Вариант: `alg | stack | harv | hw | instr | binary | stream | port | cstr | prob2 | cache`
## Язык программирования
___
### Pharos: the lighthouse
![Pharos-Logo](/media/Pharos.png)
![Pharos-platinum](/media/Pharos_Platinum.png)
![Pharos-Green](/media/Pharos_Green.png)
По варианту необходимо реализовать C-подобный структурный язык.
```

```
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?

Память для строковых литералов, строковых буферов выделяется ...?
## Организация памяти
___
По варианту используется гарвардская архитектура, поэтому память инструкций и память данных разделена.

Память инструкции представляет собой список объектов, которые описывают инструкции.

Память данных — линейное адресное пространство, где одно машинное слово — 32 бит. В коде реализуется словарем, чтобы не хранить все нули между началом памяти и вершиной стека.
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
## Система команд
___
Особенности процессора:
- ?
- ?
- ?
- ?
Пример команды:
```

```
- ?
- ?
  - ?
  - ?
  - ?
  - ?
  - ?
  - ?
- ?
- ?
- ?
### Набор инструкции
- Вычисления
  - ADD operand
  - SUB operand
  - AND operand
  - OR operand
  - SHL operand
  - SHR operand
- Доступ к памяти
  - LD operand
  - ST address
- Работа со стеком
  - PUSH
  - POP
- Ветвления
  - CMP operand
  - JZ address
  - JNZ address
  - JB address
  - JBE address
  - JA address
  - JAE address
  - JMP address
- Управление Control Unit
  - HLT — Устанавливает флаг HLT в Control Unit

## Транслятор
___
Транслятор состоит из 3 частей:
- Lexer — разбивает исходный поток символов на токены, проверяет на самые простые ошибки по типу незакрытых скобок;
- AST — используя токены строит абстрактное синтаксическое дерево, проверяет синтаксис;
- Backend — используя AST производит упакованную программу, в которой есть все инструкции, статически выделенные данные в памяти. Используется шаблон проектирования `Visitor` для обхода дерева.
Интерфейс командной строки:
```
$ poetry install
$ poetry shell
$ python -m Pharos3.compiler <input_file> <output_file> 
```
## Модель процессора
___
### Data Path

- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
- ?
?
- ?
- ?
- ?
- ?
- ?
### Control Unit
Данная часть модели занимается декодированием микрокоманд.
Существуют 2 вида микрокоманд:
- Управляющие — отправляют сигнал;
- Ветвление — работают как одна большая формула логического И по входящим в Control Unit сигналы. Если результат 1, то микрокомандных счетчик принимает значение, указанное в команде. Также есть специальный вид данной команды, где игнорируются все остальные биты и происходит ветвление по результату декодера `OP_CODE`.
Листинг микрокоманд:
```
???
```
Запуск через командную строку:
```
$ poetry install
$ poetry shell
$ python -m Pharos3.compiler <input_file> <output_file> 
```
## Тестирование
___
В качестве тестов реализовано 5 алгоритмов:
- 🐱‍
- Hello World!
- Hello, `<name>`!
- Project Euler Problem 1
- Project Euler Problem 5
Было созданы 2 вида тестов:
- Unit-tests на компонент АЛУ
- Golden tests на программы
Запуск тестов через командную строку:
```
$ poetry install
$ poetry shell
$ make test-cov
```
## CI
___
CI был настроен для платформы GitHub и GitLab:
```
<Insert CI/CD here>
```
Используемые инструменты:
- `pylint` — утилита для проверки качества кода;
- `pytest` — утилита для запуска тестов;
- `poetry` — утилита дл настраивания зависимостей и виртуальной среды;
- `make` — чтобы не писать команды в полном виде;
- `black` — форматирование;
- `isort` — сортировка импортов.
Пример использования и журнал работы на примере `cat`:
```
$ poetry install
$ poetry shell
$ make
poetry run python -m comp3.compiler examples/euler_problem.lisq output/examples/euler_problem.json
poetry run python -m comp3.compiler examples/hello.lisq output/examples/hello.json
poetry run python -m comp3.compiler examples/euler_problem_1.lisq output/examples/euler_problem_1.json
poetry run python -m comp3.compiler examples/hello_user_name.lisq output/examples/hello_user_name.json
poetry run python -m comp3.compiler examples/cat.lisq output/examples/cat.json
$ poetry run python -m comp3.machine output/examples/cat.json foo --show-statistics --logs
[Results omitted]
```
Сами логи
Пример проверки исходного кода:
```
$ poetry install
$ poetry shell
$ make test
=====================================test session starts ==================================
<Insert test log here>
```
## Статистика по задачам
___
```
|        ФИО        | алг             | LoC | code байт | code инстр. | инстр. | такт. |
| ------------------------------------------------------------------------------------ |
| Болорболд Аригуун | hello           |  3  | -         |     558     | 575    | 8007  |
| Болорболд Аригуун | hello           |  3  | -         |     21      | 58     | 804   |
| Болорболд Аригуун | hello           |  7  | -         |     623     | 1773   | 23822 |
```
