# Прогнозирование продаж (Intermittent)

**Данные**
Имеются данные о продажах двух товарных номенклатур интернет-магазина. Каждая строчка в файле содержит дату и количество номенклатур, купленных в этот день. Лбе номенклатуры резко отличаются частотой реализиции.

**Задача:** Требуется найти модель, способную прогнозировать обе номенклатуры с приемлемой точностью на 30-40 дней вперёд. 

**Метрики:** Клиент оценивает качество прогнозирования по метрике buying score. Перезакуп buying score > 1 более вреден, чем недозакуп buying score < 1.  

Решение поставленной задачи выполнялось в три основных этапа:
1. Анализ исходных данных.
2. Анализ существующих методов решения. Поиск наиболее оптимального и эффективного
3. Выполнение поставленной задачи, используя выбранный метод.


## Этап 1. Анализ исходных данных

Первым этапом был проведен анализ исходных данных. В результате анализа было выявлено, что:
1. Исходные данные в таблице расположены не в хронологическом порядке. Было принято решение отсортировать исходный ряд в хронологическом порядке.
2. Некоторые даты в списке повторялись дважды (18 строк). При изучении повторяющихся данных можно было предположить два варианты:

     а) Это случайные дубликаты, которые необходимо удалтить;

     б) В данный день было сделано несколько продаж, но в разное время, а из-за возможной специфики БД эти продажи расположились на разных строках.

      В результате было принято решение опираться на вариант _б_. Поэтому была создана дополнительная функция. Данная функция автоматически проверяет набор данных и извлекает           
      дублирующиеся строки, затем суммирует их значения, и удалет лишиние данные. 
3. В представленных данных присутствуют относительно большие хронологические разрывы. Это говорит о том, что в пропущенные дни не было продаж сосвсем. Использование этих дополнительных вводных в значительной степени увеличивает точность работы исходной модели. Было принято решение добавить в набор данных пропущенные даты и присвоить значение продаж, равное нулю.

## Этап 2. Анализ методов
Для поиска оптимальной модели было проведено несколько экспериментов. Было проверено пять моделей, обычно применяемых при анализе временных рядов: Модель Хольта-Винтерса, Модель SARIMA, Модель fbProphet, модель нейронной сети LSTM и модель SimpleRNN. В результате анализ было выявлено, что наиболее эффективной моделью при решении данной задачи является модель нейронной сети SimpleRNN.

## Этап 3. Выполнение поставленной задачи

Для наглядности выполнения задачи был использован формат представления данных в виде .ipynb Jupyter ноутбука. Таким образом можно более наглядно продемонстрировать все этапы выполнения поставленной задачи. 

Первым этапом выполняется отчистка и подготовка данных
Вторым этапом выполняется предобработка данных с помощью метода масштабирования , включенного в стандартную библиотеку sklearn.preprocessing
Третьим этапом была разработана и обучена модель ИИ. Подбор числа слоев, видов слоев и гиперпараметров в основном выполнялся эмперическим путем на основе имеющегося опыта.
Четвертым этапом выполнялось тестирование разработанной модели на тестовом наборе данных, а так же на данных со второго артикула.

Результаты работы представлены в .ipynb Jupyter ноутбуке. 
