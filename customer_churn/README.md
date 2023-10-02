# Отток клиентов

## Задача
Спрогнозировать, уйдёт клиент из банка в ближайшее время или нет. Исследование 3х моеделей машинного обучения: LogisticRegression, DecisionTreeClassifier, RandomForestClassifier. Исследование разных методов борьбы с дисбалансом классов: upsampling, downsampling, внутринние механизмы моделей.

F1-мера должна быть не менее 0.6.

Источник данных: https://www.kaggle.com/barelydedicated/bank-customer-churn-modeling

## Описание данных

Признаки

* RowNumber — индекс строки в данных
* CustomerId — уникальный идентификатор клиента
* Surname — фамилия
* CreditScore — кредитный рейтинг
* Geography — страна проживания
* Gender — пол
* Age — возраст
* Tenure — сколько лет человек является клиентом банка
* Balance — баланс на счёте
* NumOfProducts — количество продуктов банка, используемых клиентом
* HasCrCard — наличие кредитной карты
* IsActiveMember — активность клиента
* EstimatedSalary — предполагаемая зарплата

Целевой признак
* Exited — факт ухода клиента

## Используемые библиотеки
*pandas, numpy, matplotlib, seaborn, sklearn*

## Выводы:
Проведена подготовка данных к исследованию:
* Числовые признаки масштабированы.
* Категориальные признаки преобразованы в численные методом One-Hot Encoding.
Целевой признак exited имеет явный дисбаланс: количество ушедших клиентов более чем в 3 раза меньше оставшихся клиентов.
Данные раздлены на 3 выборки: обучающую, валидационную и тестовую. В соотношении 3:1:1.

Рассмотрены 3 функции классификации. И ни одна из них не дала требуемое значение метрики f1.

| ML model | F1-score без учета дисбаланса | F1-score на сбалансированных данных сбалансированных данных|                          
| ---------------------- |:-----:| -----:|
| DecisionTreeClassifier | 0.558 | 0.617 |
| RandomForestClassifier | 0.532 | 0.621 |
| LogisticRegression     | 0.276 | 0.464 |

Для борьбы с дисбалансом использовали 3 метода:
* взвешивание классов;
* увеличение выборки объектов редкого класса;
* уменьшение выборки объектов частого класса;
*downsampling* сильнее всех просадил метрику. 

| ML model | classweight='balanced' | upsampling | downsampling |
| ---------------------- |:-----:| -----:| -----:|
| DecisionTreeClassifier | 0.578 | 0.605 | 0.549 |
| RandomForestClassifier | 0.621 | 0.602 | 0.601 |
| LogisticRegression     | 0.464 | 0.420 | 0.460 |

Сравнили модели логистической регрессии, дерева решений и случайного леса с настроиными гиперпараметрами и на сбалансированных данных. В данном проекте поиск гиперпараметров провел вручную (в цикле перебирая параметры).

На тесте лучший результат метрики f1-score 0.620 показала меодель RandomForestClassifier, AUC-ROC 0.861