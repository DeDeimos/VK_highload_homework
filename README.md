# Расчетно-пояснительная записка

## Тема и целевая аудитория

В качестве типа сервиса для проектирования я выбрал маркетплейс **Яндекс Маркет**. Данный сервис отвечает требованиям к теме:

- **Имеет реальные аналоги**, доказывающие существование рыночной ниши — Ozon, Wildberries, Купер.
- **Аудитория сервиса** свыше 1 миллиона активных пользователей по данным [inclient.ru](https://inclient.ru/yandex-stats).
  
  | Яндекс Маркет           | Количество  |
  |-------------------------|-------------|
  | **Активные покупатели** | 18.2 млн    |
  | **Активные продавцы**   | 80.6 тысяч  |

- Наибольшим спросом **Яндекс Маркет** пользуется в России (94.48% интернет-трафика), Беларуси (0.97%), Узбекистане (0.74%) и Казахстане (0.73%).
- **Имеет сложную, нетривиальную архитектуру**.

## Функционал

Ключевой функционал для данного сервиса:

1. **Поиск и фильтрация товаров**
   - Система поиска использует **алгоритмы машинного обучения** для более точного подбора результатов на основе предпочтений пользователя. Это также включает умные фильтры, которые позволяют пользователям быстро находить подходящие товары.

2. **Система отзывов и рейтингов**
   - Интегрированная система отзывов с **верификацией подлинности** (например, отзывы только от пользователей, которые действительно купили товар) и **фильтры для сортировки отзывов** по полезности, дате или оценке.
  
3. **Рекомендации товаров в ленте**
   - **Рекомендации товаров в ленте** на основе пользовательских просмотров и ранее совершенных покупок. Это позволяет персонализиовать ленту товаров для пользователя и его удобства.

4. **Оформление заказа**
   - Возможность выбора из нескольких вариантов доставки (курьером, в пункт выдачи, постамат) и множества способов оплаты (банковские карты, электронные кошельки, наложенный платеж). Платформа также предлагает **расчёт стоимости доставки** и позволяет пользователям сохранять несколько адресов доставки.

5. **Сравнение товаров**
   - **Сравнение товаров** с выделением ключевых характеристик и различий, что помогает пользователям принять обоснованное решение.

6. **Управление учетной записью и заказами**
   - **Личный кабинет** с возможностью настройки профиля, просмотра истории покупок и отслеживания текущих заказов.

## Сокращение до MVP

Для создания MVP (минимально жизнеспособного продукта) Яндекс Маркета можно урезать функционал до следующих ключевых функций:

1. **Поиск и фильтрация товаров** (с базовыми фильтрами).
2. **Система отзывов и рейтингов** (с текстовыми отзывами и оценками).
3. **Рекомендации товаров в ленте**.
4. **Оформление заказа** (с одним способом доставки и оплаты).
5. **Сравнение товаров** (базовое сравнение двух товаров по ключевым характеристикам).
6. **Управление учетной записью и заказами** (с основными функциями).
## Расчет нагрузки
### Продуктовык метрики
- **MAU** - 30,66 млн (https://dzen.ru/a/ZkT8wKCKkBgtJMT-)
- **DAU** - 8,76 млн

Данные о товаре на Яндекс Маркете необходимые для его публикации (https://yandex.ru/support2/marketplace/ru/assortment/fields/)
  | Данные           | Размер (предполагаемый)  |
  |---------|-------------|
  | **SKU** | 0.51 КБ    |
  | **Название**   | 0.51 КБ |
  | **Изображения**   | 30*10 МБ  |
  | **Базовая цена**   | 0.0039 КБ |
  | **Фото 360**   | 72*10 МБ  |
  | **Видео**   | 3*60 МБ  |
  | **Описание**   | 12 КБ  |
  | **Категория товара**   | 0.2 КБ  |
  | **...**   | ...  |
  
Размеры в мегабайтах:
0.00051 + 0.00051 + 300 + 720 + 180 + 0.012 + 0.0002 = 1200.02321 МБ.

Округлим до 1200 МБ, потому как так еще остались возможные характеристики товаров, но по сравнению с размерами медиа-файлов их размел мал.
Таким образом, предполагаемый общий объем данных составляет около 1200 МБ, или 1.2 ГБ.*

>*Яндекс не храниит большие размеры медиа-файлов, а сжимает до нескольких копий для разного размера экрана:
>
> **Изображения:**
> | Размер изображения | Память                |
> |--------------------|-----------------------|
> | 190×250            | 0.14 МБ               |
> | 240×320            | 0.23 МБ               |
> | 300×400            | 0.36 МБ               |
> | 351×468            | 0.49 МБ               |
> | 402×536            | 0.65 МБ               |
> | 450×600            | 0.81 МБ               |
> | 501×668            | 1.00 МБ               |
> | 552×736            | 1.22 МБ               |
> | 600×800            | 1.44 МБ               |
> | **Всего сумма**    | **6.34 МБ**           |
>
>  **Видео:**
> | Тип данных         | Разрешение  | Память                |
> |--------------------|-------------|-----------------------|
> | Прелоад изображения | 600×800     | 1.44 МБ               |
> | Первоначальный кадр видео | 1080×1920 | 6.22 МБ               |
> | Стриминг видео (прогрессивный) | Зависит от сегментации и сети | Переменная (зависит от продолжительности и качества) |
> | **Всего (без учёта стрима)**  |             | **7.66 МБ + стрим**  |
>
> Таким образом размеры стоит пересчитать, взяв что в среднем на товар приходится 10 фотографий и 1 видео, а не 30 и 3 соответсвенно: 
> 0.00051 + 0.00051 + 10*6.4 + 24*6,4 + 60 + 0.012 + 0.0002 = 278 МБ.
>
> Это кажется не слишком сильно сократило размер хранения, но это сильно уменьшило размеры подгружаемых файлов файлов, потому загружается только фотография нужного формата для ленты, а видео там нет вообще. Возьмем среднее значение для изображений для ленты 402х556 - **0,65 МБ**


Основные действия по функционалу MVP:

  | Действие | Кол-во в день на одного пользователя в среднем  |
  |---------|-------------|
  | **Поиск и фильтрация товаров** | 4 |
  | **Система отзывов и рейтингов**   | 0.03 (1 в месяц) |
  | **Оформление заказа**   | 0.14 ( 1 в неделю )   |
  | **Сравнение товаров**   | 1 |
  | **Управление учетной записью и заказами**   | 0.14 ( 1 в неделю )  |
  
### Технические метрики

- **Хранилище**:  
  Количество товаров на Яндекс Маркете — **108 млн** ([Источник](https://yastatic.net/s3/ir-docs/docs/2024/q2/57a1cu049ffbd144aeged36d47h173c2/MKPAO_Press_Release_RUS_rs94k.pdf)).

  Посчитав до этого, сколько примерно нужно для хранения одного товара, получаем **3.1 петабайта** памяти.

- **Сетевой трафик**  
  Расчитаем трафик для активностей, выбранных в MVP:

  - **Поиск товаров (лента)**:  
    4 запроса/день, при которых загружаются 20 товаров с одной фотографией среднего размера (который мы выбрали до этого — **0.65 МБ**), названием (**0.51 КБ**) и ценой (**0.0039 КБ**).  
    Рассчитаем:  
    `4 * 20 * (665 + 0.51 + 0.0039) КБ = 52 МБ`

  - **Оставление отзыва**:  
    0.03 запроса/день. Средний размер отзыва — 3 текстовых поля по 200 символов и 3 фотографии 600×800, что в сумме составляет **4.32 МБ**.  
    Рассчитаем:  
    `0.03 * 4.32 МБ = 0.144 МБ`

  - **Оформление заказа**:  
    0.14 запроса/день. В среднем заказ включает 3–4 товара, возьмем 4. Размер одного товара:  
    `0.00051 КБ + 0.00051 КБ + 6.4 МБ + 0.012 КБ + 0.0002 КБ = 6.5 МБ`,  
    так как при загрузке не отображаются видео и Фото 360, а показывается 1 фотография.  
    Рассчитаем:  
    `0.14 * 4 * 6.5 МБ = 3.64 МБ`

  - **Сравнение товаров**:  
    1 запрос/день. Возьмем те же условия, что и в прошлом пункте, но товары для сравнения загружаются в количестве 2–3.  
    Рассчитаем:  
    `1 * 3 * 6.5 МБ = 19.5 МБ`

  **Итого сетевой трафик на одного пользователя в день**:  
  `52 + 0.144 + 3.64 + 19.5 = 72.2 МБ`
- **Сетевой трафик по видам активности (дневная аудитория 8.76 млн. пользователей):**

  Пиковое значение активности пользователей(соответственно RPS тоже) приблизительно в 1.66 раза выше среднего значения. Возьмем коэффициент запаса равный 2
  
  Тип                           | Отправка (дневная аудитория 8.76 млн) | Отправка Гб/сек | Пиковое значение | Значение с коэффициентом запаса 2 |
  -------------                 | ------------------------------------  |---------------- |----------------- |---------------------------------- |
  Поиск товаров                 | 8.76 млн * 52 МБ = 434 ТБ             | 5.14            | 8.53             | 10.28                            |
  Оставление отзывов            | 8.76 млн * 0.144 МБ = 1.2 ТБ          | 0.014           | 0.023            | 0.028                              |
  Оформление заказа             | 8.76 млн * 3.64 МБ = 30 ТБ            | 0.35            | 0.581            | 0.7                              |
  Сравнение товаров             | 8.76 млн * 19.5 МБ = 162 ТБ           | 1.92            | 3.19             | 3.84                             |
  Итого                         | 627,2 ТБ	                            | 7.424           | 12.32            | 14.85                              |
- **RPS**
 
  * Поиск товаров: 8.76 млн * 4 / 86400 = 387 RPS
  * Добавление товаров в корзину: 8.76 млн * 0.03 / 86400 = 2.9 RPS
  * Оформление заказов: 8.76 млн. * 0.14 / 86400 = 13.5 RPS
  * Оставление отзывов: 8.76 млн. * 1 / 86400 = 96.8 RPS
  
  Действие                            | RPS  | Пиковое значение | Пиковое значение с коэффициентом запаса 2  |
  ------------------------------------| ---  |----------------- |------------------------------------------- |
  Поиск товаров                       | 387  | 642              | 774                                        |
  Добавление товаров в корзину        | 2.9  | 4.8              | 5.8                                        |
  Оформление заказов                  | 13.5 | 22.4             | 27                                         |
  Оставление отзывов                  | 96.8 | 160.7            | 193.6                                      |
  **Итого**                           | 500.2| 830              | 1000                                       | 

## Глобальная балансировка нагрузки

### География пользователей

Целевая аудитория Яндекс Маркета распределена по странам СНГ, с преобладанием в России. Вот как распределяются пользователи по регионам:

Страна       | Процентное соотношение
-------------| ----------------------
Россия       | 84.8%
Азербайджан     | 3.1% 
Китай    | 1.4%
Казахстан       | 1.2% 

Это определяет необходимость расположения датацентров (ДЦ) преимущественно в России и других странах СНГ для обеспечения низкой задержки и высокой производительности.

### Функциональное разбиение по доменам

Для оптимизации работы и распределения нагрузки по различным функциональным модулям можно применить функциональное разбиение по доменам. Это позволяет отдельным частям системы работать независимо друг от друга, улучшая масштабируемость и отказоустойчивость.

Примеры функциональных доменов:

* market.yandex.ru — API-сервисы для мобильных приложений и веб-версии.
* mc.yandex.ru — доставка медиа-контента (фото товаров, видео, баннеры).

Такое разбиение позволяет улучшить управляемость трафика, распределять нагрузку на отдельные системы, а также внедрять более гибкие методы балансировки.

### Обоснование расположения ДЦ

На основе (https://telegra.ph/Gde-data-centry-YAndeksa-03-07), [склады](https://yandex.ru/maps/?from=mapframe&ll=52.821695%2C53.073344&mode=usermaps&source=mapframe&um=constructor%3Acbecbebc1953af83c4a0453d8ace4feb7dc239f35d3278858320e5e86909535d&utm_source=mapframe&z=5.86) и [ПВЗ](https://yandex.ru/maps/?ll=91.148707%2C60.336308&mode=search&sctx=ZAAAAAgBEAAaKAoSCZ5eKcsQz0JAEdOgaB7A4EtAEhIJA137Anqh8j8RmPxP%2Fu4d7D8iBgABAgMEBSgKOABA4QFIAWoCcnWdAc3MzD2gAQCoAQC9AUi2ORzCAZIBieaipIME2ezzwqcBr6TszPMDitXvyckD7LrwnZ4G7deH0pUD9cnavIIH9ru3oo4Dzv6nl58F7%2FSv2OsD686Zr%2B0CiZX99mOP8OCVsAWpo9PI3AbI%2Bd%2B6oALm0OywvgbN7P2ZqwWWkZnrVsyR1KM%2Fivnh2NgCyvae27UGscn6yKQBsfvy4fYEmLeSkzf6uu7YmQOCAkPQv9GD0L3QutGC0Ysg0LLRi9C00LDRh9C4INGP0L3QtNC10LrRgSDQvNCw0YDQutC10YIg0L3QsCDQutCw0YDRgtC1igIAkgIAmgIMZGVza3RvcC1tYXBzqgIZMTM5NzIyMjgxMTE5LDIzNzkyMzg3NjQ5NrACAQ%3D%3D&sll=91.148707%2C60.336308&sspn=124.433297%2C36.312187&text=пункты%20выдачи%20яндекс%20маркет%20на%20карте&z=4.22) можно обосновать расположение датацентров. Основная цель — снизить сетевые задержки и улучшить производительность для конечных пользователей.

Страна    | Локация ДЦ                | Обоснование
----------| --------------------------| ---------------------------------------------------------------------------
Россия    |	Москва и подмосковье	  | 95.7% пользователей из России, оптимизация для западной части страны и Европы
Россия    |	Калуга	 | Поддержка основных пользователей западной части России и Европы
Россия    |	Рязанская область	| Поддержка основных пользователей западной части России и Европы
Россия    |	Новосибирск	 | Покрытие для пользователей Центральной России, Урала, Сибири
Россия  |	Владимирская область | Поддержка основных пользователей западной части России и Европы
Китай   |	       -          | Поддержка пользователей из Китая и Казахстана
Финляндия   |	       -          | Поддержка пользователей из Европы (еропейской чатси Яндекса)

Основное внимание уделяется России, так как большинство пользователей находится в этой стране. Однако наличие датацентров в соседних странах (Китай, Казахстан) помогает улучшить доступ к сервису и уменьшить задержки для пользователей этих регионов.

### Расчет распределения запросов по типам

На основе данных о нагрузке и географии пользователей можно рассчитать распределение запросов по типам для каждого датацентра.

Тип запроса                  |	RPS (Запад России) |	RPS (Центр России) |	RPS (Китай)	| RPS (Казахстан) |	RPS (Финляндия)
-----------------------------| -------------------| -------------------|---------------| ----------------| -------------
Поиск товаров                |	580.4             |	116.1                          |	30.96          |	23.22          |	13.22
Добавление товаров в корзину |	4.35            |	0.86                          | 0.232          |	0.174	          | 0.185
Оформление заказов           |	10.12             |	2.02                           |	0.5           |	2.3            |	2.46
Оставление отзывов           |	72.6             |	14.52                          |	2.9          |	2.18           |	3.87
Итого                        |	667.51           |	133.87                       |	34.6         |	27.87          |	19.74

Общая нагрузка распределена пропорционально процентному соотношению пользователей в каждом регионе. Запад России несет наибольшую нагрузку, следом идут центральные регионы России.

### Схема DNS-балансировки

DNS-балансировка позволяет распределять трафик на уровне DNS-запросов, направляя пользователей к наиболее подходящему датацентру в зависимости от их географического местоположения.

Пример работы DNS-балансировки:
1. Пользователь из России отправляет запрос на market.yandex.ru.
2. DNS-сервер будет направлять пользователей на ближайший ДЦ с учетом их географического расположения. Для пользователей в центральной России и Сибири трафик будет перенаправляться в Новосибирск, а пользователи из западной части России будут обслуживаться в Москве и подмосковье.
3. Если российские датацентры перегружены, можно перенаправить запросы на ближайший доступный ДЦ, например, в Китай.

### Схема Anycast-балансировки

Anycast-балансировка позволяет направлять запросы к ближайшему датацентру с минимальной задержкой. Использование Anycast помогает автоматически балансировать нагрузку на основе топологии сети и состояния датацентров.

Пример Anycast-балансировки:
1. Пользователь отправляет запрос на market.yandex.ru.
2. Протокол Anycast направляет запрос в ближайший CDN-сервер (например, в Москве, если пользователь из России).
3. Если датацентр перегружен или недоступен, Anycast перенаправляет запрос к следующему ближайшему датацентру, например, в Китай.

### Механизм регулировки трафика между ДЦ

Для динамической балансировки нагрузки между датацентрами можно использовать такие механизмы, как:
1. GeoDNS — направляет пользователей в ближайший датацентр на основе географической локации.
2. Мониторинг нагрузки — автоматическая оценка текущей загрузки ДЦ и переключение на менее загруженные датацентры в случае перегрузки.
3. Технология GSLB (Global Server Load Balancing) — глобальное распределение запросов между датацентрами с учетом нагрузки, доступности и производительности каждого ДЦ.

