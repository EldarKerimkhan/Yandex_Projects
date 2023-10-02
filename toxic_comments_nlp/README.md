# nlp классификация комментариев

## Задача
Построить модель для классификации комментариев на позитивные и негативные со значением метрики качества F1 не меньше 0.75.

## Описание данных

В распоряжении набор данных с разметкой о токсичности правок.

* text - содержит текст комментария
* toxic — целевой признак

## Используемые библиотеки
*pandas, numpy, matplotlib, seaborn, sklearn, tqdm, torch, transformers, nltk, re + нейронная сеть BERT** 

## Выводы:
В связи с тем, что вычисления объемные - удалось подобрать модель BERT (также была опробована AutoModelForSequenceClassification
и AutoModelForMaskedLM), количество сэмплов и батчей для обучения модели и дальнейшего предсказания.

| ML model | F1-train | F1-test|                          
| -------------------- |:-----:| -----:|
| LogisticRegression   | 0.90 |  NaN |
| LinearSVC            | 0.86 |  NaN |
| KNeighborsClassifier | 0.92 |  NaN |
| Dummy                |  NaN | 0.14 |

По данным предсказаниям токсичных комментариев лучше метрика f1 на тестовых данных получилось у KNeighborsClassifier и LogisticRegression.

Стоит отметить, что и LinearSVC показал результат выше требуемого (0,75).