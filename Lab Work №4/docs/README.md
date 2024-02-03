# Лабораторная работа №4 REST API

Работу выполнили: [Полыгалов Богдан](https://github.com/miamib34ch) и [Тетенова Алёна](https://github.com/alenatetenova)
 
## Документация по API

### Работа с пользователем



#### POST /user/

**Описание:** Создание пользователя

**Заголовки:**
- `Content-Type: application/json`

**Входные параметры:** 
Body:  
- `username` (строка) - Имя пользователя
- `email` (строка) - Адрес электронной почты
- `password` (строка) - Пароль пользователя

**Пример входных параметров:**
```json
{
  "username": "john_doe",
  "email": "john.doe@example.com",
  "password": "securepassword123"
}
```

**Код статусы ответа:**
- `201 Created` Успешно создан
- `400 Bad Request` - Некорректный запрос (например, отсутствие обязательных параметров)
- `409 Conflict` - Конфликт (например, пользователь с таким именем или адресом электронной почты уже существует)

**Пример ответа:**
```json
{
  "user_id": 123,
  "username": "john_doe",
  "email": "john.doe@example.com"
}
```

**cURL:**
```
curl -X POST -H "Content-Type: application/json" -d '{"username":"john_doe","email":"john.doe@example.com","password":"securepassword123"}' https://api.example.com/user/
```



#### GET /user/{user_id}

**Описание:** Получение данных о пользователе

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:** 
Query: 
- `user_id` (число) - Идентификатор пользователя, информацию о котором необходимо получить.

**Пример входных параметров:**
```
/user/123
```

**Код статусы ответа:**
- `200 OK` - Успешный запрос, возвращается информация о пользователе
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Пользователь с указанным user_id не найден

**Пример ответа:**
```json
{
  "user_id": 123,
  "username": "john_doe",
  "email": "john.doe@example.com"
}
```

**cURL:** 
```
curl -X GET -H "Authorization: Bearer {ваш_токен}" https://api.example.com/user/123
```



#### PUT /user/{user_id}

**Описание:** Обновление данных пользователя

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 
- `user_id` (число) - Идентификатор пользователя, информацию о котором необходимо получить.
Body:
- `username` (строка, необязательно) - Новое имя пользователя
- `email` (строка, необязательно) - Новый адрес электронной почты
- `password` (строка, необязательно) - Новый пароль пользователя

**Пример входных параметров:**
```json
{
  "username": "new_john_doe",
  "email": "new_john.doe@example.com",
  "password": "new_securepassword123"
}
```

**Код статусы ответа:**
- `200 OK` - Успешное обновление данных пользователя
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `400 Bad Request` - Некорректный запрос (например, неверные параметры в теле запроса)
- `404 Not Found` - Пользователь с указанным user_id не найден

**Пример ответа:**
```json
{
  "user_id": 123,
  "username": "new_john_doe",
  "email": "new_john.doe@example.com"
}
```

**cURL:** 
```
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"username":"new_john_doe","email":"new_john.doe@example.com","password":"new_securepassword123"}' https://api.example.com/user/123
```


#### DELETE /user/{user_id} 

**Описание:** Удаление пользователя

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 
- `user_id` (число) - Идентификатор пользователя, информацию о котором необходимо получить.

**Пример входных параметров:**
```
/user/123
```

**Код статусы ответа:**
- `204 No Content` - Успешное удаление пользователя
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Пользователь с указанным user_id не найден

**Пример ответа:**
```json
{}
```

**cURL:** 
```
curl -X DELETE -H "Authorization: Bearer {ваш_токен}" https://api.example.com/user/123
```


### Работа с маршрутом

#### POST /route/

**Описание:** Создание маршрута

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Body:  
- `name` (строка) - Название маршрута
- `description` (строка) - Описание маршрута
- `waypoints` (массив объектов) - Список точек маршрута, каждая точка содержит координаты, описание и материалы.

**Пример входных параметров:**
```json
{
  "name": "Путешествие по городу",
  "description": "Замечательный тур по основным достопримечательностям города",
  "waypoints": [
    {
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Красная площадь",
      "materials": [
        {"material_id": 1, "title": "Фото Красной площади"},
        {"material_id": 2, "title": "История Красной площади"}
      ]
    },
    {
      "latitude": 55.7517,
      "longitude": 37.6188,
      "description": "Кремль",
      "materials": [
        {"material_id": 3, "title": "Фото Кремля"},
        {"material_id": 4, "title": "История Кремля"}
      ]
    },
    {
      "latitude": 55.7479,
      "longitude": 37.5841,
      "description": "Арбат",
      "materials": [
        {"material_id": 5, "title": "Фото Арбата"},
        {"material_id": 6, "title": "История Арбата"}
      ]
    }
  ]
}
```

**Код статусы ответа:**
- `201 Created` - Маршрут успешно создан
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `400 Bad Request` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```
{
  "route_id": 456,
  "name": "Путешествие по городу",
  "description": "Замечательный тур по основным достопримечательностям города",
  "waypoints": [
    {
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Красная площадь",
      "materials": [
        {"material_id": 1, "title": "Фото Красной площади"},
        {"material_id": 2, "title": "История Красной площади"}
      ]
    },
    {
      "latitude": 55.7517,
      "longitude": 37.6188,
      "description": "Кремль",
      "materials": [
        {"material_id": 3, "title": "Фото Кремля"},
        {"material_id": 4, "title": "История Кремля"}
      ]
    },
    {
      "latitude": 55.7479,
      "longitude": 37.5841,
      "description": "Арбат",
      "materials": [
        {"material_id": 5, "title": "Фото Арбата"},
        {"material_id": 6, "title": "История Арбата"}
      ]
    }
  ]
}
```

**cURL:** 
```
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"name":"Путешествие по городу","description":"Замечательный тур по основным достопримечательностям города","waypoints":[{"latitude":55.7558,"longitude":37.6176,"description":"Красная площадь","materials":[{"material_id":1,"title":"Фото Красной площади"},{"material_id":2,"title":"История Красной площади"}]},{"latitude":55.7517,"longitude":37.6188,"description":"Кремль","materials":[{"material_id":3,"title":"Фото Кремля"},{"material_id":4,"title":"История Кремля"}]},{"latitude":55.7479,"longitude":37.5841,"description":"Арбат","materials":[{"material_id":5,"title":"Фото Арбата"},{"material_id":6,"title":"История Арбата"}]}]}' https://api.example.com/route/
```


#### GET /route/{route_id}

**Описание:** Получение данных о маршруте

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 
- `route_id` (число) - Идентификатор маршрута, информацию о котором необходимо получить.

**Пример входных параметров:**
```
/route/456
```

**Код статусы ответа:**
- `200 OK` - Успешный запрос, возвращается информация о маршруте
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Маршрут с указанным route_id не найден

**Пример ответа:**
```json
{
  "route_id": 456,
  "name": "Путешествие по городу",
  "description": "Замечательный тур по основным достопримечательностям города",
  "waypoints": [
    {
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Красная площадь",
      "materials": [
        {"material_id": 1, "title": "Фото Красной площади"},
        {"material_id": 2, "title": "История Красной площади"}
      ]
    },
    {
      "latitude": 55.7517,
      "longitude": 37.6188,
      "description": "Кремль",
      "materials": [
        {"material_id": 3, "title": "Фото Кремля"},
        {"material_id": 4, "title": "История Кремля"}
      ]
    },
    {
      "latitude": 55.7479,
      "longitude": 37.5841,
      "description": "Арбат",
      "materials": [
        {"material_id": 5, "title": "Фото Арбата"},
        {"material_id": 6, "title": "История Арбата"}
      ]
    }
  ]
}
```

**cURL:** 
```
curl -X GET -H "Authorization: Bearer {ваш_токен}" https://api.example.com/route/456
```


#### PUT /route/{route_id}

**Описание:** Обновление данных о маршруте

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 
- `route_id` (число) - Идентификатор маршрута, информацию о котором необходимо обновить.
Body:  
- `name` (строка, необязательно) - Новое название маршрута
- `description` (строка, необязательно) - Новое описание маршрута
- `waypoints` (массив объектов, необязательно) - Новый список точек маршрута.

**Пример входных параметров:**
```json
{
  "name": "Новое название маршрута",
  "description": "Новое описание маршрута",
  "waypoints": [
    {
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Новая точка",
      "materials": [
        {"material_id": 7, "title": "Новый материал"}
      ]
    }
  ]
}
```

**Код статусы ответа:**
- `200 OK` - Успешное обновление данных маршрута
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Маршрут с указанным route_id не найден
- `400 Bad Request` - Некорректный запрос (например, неверные параметры в теле запроса)

**Пример ответа:**
```json
{
  "route_id": 456,
  "name": "Новое название маршрута",
  "description": "Новое описание маршрута",
  "waypoints": [
    {
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Новая точка",
      "materials": [
        {"material_id": 7, "title": "Новый материал"}
      ]
    }
  ]
}
```

**cURL:** 
```
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"name":"Новое название маршрута","description":"Новое описание маршрута","waypoints":[{"latitude":55.7558,"longitude":37.6176,"description":"Новая точка","materials":[{"material_id":7,"title":"Новый материал"}]}]}' https://api.example.com/route/456
```


#### DELETE /route/{route_id}

**Описание:** Удаление маршрута

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



### Работа с точкой интереса на маршруте

#### POST /point/

**Описание:** Создание точки интереса

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Body:  

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



#### GET /point/{point_id}

**Описание:** Получение данных о точке интереса

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



#### PUT /point/{point_id}

**Описание:** Обновление данных о точки интереса

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 
Body:  

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



#### DELETE /point/{point_id}

**Описание:** Удаление точки интереса

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



### Работа с материалами

#### POST /material/

**Описание:** Загрузка материала

**Заголовки:**
mimetype
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Body: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



#### GET /material/{material_id}

**Описание:** Получение материала

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



#### PUT /material/{material_id}

**Описание:** Обновление материала

**Заголовки:**
mimetype
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 
Body: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



#### DELETE /material/{material_id}

**Описание:** Удаление материала

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**
Query: 

**Пример входных параметров:**

**Код статусы ответа:**

**Пример ответа:**

**cURL:** 



## Реализация API

## Тестирование API
