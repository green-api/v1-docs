# Получение уведомлений

`/v1/notifications`

Для получения входящих уведомлений используйте узел `notifications`. 
Уведомления содержат данные о входящих сообщениях, статусах ранее отправленных сообщений и др. После получения и обработки уведомления его трубется [удалить](delete.md), чтобы получить следующее уведомление.

> Для получения входящих уведомлений используется технология [Long polling](https://en.wikipedia.org/wiki/Push_technology#Long_polling). Вызов ожидает получения уведомления в течение 20 сек. Вызов метода завершается с пустым ответом в случае достижения таймаута. Если в течение 20 сек в очереди появляется уведомление, то вызов метода завешается, и метод возвращает одно полученное уведомление. 

> Срок хранения уведомлений в очереди составляет 24 часа.

> Уведомления отдаются из очереди в порядке [FIFO](https://ru.wikipedia.org/wiki/FIFO)

## Запрос {#request}

Для получения уведомления требуется выполнить запрос по адресу:
```
GET https://api.green-api.com/v1/notifications
```

## Ответ {#response}

При успешном ответе возвращается код HTTP `200`

Ответ содержит одно входящее уведомление в [заданном формате](../notifications-format/index.md).

### Пример тела ответа {#response-example-body}

```
200
```

```json
{
    "receipt": 1234567,
    "notifications": [
        {
            "type": "inbound_message",
            "account": {
                "id": 22123456,
                "wa_id": "79001234567"
            },
            "messages": [
                {
                    "from": "79001234568",
                    "id": 1234,
                    "timestamp": 1603666324,
                    "text": {
                        "body": "I use Green-API to get this message from you!"
                    },
                    "type": "text"
                }
            ],
            "contacts": [
                {
                    "profile": {
                        "name": "Andrew"
                    },
                    "wa_id": "79001234568"
                }
            ]
        }
    ]
}
```

### Ошибки {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../errors.md)

В случае ошибки возвращается код HTTP `400` с подробным описанием ошибки в теле ответа.

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/v1/notifications"

payload = {}
headers = {
  'Authorization': 'Bearer {{AuthToken}}'
}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```