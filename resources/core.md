# Основы SQL

> Список терминов: [Административная команда (administration command)](/resources/glossary.md?id=Административная-команда-administration-command), [Агрегация (aggregation)](/resources/glossary.md?id=Агрегация-aggregation), [Агрегатная функция (aggregation function)](/resources/glossary.md?id=Агрегатная-функция-aggregation-function), [Исключающее ИЛИ (exclusive or)](/resources/glossary.md?id=Исключающее-ИЛИ-exclusive-or), [Фильтрация (filter)](/resources/glossary.md?id=Фильтрация-filter), [Группа (group)](/resources/glossary.md?id=Группа-group), [База данных в памяти (in-memory database)](/resources/glossary.md?id=База-данных-в-памяти-in-memory-database), [Включающее ИЛИ (inclusive or)](/resources/glossary.md?id=Включающее-ИЛИ-inclusive-or), [Нуль (null)](/resources/glossary.md?id=Нуль-null), [Запрос](/resources/glossary.md?id=Запрос-query), [Трехзначная логика (ternary logic)](/resources/glossary.md?id=Трехзначная-логика-ternary-logic), [Надгробный камень (tombstone)](/resources/glossary.md?id=Надгробный-камень-tombstone)

**SELECT** (выбрать) - это ключевое слово, которое обычно используется для получения данных из базы в языке SQL

## Получение всех данных из таблицы

```sql
select * from little_penguins;
```

```
Gentoo|Biscoe|51.3|14.2|218.0|5300.0|MALE
Adelie|Dream|35.7|18.0|202.0|3550.0|FEMALE
Adelie|Torgersen|36.6|17.8|185.0|3700.0|FEMALE
Chinstrap|Dream|55.8|19.8|207.0|4000.0|MALE
Adelie|Dream|38.1|18.6|190.0|3700.0|FEMALE
Adelie|Dream|36.2|17.3|187.0|3300.0|FEMALE
Adelie|Dream|39.5|17.8|188.0|3300.0|FEMALE
Gentoo|Biscoe|42.6|13.7|213.0|4950.0|FEMALE
Gentoo|Biscoe|52.1|17.0|230.0|5550.0|MALE
Adelie|Torgersen|36.7|18.8|187.0|3800.0|FEMALE
```

Результат выполнения можно посмотреть на [SQlize online](https://sqlize.online/sql/sqlite3_data/970e5de956dad37e24ca99f030d5ac13/)

Рассмотрим этот запрос:
- SELECT (выбрать) - ключевое слово для получения любых данных 
- Используем `*` для обозначения «все столбцы».
- Используем `from tablename` где tablename - имя таблицы из которой извлекаем данные.
- В большинстве диалектов SQL требуется разделитель точка с запятой в конце запроса`;`
  
Выходной формат будет не всегда понятнен для вас.

##  Административные команды базы данных SQLite

- .headers on - показывать заголовки столбцов таблицы
- .mode markdown - использовать разметку отображения

.mode markdown и .headers делают вывод более читабельным. После примнения этих команд вывод данных примет следующий вид.

```sql
select * from little_penguins;
```
```
|  species  |  island   | bill_length_mm | bill_depth_mm | flipper_length_mm | body_mass_g |  sex   |
|-----------|-----------|----------------|---------------|-------------------|-------------|--------|
| Gentoo    | Biscoe    | 51.3           | 14.2          | 218.0             | 5300.0      | MALE   |
| Adelie    | Dream     | 35.7           | 18.0          | 202.0             | 3550.0      | FEMALE |
| Adelie    | Torgersen | 36.6           | 17.8          | 185.0             | 3700.0      | FEMALE |
| Chinstrap | Dream     | 55.8           | 19.8          | 207.0             | 4000.0      | MALE   |
| Adelie    | Dream     | 38.1           | 18.6          | 190.0             | 3700.0      | FEMALE |
| Adelie    | Dream     | 36.2           | 17.3          | 187.0             | 3300.0      | FEMALE |
| Adelie    | Dream     | 39.5           | 17.8          | 188.0             | 3300.0      | FEMALE |
| Gentoo    | Biscoe    | 42.6           | 13.7          | 213.0             | 4950.0      | FEMALE |
| Gentoo    | Biscoe    | 52.1           | 17.0          | 230.0             | 5550.0      | MALE   |
| Adelie    | Torgersen | 36.7           | 18.8          | 187.0             | 3800.0      | FEMALE |
```

Административные команды SQLite начинаются с  точки . и не являются частью стандарта SQL. Специальные команды PostgreSQL начинаются с косой черты \
Каждая команда должна располагаться на отдельной строке.
Используйте .help для получения полного списка.
И, как упоминалось ранее, используйте .quit для выхода.

## Получение данных заданных колонок 

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/9484db9d3625b78b2ad204aa48596150/))

```sql
select
    -- перечисляум колонки, которые хотим увидеть
    species,
    island,
    sex
from little_penguins;
```
```
|  species  |  island   |  sex   |
|-----------|-----------|--------|
| Gentoo    | Biscoe    | MALE   |
| Adelie    | Dream     | FEMALE |
| Adelie    | Torgersen | FEMALE |
| Chinstrap | Dream     | MALE   |
| Adelie    | Dream     | FEMALE |
| Adelie    | Dream     | FEMALE |
| Adelie    | Dream     | FEMALE |
| Gentoo    | Biscoe    | FEMALE |
| Gentoo    | Biscoe    | MALE   |
| Adelie    | Torgersen | FEMALE |
```

Для выбора определённых колонок укажите их имена разделенные запятыми.
В любом порядке!
Дубликаты разрешены!
Разрывы строк приветствуются для удобства чтения, вам все вернется.

## Получение констант

`SELECT` обычно используется для выбора данных из таблицы... но если все, что нам нужно, это констаната, нам не нужно указывать указывать имя таблицы.

```sql
select 1; -- Результатом этого запроса будет константа - 1
```
- В результате выполнения команды `select` всегда получаем таблицу. В данном случае таблица состоит из одного столбца и содержит одну сторку. 
- Любой текст начиная с `-- ` и до конца строки является комментарием и игнорируется интерпритатором команд.  

```
| 1 |
```

## Вычисления

([онлайн sql песочница](https://sqlize.online/sql/sqlite3_data/c09ccf5e590727eefd505201c9bf8cd6/))

```sql
select 2 + 3; -- простой расчет

select 60 * 60 * 24; -- вычислить секунды в 24 часах

select 'Happy ' || 'New Year!'; -- конкатенация строк

select PI() * POW(5, 2); -- использование функций

select current_date, current_time; -- текущая дата и время
```
```
|-------|
| 2 + 3 |
|-------|
| 5     |

|--------------|
| 60 * 60 * 24 |
|--------------|
| 86400        |

|-------------------------|
| 'Happy ' || 'New Year!' |
|-------------------------|
| Happy New Year!         |

|------------------|
| PI() * POW(5, 2) |
|------------------|
| 78.539816339745  |

|--------------|--------------|
| current_date | current_time |
|--------------|--------------|
| 2024-12-30   | 13:58:27     |
```

- SQL может выполнять простые операции с числами, строками и датами.
- Вы можете использовать различные встроенные функции для более сложных операций.
- Полный список и документацию встроенных функций SQL см. в [официальной документации SQLite](https://www.sqlite.org/lang_corefunc.html).

## Cортировка результатов запроса

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/528cad2f89530cb59775b1d8ae00b4f2/))

```sql
select
    -- перечисляем колонки, которые хотим увидеть
    species,
    sex,
    island
-- из таблицы little_penguins
from little_penguins
-- сортируем результаты
order by 
    island asc, -- сначала сортируем по острову
    sex desc; -- затем по полу по убыванию (MALE -> FEMALE)
```
```
|  species  |  sex   |  island   |
|-----------|--------|-----------|
| Gentoo    | MALE   | Biscoe    |
| Gentoo    | MALE   | Biscoe    |
| Gentoo    | FEMALE | Biscoe    |
| Chinstrap | MALE   | Dream     |
| Adelie    | FEMALE | Dream     |
| Adelie    | FEMALE | Dream     |
| Adelie    | FEMALE | Dream     |
| Adelie    | FEMALE | Dream     |
| Adelie    | FEMALE | Torgersen |
| Adelie    | FEMALE | Torgersen |
```

- `order by` должен следовать после `from` (который должен следовать после `select`)
- `asc` — сортировка по возрастанию,
- `desc` — по убыванию.
- строки сортируются в алфавитном порядке, даты - в календарном.
- По умолчанию — выполняется сортировка по возрастанию, но лучше укажите, пожалуйста.
- Сортировка выполняется по одному или нескольким столбцам. Порядок сортировки указывается после каждого столбца.
- Порядок строк с одинаковыми значениями не определен.

#### Упражнения

- Напишите SQL-запрос для выбора столбцов `sex` - пол и `body_mass_g` - масса тела из таблицы `little_penguins`, отсортированных таким образом, чтобы сначала отображалась наибольшая масса тела. [SQL тренажёр онлайн](https://sqltest.online/ru/question/sqlite/sort-penguins)


## Ограничение результата запроса

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/7b9ec307409f3d84a132e00c0bff3908/))

```sql
select
    species,
    sex,
    island
from penguins
order by species, sex, island -- сортируем результаты по возврастанию вида, пола и острова
limit 10; -- ограничиваем количество строк первыми 10
```
```
| species |  sex   |  island   |
|---------|--------|-----------|
| Adelie  |        | Dream     |
| Adelie  |        | Torgersen |
| Adelie  |        | Torgersen |
| Adelie  |        | Torgersen |
| Adelie  |        | Torgersen |
| Adelie  |        | Torgersen |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
```

- Оператор `limit N` ограничивает количество строк возвращаемых запросом. 
- Число N указывает максимальное количество строк. Если результат содержит меньше строк - будут выведены все.
- Ограничение следует использовать только после сортировки. В противном случае результат непредсказуем!

#### Упражнения

1. Напишите запрос для выбора вида (`species`) и острова обитания (`island`) трёх самых лёгких пингвинов из таблицы `penguins`. [SQL тренажёр онлайн](https://sqltest.online/ru/question/sqlite/light-weight-penguins)

## Постраничный вывод (пагинация)

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/f223fa3e3a3eea42d51edd2e6c9ff915/))

```sql
select
    species,
    sex,
    island
from penguins
order by species, sex, island
limit 10 offset 3; -- пропускаем первые 3 строки и показываем следующие 10
```
```
| species |  sex   |  island   |
|---------|--------|-----------|
| Adelie  |        | Torgersen |
| Adelie  |        | Torgersen |
| Adelie  |        | Torgersen |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
| Adelie  | FEMALE | Biscoe    |
```

- Оператор `offset N` должен следовать после `limit M`
- Число N указывает количество строк, которые нужно пропустить с начала результата запроса.
- Таким образом, запрос `limit 10 offset 3` пропускает первые 3 строки и показывает следующие 10.

## Удаление дубликатов из результата запроса

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/31e1f865c5de14af77eca070cd985d63/))

```sql
select distinct -- выбираем только уникальные строки
    species,
    sex,
    island
-- из таблицы penguins
from penguins;
```
```
|  species  |  sex   |  island   |
|-----------|--------|-----------|
| Adelie    | MALE   | Torgersen |
| Adelie    | FEMALE | Torgersen |
| Adelie    |        | Torgersen |
| Adelie    | FEMALE | Biscoe    |
| Adelie    | MALE   | Biscoe    |
| Adelie    | FEMALE | Dream     |
| Adelie    | MALE   | Dream     |
| Adelie    |        | Dream     |
| Chinstrap | FEMALE | Dream     |
| Chinstrap | MALE   | Dream     |
| Gentoo    | FEMALE | Biscoe    |
| Gentoo    | MALE   | Biscoe    |
| Gentoo    |        | Biscoe    |
```

- Ключевое слово `distinct` пишется сразу после `select` (потому что SQL должен был читаться как английский)
- Показывает только уникальные строки в результате запроса. Дипликаты игнорируются и не выводятся.
- Пробелы в столбце `sex` указывают на недостающие данные. Мы поговорим об этом немного позже

#### Упражнения 

1. Составьте SQL-запрос для извлечения данных об островах и видах пингвинов из таблицы `penguins` в порядке возрастания массы тела, начиная с 50-й и заканчивая 60-й записью. *Ваш результат должен состоять из 11 строк.* [SQL тренажёр онлайн](https://sqltest.online/en/question/sqlite/penguins-pagination)
2. Измените свой запрос, чтобы выбрать различные комбинации островов и проживающих на них видов пингвинов, и сравните результат с тем, что вы получили в части 1. [SQL тренажёр онлайн](https://sqltest.online/ru/question/sqlite/penguins-islands-distribution)


## Фильтрация результатов запроса

```sql
-- выбираем колонки, которые хотим увидеть
select
    species,
    sex,
    island
-- из таблицы penguins
from penguins
-- фильтруем результаты (оставляем только строки с островом Biscoe)
where island = 'Biscoe';
```
```
| species | sex    | island |
|---------|--------|--------|
| Adelie  | FEMALE | Biscoe |
| Adelie  | MALE   | Biscoe |
| Adelie  | FEMALE | Biscoe |
| Adelie  | MALE   | Biscoe |
| ...     | ...    | ...    |
```
**Примечание**: Результаты запроса были обрезаны для удобства чтения. Полную таблицу можно посмотреть на [SQLize online](https://sqlize.online/sql/sqlite3_data/1268807b7d1a5dd5731b1baf19f0d062/)

- Команда `where` фильтрует строки, полученные в результате выбора.
- Условие проверяется независимо для каждой строки
- В результатах отображаются только строки, прошедшие проверку.
*Используйте одинарные кавычки для 'текстовых данных' и двойные кавычки для "странных имен столбцов".
SQLite будет принимать текстовые данные в двойных кавычках, но SQLFluff будет жаловаться*

#### Упражнения

1. Напишите запрос для выбора пингвинов с массой тела менее 3000 граммов. [SQL тренажёр онлайн](https://sqltest.online/ru/question/sqlite/small-penguins)
2. Напишите еще один запрос, чтобы выбрать вид и пол пингвинов весом менее 3000 граммов. *Это показывает, что отображаемые столбцы и столбцы, используемые при фильтрации, независимы друг от друга.* [SQL тренажёр онлайн](https://sqltest.online/ru/question/sqlite/small-penguins-species)

## Фильтрация с более сложными условиями

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/c99103b164cab302cf03bc976f9a6beb/))

```sql
select distinct -- выбираем только уникальные строки (после фильтрации)
    species,
    sex,
    island
-- из таблицы penguins
from penguins
-- фильтруем результаты (оставляем только строки с островом Biscoe и не мужского пола)
where island = 'Biscoe' and sex != 'MALE';
```
```
| species |  sex   | island |
|---------|--------|--------|
| Adelie  | FEMALE | Biscoe |
| Gentoo  | FEMALE | Biscoe |
```
- Можно комбинировать условия ипользуя союзы `and` и `or`
- `and` - требует чтобы оба подусловия были истинными.
- `or`  - достаточно что одно из условий верно.
- `not` - инвертирует результат проверки условия.
- Сначала выполняется проверка  `and`, затем `or`. В сложных случаях используйте скобки.
- Обратите внимание, что строка для пингвинов Генту на острове Биско с неизвестным (пустым) полом не прошла проверку.
- Мы поговорим об этом немного позже.

#### Упражнения

1. Используйте оператор `not`, чтобы выбрать пингвинов, которые не относятся к виду Gentoo.
2. В SQL оператор `or` является включающим оператором: он выполняется успешно, если одно или оба условия истинны. SQL не предоставляет специального оператора для исключающего или, который верен, если истинно одно из условий, но не оба, но того же эффекта можно достичь, используя and, `or` и `not`. Напишите запрос, чтобы выбрать пингвинов-самок или пингвинов на острове Torgersen, но не обоих сразу.

## Комбинация: фильтрация + сортировка + пагинация

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/95248b8ed98c338ce76ac65eb2f565c0/))

Иногда нам нужно не только отфильтровать данные, но и отсортировать их (и возможно ограничить количество строк в результате). Язык SQL позволяет сделать всё это одним запросом.
Рассмотрим пример, где мы выбираем пингвинов вида `Adelie`, сортируем их по массе тела в порядке убывания и ограничиваем результат первыми пятью строками.

```sql
select
    species,
    body_mass_g,
    island
from penguins
where species = 'Adelie' -- фильтруем только пингвинов вида Adelie
order by body_mass_g desc -- сортируем по массе тела в порядке убывания
limit 5; -- ограничиваем результат первыми пятью строками
```
```
| species | body_mass_g | island    |
|---------|-------------|-----------|
| Adelie  | 4775        | Biscoe    |
| Adelie  | 4725        | Biscoe    |
| Adelie  | 4700        | Torgersen |
| Adelie  | 4675        | Torgersen |
| Adelie  | 4650        | Dream     |
```

- В этом запросе мы сначала используем `where`, чтобы отфильтровать строки, соответствующие виду "Adelie".
- Затем мы используем `order by`, чтобы отсортировать результаты по массе тела (`body_mass_g`) в порядке убывания (`desc`).
- Наконец, мы используем `limit`, чтобы ограничить результат первыми пятью строками.

Этот подход позволяет нам получить наиболее пять тяжелых пингвинов вида `Adelie` и упорядочить их по массе тела.

#### Упражнения

1. Измените запрос так чтобы он вывел вторую пятёрку результатов, содержащую пингвинов вида "Gentoo", отсортированных по длине клюва в порядке возрастания.
2. [Напишите запрос, чтобы выбрать остров обитания, пол и массу пингвинов вида "Chinstrap" с массой тела более четырёх килограмм, отсортированных по длине ласт в порядке убывания](https://sqltest.online/ru/question/sqlite/heavy-chinstrap-penguins).

## Выполнение расчетов

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/5263669b94cf065f18343dcc33248739/))

```sql
select
    flipper_length_mm / 10.0, -- переводим миллиметры в сантиметры
    body_mass_g / 1000.0 -- переводим граммы в килограммы
from penguins
limit 3;
```
```
| flipper_length_mm / 10.0 | body_mass_g / 1000.0 |
|--------------------------|----------------------|
| 18.1                     | 3.75                 |
| 18.6                     | 3.8                  |
| 19.5                     | 3.25                 |
```

- SQL может выполнять различные операции с отдельными значениями.
- Расчет производится для каждой строки отдельно.
- Название столбца (`flipper_length_mm / 10.0`, `body_mass_g / 1000.0`) показывает выполненный расчет. 

## Псевдонимы колонок

```sql
select
    flipper_length_mm / 10.0 as flipper_cm, -- переводим миллиметры в сантиметры и называем столбец flipper_cm
    body_mass_g / 1000.0 as weight_kg, -- переводим граммы в килограммы и называем столбец weight_kg
    island as where_found
from penguins
-- сортируем результаты по убыванию массы тела и длины ласт
order by weight_kg desc, flipper_cm desc
-- ограничиваем количество строк (3 самых тяжелых пингвина)
limit 3;
```
```
| flipper_cm | weight_kg | where_found |
|------------|-----------|-------------|
| 18.1       | 3.75      | Torgersen   |
| 18.6       | 3.8       | Torgersen   |
| 19.5       | 3.25      | Torgersen   |
```
([проверить sql онлайн](https://sqlize.online/sql/sqlite3_data/05bde8ecc4459418c669e0637deb290d/))

- Используйте `выражение as имя` для назначения псевдонима.
- Используйте осмысленные псевдонимы.
- Также можно давать псевдонимы столбцам без вычислений. Например, `island as place`.

#### Упражнения

Напишите один запрос, который вычисляет и возвращает:
1. Столбец `bill_ratio`, в котором указано соотношение длины клюва к его глубине.
2. [Найдите отношение длины плавника к массе тела для всех пингвинов из таблицы](https://sqltest.online/ru/question/sqlite/flipper-length-to-body-mass-rate).
3. Столбец под названием `what_where`, в котором вид и остров каждого пингвина разделены одним пробелом<sup>*</sup>.

<sup>*</sup> *Вы можете использовать || оператор для объединения текста для решения части 1 или посмотрите документацию по функции [SQLite format()](https://sqlite.org/printf.html).*

## SELECT: концептуальная схема

<img src="./assets/select_concept_map.svg" alt="SELECT: концептуальная схема" style="max-width:100%; height:auto;">

## Отсутствующие значения (null)

- SQL использует специальное значение `null` для представления отсутствующих данных.
- `null` это не 0 или пустая строка, а «Я не знаю».

### Вычисления с `null`

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/05bde8ecc4459418c669e0637deb290d/))

```sql
select
    flipper_length_mm / 10.0 as flipper_cm,
    body_mass_g / 1000.0 as weight_kg,
    island as where_found
from penguins
limit 5;
```
```
| flipper_cm | weight_kg | where_found |
|------------|-----------|-------------|
| 18.1       | 3.75      | Torgersen   |
| 18.6       | 3.8       | Torgersen   |
| 19.5       | 3.25      | Torgersen   |
|            |           | Torgersen   |
| 19.3       | 3.45      | Torgersen   |
```

- Длина ласт и масса тела ни одного из первых пяти пингвинов неизвестны.
- «Я не знаю», разделенное на 10 или 1000 — это тоже «Я не знаю».

#### Упражнения
1. Используйте команду SQLite .nullvalue, чтобы изменить печатное представление значения null на строку null, а затем повторно запустите предыдущий запрос. Когда будет легче понять отображение null как null? Когда это может ввести в заблуждение?

### Сравнение с `null`

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/0c62d806cfb999a431d3c78b488d965d/))

Выполним запрос, который уже использовали ранее. Видно что в одной строке отсутствуют данные о поле пингвина.

```sql
select distinct
    species,
    sex,
    island
from penguins
where island = 'Biscoe';
```
```
| species |  sex   | island |
|---------|--------|--------|
| Adelie  | FEMALE | Biscoe |
| Adelie  | MALE   | Biscoe |
| Gentoo  | FEMALE | Biscoe |
| Gentoo  | MALE   | Biscoe |
| Gentoo  |        | Biscoe |
```

Если мы спросим о самках пингвинов, строка с отсутствующим полом будет отфильтрована и мы получаем следующий результат.

```sql 
select distinct
    species,
    sex,
    island
from penguins
where island = 'Biscoe' and sex = 'FEMALE';
```
```
| species |  sex   | island |
|---------|--------|--------|
| Adelie  | FEMALE | Biscoe |
| Gentoo  | FEMALE | Biscoe |
```

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/b77d9e619645f3562fe18b0bec573ed6/))

Но если мы спросим о пингвинах, не являющихся самками, их мы тоже не получим эту строку.

```sql
select distinct
    species,
    sex,
    island
from penguins
where island = 'Biscoe' and sex != 'FEMALE';
```
```
| species | sex  | island |
|---------|------|--------|
| Adelie  | MALE | Biscoe |
| Gentoo  | MALE | Biscoe |
```

### Тернарная логика

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/f42a97eea4aabe84ac06069c2def564e/))

- это логика, которая работает с тремя значениями: истиной, ложью и неопределенностью. В SQL это представлено значениями `true`, `false` и `null`.

```sql
select null = null;
```
```
| null = null |
|-------------|
|             |
```

- Если мы не знаем ни левого ни правого значений, мы не знаем, равны они или нет.
- Итак, результат нулевой
- Тот же результат будет для сравнения **null != null**

```
| Равенство (X != Y)                                    |
|-------------|-------------|-------------|-------------|
|             | X           | Y           | null        |
| X           | true        | false       | null        |
| Y           | false       | true        | null        |
| null        | null        | null        | null        |
```

### Безопасная обработка `null` значений

([выполнить sql онлайн](https://sqlize.online/sql/sqlite3_data/9fcfbdccb6ba09efcdfba07940429a40/))

```sql
 select
    species,
    sex,
    island
from penguins
where sex is null;
```
```
| species | sex |  island   |
|---------|-----|-----------|
| Adelie  |     | Torgersen |
| Adelie  |     | Torgersen |
| Adelie  |     | Torgersen |
| Adelie  |     | Torgersen |
| Adelie  |     | Torgersen |
| Adelie  |     | Dream     |
| Gentoo  |     | Biscoe    |
| Gentoo  |     | Biscoe    |
| Gentoo  |     | Biscoe    |
| Gentoo  |     | Biscoe    |
| Gentoo  |     | Biscoe    |
```

- Используйте `is null` и `is not null` для безопасной обработки null в условиях запроса.
- В других частях SQL отсутствующие значения могут обрабатываться другими способами.

#### Упражнения

1. Напишите еще один запрос, чтобы найти пингвинов у которых неизвестны ни длина ни глубина клюва.
2. [Напишите запрос, чтобы найти пингвинов, масса тела которых известна, но пол неизвестен](https://sqltest.online/ru/question/sqlite/penguins-whose-sex-is-unknown). 
3. [Найдите все записи о пингвинах, где хотя бы один столбец не имеет значения](https://sqltest.online/ru/question/sqlite/absent-data).

### NULL: концептуальная схема

<img src="./assets/null_concept_map.svg" alt="концептуальная схема" style="max-width:100%; height:auto; margin-top: 2em;">