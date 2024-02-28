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

### Мост / Bridge

**Назначение:**  
Разделяет абстракцию от ее реализации, чтобы они могли изменяться независимо.

**Пример:**  
Класс содержит объект интерфейса, но его можно подменить при использовании объекта класса.

**UML:**  
<img width="642" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/9de54ee1-e6da-4113-97cf-7609c2d296ac">
```PlantUML
@startuml
interface MapRenderer {
  + renderMap(): void
}

class SimpleMapRenderer implements MapRenderer {
  + renderMap(): void
}

class DetailedMapRenderer implements MapRenderer {
  + renderMap(): void
}

class Route {
  - mapRenderer: MapRenderer
  + setMapRenderer(renderer: MapRenderer): void
  + planRoute(): void
}

Route *-- MapRenderer
@enduml
```

**Код:**
```Swift
// Абстрактный класс для отрисовки карты
class MapRenderer {
    func renderMap() {
        // Абстрактный метод
    }
}

// Конкретный класс для отрисовки простой карты
class SimpleMapRenderer: MapRenderer {
    override func renderMap() {
        print("Отрисовка простой карты")
    }
}

// Конкретный класс для отрисовки детальной карты
class DetailedMapRenderer: MapRenderer {
    override func renderMap() {
        print("Отрисовка детальной карты")
    }
}

// Класс для представления маршрута
class Route {
    var mapRenderer: MapRenderer

    init(mapRenderer: MapRenderer) {
        self.mapRenderer = mapRenderer
    }

    func setMapRenderer(renderer: MapRenderer) {
        self.mapRenderer = renderer
    }

    func planRoute() {
        print("Планирование маршрута")
        // Дополнительная логика
        self.mapRenderer.renderMap()
    }
}

// Создаем экземпляры рендереров карт
let simpleRenderer = SimpleMapRenderer()
let detailedRenderer = DetailedMapRenderer()

// Создаем маршрут с использованием простого рендерера
var route = Route(mapRenderer: simpleRenderer)
route.planRoute()

// Переключаем рендерер на детальный и повторно планируем маршрут
route.setMapRenderer(renderer: detailedRenderer)
route.planRoute()
```

### Декоратор / Decorator

**Назначение:**  
Динамически добавляет объекту новые возможности. Является гибкой альтернативой наследованию для расширения функциональности.

**Пример:**  
Создаём набор классов-декораторов, которые оборачивают базовый объект, добавляя ему новые возможности. Каждый декоратор реализует тот же интерфейс, что и базовый объект, что позволяет им быть взаимозаменяемыми.

**UML:**  
<img width="876" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/940240d6-485a-48da-b74b-3c563c572401">
```PlantUML
@startuml

class Route {
  + planRoute()
}

class TouristRoute {
  + planRoute()
}

class RouteDecorator {
  - decoratedRoute: Route
  + planRoute()
}

class ScenicViewDecorator {
  + planRoute()
}

class RestStopDecorator {
  + planRoute()
}

Route --|> TouristRoute
RouteDecorator <|-- ScenicViewDecorator
RouteDecorator <|-- RestStopDecorator
Route --|> RouteDecorator

@enduml
```

**Код:**
```Swift
import Foundation

// Протокол для определения базового класса маршрута
protocol Route {
    func planRoute()
}

// Конкретная реализация маршрута для туристического маршрута
class TouristRoute: Route {
    func planRoute() {
        print("Планирование туристического маршрута")
    }
}

// Базовый класс для декоратора маршрута
class RouteDecorator: Route {
    private let decoratedRoute: Route

    init(decoratedRoute: Route) {
        self.decoratedRoute = decoratedRoute
    }

    func planRoute() {
        decoratedRoute.planRoute()
    }
}

// Декоратор для добавления живописных видов к маршруту
class ScenicViewDecorator: RouteDecorator {
    override func planRoute() {
        super.planRoute()
        print("Добавление живописных видов к маршруту")
    }
}

// Декоратор для добавления отдыхающих на маршрут
class RestStopDecorator: RouteDecorator {
    override func planRoute() {
        super.planRoute()
        print("Добавление мест отдыха к маршруту")
    }
}

// Пример использования
let baseTouristRoute = TouristRoute()

// Декорирование маршрута с живописными видами
let routeWithScenicViews = ScenicViewDecorator(decoratedRoute: baseTouristRoute)
routeWithScenicViews.planRoute()

// Декорирование маршрута с живописными видами и местами отдыха
let routeWithScenicViewsAndRestStops = RestStopDecorator(decoratedRoute: routeWithScenicViews)
routeWithScenicViewsAndRestStops.planRoute()
```

### Компоновщик / Composite

**Назначение:**  
Компонует объекты в древовидные структуры для представления иерархий «часть — целое». Позволяет клиентам единообразно трактовать индивидуальные и составные объекты.

**Пример:**  
1. Создаём абстрактный класс, который будет представлять как отдельные объекты, так и их композиции. В данном случае, `Route` служит абстрактным компонентом.
2. Реализуем конкретные классы, представляющие листовые компоненты, в данном случае `SimpleRoute`.
3. Реализуем классы, которые могут содержать как отдельные объекты `Route`, так и их композиции `RouteCollection`.
4. Гарантия того, что как листовые, так и составные компоненты могут быть обработаны единообразно через общий интерфейс (метод `planRoute`).

**UML:**  
<img width="539" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/9f335adf-1199-467e-b49d-d6df90a5ba02">
```PlantUML
@startuml

class Route {
  +planRoute(): void
}

class SimpleRoute {
  +planRoute(): void
}

class RouteCollection {
  -routes: List<Route>
  +addRoute(route: Route): void
  +planRoute(): void
}

Route <|-- SimpleRoute
Route <|-- RouteCollection

@enduml
```

**Код:**
```Swift
import Foundation

// Абстрактный класс маршрута
class Route {
    func planRoute() {
        // Абстрактный метод для планирования маршрута
    }
}

// Простой маршрут
class SimpleRoute: Route {
    override func planRoute() {
        print("Планирование простого маршрута")
    }
}

// Коллекция маршрутов
class RouteCollection: Route {
    private var routes: [Route] = []

    // Добавление маршрута в коллекцию
    func addRoute(route: Route) {
        routes.append(route)
    }

    // Планирование всех маршрутов в коллекции
    override func planRoute() {
        for route in routes {
            route.planRoute()
        }
    }
}

// Пример использования
let simpleRoute1 = SimpleRoute()
let simpleRoute2 = SimpleRoute()

let routeCollection = RouteCollection()
routeCollection.addRoute(route: simpleRoute1)
routeCollection.addRoute(route: simpleRoute2)

routeCollection.planRoute()
```


## Поведенческие шаблоны

### Стратегия / Strategy

**Назначение:**  
Определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми. Стратегия позволяет изменять алгоритмы независимо от клиентов, которые ими пользуются.

**Пример:**  
Клиент выполняет одно действие, но с разными классами одного интерфейса

**UML:**  
<img width="1206" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/19ea0756-3eed-4c13-bfb2-9a16792cbd30">
```PlantUML
@startuml

interface NavigationStrategy {
    + navigate(): void
}

class WalkingStrategy {
    + navigate(): void
}

class CyclingStrategy {
    + navigate(): void
}

class DrivingStrategy {
    + navigate(): void
}

class Navigator {
    - navigationStrategy: NavigationStrategy
    + setNavigationStrategy(strategy: NavigationStrategy): void
    + navigate(): void
}

Navigator --|> NavigationStrategy
Navigator *-down-> WalkingStrategy: strategy
Navigator *-down-> CyclingStrategy: strategy
Navigator *-down-> DrivingStrategy: strategy

@enduml
```

**Код:**
```Swift
// Протокол для стратегии навигации
protocol NavigationStrategy {
    func navigate()
}

// Конкретные классы стратегий

class WalkingStrategy: NavigationStrategy {
    func navigate() {
        print("Используется стратегия пешеходной навигации")
    }
}

class CyclingStrategy: NavigationStrategy {
    func navigate() {
        print("Используется стратегия велосипедной навигации")
    }
}

class DrivingStrategy: NavigationStrategy {
    func navigate() {
        print("Используется стратегия автомобильной навигации")
    }
}

// Класс навигатора

class Navigator {
    var navigationStrategy: NavigationStrategy

    init(navigationStrategy: NavigationStrategy) {
        self.navigationStrategy = navigationStrategy
    }

    // Метод для установки новой стратегии навигации
    func setNavigationStrategy(strategy: NavigationStrategy) {
        navigationStrategy = strategy
    }

    // Метод для выполнения навигации с текущей стратегией
    func navigate() {
        navigationStrategy.navigate()
    }
}

// Пример использования

// Создаем экземпляры стратегий
let walkingStrategy = WalkingStrategy()
let cyclingStrategy = CyclingStrategy()
let drivingStrategy = DrivingStrategy()

// Создаем экземпляр навигатора с начальной стратегией (например, пешеходной)
let navigator = Navigator(navigationStrategy: walkingStrategy)

// Выполняем навигацию с текущей стратегией
navigator.navigate()

// Меняем стратегию на велосипедную и выполняем навигацию
navigator.setNavigationStrategy(strategy: cyclingStrategy)
navigator.navigate()

// Меняем стратегию на автомобильную и выполняем навигацию
navigator.setNavigationStrategy(strategy: drivingStrategy)
navigator.navigate()
```

### Наблюдатель / Observer

**Назначение:**  
Определяет зависимость "один ко многим" между объектами так, что при изменении состояния одного объекта все зависящие от него оповещаются и обновляются автоматически.

**Пример:**  
1. Есть два класса: `TouristObserver` и `TouristSubject`. Класс `TouristObserver` имеет метод `updateLocation`, а класс `TouristSubject` содержит список наблюдателей и методы для добавления, удаления и уведомления наблюдателей.
2. Когда вызываем уведомление, то у всех наблюдателей вызывается метод `updateLocation`.

**UML:**  
<img width="770" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/10ff1f03-9d9d-40c2-ab3a-8b7dc30e07c9">
```PlantUML
@startuml
class TouristObserver {
    + updateLocation(latitude: double, longitude: double): void
}

class TouristSubject {
    - observers: List<TouristObserver>
    + addObserver(observer: TouristObserver): void
    + removeObserver(observer: TouristObserver): void
    + notifyObservers(latitude: double, longitude: double): void
}

TouristObserver --|> TouristSubject
@enduml
```

**Код:**
```Swift
import Foundation

// Наблюдатель
protocol TouristObserver: AnyObject {
    func updateLocation(latitude: Double, longitude: Double)
}

// Субъект (Турист)
class TouristSubject {
    private var observers: [TouristObserver] = []

    // Добавить наблюдателя
    func addObserver(observer: TouristObserver) {
        observers.append(observer)
    }

    // Удалить наблюдателя
    func removeObserver(observer: TouristObserver) {
        observers.removeAll { $0 === observer }
    }

    // Уведомить наблюдателей о изменении местоположения
    func notifyObservers(latitude: Double, longitude: Double) {
        for observer in observers {
            observer.updateLocation(latitude: latitude, longitude: longitude)
        }
    }
}

// Пример использования
class ExampleTourist: TouristObserver {
    let name: String

    init(name: String) {
        self.name = name
    }

    func updateLocation(latitude: Double, longitude: Double) {
        print("\(name) получил обновление местоположения: Широта \(latitude), Долгота \(longitude)")
    }
}

// Создаем объект субъекта (Турист)
let touristSubject = TouristSubject()

// Создаем и добавляем наблюдателей
let observer1 = ExampleTourist(name: "Наблюдатель 1")
let observer2 = ExampleTourist(name: "Наблюдатель 2")

touristSubject.addObserver(observer: observer1)
touristSubject.addObserver(observer: observer2)

// Посылаем уведомление об изменении местоположения
touristSubject.notifyObservers(latitude: 55.7558, longitude: 37.6176)

// Результат в консоли:
// Наблюдатель 1 получил обновление местоположения: Широта 55.7558, Долгота 37.6176
// Наблюдатель 2 получил обновление местоположения: Широта 55.7558, Долгота 37.6176
```

### Состояние / State

**Назначение:**  
Позволяет объекту варьировать свое поведение в зависимости от внутреннего состояния. Извне создается впечатление, что изменился класс объекта. 

**Пример:**  
Объект делегирует выполнение своих операций текущему объекту-состоянию.

**UML:**  
<img width="770" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/83c47410-f690-4ebe-b5be-cc2932e96f11">
```PlantUML
@startuml

class TouristState {
  {abstract} +handle()
}

class NormalTouristState {
  +handle()
}

class LostTouristState {
  +handle()
}

class TouristStateContext {
  -state: TouristState
  +init(initialState: TouristState)
  +setState(newState: TouristState)
  +requestState()
}

TouristState <|-- NormalTouristState
TouristState <|-- LostTouristState
TouristStateContext *-- TouristState

@enduml
```

**Код:**
```Swift
import Foundation

// Базовый класс состояния туриста
class TouristState {
    func handle() {
        // Базовая реализация обработки состояния
    }
}

// Конкретное состояние: турист в нормальном состоянии
class NormalTouristState: TouristState {
    override func handle() {
        print("Турист находится в нормальном состоянии")
    }
}

// Конкретное состояние: турист потерян
class LostTouristState: TouristState {
    override func handle() {
        print("Турист потерян")
    }
}

// Класс контекста, который использует состояние туриста
class TouristStateContext {
    private var state: TouristState
    
    init(initialState: TouristState) {
        self.state = initialState
    }
    
    func setState(newState: TouristState) {
        self.state = newState
    }
    
    func requestState() {
        self.state.handle()
    }
}

// Пример использования

// Создаем объекты состояний
let normalState = NormalTouristState()
let lostState = LostTouristState()

// Создаем объект контекста с начальным состоянием
let context = TouristStateContext(initialState: normalState)

// Вызываем метод requestState для обработки текущего состояния
context.requestState()

// Меняем состояние
context.setState(newState: lostState)

// Снова вызываем метод requestState для обработки нового состояния
context.requestState()
```

### Команда / Command

**Назначение:**  
Инкапсулирует запрос как объект, позволяя тем самым задавать параметры клиентов для обработки соответствующих запросов, ставить запросы в очередь или протоколировать их, а также поддерживать отмену операций.

**Пример:**  
Создаём класс-метод, будет выполнять одну операцию - реализация интерфейса.

**UML:**  
<img width="791" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/0771ffb2-e189-4949-a83a-f63b313b307e">
```PlantUML
@startuml

class Tourist {
    + moveForward()
    + moveBackward()
}

interface TouristCommand {
    + execute()
}

class MoveForwardCommand {
    - tourist: Tourist
    + MoveForwardCommand(tourist: Tourist)
    + execute()
}

class MoveBackwardCommand {
    - tourist: Tourist
    + MoveBackwardCommand(tourist: Tourist)
    + execute()
}

TouristCommand <|.. MoveForwardCommand
TouristCommand <|.. MoveBackwardCommand

Tourist --> TouristCommand
MoveForwardCommand --> Tourist
MoveBackwardCommand --> Tourist

@enduml
```

**Код:**
```Swift
// Протокол команды
protocol TouristCommand {
    func execute()
}

// Класс представляющий туриста
class Tourist {
    func moveForward() {
        print("Турист движется вперёд")
    }

    func moveBackward() {
        print("Турист движется назад")
    }
}

// Класс команды для движения вперёд
class MoveForwardCommand: TouristCommand {
    private let tourist: Tourist

    init(tourist: Tourist) {
        self.tourist = tourist
    }

    func execute() {
        tourist.moveForward()
    }
}

// Класс команды для движения назад
class MoveBackwardCommand: TouristCommand {
    private let tourist: Tourist

    init(tourist: Tourist) {
        self.tourist = tourist
    }

    func execute() {
        tourist.moveBackward()
    }
}

// Пример использования
let tourist = Tourist()

let moveForwardCommand = MoveForwardCommand(tourist: tourist)
let moveBackwardCommand = MoveBackwardCommand(tourist: tourist)

// Выполнение команд
moveForwardCommand.execute()
moveBackwardCommand.execute()
```

### Шаблонный метод / Template Method

**Назначение:**  
Шаблонный метод определяет основу алгоритма и позволяет подклассам переопределять некоторые шаги алгоритма, не изменяя его структуры в целом.

**Пример:**  
1. Определяем родительский класс `TravelPlanTemplate`, содержащий "шаблонный метод" `executeTravelPlan` и методы `startTravel`, `visitDestinations` и `endTravel`, которые выполняются в "шаблонном методе".
2. Создаём конкретные классы, реализующие методы из `TravelPlanTemplate` - `RoadTripPlan` и `CruisePlan`.
3. Шаблонный метод нельзя переопределить.

**UML:**  
<img width="791" alt="image" src="https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/d3a1fdd0-f1c9-47fc-a65c-decb16bb6ecc">
```PlantUML
@startuml

abstract class TravelPlanTemplate {
    +executeTravelPlan()
    #startTravel()
    #visitDestinations()
    #endTravel()
}

class RoadTripPlan {
    +startTravel()
    +visitDestinations()
    +endTravel()
}

class CruisePlan {
    +startTravel()
    +visitDestinations()
    +endTravel()
}

TravelPlanTemplate <|-- RoadTripPlan
TravelPlanTemplate <|-- CruisePlan

RoadTripPlan --> TravelPlanTemplate
CruisePlan --> TravelPlanTemplate

@enduml
```

**Код:**
```Swift
import Foundation

// Абстрактный класс, определяющий "шаблонный метод".
// Этот метод определяет последовательность шагов алгоритма, а конкретные шаги реализуются в подклассах.
class TravelPlanTemplate {

    // Шаблонный метод, представляющий собой последовательность шагов путешествия.
    // Этот метод является финальным, чтобы подклассы не могли изменить порядок шагов.
    final func executeTravelPlan() {
        startTravel()    // Шаг 1: Начало путешествия
        visitDestinations()  // Шаг 2: Посещение различных мест
        endTravel()      // Шаг 3: Завершение путешествия
    }

    // Абстрактные методы, которые будут реализованы в подклассах.
    func startTravel() {
        fatalError("Метод startTravel должен быть переопределен в подклассе")
    }

    func visitDestinations() {
        fatalError("Метод visitDestinations должен быть переопределен в подклассе")
    }

    func endTravel() {
        fatalError("Метод endTravel должен быть переопределен в подклассе")
    }
}

// Конкретный класс, реализующий шаблонный метод собственными шагами.
class RoadTripPlan: TravelPlanTemplate {
    override func startTravel() {
        print("Начинаем дорожное путешествие.")
    }

    override func visitDestinations() {
        print("Посещаем города и достопримечательности вдоль маршрута.")
    }

    override func endTravel() {
        print("Завершаем дорожное путешествие.")
    }
}

// Конкретный класс, реализующий шаблонный метод собственными шагами.
class CruisePlan: TravelPlanTemplate {
    override func startTravel() {
        print("Начинаем круизное путешествие.")
    }

    override func visitDestinations() {
        print("Плаваем по разным портам и островам.")
    }

    override func endTravel() {
        print("Завершаем круизное путешествие.")
    }
}

// Пример использования:

let roadTrip = RoadTripPlan()
roadTrip.executeTravelPlan()

let cruise = CruisePlan()
cruise.executeTravelPlan()
```
