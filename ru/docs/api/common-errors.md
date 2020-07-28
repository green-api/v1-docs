# Стандартные ошибки

Код HTTP | Идентификатор ошибки | Описание
----- | ----- | -----
1010 | `Error` |
1011 | `Invalid parameter` | В метод передан некорректный параметр
1020 | `Parameter -to- is missing` | Требуется указать получателя сообщения в параметре `to`
1021 | `Invalid parameter -to-` | Параметр `to` не соответствует формату [идентификатора контакта или группы](chat-id.md)
1022 | `Subscriber not found` | Подписчик не найден
1023 | `Subscriber is unsubscribed or not processed` | Подписчик отписан или не обработан
1024 | `Failed to update subscriber details` | Не удалось обновить данные подписчика
1030 | `Parameter -text- is missing` | Требуется указать текст сообщения в параметре `text`
1031 | `Invalid parameter -text-` | Параметр `text` содержит недопустимые символы
1032 | `Message length exceeded` | Превышена длина сообщения. Максимальная длина сообщения 4096 символов
1040 | `Authorization key is missing` | Требуется указать ключ авторизации в заголовке запроса
1041 | `Authorization key is not allowed` | Ключ авторизации некорректный или недействительный
1042 | `System error` | Возникла внутренняя ошибка сервера. Обратитесь в службу поддержки
1050 | `Parameter -messageId- is missing` | В метод не передан обязательный параметр `messageId`
1051 | `Invalid parameter -messageId-` | Сообщение с идентификатором `messageId` не найдено
1052 | `Failed to get message array` | Не удалось получить массив сообщений
1060 | `Failed to create task to send message` | Не удалось создать задание на отправку сообщения
1061 | `Data not found` | Данные не найдены
1062 | `Buying subscription is needed` | Необходимо приобрести или оплатить тариф
1071 | `Senders not found` | Отправители не найдены
1072 | `Senders are overflow` | Отправители переполнены