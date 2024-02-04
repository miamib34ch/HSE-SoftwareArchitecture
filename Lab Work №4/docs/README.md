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
- `user_id` (число) - Идентификатор пользователя, информацию о котором необходимо получить.

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
- `user_id` (число) - Идентификатор пользователя, информацию о котором необходимо обновить.

Body:  
- `username` (строка) - Имя пользователя
- `password` (строка) - Пароль пользователя
- `is_tourist` (булевое) - Является ли пользователь туристом

**Пример входных параметров:**
```
"user_id": 123
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
- `user_id` (число) - Идентификатор пользователя, информацию о котором необходимо удалить.

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
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"name":"Путешествие по городу","description":"Замечательный тур по основным достопримечательностям города","waypoints":[{"latitude":55.7558,"longitude":37.6176,"description":"Красная площадь","materials":[{"material_id":1,"title":"Фото Красной площади"},{"material_id":2,"title":"История Красной площади"}]},{"latitude":55.7517,"longitude":37.6188,"description":"Кремль","materials":[{"material_id":3,"title":"Фото Кремля"},{"material_id":4,"title":"История Кремля"}]},{"latitude":55.7479,"longitude":37.5841,"description":"Арбат","materials":[{"material_id":5,"title":"Фото Арбата"},{"material_id":6,"title":"История Арбата"}]}]}' https://api.example.com/route/
```


#### *GET /route/{route_id}*

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
- `route_id` (число) - Идентификатор маршрута, информацию о котором необходимо обновить.

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
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"name":"Новое название маршрута","description":"Новое описание маршрута","waypoints":[{"latitude":55.7558,"longitude":37.6176,"description":"Новая точка","materials":[{"material_id":7,"title":"Новый материал"}]}]}' https://api.example.com/route/456
```


#### *DELETE /route/{route_id}*

**Описание:** Удаление маршрута

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `route_id` (число) - Идентификатор маршрута, который необходимо удалить.

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
- `latitude` (число) - Широта точки интереса.
- `longitude` (число) - Долгота точки интереса.
- `description` (строка) - Описание точки интереса.
- `materials` (массив объектов) - Список материалов, связанных с точкой интереса.

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
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"latitude":55.7558,"longitude":37.6176,"description":"Новая точка интереса","materials":[{"material_id":7,"title":"Новый материал"}]}' https://api.example.com/point/
```


#### *GET /point/{point_id}*

**Описание:** Получение данных о точке интереса

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `point_id` (число) - Идентификатор точки интереса, информацию о которой необходимо получить.

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
- `point_id` (число) - Идентификатор точки интереса, информацию о которой необходимо обновить.

Body:
- `latitude` (число, необязательно) - Новая широта точки интереса.
- `longitude` (число, необязательно) - Новая долгота точки интереса.
- `description` (строка, необязательно) - Новое описание точки интереса.
- `materials` (массив объектов, необязательно) - Новый список материалов, связанных с точкой интереса.

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
curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer {ваш_токен}" -d '{"latitude":55.756,"longitude":37.618,"description":"Обновленная точка интереса","materials":[{"material_id":8,"title":"Еще один новый материал"}]}' https://api.example.com/point/789
```


#### *DELETE /point/{point_id}*

**Описание:** Удаление точки интереса

**Заголовки:**
- `Authorization: Bearer {ваш_токен}`

**Входные параметры:**  
Query:  
- `point_id` (число) - Идентификатор точки интереса, которую необходимо удалить.

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
- `400 Bad Request` - Некорректный запрос (например, отсутствие обязательных параметров)

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
- `material_id` (число) - Идентификатор материала, который необходимо удалить.

**Пример входных параметров:**
```
/material/9
```

**Код статусы ответа:**
- `204 No Content` - Успешное удаление материала
- `401 Unauthorized` - Ошибка авторизации, отсутствует или неверный токен
- `404 Not Found` - Материал с указанным material_id не найден

**Пример ответа:**
```json
{}
```

**cURL:** 
```
curl -X DELETE -H "Authorization: Bearer {ваш_токен}" https://api.example.com/material/9
```

## *Реализация API*

## *Тестирование API*
