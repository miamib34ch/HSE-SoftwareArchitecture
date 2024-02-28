# Лабораторная работа № 6 - Шаблоны проектирования

# Шаблоны проектирования GoF (Gang of Four)

## Порождающие шаблоны

### Фабричный метод / Factory Method

**Назначение:**  
Определяет интерфейс для создания объекта, но оставляет подклассам решение о том, какой класс инстанцировать.  

**Пример:**  
Есть интерфейс объекта `Route`, есть классы объектов, которые исполняют интерфейс `FullRoute` и `DemoRoute`.
Есть интерфейс фабрики `RouteFactory`, в которой есть метод создания маршрута, есть классы фабрики, которые создают маршруты `FullRouteFactory` и `DemoRouteFactory`.  
Благодаря тому, что `FullRoute` и `DemoRoute` наследюутся от `Route`, то метод фабрики `RouteFactory` необязан реализовать каждый тип объекта, а только Route, остальное уже решают подклассы.

**UML:**  
<img width="1255" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/744f9148-077a-4396-aef1-fd7091d95836">  
```PlantUML
@startuml

interface Route {
  + planRoute(): void
}

class FullRoute implements Route {
  + planRoute(): void
}

class DemoRoute implements Route {
  + planRoute(): void
}

interface RouteFactory {
  + createRoute(): Route
}

class FullRouteFactory implements RouteFactory {
  + createRoute(): Route
}

class DemoRouteFactory implements RouteFactory {
  + createRoute(): Route
}

RouteFactory <|.. FullRouteFactory
RouteFactory <|.. DemoRouteFactory
Route <|.. FullRoute
Route <|.. DemoRoute
FullRouteFactory --> FullRoute
DemoRouteFactory --> DemoRoute

@enduml
```

**Код:**
```Swift
// Интерфейс объекта Route
protocol Route {
    func planRoute()
}

// Класс маршрута с полной информацией
class FullRoute: Route {
    func planRoute() {
        print("Planning a full route")
    }
}

// Класс маршрута для демонстрации
class DemoRoute: Route {
    func planRoute() {
        print("Planning a demo route")
    }
}

// Протокол фабрики маршрутов
protocol RouteFactory {
    func createRoute() -> Route
}

// Реализация фабрики маршрутов с полной информацией
class FullRouteFactory: RouteFactory {
    func createRoute() -> Route {
        return FullRoute()
    }
}

// Реализация фабрики маршрутов для демонстрации
class DemoRouteFactory: RouteFactory {
    func createRoute() -> Route {
        return DemoRoute()
    }
}

// Пример использования

let fullRouteFactory: RouteFactory = FullRouteFactory()
let fullRoute: Route = fullRouteFactory.createRoute()
fullRoute.planRoute()

let demoRouteFactory: RouteFactory = DemoRouteFactory()
let demoRoute: Route = demoRouteFactory.createRoute()
demoRoute.planRoute()
```

### 

**Назначение:**

**UML:**

**Код:**

### 

**Назначение:**

**UML:**

**Код:**

##

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

##

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

### 

**Название:**

**Назначение:**

**UML:**

**Код:**

