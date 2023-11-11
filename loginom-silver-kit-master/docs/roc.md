# ROC-анализ

[Назад к списку компонентов](../README.md)

## Назначение

Оценка качества модели оценки вероятности некоторого события и расчет различных метрик, принятых в ROC-анализе:

* расчет чувствительности, специфичности, и других показателей ROC-анализа для каждого значения порога отсечения, заданного с указанной точностью;
* расчет коэффициента KS (статистика Колмогорова-Смирнова);
* выбор порога отсечения с помощью различных методов.

## Входные порты

| Название             | Тип        |
|:---------------------|:-----------|
| Входной набор данных | Таблица    |
| Параметры алгоритма  | Переменные |

### Структура таблицы "Входной набор данных"

| Метка   | Тип                                    | Описание                                                               |
|:--------|:---------------------------------------|:-----------------------------------------------------------------------|
| Событие | ![](./img/logical.svg) Логический      | **true** — соответствует событию, **false** — соответствует не событию |
| Порог   | ![](./img/realnumber.svg) Вещественный | Значение вероятности события                                           |

### Переменные в порте "Параметры алгоритма"

| № | Метка                            | Тип                                    | Значение |
|:--|:---------------------------------|:---------------------------------------|:---------|
| 1 | Точность                         | ![](./img/integer.svg) Целый           |        4 |
| 2 | Уровень чувствительности         | ![](./img/realnumber.svg) Вещественный |       90 |
| 3 | Цена ошибки - ложноположительные | ![](./img/realnumber.svg) Вещественный |        1 |
| 4 | Цена ошибки - ложноотрицательные | ![](./img/realnumber.svg) Вещественный |        1 |
| 5 | Метод выбора порога отсечения    | ![](./img/string.svg) Строковый        |        3 |

1. **Точность** — количество знаков после запятой, до которого требуется округлить пороговое значение.

2. **Уровень чувствительности** — уровень чувтвительности для выбора порога отсечения по выбранному методу.

3. **Цена ошибки - ложноположительные**/**Цена ошибки - ложноотрицательные** — веса ошибок.

4.  **Метод выбора порога отчесения**:

* Заданная чувствительность;
* Чувствительность, равная проценту точности события;
* Максимальное значение KS;
* Минимум издержек ошибок классификации;
* Максимум точности события.

## Выходные порты

| Название              | Тип        |
|:----------------------|:-----------|
| Набор данных          | Таблица    |
| KS, %                 | Переменные |
| Порог отсечения       | Таблица    |

### Структура таблицы "Набор данных"

| Метка                                     | Тип                                    | Описание                                                                                 |
|:------------------------------------------|:---------------------------------------|:-----------------------------------------------------------------------------------------|
| Порог округлённый                         | ![](./img/realnumber.svg) Вещественный | Пороговое значение, округленное до заданной точности                                     |
| Истинноположительные случаи               | ![](./img/integer.svg) Целый           | Количество истинноположительных (TP)                                                     |
| Ложноположительные случаи                 | ![](./img/integer.svg) Целый           | Количество ложноположительных (FP)                                                       |
| Предсказанные положительные               | ![](./img/integer.svg) Целый           | TP+FP                                                                                    |
| Истинноотрицательные случаи               | ![](./img/integer.svg) Целый           | Количество истинноотрицательных (TN)                                                     |
| Ложноотрицательные случаи                 | ![](./img/integer.svg) Целый           | Количество ложноотрицательных (FN)                                                       |
| Предсказанные отрицательные               | ![](./img/integer.svg) Целый           | TN+FN                                                                                    |
| Чувствительность, %                       | ![](./img/realnumber.svg) Вещественный | ![\frac{TP}{(TP+FN)\cdot 100}](./img/7_roc.svg)                                          |
| Специфичность, %                          | ![](./img/realnumber.svg) Вещественный | ![\frac{TN}{(TN+FP)\cdot 100}](./img/8_roc.svg)                                          |
| (Процент событий) - (Процент не-событий)  | ![](./img/realnumber.svg) Вещественный | ![(\frac{TP}{(TP+FN)\cdot 100}  - \frac{FP}{(TN+FP)\cdot 100})\cdot 100](./img/9_roc.svg)|
| Изменение количества истинноположительных | ![](./img/integer.svg) Целый           | Разница между текущим и следующим значением TP                                           |
| Изменение количества ложноположительных   | ![](./img/integer.svg) Целый           | Разница между текущим и следующим значением FP                                           |
| % ошибок                                  | ![](./img/realnumber.svg) Вещественный | ![\frac{FP+FN}{(TP+FP+TN+FN)\cdot 100}](./img/10_roc.svg)                                |
| % ложноположительных                      | ![](./img/realnumber.svg) Вещественный | ![\frac{FP}{(TN+FP)\cdot 100}](./img/11_roc.svg)                                         |
| % ложноотрицательных                      | ![](./img/realnumber.svg) Вещественный | ![\frac{FN}{(TP+FN)\cdot 100}](./img/12_roc.svg)                                         |
| Издержки классификации                    | ![](./img/realnumber.svg) Вещественный | Ошибки, взвешенные через их цену                                                         |
| % точности классификации                  | ![](./img/realnumber.svg) Вещественный | ![\frac{TP+TN}{(TP+TN+FP+FN)\cdot 100}](./img/13_roc.svg)                                |
| % точности события                        | ![](./img/realnumber.svg) Вещественный | ![\frac{TP}{(TP+FP)\cdot 100}](./img/14_roc.svg)                                         |
| % точности не-события                     | ![](./img/realnumber.svg) Вещественный | ![\frac{TN}{(TN+FN)\cdot 100}](./img/15_roc.svg)                                         |

### Переменные в порте "KS, %"

| № | Метка | Тип                                    | Описание                                  |
|:--|:----- |:---------------------------------------|:------------------------------------------|
| 1 | KS, % | ![](./img/realnumber.svg) Вещественный | Значение статистики Колмогорова-Смирнова  |

### Структура таблицы "Порог отсечения"

| Метка                                     | Тип                                    | Описание                 |
|:------------------------------------------|:---------------------------------------|:--------------------------------------|
| Метод выбора порога                       | ![](./img/string.svg) Строковый        | Наименование метода                                         |
| Порог округлённый                         | ![](./img/realnumber.svg) Вещественный | Выбранное значение порога отсечения, округленное до заданной точности         |
| Истинноположительные случаи               | ![](./img/integer.svg) Целый           | Количество истинноположительных (TP)                             |
| Ложноположительные случаи                 | ![](./img/integer.svg) Целый           | Количество ложноположительных (FP)                                    |
| Предсказанные положительные               | ![](./img/integer.svg) Целый           | TP+FP                                                                 |
| Истинноотрицательные случаи               | ![](./img/integer.svg) Целый           | Количество истинноотрицательных (TN)                   |
| Ложноотрицательные случаи                 | ![](./img/integer.svg) Целый           | Количество ложноотрицительных (FN)                      |
| Предсказанные отрицательные               | ![](./img/integer.svg) Целый           | TN+FN                                                           |
| Чувствительность, %                       | ![](./img/realnumber.svg) Вещественный | ![\frac{TP}{(TP+FN)\cdot 100}](./img/7_roc.svg)       |
| Специфичность, %                          | ![](./img/realnumber.svg) Вещественный | ![\frac{TN}{(TN+FP)\cdot 100}](./img/8_roc.svg)           |
| (Процент событий) - (Процент не-событий)  | ![](./img/realnumber.svg) Вещественный | ![(\frac{TP}{(TP+FN)\cdot 100}  - \frac{FP}{(TN+FP)\cdot 100})\cdot 100](./img/9_roc.svg)|
| Изменение количества истинноположительных | ![](./img/integer.svg) Целый           | Разница между текущим и следующим значением TP          |
| Изменение количества ложноположительных   | ![](./img/integer.svg) Целый           | Разница между текущим и следующим значением FP               |
| % ошибок                                  | ![](./img/realnumber.svg) Вещественный | ![\frac{FP+FN}{(TP+FP+TN+FN)\cdot 100}](./img/10_roc.svg)              |
| % ложноположительных                      | ![](./img/realnumber.svg) Вещественный | ![\frac{FP}{(TN+FP)\cdot 100}](./img/11_roc.svg)               |
| % ложноотрицательных                      | ![](./img/realnumber.svg) Вещественный | ![\frac{FN}{(TP+FN)\cdot 100}](./img/12_roc.svg)                   |
| Издержки классификации                    | ![](./img/realnumber.svg) Вещественный | Ошибки, взвешенные через их цену                                 |
| % точности классификации                  | ![](./img/realnumber.svg) Вещественный | ![\frac{TP+TN}{(TP+TN+FP+FN)\cdot 100}](./img/13_roc.svg)              |
| % точности события                         | ![](./img/realnumber.svg) Вещественный | ![\frac{TP}{(TP+FP)\cdot 100}](./img/14_roc.svg)                        |
| % точности не-события                      | ![](./img/realnumber.svg) Вещественный | ![\frac{TN}{(TN+FN)\cdot 100}](./img/15_roc.svg)                   |

## Алгоритмы

Псевдокоды алгоритма ROC-анализа доступны в статье по [ссылке](http://web.ydu.edu.tw/~alan9956/docu/refer/roc_introduction.pdf).

## Дополнительная литература

1. [ROC-кривая - материал из Wikipedia (рус.)](https://ru.wikipedia.org/wiki/ROC-%D0%BA%D1%80%D0%B8%D0%B2%D0%B0%D1%8F)
2. [ROC-анализ - материал из Wikipedia (англ.)](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)
3. [Bradley, A. The use of the area under the ROC curve in the evaluation of machine learning algorithms](https://www.cse.ust.hk/nevinZhangGroup/readings/yi/Bradley_PR97.pdf) — статья в журнале Pattern Recognition, июль 1997.