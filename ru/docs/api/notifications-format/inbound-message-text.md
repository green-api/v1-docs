# Входящее текстовое сообщение

Уведомление приходит при получении входящего текстового сообщения.

## Формат уведомления

```json
{
    "messages": [
      {
        "from": "sender-wa-id",
        "id": "message-id",
        "text": {
          "body": "text-message-content"
        },
        "timestamp": "message-timestamp",
        "type": "text"
      }
    ],
    "contacts": [
      {
        "profile": {
          "name": "sender-profile-name"
        },
        "wa_id": "wa-id-of-contact"
      }
    ]
}
```

## Параметры уведомления {#notification-parameters}

Параметр | Тип | Описание
----- | ----- | -----
`messages ` | **object** | [Объект сообщения]()
`contacts ` | **object** | [Объект контакта]()

### Пример тела уведомления {#notification-example-body}

```json
{
    "messages": [
      {
        "from": "79001234567",
        "id": "1234",
        "text": {
          "body": "I use Green-API to get this message from you!"
        },
        "timestamp": "1597316093",
        "type": "text"
      }
    ],
    "contacts": [
      {
        "profile": {
          "name": "Andrew"
        },
        "wa_id": "79001234567"
      }
    ]
}
```