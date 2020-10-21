# Получение уведомлений

`/v1/notifications`

Для получения входящих уведомлений используйте узел `notifications`. 
Уведомления содержат данные о входящих сообщениях, статусах ранее отправленных сообщений и др. После получения и обработки уведомления его трубется [удалить](), чтобы получить следующее уведомление.

> Вызов ожидает получения уведомления в течение 20 сек. Вызов метода завершается с пустым ответом в случае достижения таймаута. Если в течение 20 сек в очереди появляется уведомление, то вызов метода завешается, и метод возвращает полученное уведомление. 

> Срок хранения уведомлений в очереди составляет 24 часа.

> Уведомления отдаются из очереди в порядке [FIFO](https://ru.wikipedia.org/wiki/FIFO)

## Запрос {#request}

Для получения уведомления требуется выполнить запрос по адресу:
```
GET https://api.green-api.com/v1/notifications
```

## Ответ {#response}

При успешном ответе возвращается код HTTP `200`

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | -----
`messages` | **array** | Массив идентификаторов отправленных сообщений 


Массив `messages`

Поле | Тип |  Описание
----- | ----- | -----
`id ` | **string** | Идентификатор отправленного сообщения 

### Пример тела ответа {#response-example-body}

```
200
```

```json
{
    "messages": [
        {
            "id": "1234"
        }
    ],
    "meta": {
        "api_status": "stable",
        "version": "2.0.1"
    }
}
```

### Ошибки {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../errors.md)

В случае ошибки возвращается код HTTP `400` с подробным описанием ошибки в теле ответа.

### Пример тела ответа с ошибкой {#response-example-body-error}

```json
{
    "errors": [
        {
            "code": 82,
            "details": "Outgoing messages limit exceeded",
            "title": "Превышено колличество исходящих сообщений"
        }
    ],
    "meta": {
        "api_status": "stable",
        "version": "2.0.1"
    }
}
```

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/v1/messages"

payload = "{\r\n    \"to\": \"79001234567\",\r\n    \"type\":\"text\",    \r\n    \"text\": {\r\n        \"body\": \"I use Green-API to send this message to you!\"\r\n    }    \r\n}"
headers = {
  'Authorization': 'Bearer {{AuthToken}}',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```