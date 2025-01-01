# ✨ Integration

Описание взаимодействия между системой DOCR и внутренней системой учета работ



## Сценраий повдения системы 
1. Запрос на резервироывание ИД для передачи документов (с типом документов = 4)
2. Создание документов на количество ИД
3. Передача в ДОКР


## DOCR
1. Обновляет документ в системе и возвращает перечень 
2. Нужна защита от обновления других документов
3. Логирование операции генерации и обновления документов


## Structure documents

```json
[
   Document: ID
         [Materials]
         [Works]
]
```

Получение - резервирование документов по ИД с типом = 4

## Описание методов
|Point|Method|Description|
|-----|-------|-----------|
|GET  | api/order/productions/add/:ids      | Резервирование документов по ИД      |
|POST | api/order/productions/update        | Обновление документов по ИД          |
|GET  | api/order/productions/lastdocs/:ids | Получение последних документов по ИД |


Где ids - количество документов

## Документы 

| Поле             | Тип данных | JSON ключ           | Описание                                                          |
|------------------|------------|---------------------|------------------------------------------------------------------|
| Id               | int64      | `id`                | Id                                                              |
| Num              | string     | `num`               | Номер ордера                                                    |
| Typ              | int64      | `typ`               | Тип документа (0=подготовка, 1=проверка, 2=расход, 3=сверка)    |
| Tag              | string     | `tag`               | Тег для поиска                                                  |
| TypName          | string     | `typ_name`          | Наименование типа документа                                     |
| TypeId           | int64      | `type_id`           | Тип ID документа                                                |
| TdId             | int64      | `td_id`             | Id таможенной декларации                                        |
| TdNum            | string     | `td_num`            | Номер таможенной декларации                                     |
| Ttn              | string     | `ttn`               | Номер ТТН                                                      |
| TtnDate          | time.Time  | `ttn_date`          | Дата ТТН                                                       |
| Invoice          | string     | `invoice`           | Номер накладной от поставщика                                   |
| InvoiceDate      | time.Time  | `invoice_date`      | Дата накладной от поставщика                                    |
| CreatedAt        | time.Time  | `created_at`        | Дата операции                                                  |
| UpdatedAt        | time.Time  | `updated_at`        | Дата обновления                                                |
| ClosedAt         | time.Time  | `closed_at`         | Дата закрытия (после смены статуса "проведений")                |
| CompanyId        | int64      | `company_id`        | Id компании (контрагент)                                        |
| Company          | string     | `company`           | Название компании (контрагент)                                  |
| LocationId       | int64      | `location_id`       | Id локации                                                     |
| Location         | string     | `location`          | Название локации                                               |
| StockFrom        | int64      | `stock_from`        | Id склада отправителя                                          |
| StockFromName    | string     | `stock_from_name`   | Название склада отправителя                                    |
| StockId          | int64      | `stock_id`          | Id склада получателя                                           |
| Stock            | string     | `stock`             | Название склада получателя                                     |
| BoilerId         | int64      | `boiler_id`         | Id бойлера                                                     |
| BoilerName       | string     | `boiler_name`       | Название бойлера                                               |
| ProductId        | int64      | `product_id`        | Id продукта                                                    |
| ProductName      | string     | `product_name`      | Название продукта                                              |
| StatusId         | int64      | `status_id`         | Id статуса                                                     |
| Status           | string     | `status`            | Название статуса                                               |
| Account          | float64    | `account`           | Общая сумма счета                                              |
| Nds              | float64    | `nds`               | НДС                                                           |
| WithoutNds       | float64    | `without_nds`       | Сумма без НДС                                                  |
| Payment          | float64    | `payment`           | Сумма оплачено                                                 |
| Saldo            | float64    | `saldo`             | Остаток средств                                                |
| Qty              | float64    | `qty`               | Количество позиций в ордере                                    |
| Qt               | float64    | `qt`                | Количество после снятия по FIFO                                |
| Currency         | string     | `currency`          | Валюта                                                        |
| Weight           | float64    | `weight`            | Общий вес                                                     |
| WeightFact       | float64    | `weight_fact`       | Фактический вес                                               |
| Typeget          | int64      | `typeget`           | Тип документа для получения груза                             |
| Recipient        | string     | `recipient`         | Имя получателя                                                |
| RecipientId      | int64      | `recipient_id`      | Id получателя                                                 |
| RecipientTel     | string     | `recipient_tel`     | Телефон получателя                                            |
| DovNum           | string     | `dov_num`           | Номер доверенности                                            |
| DovDate          | string     | `dov_date`          | Дата доверенности                                             |
| ReqNum           | string     | `req_num`           | Номер заявки                                                  |
| ReqDate          | string     | `req_date`          | Дата заявки                                                   |
| Flag             | string     | `flag`              | Флаг                                                         |
| Uuid             | string     | `uuid`              | UUID                                                         |
| Contract         | string     | `contract`          | Номер контракта                                              |
| ContractId       | int64      | `contract_id`       | Id контракта                                                 |
| UserId           | int64      | `user_id`           | Id пользователя                                              |
| IsDeleted        | int64      | `is_deleted`        | Удален и обработке не подлежит                               |
| InStock          | int64      | `in_stock`          | Доставлен на склад                                           |
| Remark           | string     | `remark`            | Примечание                                                   |
| Comment          | string     | `comment`           | Комментарий для бухгалтерии                                  |
| Description      | string     | `description`       | Описание товара                                              |
| Note             | string     | `note`              | Примечание системное                                         |
| RawId            | int64      | `raw_id`            | Id сырья                                                     |
| RawName          | string     | `raw_name`          | Название сырья                                               |
| Items            | []OrderItems | N/A               | Продукты входящие в документ                                 |

## Материалы
| Поле           | Тип данных | JSON ключ        | Описание                                                     |
|----------------|------------|------------------|-------------------------------------------------------------|
| Id             | int64      | `id`             | Ид записи                                                   |
| OrderId        | int64      | `order_id`       | Ид связанного документа                                     |
| StockId        | int64      | `stock_id`       | Ид стока                                                    |
| Stock          | string     | `stock`          | Название стока                                              |
| MaterialId     | int64      | `material_id`    | Ид материала                                                |
| Material       | string     | `material`       | Название материала                                          |
| MaterialType   | int64      | `material_type`  | Тип материала: 1 - сырьё (деревина), 2 - товар (бензин и др.) |
| Qty            | float64    | `qty`            | Количество                                                 |
| Price          | float64    | `price`          | Цена                                                        |
| Summ           | float64    | `summ`           | Общая сумма                                                 |
| Ei             | string     | `ei`             | Единица измерения                                           |
| Status         | string     | `status`         | Статус: 1 - созданный, 3 - утверждённый                    |
| Stage          | int64      | `stage`          | Фаза готовности                                             |

## Работы

| Поле       | Тип данных | JSON ключ      | Описание                                                              |
|------------|------------|----------------|-----------------------------------------------------------------------|
| Id         | int64      | `id`           | Ид работ                                                             |
| OrderId    | int64      | `order_id`     | Ид документа                                                         |
| ProdId     | int64      | `prod_id`      | Ид продукта производства                                             |
| StockId    | int64      | `stock_id`     | Склад ИД                                                             |
| WorkId     | int64      | `work_id`      | Ид работы со справочника работ Works                                 |
| Title      | string     | `title`        | Наименование работ                                                   |
| HrsFact    | float64    | `hrs_fact`     | Часы: Fact - отработанные по данной работе (Общее)                   |
| HrsNorm    | float64    | `hrs_norm`     | Часы: Norm - плановые                                                |
| HrsDiff    | float64    | `hrs_diff`     | Часы: Diff - Разница                                                 |
| VolFact    | float64    | `vol_fact`     | Объем: Fact - выполненной работы                                     |
| VolNorm    | float64    | `vol_norm`     | Объем: Norm - плановые                                               |
| VolDiff    | float64    | `vol_diff`     | Объем: Diff - Разница                                                |
| MoneyFact  | float64    | `money_fact`   | Деньги: Fact - выполненной работы                                    |
| MoneyNorm  | float64    | `money_norm`   | Деньги: Norm - плановые                                              |
| MoneyDiff  | float64    | `money_diff`   | Деньги: Diff - Разница                                               |
| Koef       | float64    | `koef`         | Деньги: Koef - премиальные                                           |
| KoefWork   | float64    | `koef_work`    | Koef работы - Часовая тарифная ставка                                |
| RoleId     | int64      | `role_id`      | Роль ИД                                                              |
| RoleName   | string     | `role`         | Роль название                                                        |
| EmpId      | int64      | `emp_id`       | Ид сотрудника                                                        |
| Emp        | string     | `emp`          | Фамилия и имя сотрудника                                             |
| Ei         | string     | `ei`           | Единица измерения                                                    |
| Status     | string     | `status`       | Статус                                                               |
| Remark     | string     | `remark`       | Примечание                                                           |
