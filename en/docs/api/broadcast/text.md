# Отправка массовых рассылок

`/v1/broadcast`

Для отправки массовых рассылок своим контактам используйте узел `broadcast`. Поддерживается отправка текстовых рассылок, а также рассылок с изображениями, видео, аудио и документами. Количество получателей рассылки не ограничено.

## Условия доставки сообщений рассылки {#broadcast-delivery}

Сообщения рассылки будут доставлены до получателей при выполнении следующих условий:

- телефон аккаунта, с которого выполняется рассылка, должен быть занесен в контакты на телефоне получателя
- получатель рассылки должен предварительно получить хотя бы одно сообщение от текущего аккаунта

## Ограничения {#broadcast-limitations}

При отправке массовых рассылок установлены следующие ограничения:

- Максимальный размер изображения: 1000x1000 px
- Минимальная длина текста рассылки: 10 символов 
- Максимальная длина текста рассылки: 2000 символов
- Минимальное количество получателей рассылки: 2 контакта
- Максимальное количество получателей рассылки: не ограничено

## Отбор получателей рассылки {#broadcast-filter}

Имеется возможность гибко задавать получателей рассылки:

- отправить рассылку всем контактам (не указывайте ни один из параметров: `to`, `period`, `active`)
- отправить рассылку списку контактов (используйте параметр `to`)
- отправить рассылку контактам, зарегистрированным в заданный период (используйте параметр `period`)
- отправить рассылку контактам, активным в заданный период (используйте параметр `active`)

Параметры `period` и `active` можно сочетать между собой. Параметр `to` не сочитается ни с одним параметром и применяется отдельно.

## Запрос {#request}

Для отправки рассылки требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/v1/broadcast
```

```json
{
    "name": "broadcast-name",
    "to": [
        {"wa_id": "whatsapp-id-1"},
        {"wa_id": "whatsapp-id-2"},
        {"wa_id": "whatsapp-id-3"}
    ],
    "period": {
        "from": "registration-period-from",
        "to": "registration-period-to"
    },
    "active": {
        "from": "contact-active-from",
        "to": "contact-active-to"
    },

    "type": "text" | "image" | "video" | "audio" | "document",

    "text": {
        "body": "your-text-message-content"
    },

    "image": {
        "id": "your-media-id",
        "caption": "your-image-caption"
    },

    "image": {
        "link": "http(s)://the-url",
        "caption": "your-image-caption"
    },
    
    "video": {
        "id": "your-media-id"  
    },    

    "video": {
        "link": "http(s)://the-url"
    },

    "audio": {
        "id": "your-media-id"  
    },      

    "audio": {
        "link": "http(s)://the-url"
    },

    "document": {
        "id": "your-media-id",
    },

    "document": {
        "link": "http(s)://the-url",
    },

    "startAt": "date-to-start-broadcast"
}
```

> Тело запроса приведено в качестве примера. В примере перечислены все возможные варианты отправки медиаданных. Тело действительного запроса может содержать только один объект медиаданных или только объект текстового сообщения.

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`name ` | **string** | Да | Наименование рассылки 
`to` | **array** | Нет | Отбор по получателям рассылки. Если параметр указан, то рассылку получат только корреспонденты из массива. Минимальное количество элементов в массиве - два. Максимальное значение не ограничено.
`period` | **object** | Нет | Отбор по периоду регистрации корреспондента в контактах. Если параметр указан, то рассылку получат только контакты, зарегистрированные в указанном диапазоне дат
`active` | **object** | Нет | Отбор по периоду активности корреспондента. Если параметр указан, то рассылку получат только контакты, активные в указанном диапазоне дат
`type` | **string** | Нет | Тип отправляемого сообщения. Может принимать значения: `text`, `image`, `video`, `audio`, `document`. При отправке текстового сообщения указывать параметр не обязательно. Значение по умолчанию: `text`
`text ` | **object** | Да, если `"type": "text"`| Объект текстового сообщения. Подробнее в разделе [Отправка текстовых сообщений](../messages/text.md)
`image ` | **object** | Да, если `"type": "image"` | Объект с данными изображения. Подробнее в разделе [Отправка сообщений с медиаданными](../messages/media.md)
`video ` | **object** | Да, если `"type": "video"` | Объект с данными видео. Подробнее в разделе [Отправка сообщений с медиаданными](../messages/media.md)
`audio ` | **object** | Да, если `"type": "audio"` | Объект с данными аудио. Подробнее в разделе [Отправка сообщений с медиаданными](../messages/media.md)
`document ` | **object** | Да, если `"type": "document"` | Объект с данными документа. Подробнее в разделе [Отправка сообщений с медиаданными](../messages/media.md)
`startAt ` | **date** | Нет | Дата начала рассылки. Если значение не указано, то рассылка запускается сразу

Массив `to`

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`wa_id` | **string** | Да | [Идентификатор корреспондента](../chat-id.md#cus). Минимальное количество элементов в массиве - два. Максимальное значение не ограничено.

Объект `period`

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`from` | **date** | Да | Нижняя граница отбора по дате регистрации корреспондента в контактах
`to` | **date** | Да | Вехрняя граница отбора по дате регистрации корреспондента в контактах

Объект `active`

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`from` | **date** | Да | Нижняя граница отбора по дате активности корреспондента
`to` | **date** | Да | Вехрняя граница отбора по дате активности корреспондента

Объект `text`

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`body ` | **string** | Да | Текст сообщения. Может содержать несколько URL и [форматирование](../formatting.md). Минимальная длина текста рассылки 10 символов, максимальная длина 2000 символов. Поддерживаются символы emoji 😃

### Пример тела запроса {#request-example-body}

Отправка рассылки всем контактам:
```json
{
    "name": "Broadcast from Green-API",
    "type": "text",
    "text": {
        "body": "I use Green-API to send this broadcast to you!"
    }
}
```

Отправка рассылки списку контактов:
```json
{
    "name": "Broadcast from Green-API",
    "to": [
        {"wa_id": "79001234560"},
        {"wa_id": "79001234561"},
        {"wa_id": "79001234562"}
    ],    
    "type": "text",
    "text": {
        "body": "I use Green-API to send this broadcast to you!"
    }
}
```

Отправка рассылки контатам, зарегистрированным в январе 2020:
```json
{
    "name": "Broadcast from Green-API",
    "period": {
        "from": "2020-01-01 00:00:00",
        "to": "2020-01-31 23:59:59"
    },   
    "type": "text",
    "text": {
        "body": "I use Green-API to send this broadcast to you!"
    }
}
```

Отправка рассылки всем контактам с изображением и описанием под изображением. В примере файл изображения был предварительно [выгружен](../media/upload.md) в облачное хранилище `media` и получен идентификатор файла `bca567ba-0bd7-4211-8792-0c123fbd2716`:
```json
{
    "name": "Broadcast from Green-API",
    "type":  "image",
    "image": {
        "id": "bca567ba-0bd7-4211-8792-0c123fbd2716",
        "caption": "I use Green-API to send this broadcast to you!"
    }
}
```

## Ответ {#response}

При успешном ответе возвращается код HTTP `201`

Поле | Тип |  Описание
----- | ----- | -----
`broadcast` | **array** | Массив идентификаторов созданных рассылок 

Массив `broadcast`

Поле | Тип |  Описание
----- | ----- | -----
`id ` | **string** | Идентификатор созданной рассылки 

### Пример тела ответа {#response-example-body}

```
201 Created
```

```json
{
    "broadcast": [
        {
            "id": "5f205403eb8c561bd4a51f27"
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
            "code": 81,
            "details": "Failed to create broadcast",
            "title": "Не удалось создать рассылку"
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

url = "https://api.green-api.com/v1/broadcast"

payload = "{\r\n    \"name\": \"Broadcast from Green-API\",\r\n    \"to\": [\r\n        {\"wa_id\": \"79001234560\"},\r\n        {\"wa_id\": \"79001234561\"},\r\n        {\"wa_id\": \"79001234562\"}\r\n    ],    \r\n    \"type\": \"text\",\r\n    \"text\": {\r\n        \"body\": \"I use Green-API to send this broadcast to you!\"\r\n    }\r\n}"
headers = {
  'Authorization': 'Bearer <your api token>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```