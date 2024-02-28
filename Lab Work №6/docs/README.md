# Лабораторная работа № 6 - Шаблоны проектирования

# Шаблоны проектирования Gang of Four (GoF)

## Порождающие шаблоны

### Фабричный метод / Factory Method

**Назначение:**  
Определяет интерфейс для создания объекта, но оставляет подклассам решение о том, какой класс инстанцировать.  

**Пример:**  
1. Есть интерфейс объекта `Route`, есть классы объектов, которые исполняют интерфейс `FullRoute` и `DemoRoute`.  
2. Есть интерфейс фабрики `RouteFactory`, в которой есть метод создания маршрута, есть классы фабрики, которые создают маршруты `FullRouteFactory` и `DemoRouteFactory`.  
3. Благодаря тому, что `FullRoute` и `DemoRoute` наследюутся от `Route`, то метод фабрики `RouteFactory` необязан реализовать каждый тип объекта, а только Route, остальное уже решают подклассы.

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

### Абстрактная фабрика / Abstract Factory

**Назначение:**  
Предоставляет интерфейс для создания семейств связанных или зависимых объектов без указания их конкретных классов.

**Пример:**  
1. Вводятся два протокола: `Backpack` и `Tent`, cоздаются конкретные классы, реализующие эти протоколы. В данном случае, `SimpleBackpack` и `FancyBackpack` - это два варианта рюкзака, а `SimpleTent` и `FancyTent` - два варианта палатки. Каждый из них реализует соответствующие методы протоколов.  
2. Создается протокол `TouristEquipmentFactory`, предоставляющий интерфейс для создания связанных объектов рюкзака и палатки. Cоздаются две конкретные реализации абстрактной фабрики: `SimpleTouristEquipmentFactory` и `FancyTouristEquipmentFactory`. Каждая из этих фабрик реализует методы `createBackpack` и `createTent`, возвращая соответствующие объекты рюкзака и палатки.
3. Есть класс клиент `TouristClient`, который не содержит конкретные объекты палатки и рюкзака (может быть любой) и объекта фабрики (может быть любая). И уже, в зависимости от использования класса клиента, будет определяться, какие именно у него рюкзак и палатка.

**UML:**  
<img width="1380" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/4abef3a9-ba3b-49eb-a322-8a42e6c74549">  
```PlantUML
@startuml
interface TouristEquipmentFactory {
  + createBackpack(): Backpack
  + createTent(): Tent
}

class Backpack {
  + pack(): void
}

class Tent {
  + setup(): void
}

class SimpleBackpack implements Backpack {
  + pack(): void
}

class FancyBackpack implements Backpack {
  + pack(): void
}

class SimpleTent implements Tent {
  + setup(): void
}

class FancyTent implements Tent {
  + setup(): void
}

class SimpleTouristEquipmentFactory implements TouristEquipmentFactory {
  + createBackpack(): SimpleBackpack
  + createTent(): SimpleTent
}

class FancyTouristEquipmentFactory implements TouristEquipmentFactory {
  + createBackpack(): FancyBackpack
  + createTent(): FancyTent
}

class TouristClient {
  - backpack: Backpack
  - tent: Tent
  + prepareForTour(): void
}

TouristClient --> TouristEquipmentFactory
TouristClient --> Backpack
TouristClient --> Tent

@enduml
```

**Код:**
```Swift
import Foundation

// Абстрактные классы объектов
protocol Backpack {
    func pack()
}

protocol Tent {
    func setup()
}

// Конкретные классы объектов
class SimpleBackpack: Backpack {
    func pack() {
        print("Packing a simple backpack")
    }
}

class FancyBackpack: Backpack {
    func pack() {
        print("Packing a fancy backpack")
    }
}

class SimpleTent: Tent {
    func setup() {
        print("Setting up a simple tent")
    }
}

class FancyTent: Tent {
    func setup() {
        print("Setting up a fancy tent")
    }
}

// Абстрактная фабрика
protocol TouristEquipmentFactory {
    func createBackpack() -> Backpack
    func createTent() -> Tent
}

// Конкретные фабрики
class SimpleTouristEquipmentFactory: TouristEquipmentFactory {
    func createBackpack() -> Backpack {
        return SimpleBackpack()
    }

    func createTent() -> Tent {
        return SimpleTent()
    }
}

class FancyTouristEquipmentFactory: TouristEquipmentFactory {
    func createBackpack() -> Backpack {
        return FancyBackpack()
    }

    func createTent() -> Tent {
        return FancyTent()
    }
}

// Клиентский код
class TouristClient {
    private var backpack: Backpack
    private var tent: Tent

    init(factory: TouristEquipmentFactory) {
        self.backpack = factory.createBackpack()
        self.tent = factory.createTent()
    }

    func prepareForTour() {
        backpack.pack()
        tent.setup()
    }
}

// Пример использования
let simpleFactory = SimpleTouristEquipmentFactory()
let fancyFactory = FancyTouristEquipmentFactory()

let simpleClient = TouristClient(factory: simpleFactory)
simpleClient.prepareForTour()

let fancyClient = TouristClient(factory: fancyFactory)
fancyClient.prepareForTour()
```

### Одиночка / Singleton

**Назначение:**  
Гарантирует, что у класса есть только один экземпляр и предоставляет к нему глобальную точку доступа.

**Пример:**  
1. Есть класс `TouristInformationCenter`, в нём есть статическая переменная экземляра данного класса, инициализатор приватный, чтобы не могли создавать другие сущности.
2. Вызываем методы класса по информированию через статическую переменную экземляра.

**UML:**  
<img width="1183" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/5246a7f6-d39d-4015-b8db-463f53aabdc4">  
```PlantUML
@startuml
class TouristInformationCenter {
  - shared: TouristInformationCenter
  - constructor(): void
  + provideInfo(): void
  + getSharedInstance(): TouristInformationCenter
}

TouristInformationCenter --> TouristInformationCenter : shared
@enduml
```

**Код:**
```Swift
import Foundation

// Класс туристического информационного центра
class TouristInformationCenter {
    static let shared = TouristInformationCenter()

    private init() {
        // Инициализационная логика здесь
    }

    func provideInfo() {
        print("Providing tourist information")
    }
}

// Пример использования

let touristCenter1 = TouristInformationCenter.shared
let touristCenter2 = TouristInformationCenter.shared

print(touristCenter1 === touristCenter2)  // true
```


## Структурные шаблоны

### Адаптер / Adapter

**Назначение:**  
Преобразует интерфейс одного класса в интерфейс другого, который ожидают клиенты. Адаптер делает возможной совместную работу классов с несовместимыми интерфейсами.

**Пример:**  
Создаём класс адаптера, где он реализует нужный метод через обработку несовместимых интерфейсов.

**UML:**  
<img width="642" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/2c7c0e66-2982-495b-8fa6-5edf7e5cc025">
```PlantUML
@startuml

class ExternalRouteService {
    + fetchRoute(): [String: Any]
}

class ExternalRouteServiceProvider {
    + getExternalRouteService(): ExternalRouteService
}

class Route {
    + planRoute()
}

class RouteAdapter {
    - externalService: ExternalRouteService
    + init(externalService: ExternalRouteService)
    + planRoute()
}

ExternalRouteService --|> RouteAdapter : «use»
RouteAdapter --|> Route : «inherit»

ExternalRouteServiceProvider --|> ExternalRouteService

@enduml
```

**Код:**
```Swift
// Класс для взаимодействия с внешним сервисом маршрутизации
class ExternalRouteService {
    func fetchRoute() -> [String: Any] {
        // Симуляция получения информации о маршруте от внешнего сервиса
        return ["name": "Внешний маршрут", "description": "Маршрут из внешнего сервиса", "waypoints": []]
    }
}

// Поставщик внешнего сервиса маршрутизации
class ExternalRouteServiceProvider {
    func getExternalRouteService() -> ExternalRouteService {
        return ExternalRouteService()
    }
}

// Абстрактный класс для представления маршрута
class Route {
    func planRoute() {
        // Базовая реализация планирования маршрута
    }
}

// Адаптер маршрута, приспосабливающий внешний сервис маршрутизации
class RouteAdapter: Route {
    let externalService: ExternalRouteService

    init(externalService: ExternalRouteService) {
        self.externalService = externalService
    }

    override func planRoute() {
        let routeInfo = externalService.fetchRoute()
        print("Планирование маршрута: \(routeInfo["name"] ?? ""), \(routeInfo["description"] ?? "")")
        // Дополнительная логика для адаптации информации о внешнем маршруте
    }
}

// Использование адаптера маршрута
let externalRouteServiceProvider = ExternalRouteServiceProvider()
let externalRouteService = externalRouteServiceProvider.getExternalRouteService()

let routeAdapter = RouteAdapter(externalService: externalRouteService) // можно подменить другим
routeAdapter.planRoute()
```


### 

**Назначение:**

**Пример:**  

**UML:**

**Код:**


### 

**Назначение:**

**Пример:**  

**UML:**

**Код:**


### 

**Назначение:**

**Пример:**  

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

