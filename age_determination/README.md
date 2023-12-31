# CV определение возраста покупателей

## Задача
Построить модель, которая по фотографии определит приблизительный возраст человека.

## Описание данных

В вашем распоряжении набор фотографий людей с указанием возраста.

* папка со всеми изображениями /final_files
* csv-файл labels.csv с двумя колонками: file_name и real_age

## Используемые библиотеки
*pandas, numpy, matplotlib, seaborn, tensorflow*

## Выводы:
### Анализ выборки: 
Выборка скошена в левую сторону - то есть чаще встречаются люди с возрастом 20-40. Медиана данной выборки 29 лет. Также, фото имеют различное качество и посторонние предметы - на лицах(очки, наушники, микрофон), которые могут усложнять определение возраста.

### Анализ модели: 
Обученная свёрточная нейронная сеть ResNet50 показала метрику качества 5.89, что соответствует целям исследования. Модель может ошибаться в предсказании на 5 лет. Что позволяет внедрить ее для:

* Анализа покупок и предложения товаров, которые могут заинтересовать покупателей определенной возрастной группы;
* Контроля добросовестности кассиров при продаже алкоголя.

Для улучшения качества метрики mae - уменьшили 'скорость обучения' - гиперпараметр в алгоритме Adam.

А также увеличено количество эпох до 19.

Модель работает на архитектуре ResNet50, адаптированной для данной задачи..

Как можно было бы улучишь качество: 
- Качество данных на входе: оценить еще раз возраст по фото.
- Анализ ошибок: к примеру модель сильно ошибается на сегменте пожилых людей, зато почти идеально работает с детьми. Тогда мы поймем, каких возрастов фото было бы хорошо добавить в выборку для дообучения.
- Посмотреть, каких возрастных групп представлено мало, чтобы их потом добавить в выборку.
- Так как имеются черно-булые фотографии и цветные - либо сделать все фото ч/б, либо добавить больше фото.
