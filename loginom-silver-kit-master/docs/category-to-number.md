# Категория к числу

[Назад к списку компонентов](../README.md)

## Назначение

Компонент осуществляет кодирование каждой категории в целое число. Расстояние между соседними целыми числами зависит от переменной **Инкремент**.

## Входные порты

| Название   | Тип        |
|:-----------|:-----------|
| Категории  | Таблица    |
| Переменные | Переменные |

### Структура таблицы "Номинальные данные"

| Метка     | Тип                             | Описание                                |
|:----------|:--------------------------------|:----------------------------------------|
| Категория | ![](./img/string.svg) Строковый | Наименование или идентификатор категории|

### Переменные в порте "Переменные"

| № | Метка              | Тип                               | Значение |
|:--|:-------------------|:----------------------------------|:---------|
| 1 | Начальное значение | ![](./img/integer.svg) Целый      | 0        |
| 2 | Инкремент          | ![](./img/integer.svg) Целый      | 1        |
| 3 | Считать пустые     | ![](./img/logical.svg) Логический | true     |

1. **Начальное значение** — значение, которое будет присвоено первой категории.

2. **Инкремент** — категории присваивается номер по принципу: *Начальное значение + Инкремент &#42; Позиция категории*.

3. **Считать пустые** — задает способ обработки пустых значений. При значении **true** (по умолчанию) пустой категории будет присвоен номер, **false** — пустые категории останутся пустыми.

## Выходные порты

| Название      | Тип        |
|:--------------|:-----------|
| Набор данных  | Таблица    |
| Таблица замен | Таблица    |

### Структура таблицы "Набор данных"

| Метка               | Тип                          | Описание                    |
|:--------------------|:-----------------------------|:----------------------------|
| Категория (замена)  | ![](./img/integer.svg) Целый | Числовые значения категорий |

### Структура таблицы "Таблица замен"

| Метка                | Тип                              | Описание                                         |
|:---------------------|:---------------------------------|:-------------------------------------------------|
| Категория (Category) | ![](./img/string.svg) Строковый  | Список уникальных значений категорий             |
| Категория (замена)   | ![](./img/integer.svg) Целый     | Список уникальных номеров, присвоенных категориям|
