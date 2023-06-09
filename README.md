# kpo-microservices
build & up
```
sudo docker-compose build
sudo docker-compose up
``

## Тестирование
`localhost:8010` - сервис авторизации Swagger: `localhost:8010/docs`
`localhost:8080` - сервис заказов Swagger: `localhost:8080/docs`
спецификация API доступна в Swagger.

### Авторизация и аутентификация
1. Пройти регистрацию в сервисе авторизации через ручку `sign_up`
2. Получить токен через ручку `token`
3. Повысить роль своего пользователя до менеджера. Для этого сходить в  `POST users/me/role` с паролем `123` для роли менеджера или `321` для роли администратора (не забыть приложить к запросу токен, можно авторизоваться через интерфейс Swagger-а).
4. Проверить результаты в ручках `/users/me` и `/users/me/role` (приложить токен)
5. Скопировать токен - с ним нужно будет отправлять запросы ко второму микросервису.
6. Все запросы сервиса заказов (кроме получения меню) требуют аутентификации. К запросам нужно прикладывать токен.

### Заказы

1. Наполним базу блюд. ручка `order_service/dish/new`
2. Изменение количества блюд (отрицательное количество - уменьшение количества блюд) `order_service/dish`
3. Теперь можно создавать заказы. Ручка `order_service/orders`
4. Получение меню - `order_service/menu`
Заказы обрабатываются автоматически. Раз в 180 секунд все заказы меняют статус на следующий.
Заказы на которые не хватает блюд отменяются при создании.
