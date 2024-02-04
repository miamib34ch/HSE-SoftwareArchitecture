# Лабораторная работа №4 REST API

Работу выполнили: [Полыгалов Богдан](https://github.com/miamib34ch) и [Тетенова Алёна](https://github.com/alenatetenova)

**Оглавление:**
- [Документация по API](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-api)
  - [Работа с пользователем](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D0%B5%D0%BC)
     - [POST /user/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-user)
     - [GET /user/{user_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#get-useruser_id)
     - [PUT /user/{user_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#put-useruser_id)
     - [DELETE /user/{user_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-useruser_id)
  - [Работа с маршрутом](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%BE%D0%BC)
     - [POST /route/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-route)
     - [GET /route/{route_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#get-routeroute_id)
     - [PUT /route/{route_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#put-routeroute_id)
     - [DELETE /route/{route_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-routeroute_id)
  - [Работа с точкой интереса на маршруте](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%82%D0%BE%D1%87%D0%BA%D0%BE%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%B5%D1%81%D0%B0-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B5)
     - [POST /point/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-point)
     - [GET /point/{point_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#get-pointpoint_id)
     - [PUT /point/{point_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#put-pointpoint_id)
     - [DELETE /point/{point_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-pointpoint_id)
  - [Работа с материалами](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BC%D0%B0%D1%82%D0%B5%D1%80%D0%B8%D0%B0%D0%BB%D0%B0%D0%BC%D0%B8)
     - [POST /material/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-material)
     - [DELETE /material/{material_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-materialmaterial_id)
- [Реализация API](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B5%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-api)
- [Тестирование API](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%82%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-api)
  - [Работа с пользователем](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D0%B5%D0%BC-1)
     - [POST /user/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-user-1)
     - [GET /user/{user_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#get-useruser_id-1)
     - [PUT /user/{user_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#put-useruser_id-1)
     - [DELETE /user/{user_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-useruser_id-1)
  - [Работа с маршрутом](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%BE%D0%BC-1)
     - [POST /route/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-route-1)
     - [GET /route/{route_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#get-routeroute_id-1)
     - [PUT /route/{route_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#put-routeroute_id-1)
     - [DELETE /route/{route_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-routeroute_id-1)
  - [Работа с точкой интереса на маршруте](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%82%D0%BE%D1%87%D0%BA%D0%BE%D0%B9-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%B5%D1%81%D0%B0-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B5-1)
     - [POST /point/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-point-1)
     - [GET /point/{point_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#get-pointpoint_id-1)
     - [PUT /point/{point_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#put-pointpoint_id-1)
     - [DELETE /point/{point_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-pointpoint_id-1)
  - [Работа с материалами](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BC%D0%B0%D1%82%D0%B5%D1%80%D0%B8%D0%B0%D0%BB%D0%B0%D0%BC%D0%B8-1)
     - [POST /material/](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#post-material-1)
     - [DELETE /material/{material_id}](https://github.com/miamib34ch/HSE-SoftwareArchitecture/tree/LabWork4/Lab%20Work%20%E2%84%964/docs#delete-materialmaterial_id-1)

## *Документация по API*

### *Работа с пользователем*

#### *POST /user/*

**Описание:** Создание пользователя

**Заголовки:**
- `Content-Type: application/json`

**Входные параметры:**  
Body:  
- `username` (строка) - Имя пользователя
- `password` (строка) - Пароль пользователя
- `is_tourist` (булевое) - Является ли пользователь туристом

**Пример входных параметров:**
```json
{
  "username": "john_doe",
  "is_tourist": true,
  "password": "securepassword123"
}
```

**Код статусы ответа:**
- `201 Created` Успешно создан
- `409 Conflict` - Конфликт пользователь с таким именем уже существует
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "token": "debsmahdb-asdbfasbfb-e9ueyfask-dasdasasd",
  "user_id": 123,
  "username": "john_doe",
  "is_tourist": true,
  "created_routes": []
}
```

**cURL:**
```
curl -X POST -H "Content-Type: application/json" -d '{"username":"john_doe", "is_tourist":true,"password":"securepassword123"}' https://api.example.com/user/
```


#### *GET /user/{user_id}*

**Описание:** Получение данных о пользователе

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `user_id` (целочисленное число) - Идентификатор пользователя, информацию о котором необходимо получить.

**Пример входных параметров:**
```
/user/123
```

**Код статусы ответа:**
- `200 OK` - Успешный запрос, возвращается информация о пользователе
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Пользователь с указанным user_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "token": "debsmahdb-asdbfasbfb-e9ueyfask-dasdasasd",
  "user_id": 123,
  "username": "john_doe",
  "is_tourist": true,
  "created_routes": []
}
```

**cURL:** 
```
curl -X GET -H "Authorization: Bearer {ваш_токен}" https://api.example.com/user/123
```


#### *PUT /user/{user_id}*

**Описание:** Обновление данных пользователя

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `user_id` (целочисленное число) - Идентификатор пользователя, информацию о котором необходимо обновить.

Body:  
- `username` (строка) - Имя пользователя
- `password` (строка) - Пароль пользователя
- `is_tourist` (булевое) - Является ли пользователь туристом

**Пример входных параметров:**
```
/user/123
```
```json
{
  "username": "john_doe",
  "is_tourist": true,
  "password": "securepassword123"
}
```

**Код статусы ответа:**
- `200 OK` - Успешное обновление данных пользователя
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Пользователь с указанным user_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "token": "debsmahdb-asdbfasbfb-e9ueyfask-dasdasasd",
  "user_id": 123,
  "username": "john_doe",
  "is_tourist": true,
  "created_routes": []
}
```

**cURL:** 
```
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"username":"new_john_doe","is_tourist": true,"password":"new_securepassword123"}' https://api.example.com/user/123
```


#### *DELETE /user/{user_id}*

**Описание:** Удаление пользователя

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `user_id` (целочисленное число) - Идентификатор пользователя, информацию о котором необходимо удалить.

**Пример входных параметров:**
```
/user/123
```

**Код статусы ответа:**
- `204 No Content` - Успешное удаление пользователя
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Пользователь с указанным user_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{}
```

**cURL:** 
```
curl -X DELETE -H "Authorization: Bearer {ваш_токен}" https://api.example.com/user/123
```





### *Работа с маршрутом*

#### *POST /route/*

**Описание:** Создание маршрута

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Body:  
- `name` (строка) - Название маршрута
- `description` (строка) - Описание маршрута
- `waypoints` (массив объектов) - Список точек маршрута, каждая точка содержит координаты, описание.

**Пример входных параметров:**
```json
{
  "name": "Путешествие по городу",
  "description": "Замечательный тур по основным достопримечательностям города",
  "waypoints": [
    {
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Красная площадь"
    }
  ]
}
```

**Код статусы ответа:**
- `201 Created` - Маршрут успешно создан
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "route_id": 456,
  "name": "Путешествие по городу",
  "description": "Замечательный тур по основным достопримечательностям города",
  "waypoints": [
    {
      "point_id": 1,
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Красная площадь",
      "materials": []
    }
  ]
}
```

**cURL:** 
```
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"name":"Путешествие по городу","description":"Замечательный тур по основным достопримечательностям города","waypoints":[{"latitude":55.7558,"longitude":37.6176,"description":"Красная площадь"}]}' https://api.example.com/route/
```


#### *GET /route/{route_id}*

**Описание:** Получение данных о маршруте

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `route_id` (целочисленное число) - Идентификатор маршрута, информацию о котором необходимо получить.

**Пример входных параметров:**
```
/route/456
```

**Код статусы ответа:**
- `200 OK` - Успешный запрос, возвращается информация о маршруте
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Маршрут с указанным route_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "route_id": 456,
  "name": "Путешествие по городу",
  "description": "Замечательный тур по основным достопримечательностям города",
  "waypoints": [
    {
      "point_id": 1,
      "latitude": 55.7558,
      "longitude": 37.6176,
      "description": "Красная площадь",
      "materials": [
        {"material_id": 1, "title": "Фото Красной площади"},
        {"material_id": 2, "title": "История Красной площади"}
      ]
    }
  ]
}
```

**cURL:** 
```
curl -X GET -H "Authorization: Bearer {ваш_токен}" https://api.example.com/route/456
```


#### *PUT /route/{route_id}*

**Описание:** Обновление данных о маршруте

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `route_id` (целочисленное число) - Идентификатор маршрута, информацию о котором необходимо обновить.

Body:  
- `name` (строка, необязательно) - Новое название маршрута
- `description` (строка, необязательно) - Новое описание маршрута

**Пример входных параметров:**
```
/route/456
```
```json
{
  "name": "Новое название маршрута",
  "description": "Новое описание маршрута"
}
```

**Код статусы ответа:**
- `200 OK` - Успешное обновление данных маршрута
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Маршрут с указанным route_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "route_id": 456,
  "name": "Новое название маршрута",
  "description": "Новое описание маршрута",
  "waypoints": [
    {
      "point_id": 1,
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
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"name":"Новое название маршрута","description":"Новое описание маршрута"}' https://api.example.com/route/456
```


#### *DELETE /route/{route_id}*

**Описание:** Удаление маршрута

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `route_id` (целочисленное число) - Идентификатор маршрута, который необходимо удалить.

**Пример входных параметров:**
```
/route/456
```

**Код статусы ответа:**
- `204 No Content` - Успешное удаление маршрута
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Маршрут с указанным route_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{}
```

**cURL:** 
```
curl -X DELETE -H "Authorization: Bearer {ваш_токен}" https://api.example.com/route/456
```





### *Работа с точкой интереса на маршруте*

#### *POST /point/*

**Описание:** Создание точки интереса

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Body:  
- `latitude` (вещественное число) - Широта точки интереса.
- `longitude` (вещественное число) - Долгота точки интереса.
- `description` (строка) - Описание точки интереса.

**Пример входных параметров:**
```json
{
  "latitude": 55.7558,
  "longitude": 37.6176,
  "description": "Новая точка интереса"
}
```

**Код статусы ответа:**
- `201 Created` - Точка интереса успешно создана
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "point_id": 789,
  "latitude": 55.7558,
  "longitude": 37.6176,
  "description": "Новая точка интереса",
  "materials": [
    {"material_id": 7, "title": "Новый материал"}
  ]
}
```

**cURL:** 
```
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"latitude":55.7558,"longitude":37.6176,"description":"Новая точка интереса"}' https://api.example.com/point/
```


#### *GET /point/{point_id}*

**Описание:** Получение данных о точке интереса

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `point_id` (целочисленное число) - Идентификатор точки интереса, информацию о которой необходимо получить.

**Пример входных параметров:**
```
/point/789
```

**Код статусы ответа:**
- `200 OK` - Успешный запрос, возвращается информация о точке интереса
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Точка интереса с указанным point_id не найдена
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "point_id": 789,
  "latitude": 55.7558,
  "longitude": 37.6176,
  "description": "Новая точка интереса",
  "materials": [
    {"material_id": 7, "title": "Новый материал"}
  ]
}
```

**cURL:** 
```
curl -X GET -H "Authorization: Bearer {ваш_токен}" https://api.example.com/point/789
```


#### *PUT /point/{point_id}*

**Описание:** Обновление данных о точки интереса

**Заголовки:**
- `Content-Type: application/json`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `point_id` (целочисленное число) - Идентификатор точки интереса, информацию о которой необходимо обновить.

Body:
- `latitude` (вещественное число, необязательно) - Новая широта точки интереса.
- `longitude` (вещественное число, необязательно) - Новая долгота точки интереса.
- `description` (строка, необязательно) - Новое описание точки интереса.

**Пример входных параметров:**
```
/point/789
```

```json
{
  "latitude": 55.756,
  "longitude": 37.618,
  "description": "Обновленная точка интереса"
}
```

**Код статусы ответа:**
- `200 OK` - Успешное обновление данных точки интереса
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Точка интереса с указанным point_id не найдена
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "point_id": 789,
  "latitude": 55.756,
  "longitude": 37.618,
  "description": "Обновленная точка интереса",
  "materials": [
    {"material_id": 8, "title": "Еще один новый материал"}
  ]
}
```

**cURL:** 
```
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"latitude":55.756,"longitude":37.618,"description":"Обновленная точка интереса"}' https://api.example.com/point/789
```


#### *DELETE /point/{point_id}*

**Описание:** Удаление точки интереса

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `point_id` (целочисленное число) - Идентификатор точки интереса, которую необходимо удалить.

**Пример входных параметров:**
```
/point/789
```

**Код статусы ответа:**
- `204 No Content` - Успешное удаление точки интереса
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Точка интереса с указанным point_id не найдена
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{}
```

**cURL:** 
```
curl -X DELETE -H "Authorization: Bearer {ваш_токен}" https://api.example.com/point/789
```





### *Работа с материалами*

#### *POST /material/*

**Описание:** Загрузка материала

**Заголовки:**
- `Content-Type: multipart/form-data`
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Body:  
- `file` (файл) - Загружаемый файл.

**Пример входных параметров:**
```
Файл: material_photo.jpg
```

**Код статусы ответа:**
- `201 Created` - Материал успешно загружен
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{
  "material_id": 9,
  "title": "material_photo.jpg"
}
```

**cURL:** 
```
curl -X POST -H "Authorization: Bearer {ваш_токен}" -F "file=@material_photo.jpg" https://api.example.com/material/
```


#### *DELETE /material/{material_id}*

**Описание:** Удаление материала

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `material_id` (целочисленное число) - Идентификатор материала, который необходимо удалить.

**Пример входных параметров:**
```
/material/9
```

**Код статусы ответа:**
- `204 No Content` - Успешное удаление материала
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Материал с указанным material_id не найден
- `422 Unprocessable Entity` - Некорректный запрос (например, отсутствие обязательных параметров)

**Пример ответа:**
```json
{}
```

**cURL:** 
```
curl -X DELETE -H "Authorization: Bearer {ваш_токен}" https://api.example.com/material/9
```

## *Реализация API*

Код в папке src

## *Тестирование API*

### *Работа с пользователем*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/a7296767-42d5-47d4-aa4e-744117e6ae36)

#### *POST /user/*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/e5276ddf-daf2-4b30-aeb6-62bff2cf1a18)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/e7c957e9-2dc1-4976-8dee-783f7e25ae74)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/48583d57-006e-4e9b-890b-eb64e3fcabbb)

#### *GET /user/{user_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/5d28e72c-1003-465e-a1f6-67dd705ab353)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/a07569e0-39aa-43c2-97fd-bcdef6df5a2d)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/8c72cd7c-0927-44ff-bd50-d3c8b563347c)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/d1770572-73c2-4a0f-8530-12e4a98f4a37)

#### *PUT /user/{user_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/21539e61-4aa1-4231-8a5b-bb4917e24b8a)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/2e2fe089-34da-48f5-9e7c-d5f45b118368)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/4d6e66f9-d668-44a2-ac5a-addec1b3a67e)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/fbad0695-1be2-4c83-aeba-341ff9d318cb)

#### *DELETE /user/{user_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/ab966766-6123-4f2c-9db6-06c776287db9)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/44d00936-10bb-42b7-84ff-fef80c61ed87)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/597fe7df-1f10-4e47-bfab-fb3793b0118a)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/8db16ee5-9f68-45da-bb29-58d1d7ab65d4)

### *Работа с маршрутом*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/63928ffd-567b-45d8-a0c9-0143037b9162)

#### *POST /route/*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/4b5a3633-fd0d-4f96-b6fb-67a9a00023bb)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/33992465-6f7f-4557-9dd6-df51c436a66d)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/f40e354e-6f5e-4bdb-a397-e0fa00b860b9)

#### *GET /route/{route_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/ea8e91a4-3e12-4422-aa63-1dd13e0fbe8a)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/be39bdc4-b97a-4331-8ada-c1dd87a99a03)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/048cd07f-f1db-4016-ab07-fa9d2b6a66ad)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/0f3bf2dd-6ee0-4b9c-a759-dc2def05b5ba)

#### *PUT /route/{route_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/d04ad39c-a160-4426-80c6-5985a5f698e0)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/7770b685-72ed-4a5b-8ca8-54ff3825f845)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/e01c4cb1-1c7e-4998-8547-48dbfcb807be)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/4d9af0bc-2dfd-4081-b84b-816599a7f0a1)

#### *DELETE /route/{route_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/705c392d-af24-4c22-a2b5-e819c9a6f4b0)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/b1dcf3e5-aed0-4416-8df6-d30be369565a)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/92ec2c67-84f6-4a5c-b0b2-28eb3864bc00)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/61b0d9cc-4a8a-4a0a-8acf-b621a2d3719b)

### *Работа с точкой интереса на маршруте*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/55d7baf5-5966-4edb-877a-725e646f1a94)

#### *POST /point/*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/68ecb1c9-a337-42ee-98d7-400c7d28d52e)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/da6e268b-e4e8-41a6-b60d-95188e8005ed)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/f084a942-acc0-4ced-9639-f58081043eed)

#### *GET /point/{point_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/42cdb891-0930-4b0d-abce-472bb3db0060)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/6ccca049-2b46-4993-9346-f59863c79bde)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/484e184f-36f9-4fd8-8e8c-75357b859312)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/08d1d4d7-8fdb-4e2e-bc77-3ff679772b04)

#### *PUT /point/{point_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/88a878e2-5610-44e6-99e8-064005efe73e)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/ab5966b7-b0cc-4804-bf6c-da58675fe1d7)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/38269904-11d7-4ce9-b58b-c3d0ea50d377)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/bd377354-8ffc-41eb-b160-51397c16ddb7)

#### *DELETE /point/{point_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/9babddf8-b1b5-4fd9-a165-3301e34de4ae)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/7d1fd9bf-2d96-4e1f-97ee-601af199e1d4)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/e4ccd9bb-219e-4a00-a996-7f8cc4c185e4)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/2da921ac-94cf-4ef2-af47-aa1918125493)

### *Работа с материалами*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/5a15de17-eb7c-4afe-a0b3-acce1f2ea1a5)

#### *POST /material/*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/4d8fdb5c-fbf8-43b8-86dd-1be6be4d8d2c)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/12cf298a-c865-4b88-ae52-bea887cf0050)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/5d8654f2-cd29-420c-bbdb-055a97832a6d)

#### *DELETE /material/{material_id}*

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/f0eb6d58-55d7-4db8-8045-e5ce0fbef235)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/bc2c1155-2f40-4497-9ba1-293f57056568)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/d78692cb-27f8-4a4c-bcdc-cb6d8fb0d431)

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/c77899d4-982a-47e3-a610-476a63696e36)



