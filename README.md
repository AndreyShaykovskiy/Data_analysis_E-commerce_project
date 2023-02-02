### Дана некоторая платформа онлайн продаж, с которой выгружены следующие данные:
* уникальные идентификаторы пользователей
* заказы
* товарные позиции, входящие в заказы
### Необходимо проанализировать данные и ответить на следующие вопросы:
1. Сколько пользователей, которые совершили покупку только один раз?
2. Сколько заказов в месяц в среднем не доставляется по разным причинам (вывести детализацию по причинам)?
3. По каждому товару определить, в какой день недели товар чаще всего покупается.
4. Сколько у каждого из пользователей в среднем покупок в неделю (по месяцам)?

### 1
![2023-02-02_16-54-50](https://user-images.githubusercontent.com/122619433/216343851-bdfdc138-42d5-4687-b104-ffc100c8aee4.png)

### 2 
находим сколько в среднем недоставленных заказов
![2023-02-02_16-47-27](https://user-images.githubusercontent.com/122619433/216342440-ab523ee4-68ba-40f9-8e10-309cd6b6ea0f.png)

Классифицируем причины на основании данных в столбцах: order_status(статус заказа) order_approved_at(время подтверждения оплаты заказа) order_delivered_carrier_date( время передачи заказа в логистическую службу) order_delivered_customer_date(время доставки заказа) order_id(уникальный идентификатор заказа)
Проанализируем полученные данные: рассмотрим статусы: approved, invoiced, processing-все заказы были оплачены, но продавец не доставил товар в логистическую службу и тем самым заказ был недоставлен покупателю. Объеденим данные статусы под одну причину"заказ не отправлен продавцом" shipped объединим с 8ю заказами delivered, у которых нет данных по дате доставки, в группу - "логист.служба не отправила заказ покупателю". Так как данные заказы были доставлены в логист.службу, но она не отправила заказ покупателю. unavailable - товар не доступен, когда товара нет в наличии. Также данный статус можно охарактеризовать как системный сбой так как его успели заказать и оплатить(было наличие товара на сайте). created- заказ не был оплачен покупателем. canceled - заказ отменен на разных стадиях.
![2023-02-02_16-48-01](https://user-images.githubusercontent.com/122619433/216342775-d9a16a1f-95d8-4bd2-9cbe-1f29001be808.png)

#### Вывод: 
компании стоит рассмотреть другие логистические службы для доставки заказа покупателю, так большая часть заказов в месяц в среднем не доставляется по их причине. Необходимо пересмотреть внутреннюю организацию обработки, доставки заказов в логистическую службу, а также следить за актуальностью информации в интернет магазине

### 3
Для того чтобы по каждому товару определить в какой день недели товар чаще всего покупается, необходимо найти максимальные значения по "product_id" в столбце "purchases" и при этом не потерять значения столбца "day_of_week" Посчитаем отдельно максимальные значения "max_purchase" для каждого "product_id" по столбцу "purchases" Далее полученные данные мы добавим в основной датафрейм "purchases_of_day" и посчитаем разницу между столбцами(difference) max и purchases. Нулевые значения в столбце difference и будут максимальными значениями покупок по дням недели(max.знач - max.знач дает нам 0)
![2023-02-02_16-53-03](https://user-images.githubusercontent.com/122619433/216343465-0eee2c68-872c-4ff4-8e90-a8bcca5010c1.png)
