# X5.RetailHero.ai Uplift Modelling
Решение для [ML соревнования по Uplift Modelling](https://retailhero.ai/c/uplift_modeling/overview)
## Public Leadboard: 0,0955
## Описание подхода
Всего фич: 139. Обычные фичи здорового человека:
  * Кол-во и сумма покупок, сгруппированные по часам и дням
  * Кол-во и сумма покупок до и после 1st redeem date
  * Суммы покупок, отмеченных флагами "алкоголь", "own trademark"
  * Кол-во покупок товаров дороже 500 руб, 1000 руб и т.д.
  * Отношение вышеперечисленных показателей к общей сумме и кол-ву покупок клиентов
  * Еще что-то по мелочи
  
Вначале проводится небольшой data cleansing возраста клиента.

Для построения моделей используется Catboost и LGBM. В данном случае Catboost показывает немного лучшие результаты.

Реализовано три варианта моделирования:
  * 2 независимые модели
  * Многоклассовая модель (4 модели для предсказания 4-х классов)
  * Модель с трансформацией классов

**Update:** вариант с 2 и 4 моделями остался в бранче 0.2. В основном бранче теперь только трансформация классов.

Про все эти подходы и многое другое есть две отличные статьи на Хабре: [здесь](https://habr.com/ru/company/ru_mts/blog/485980/) и [здесь](https://habr.com/ru/company/ru_mts/blog/485976/).
В данном случае **трансформация классов** показывает наилучший результат.

## Описание кода
Весь код в одном ноутбуке. Постарался сделать легко читаемым, иногда в ущерб краткости, возможно, и эффективности. В коде есть комментарии, можно будет легко разобраться.

Вначале выполняется генерирование фич, дальше можно запускать отдельные куски кода для разных моделей или изучения фич. Можно легко добавлять/менять фичи и смотреть, что меняется. Для новичков должно хорошо зайти.

## Как запускать
Скачать данные соревнования, распаковать в папку data\
Запустить ноутбук в jupyter.

## Результаты
Код запускался на Windows 10. 
Время генерации фич - около 15 минут. Время обучения одной модели - пара минут, но это с использованием GPU.

**Public score: 0,0955**, получен на catboost модели трансформации классов.
Перебор разных фич и параметров моделей очень слабо влияет на локальную кросс-валидацию, но может заметно изменить public score.

## Ссылки
Данный ноутбук использует код из [scikit-uplift module](https://github.com/maks-sh/scikit-uplift/) by Maksim Shevchenko


