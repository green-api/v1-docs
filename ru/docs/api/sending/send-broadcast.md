# SendBroadcast

Метод предназначен для отправки рассылки.

## Запрос {#request}

Для отправки рассылки требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/v2/{{account}}/SendBroadcast
```

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`name ` | **string** | Да | Наименование рассылки 
`to` | **array** | Да | Массив получателей рассылки. Заполняется элементами типа [идентификатор контакта](../chat-id.md#cus). Минимальное количество элементов в массиве - два. Максимальное значение не ограничено.
`text ` | **string** | Да | Текст сообщения рассылки. Минимальная длина сообщения 10 символов, максимальная 2000 символов
`startAt ` | **date** | Нет | Дата начала рассылки. Если значение не указано, то рассылка запускается сразу в момент вызова метода. Формат даты `2000-01-01 00:00:00`

> Минимальная длина текстового сообщения рассылки составляет 10 символов

> Максимальная длина текстового сообщения рассылки составляет 2000 символов

### Пример тела запроса {#request-example-body}

```json
{
    "name": "Broadcast from Green-API",
    "to": [
        79001234560,
        79001234561,
        79001234562,
        79001234563],
    "text": "I use Green-API to send this broadcast to you!",
    "startAt": "2022-03-12 12:00:00"
}
```

## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | -----
`broadcastId ` | **string** | Идентификатор созданной рассылки 

### Пример тела ответа {#response-example-body}

```json
{
    "broadcastId": "1234"
}
```

### Ошибки SendBroadcast {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/v2/{{account}}/SendBroadcast"

payload = "{\r\n    \"name\": \"Broadcast from Green-API\",\r\n    \"to\": [\r\n        79001234560,\r\n        79001234561,\r\n        79001234562,\r\n        79001234563],\r\n    \"text\": \"I use Green-API to send this broadcast to you!\",\r\n    \"startAt\": \"2022-03-12 12:00:00\"\r\n}"
headers = {
  'Authorization': 'Bearer {{apiToken}}',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```