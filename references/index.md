# Yandex Market Partner API — индекс категорий

Источник: официальный репозиторий `github.com/yandex-market/yandex-market-partner-api`. Полный спек: [yandex-market-openapi.json](./yandex-market-openapi.json) (~1.3 МБ, 149 путей / 159 операций).

**Не читай OpenAPI целиком.** Используй `scripts/lookup_endpoint.py` (`tags`/`search`/`show`).

В квадратных скобках — модели размещения, к которым применим метод (fbs/fby/dbs/express; laas — отдельная логистика). Пусто = применим везде или модель неважна.

Категории отсортированы по числу эндпоинтов.

## reports (26)

- `POST   /v1/businesses/{businessId}/reports/marketing-detalization/generate` — Отчет по счету маркетинга [fby,dbs,fbs,express,laas]
- `POST   /v1/reports/documents/barcodes/generate` — Получение файла со штрихкодами [fby,laas]
- `POST   /v2/reports/banners-statistics/generate` — Отчет по охватному продвижению [fby,fbs,dbs,express]
- `POST   /v2/reports/boost-consolidated/generate` — Отчет по бусту продаж [fby,fbs,dbs,express]
- `POST   /v2/reports/closure-documents/detalization/generate` — Отчет по схождению с закрывающими документами [fby,dbs,fbs,express,laas]
- `POST   /v2/reports/closure-documents/generate` — Закрывающие документы [fby,dbs,fbs,express,laas]
- `POST   /v2/reports/competitors-position/generate` — Отчет «Конкурентная позиция» [fby,dbs,fbs,express]
- `POST   /v2/reports/documents/labels/generate` — Готовые ярлыки‑наклейки на все коробки в нескольких заказах [fbs,dbs,express]
- `POST   /v2/reports/documents/shipment-list/generate` — Получение листа сборки [fbs]
- `POST   /v2/reports/goods-feedback/generate` — Отчет по отзывам о товарах [fby,fbs,dbs,express]
- `POST   /v2/reports/goods-movement/generate` — Отчет по движению товаров [fby,laas]
- `POST   /v2/reports/goods-prices/generate` — Отчет «Цены» [fby,fbs,dbs,express]
- `POST   /v2/reports/goods-realization/generate` — Отчет по реализации [fby,fbs,express,dbs]
- `POST   /v2/reports/goods-turnover/generate` — Отчет по оборачиваемости [fby]
- `GET    /v2/reports/info/{reportId}` — Получение заданного отчета или документа [fby,dbs,fbs,express,laas]
- `POST   /v2/reports/jewelry-fiscal/generate` — Отчет по заказам с ювелирными изделиями [fby,fbs,dbs,express]
- `POST   /v2/reports/key-indicators/generate` — Отчет по ключевым показателям [fby,fbs,dbs,express]
- `POST   /v2/reports/sales-geography/generate` — Отчет по географии продаж [fby,fbs,dbs,express]
- `POST   /v2/reports/shelf-statistics/generate` — Отчет по полкам [fby,fbs,dbs,express]
- `POST   /v2/reports/shows-boost/generate` — Отчет по бусту показов [fby,fbs,dbs,express]
- `POST   /v2/reports/shows-sales/generate` — Отчет «Аналитика продаж» [fby,dbs,fbs,express]
- `POST   /v2/reports/stocks-on-warehouses/generate` — Отчет по остаткам на складах [fby,fbs,dbs,express,laas]
- `POST   /v2/reports/united-marketplace-services/generate` — Отчет по стоимости услуг [fby,dbs,fbs,express,laas]
- `POST   /v2/reports/united-netting/generate` — Отчет по платежам [fby,dbs,fbs,express]
- `POST   /v2/reports/united-orders/generate` — Отчет по заказам [fby,fbs,dbs,express]
- `POST   /v2/reports/united-returns/generate` — Отчет по невыкупам и возвратам [fby,fbs,dbs,express,laas]

## orders (16)

- `POST   /v1/businesses/{businessId}/orders` — Информация о заказах в кабинете [fbs,dbs,fby,express,laas]
- `POST   /v1/campaigns/{campaignId}/orders/create` — Создание заказа [laas]
- `POST   /v1/campaigns/{campaignId}/orders/update` — Изменение заказа [laas]
- `POST   /v1/campaigns/{campaignId}/orders/update-options` — Получение временных интервалов для изменения заказа [laas]
- `GET    /v2/campaigns/{campaignId}/orders` — Информация о заказах в магазине [fbs,dbs,fby,express,laas] ⚠️ deprecated
- `POST   /v2/campaigns/{campaignId}/orders/status-update` — Изменение статусов нескольких заказов [fbs,dbs,laas,express]
- `GET    /v2/campaigns/{campaignId}/orders/{orderId}` — Информация об одном заказе в магазине [fby,fbs,dbs,express,laas] ⚠️ deprecated
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/boxes` — Подготовка заказа [fbs,express,dbs]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/cancellation/accept` — Отмена заказа покупателем [dbs]
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/deliverDigitalGoods` — Передача ключей цифровых товаров [dbs]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/delivery/shipments/{shipmentId}/boxes` — Передача количества грузовых мест в заказе [dbs] ⚠️ deprecated
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/external-id` — Передача внешнего идентификатора заказа [fbs,dbs,express]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/identifiers` — Передача кодов маркировки единиц товара [dbs]
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/identifiers/status` — Статусы проверки кодов маркировки [fbs,express,laas]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/items` — Удаление товаров из заказа или уменьшение их числа [dbs]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/status` — Изменение статуса одного заказа [fbs,dbs,laas,express]

## shipments (12)

- `PUT    /v2/campaigns/{campaignId}/first-mile/shipments` — Получение информации о нескольких отгрузках [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}` — Получение информации об одной отгрузке [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/act` — Получение акта приема-передачи [fbs]
- `POST   /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/confirm` — Подтверждение отгрузки [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/discrepancy-act` — Получение акта расхождений [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/inbound-act` — Получение фактического акта приема-передачи [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/orders/info` — Получение информации о возможности печати ярлыков [fbs]
- `POST   /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/orders/transfer` — Перенос заказов в следующую отгрузку [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/pallet/labels` — Ярлыки для доверительной приемки [fbs]
- `PUT    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/pallets` — Передача количества упаковок для доверительной приемки [fbs]
- `GET    /v2/campaigns/{campaignId}/first-mile/shipments/{shipmentId}/transportation-waybill` — Получение транспортной накладной [fbs]
- `GET    /v2/campaigns/{campaignId}/shipments/reception-transfer-act` — Подтверждение ближайшей отгрузки и получение акта приема-передачи для нее [fbs]

## returns (9)

- `POST   /v1/businesses/{businessId}/returns/decisions` — Получение возможных решений по возврату [dbs,fbs,express,fby]
- `POST   /v1/campaigns/{campaignId}/returns/cancel` — Отмена возврата [laas]
- `POST   /v1/campaigns/{campaignId}/returns/create` — Создание возврата [laas]
- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/returns/{returnId}` — Информация о невыкупе или возврате [fbs,dbs,express,fby,laas]
- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/returns/{returnId}/application` — Получение заявления на возврат [fbs,fby,dbs,express]
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/returns/{returnId}/decision` — Принятие или изменение решения по возврату [dbs] ⚠️ deprecated
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/returns/{returnId}/decision/submit` — Передача решения по возврату [dbs,fbs,express,fby]
- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/returns/{returnId}/decision/{itemId}/image/{imageHash}` — Получение фотографий товаров в возврате [fbs,dbs,express,fby]
- `GET    /v2/campaigns/{campaignId}/returns` — Список невыкупов и возвратов [fbs,dbs,express,fby,laas]

## chats (7)

- `GET    /v2/businesses/{businessId}/chat` — Получение чата по идентификатору [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/chats` — Получение доступных чатов [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/chats/file/send` — Отправка файла в чат [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/chats/history` — Получение истории сообщений в чате [dbs,fbs,fby,express]
- `GET    /v2/businesses/{businessId}/chats/message` — Получение сообщения в чате [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/chats/message` — Отправка сообщения в чат [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/chats/new` — Создание нового чата с покупателем [dbs,fbs,fby,express]

## business-offer-mappings (6)

- `POST   /v1/businesses/{businessId}/offer-mappings/barcodes/generate` — Генерация штрихкодов [dbs,fby,fbs,express,laas]
- `POST   /v2/businesses/{businessId}/offer-mappings` — Информация о товарах в каталоге [dbs,fby,fbs,express,laas]
- `POST   /v2/businesses/{businessId}/offer-mappings/archive` — Добавление товаров в архив [dbs,fby,fbs,express]
- `POST   /v2/businesses/{businessId}/offer-mappings/delete` — Удаление товаров из каталога [dbs,fby,fbs,express,laas]
- `POST   /v2/businesses/{businessId}/offer-mappings/unarchive` — Удаление товаров из архива [dbs,fby,fbs,express]
- `POST   /v2/businesses/{businessId}/offer-mappings/update` — Добавление товаров в каталог и изменение информации о них [dbs,fby,fbs,express,laas]

## goods-feedback (5)

- `POST   /v2/businesses/{businessId}/goods-feedback` — Получение отзывов о товарах продавца [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/goods-feedback/comments` — Получение комментариев к отзыву [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/goods-feedback/comments/delete` — Удаление комментария к отзыву [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/goods-feedback/comments/update` — Добавление нового или изменение созданного комментария [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/goods-feedback/skip-reaction` — Пропуск реакции на отзывы [fby,fbs,dbs,express]

## order-delivery (5)

- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/buyer` — Информация о покупателе — физическом лице [dbs]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/delivery/date` — Изменение даты доставки заказа [dbs]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/delivery/storage-limit` — Продление срока хранения заказа [dbs]
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/delivery/track` — Передача трек‑номера посылки [dbs]
- `PUT    /v2/campaigns/{campaignId}/orders/{orderId}/verifyEac` — Передача кода подтверждения [express]

## outlets (5)

- `GET    /v2/campaigns/{campaignId}/outlets` — Информация о нескольких точках продаж [dbs]
- `POST   /v2/campaigns/{campaignId}/outlets` — Создание точки продаж [dbs]
- `DELETE /v2/campaigns/{campaignId}/outlets/{outletId}` — Удаление точки продаж [dbs]
- `GET    /v2/campaigns/{campaignId}/outlets/{outletId}` — Информация об одной точке продаж [dbs]
- `PUT    /v2/campaigns/{campaignId}/outlets/{outletId}` — Изменение информации о точке продаж [dbs]

## prices (5)

- `POST   /v2/businesses/{businessId}/offer-prices` — Просмотр цен на указанные товары во всех магазинах [fby,fbs,dbs,express,laas]
- `POST   /v2/businesses/{businessId}/offer-prices/updates` — Установка цен на товары для всех магазинов [fby,fbs,dbs,express,laas]
- `GET    /v2/campaigns/{campaignId}/offer-prices` — Список цен [fby,fbs,dbs,express] ⚠️ deprecated
- `POST   /v2/campaigns/{campaignId}/offer-prices` — Просмотр цен на указанные товары в конкретном магазине [fby,fbs,dbs,express,laas]
- `POST   /v2/campaigns/{campaignId}/offer-prices/updates` — Установка цен на товары в конкретном магазине [fby,fbs,dbs,express,laas]

## bids (4)

- `PUT    /v2/businesses/{businessId}/bids` — Включение буста продаж и установка ставок [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/bids/info` — Информация об установленных ставках [dbs,fbs,fby,express]
- `POST   /v2/businesses/{businessId}/bids/recommendations` — Рекомендованные ставки для заданных товаров [dbs,fbs,fby,express]
- `PUT    /v2/campaigns/{campaignId}/bids` — Включение буста продаж и установка ставок для магазина [dbs,fbs,express,fby]

## offers (4)

- `POST   /v2/businesses/{businessId}/offers/recommendations` — Рекомендации Маркета, касающиеся цен [dbs,fby,fbs,express]
- `POST   /v2/campaigns/{campaignId}/offers` — Информация о товарах, которые размещены в заданном магазине [dbs,fby,fbs,express,laas]
- `POST   /v2/campaigns/{campaignId}/offers/delete` — Удаление товаров из ассортимента магазина [dbs,fby,fbs,express,laas]
- `POST   /v2/campaigns/{campaignId}/offers/update` — Изменение условий продажи товаров в магазине [dbs,fby,fbs,express,laas]

## price-quarantine (4)

- `POST   /v2/businesses/{businessId}/price-quarantine` — Список товаров, находящихся в карантине по цене в кабинете [dbs,fby,fbs,express]
- `POST   /v2/businesses/{businessId}/price-quarantine/confirm` — Удаление товара из карантина по цене в кабинете [dbs,fby,fbs,express]
- `POST   /v2/campaigns/{campaignId}/price-quarantine` — Список товаров, находящихся в карантине по цене в магазине [dbs,fby,fbs,express]
- `POST   /v2/campaigns/{campaignId}/price-quarantine/confirm` — Удаление товара из карантина по цене в магазине [dbs,fby,fbs,express]

## promos (4)

- `POST   /v2/businesses/{businessId}/promos` — Получение списка акций [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/promos/offers` — Получение списка товаров, которые участвуют или могут участвовать в акции [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/promos/offers/delete` — Удаление товаров из акции [fby,fbs,dbs,express]
- `POST   /v2/businesses/{businessId}/promos/offers/update` — Добавление товаров в акцию или изменение их цен [fby,fbs,dbs,express]

## regions (4)

- `GET    /v2/regions` — Поиск регионов по их имени [fby,fbs,dbs,express,laas]
- `POST   /v2/regions/countries` — Список допустимых кодов стран [fby,fbs,dbs,express,laas]
- `GET    /v2/regions/{regionId}` — Информация о регионе [fby,fbs,dbs,express,laas]
- `GET    /v2/regions/{regionId}/children` — Информация о дочерних регионах [fby,fbs,dbs,express,laas]

## warehouses (4)

- `GET    /v2/businesses/{businessId}/warehouses` — Список складов и групп складов [fbs,dbs,express] ⚠️ deprecated
- `POST   /v2/businesses/{businessId}/warehouses` — Список складов [fbs,dbs,express]
- `POST   /v2/campaigns/{campaignId}/warehouse/status` — Изменение статуса склада [fbs,dbs,express]
- `GET    /v2/warehouses` — Идентификаторы фулфилмент-складов Маркета [fby,laas]

## campaigns (3)

- `GET    /v2/campaigns` — Список магазинов пользователя [dbs,express,fbs,fby,laas]
- `GET    /v2/campaigns/{campaignId}` — Информация о магазине [dbs,express,fbs,fby,laas]
- `GET    /v2/campaigns/{campaignId}/settings` — Настройки магазина [dbs,fbs,express,fby,laas]

## content (3)

- `POST   /v2/businesses/{businessId}/offer-cards` — Получение информации о заполненности карточек магазина [dbs,fby,fbs,express,laas]
- `POST   /v2/businesses/{businessId}/offer-cards/update` — Редактирование категорийных характеристик товара [dbs,fby,fbs,express,laas]
- `POST   /v2/category/{categoryId}/parameters` — Списки характеристик товаров по категориям [dbs,fby,fbs,express,laas]

## goods-questions (3)

- `POST   /v1/businesses/{businessId}/goods-questions` — Получение вопросов о товарах продавца [fby,fbs,dbs,express]
- `POST   /v1/businesses/{businessId}/goods-questions/answers` — Получение ответов на вопрос [fby,fbs,dbs,express]
- `POST   /v1/businesses/{businessId}/goods-questions/update` — Создание, изменение и удаление ответа или комментария [fby,fbs,dbs,express]

## hidden-offers (3)

- `GET    /v2/campaigns/{campaignId}/hidden-offers` — Информация о скрытых вами товарах [fby,fbs,dbs,express]
- `POST   /v2/campaigns/{campaignId}/hidden-offers` — Скрытие товаров и настройки скрытия [fby,fbs,dbs,express]
- `POST   /v2/campaigns/{campaignId}/hidden-offers/delete` — Возобновление показа товаров [fby,fbs,dbs,express]

## order-labels (3)

- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/delivery/labels` — Готовые ярлыки‑наклейки на все коробки в одном заказе [fbs,dbs,express]
- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/delivery/labels/data` — Данные для самостоятельного изготовления ярлыков [fbs,dbs,express]
- `GET    /v2/campaigns/{campaignId}/orders/{orderId}/delivery/shipments/{shipmentId}/boxes/{boxId}/label` — Готовый ярлык‑наклейка для коробки в заказе [fbs,dbs,express]

## outlet-licenses (3)

- `DELETE /v2/campaigns/{campaignId}/outlets/licenses` — Удаление лицензий для точек продаж [dbs]
- `GET    /v2/campaigns/{campaignId}/outlets/licenses` — Информация о лицензиях для точек продаж [dbs]
- `POST   /v2/campaigns/{campaignId}/outlets/licenses` — Создание и изменение лицензий для точек продаж [dbs]

## supply-requests (3)

- `POST   /v2/campaigns/{campaignId}/supply-requests` — Получение информации о заявках на поставку, вывоз и утилизацию [fby,laas]
- `POST   /v2/campaigns/{campaignId}/supply-requests/documents` — Получение документов по заявке на поставку, вывоз или утилизацию [fby,laas]
- `POST   /v2/campaigns/{campaignId}/supply-requests/items` — Получение товаров в заявке на поставку, вывоз или утилизацию [fby,laas]

## categories (2)

- `POST   /v2/categories/max-sale-quantum` — Лимит на установку кванта продажи и минимального количества товаров в заказе [fby,fbs,dbs,express] ⚠️ deprecated
- `POST   /v2/categories/tree` — Дерево категорий [fby,fbs,dbs,express,laas]

## delivery-options (2)

- `POST   /v1/campaigns/{campaignId}/delivery-options` — Получение доступных вариантов доставки заказов [laas]
- `POST   /v1/campaigns/{campaignId}/return-delivery-options` — Получение подходящих для возврата пунктов выдачи [laas]

## order-business-information (2)

- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/business-buyer` — Информация о покупателе — юридическом лице [fbs,fby,dbs,express]
- `POST   /v2/campaigns/{campaignId}/orders/{orderId}/documents` — Информация о документах [fbs,fby,dbs,express]

## ratings (2)

- `POST   /v2/businesses/{businessId}/ratings/quality` — Индекс качества магазинов [fby,fbs,dbs,express]
- `POST   /v2/campaigns/{campaignId}/ratings/quality/details` — Заказы, которые повлияли на индекс качества [fbs,dbs,express]

## stocks (2)

- `POST   /v2/campaigns/{campaignId}/offers/stocks` — Информация об остатках и оборачиваемости [fby,fbs,dbs,express,laas]
- `PUT    /v2/campaigns/{campaignId}/offers/stocks` — Передача информации об остатках [fbs,dbs,express]

## auth (1)

- `POST   /v2/auth/token` — Получение информации о токене авторизации [fby,fbs,dbs,express,laas]

## businesses (1)

- `POST   /v2/businesses/{businessId}/settings` — Настройки кабинета [dbs,fbs,fby,express,laas]

## delivery-services (1)

- `GET    /v2/delivery/services` — Справочник служб доставки [fbs,dbs,express]

## goods-stats (1)

- `POST   /v2/campaigns/{campaignId}/stats/skus` — Отчет по товарам [fby,fbs,express,dbs]

## logistic-points (1)

- `POST   /v1/businesses/{businessId}/logistics-points` — Получение точек ПВЗ Маркета [laas]

## operations (1)

- `POST   /v1/businesses/{businessId}/operations` — Получение статусов операций [laas]

## orders-stats (1)

- `POST   /v2/campaigns/{campaignId}/stats/orders` — Детальная информация по заказам [fby,fbs,dbs,express]

## tariffs (1)

- `POST   /v2/tariffs/calculate` — Калькулятор стоимости услуг [fbs,fby,dbs,express]
