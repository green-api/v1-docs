# Получение медиаданных

`/v1/media`

Для получения изображений, видео, аудио и документов из [входящих сообщений](../notifications-format/inbound-message.md) требуется выполнить запрос на узел `media`.

> Срок хранения медиаданных составляет 24 часа.

## Запрос {#request}

Для получения медиаданных требуется выполнить запрос по адресу:

> Обратите внимание, что в качестве хоста используется адрес `media.green-api.com`

```
GET https://media.green-api.com/v1/media/media-id
```

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`media-id` | **string** | Да | Идентификатор файла, который требуется загрузить. Содержится во [входящих сообщениях](../notifications-format/inbound-message.md), а также может быть получен при [отправке медиаданных](upload.md) 


## Ответ {#response}

При успешном ответе возвращается код HTTP `200` и загруженные бинарные данные.

### Пример тела ответа {#response-example-body}

```
200 OK
```

```
Content-Type: image/jpeg
Content-Length: content-size

binary-media-data
```

### Ошибки {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../errors.md)

В случае ошибки возвращается код HTTP `400` с подробным описанием ошибки в теле ответа.

Если файл не найден, будет возвращен код HTTP `404 Not Found` без текста.

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://media.green-api.com/v1/media/f32bb4f9-850b-43c6-9b91-279831914c95"

payload = {}
headers = {
  'Authorization': 'Bearer {{AuthToken}}'
}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```