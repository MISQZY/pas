# Тривиальная модель

[Назад к списку компонентов](../README.md)

## Назначение

Построение тривиальной (base) модели, оценивающей вероятность наступления события на одном входном факторе (непрерывного вида, целого или вещественного типа).
Используется логистическая регрессия с предварительной процедурой оптимального квантования.
Модели автоматически переобучаются.

## Входные порты

| Название              | Тип        |
|:----------------------|:-----------|
| Обучающая выборка     | Таблица    |
| Тестовая выборка      | Таблица    |

### Структура таблиц "Обучающая выборка", "Тестовая выборка"

| Метка                   | Тип                                    | Описание                          |
|:------------------------|:---------------------------------------|:----------------------------------|
| Идентификатор           | ![](./img/string.svg) Строковый        | Идентификатор объекта             |
| Тривиальный показатель  | ![](./img/realnumber.svg) Вещественный | Поле с тривиальным показателем    |
| Событие                 | ![](./img/logical.svg) Логический      | Поле с событием                   |


1. Поле с тривиальным показателем должно быть непрерывного вида, вещественного или целого типа.
2. Тривиальное поле для тестовой и обучающей выборок должно совпадать, но этот контроль лежит на пользователе компонента.
3. Событие содержит два уникальных значения логического типа. `True` соответствует наступлению события.

## Выходные порты

| Название              | Тип        |
|:----------------------|:-----------|
| Вероятности событий   | Таблица    |
| Метрики качества      | Переменные |

### Структура таблицы "Вероятности событий"

| Метка                   | Тип                                    | Описание                          |
|:------------------------|:---------------------------------------|:----------------------------------|
| Идентификатор           | ![](./img/string.svg) Строковый        | Идентификатор объекта             |
| Вероятность события     | ![](./img/realnumber.svg) Вещественный | Поле с тривиальным показателем    |

Объекты отсортированы в порядке убывания вероятности события.

### Переменные в порте "Метрики качества"

 № | Метка                          | Тип                                    | Описание                                               |
|:--|:-------------------------------|:---------------------------------------|:-------------------------------------------------------|
| 1 | Индекс AUC                     | ![](./img/realnumber.svg) Вещественный | Расчитанное значение индекса AUC для модели            |
| 2 | Качество                       | ![](./img/string.svg) Строковый        | Словесное описание качества модели (см. **Алгоритмы**) |
| 3 | Стандартная ошибка             | ![](./img/realnumber.svg) Вещественный | Стандартное отклонение по набору                       |
| 4 | Доверительный интервал нижний  | ![](./img/realnumber.svg) Вещественный | Нижняя граница доверительного интервала                |
| 5 | Доверительный интервал верхний | ![](./img/realnumber.svg) Вещественный | Верхняя граница доверительного интервала               |
| 6 | Z-оценка                       | ![](./img/realnumber.svg) Вещественный | Расчитанное значение Z-оценки                          |

Переменные выходного порта соответствуют компоненту [AUC](./docs/auc.md) и рассчитываются для тестовой выборки.
Диаграммы ROC-кривых для тестовой и обучающей выборок можно увидеть, зайтя внутрь компонента.