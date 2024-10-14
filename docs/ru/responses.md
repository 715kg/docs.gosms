---
title: Ответы
icon: material/arrow-u-left-top
---




## Коды состояния

Запросы вернут один из следующих кодов состояния ответа HTTP:

|Статус|Описание|
|:---------------------------|:----------------------------------------------------|
|`200 OK`|Действие с ресурсом было выполнено успешно.|
|`201 Created`|Ресурс был успешно создан. При этом ресурс может быть как уже готовым к использованию, так и находиться в процессе запуска.|
|`204 No Content`|Действие с ресурсом было выполнено успешно, и ответ не содержит дополнительной информации в теле.|
|`400 Bad Request`|Был отправлен неверный запрос, например, в нем отсутствуют обязательные параметры и т. д. Тело ответа будет содержать дополнительную информацию об ошибке.|
|`401 Unauthorized`|Ошибка аутентификации.|
|`403 Forbidden`	|Аутентификация прошла успешно, но недостаточно прав для выполнения действия. |
|`404 Not Found`| Запрашиваемый ресурс не найден. |
|`429 Too Many Requests`|Был достигнут лимит по количеству запросов в единицу времени. |
|`500 Internal Server Error`	| При выполнении запроса произошла какая-то внутренняя ошибка. Чтобы решить эту проблему, лучше всего написать в тех поддержку в панели управления.|

## Успешный ответ

Все конечные точки будут возвращать данные в формате `JSON`. 

##### Структура 200 OK
``` json title="HTTP/2.0 200 OK"
// (1)
{
    "id":"6654a4e8f1527149588c89f2",                       
    "message": "test", 					            
    "status": 0, 							      
    "callback_id": "", 					         
    "device_id": "",                              
    "phone_number": "79999999999",                  
    "message_status": "Ждет обработки",             
    "time_create": 1716812679                   
}
```

1. Эта структура может меняться в зависимости от запрашиваемого ресурса

## Ответ с ошибкой

|Название поля	|Тип	|Описание|
|:--------------|:------|:-------|
| `errors` | object | Объект, содержащий вложенные ключи "code" и "message". |
|`code` | number | Короткий числовой идентификатор ошибки. |
|`message` | string | Опционально. В большинстве случаев в ответе будет содержаться человекочитаемое подробное описание ошибки или ошибок, которые помогут понять, что нужно исправить. |

##### Структура 400 Bad Request
```json title="HTTP/2.0 400 Bad Request"
// (1)
{
    "errors": {
        "code": 2008,
        "message": "Неверно указан номер телефона в поле phone_number.",     
        "hash":"6654a4e8f152"
    }
}
```

1. Структура идентична для всех ответов ошибок

## Статусы ресурсов

Важно учесть, что при создании большинства ресурсов внутри платформы вам будет сразу возвращен ответ от сервера со статусом `200 OK` или `201 Created` и идентификатором созданного ресурса в теле ответа, но при этом этот ресурс может быть ещё в состоянии запуска.Список статусов будет отличаться в зависимости от типа ресурса. Увидеть поддерживаемый список статусов вы сможете в описании каждого конкретного ресурса.