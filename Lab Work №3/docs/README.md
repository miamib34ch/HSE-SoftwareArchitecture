# Диаграмма компонентов для мобильного приложения туристов

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/da7a70c0-beb5-4b1e-89eb-9ae8ca3b23a8)

```PlantUML
@startuml "messagebus"
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
' uncomment the following line and comment the first to use locally
' !include C4_Container.puml

AddElementTag("microService", $shape=EightSidedShape(), $bgColor="CornflowerBlue", $fontColor="white", $legendText="micro service\neight sided")
AddElementTag("storage", $shape=RoundedBoxShape(), $bgColor="lightSkyBlue", $fontColor="white")

SHOW_PERSON_OUTLINE()

Person(mt, Туристы, "Получают маршруты и просматривают их")
System(s, "Сервер", "Ответственен за обработку и передачу данных", $type="Container / C#, .NET")
Boundary(c, "Клиент туристов", "Container / iOS, Swift") {
Container(v, "Карта", "Component: UI View", "Экраны для просмотра маршрутов и точек на карте.")
Container(vm, "ViewModel", "Component: Controller", "Логика, управляющая данными и взаимодействием с View.")
Container(m, "Model", "Component: Model", "Хранит данные о маршрутах и материалах. Обрабатывает запросы от ViewModel.")
Container(ar, "Дополненная реальность", "Component: UI View", "Компонент, реализующий взаимодействие с технологией дополненной реальности.")
}
Rel_D(mt, v, "Нажатие кнопок (пользовательское взаимодействие)")
Rel_D(mt, ar, "Нажатие кнопок (пользовательское взаимодействие)")
Rel_D(v, vm, "Отправка пользовательского взаимодействия")
Rel_D(vm, v, "Уведомление об обновлении данных")
BiRel(vm, m, "Получение и обновления данных о маршрутах и материалах")
Rel_D(vm, ar, "Уведомление об обновлении данных")
BiRel(m, s, "Получение данных о маршрутах и материалах")
Rel_D(ar, vm, "Отправка пользовательского взаимодействия")

SHOW_LEGEND()
@enduml
```

# Диаграмма последовательности

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/11298299-325b-4aa8-8794-736101583364)

```PlantUML
@startuml

actor Турист as Tourist
participant "Карта" as MobileApp
participant "Дополненная реальность" as ARComponent
participant "ViewModel" as ViewModel
participant "Model" as Model
database "Сервер" as Server

Tourist -> MobileApp: Открытие приложения

activate MobileApp
Tourist -> MobileApp: Просмотр маршрута
MobileApp -> ViewModel: Запрос маршрута

activate ViewModel
ViewModel -> Model: Запрос данных маршрута

activate Model
Model -> Server: Запрос данных маршрута

activate Server
Server --> Model: Возврат данных маршрута
deactivate Server

Model --> ViewModel: Возврат данных маршрута
deactivate Model

ViewModel --> MobileApp: Возврат маршрута
deactivate ViewModel

MobileApp --> Tourist: Отображение маршрута


Tourist -> MobileApp: Выбор точки маршрута
MobileApp -> ViewModel: Запрос текстовых и медиа материалов
 
activate ViewModel
ViewModel -> Model: Запрос текстовых и медиа материалов

activate Model
Model -> Server: Запрос текстовых и медиа материалов

activate Server
Server --> Model: Возврат текстовых и медиа материалов
deactivate Server

Model --> ViewModel: Возврат текстовых и медиа материалов
deactivate Model

ViewModel --> MobileApp: Возврат текстовых и медиа материалов
deactivate ViewModel

MobileApp --> Tourist: Показ точки маршрута


Tourist -> MobileApp: Посмотреть дополненную реальность
MobileApp -> ARComponent: Запрос данных для ar

activate ARComponent
ARComponent -> ViewModel: Запрос данных для ar

activate ViewModel
ViewModel -> Model:Запрос данных для ar

activate Model
Model -> Server: Запрос данных для ar

activate Server
Server --> Model: Возврат данных для ar
deactivate Server

Model --> ViewModel: Возврат данных для ar
deactivate Model

ViewModel --> ARComponent: Возврат данных для ar
deactivate ViewModel

ARComponent --> MobileApp: Возврат данных для ar
deactivate ARComponent

MobileApp --> Tourist: Показ дополненной реальности


Tourist -> MobileApp: Закрытие приложения
@enduml
```

Краткие пояснения к предоставленной диаграмме последовательности:

1. **Открытие приложения:**  
   - Турист открывает мобильное приложение
  
2. **Просмотр маршрута:**
   - Турист запрашивает просмотр маршрута на `Карта`
   - `Карта` отправляет запрос на данные маршрута
   - `ViewModel` запрашивает данные маршрута у `Model`
   - `Model` обращается к серверу `Сервер` для получения данных маршрута
   - `Сервер` возвращает данные маршрута `Model`
   - `Model` передает данные маршрута `ViewModel`
   - `ViewModel` передает данные маршрута `Карта`, которое отображает маршрут для туриста

3. **Выбор маршрута и загрузка материалов:**
   - Турист выбирает точку маршрута
   - `Карта` отправляет запрос на текстовые и медиа материалы для выбранного маршрута `ViewModel`
   - `ViewModel` передает запрос на материалы `Model`
   - `Model` обращается к серверу (`Сервер`) для получения материалов
   - `Сервер` возвращает материалы `Model`
   - `Model` передает материалы `ViewModel`
   - `ViewModel` передает материалы `Карта`, которое отображает материалы для выбранной точки

4. **Просмотр дополненной реальности (AR):**
   - Турист переходит к просмотру дополненной реальности
   - Компонент AR (`Дополненная реальность`) запрашивает данные AR, отправляет запрос данных AR `ViewModel`
   - `ViewModel` передает запрос данных AR `Model`
   - `Model` обращается к серверу (`Сервер`) для получения данных AR
   - `Сервер` возвращает данные AR `Model`
   - `Model` передает данные AR `ViewModel`
   - `ViewModel` передает данные AR компоненту AR (`Дополненная реальность`), который отображает дополненную реальность для туриста

5. **Закрытие приложения:**  
   - Турист закрывает мобильное приложение
   
Данная диаграмма демонстрирует взаимодействие между актором (Туристом), контейнером `Клиент туристов`: компонентами `Карта`, `ViewModel`, `Model`, `Дополненная реальность`; контейнером `Сервер` при различных сценариях использования, отражая общий поток данных и запросов в системе.

# Модель базы данных

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/5fcc1a1f-7473-421c-9280-f9b7dda032ab)

Краткое пояснение к модели базы данных:

1. **`User` (Пользователь):**
   - Учетная запись пользователя системы.
   - Может создавать маршруты и связан с маршрутами, которые он создал, если isTurist == false.
2. **`Route` (Маршрут):**
   - Представляет маршрут в системе, который создан пользователем (`User`), у которого isTurist == false.
   - Содержит точки интереса и ссылку на маршрут.
   - Ассоциирован с пользователем, который создал маршрут.
3. **`PointOfInterest` (Точка интереса):**
   - Описывает ключевые места внутри маршрута.
   - Связана с материалами и AR-компонентой.
   - Содержит координаты места.
   - Принадлежит определенному маршруту.
4. **`Material` (Материал):**
   - Представляет собой контент, связанный с точками интереса.
   - Может быть текстом, изображением или видео.
   - Хранится путь на сервере до материала.
   - Привязан к точке интереса.
5. **`ARComponent` (AR-компонента):**
   - Содержит данные для расположения в пространстве в контексте дополненной реальности (AR).
   - Связана с точками интереса.
  
```PlantUML
@startuml
class Route {
  +id: int
  -name: string
  -createdBy: User
  -pointsOfInterest: Set<PointOfInterest>
  -link: string
}

class PointOfInterest {
  +id: int
  -name: string
  -description: string
  -route: Route
  -materials: Set<Material>
  -arComponent: ARComponent
  -latitude: double
  -longitude: double
}

class Material {
  +id: int
  -type: string
  -content: string
  -pointOfInterest: PointOfInterest
}

class User {
  +id: int
  -username: string
  -password: string
  -isTourist: boolean
  -createdRoutes: Set<Route>
}

class ARComponent {
  +id: int
  -name: string
  -positionX: double
  -positionY: double
  -positionZ: double
  -rotationX: double
  -rotationY: double
  -rotationZ: double
}

Route "1" -- "*" PointOfInterest: Contains
PointOfInterest "1" -- "*" Material: Includes
PointOfInterest "1" -- "0..1" ARComponent: HasARComponent
User "1" -- "*" Route: Created
@enduml
```

# Код с учетом принципов KISS, YAGNI, DRY и SOLID.
```Swift
import UIKit

protocol Service {
    associatedtype T
    var data: T { get set }
    
    func fetchData(id: Any, completion: @escaping (T?, Error?) -> Void)
}

struct Route {
    // Реализация структуры согласно бд
}

struct PointOfInterest {
    // Реализация структуры согласно бд
}

class RouteService: Service {
    typealias T = [Route]
    var data: [Route] = []
    
    func fetchData(id: Any, completion: @escaping ([Route]?, Error?) -> Void) {
        // Логика получения маршрута
        // ...
        
        // В случае успеха
        completion(data, nil)
        
        // В случае ошибки
        completion(nil, error)
    }
}

class PointOfInterestService: Service {
    typealias T = [PointOfInterest]
    var data: [PointOfInterest] = []
    
    func fetchData(id: Any, completion: @escaping ([PointOfInterest]?, Error?) -> Void) {
        // Логика получения точек интереса для конкретного маршрута
        // ...
        
        // В случае успеха
        completion(data, nil)
        
        // В случае ошибки
        completion(nil, error)
    }
}

class MainViewControler: UIViewController {
    
    var service: (any Service)?
    let link = "http://url.com/route"
    let routeId = 123
    
    func getRoute() {
        service = RouteService()
        
        // Получение маршрута
        service?.fetchData(id: link) { (routes, error) in
            if let routes = routes {
                // Обработка маршрута
            } else if let error = error {
                // Обработка ошибки
            }
        }
    }
    
    func getPointsOfInterest() {
        service = PointOfInterestService()
        
        // Получение точек интереса для конкретного маршрута
        service?.fetchData(id: routeId) { (pointsOfInterest, error) in
            if let pointsOfInterest = pointsOfInterest {
                // Обработка точек интереса
            } else if let error = error {
                // Обработка ошибки
            }
        }
    }
}
```
* **Принцип KISS (Keep It Simple, Stupid):**  
   Классы `RouteService` и `PointOfInterestService` предоставляют простые методы для получения маршрутов и точек интереса соответственно. Они скрывают сложность внутренней реализации, обеспечивая клиентскому коду простоту взаимодействия.  
* **Принцип единственной ответственности (SOLID):**  
   * S: Каждый из этих классов имеет одну основную ответственность - предоставление данных о маршрутах или точках интереса. Это облегчает поддержку, расширение и изменение кода.
   * O: Используем протокол `Service`, который позволяет добавлять новые переменные и методы, не изменяя существующий код.
   * L: Наследование не используется, не продемонстровано. Swift, на котором пишу код, больше не про ООП, а протокольно-ориентированный. 
   * I: В данном коде нет классов-клиентов, которые нереализовывали бы какие-либо методы протоколов. Все протоколы содержат лишь необходимые методы.
   * D: Создаём объект типа `Service` и можем ему подсовывать любые сервисы, выполняющие этот протокол.
* **Принцип DRY (Don't Repeat Yourself):**  
  Логика обработки ответа от сервисов вынесена в замыкания обработчиков (`completion`), что позволяет избежать повторения кода при обработке результатов.
* **Принцип YAGNI (You Aren't Gonna Need It):**  
  Реализована только минимально необходимая функциональность для получения маршрутов и точек интереса. Ненужные функции или избыточные детали отсутствуют. Например, не стали реализовывать удаление маршрутов, сейчас это не требуется и в постановке про это не сказано.

# Другие принципы разработки: 

## BDUF - Big design up front (Масштабное проектирование прежде всего)

**Применимость:** BDUF может быть полезным в случаях, когда требования к проекту хорошо определены и изменения маловероятны. Это позволяет учесть все детали проектирования на ранних этапах и избежать больших изменений в ходе разработки.

**Отказ:** В современной среде разработки, где требования могут меняться, гибкие методологии более предпочтительны. BDUF может быть избыточным и затруднить адаптацию к изменениям, особенно в долгосрочных проектах.

**Проект:** Поскольку проект разрабатывается по методологии водопада, то данный принцип может хорошо подойти. 

## SoC - Separation оf concerns (Принцип разделения ответственности)

**Применимость:** Принцип SoC содействует легкости поддержки, повторному использованию кода и тестированию. Разделение кода на логические компоненты с определенными обязанностями облегчает понимание кода и его модификацию.

**Отказ:** В некоторых случаях (например, в простых проектах) чрезмерное разделение может привести к избыточности кода и усложнению проекта без необходимости.

**Проект:** В целом можно сказать, что он уже используется, поскольку похож на S из SOLID.

## MVP - Minimum viable product (Минимально жизнеспособный продукт)

**Применимость:** Использование MVP позволяет быстро внедрить базовую функциональность продукта и получить обратную связь от пользователей. Это позволяет лучше понять требования и улучшить продукт на ранних этапах.

**Отказ:** В некоторых ситуациях (например, в проектах с высоким техническим риском) может потребоваться более детальное прототипирование или анализ перед разработкой MVP.

**Проект:** В рамках ограниченности времени (проект привязан к графику учебного процесса) может быть применён.

## PoC - Proof of concept (Доказательство концепции)

**Применимость:** PoC полезен, когда необходимо оценить техническую осуществимость или эффективность конкретной концепции перед тем, как начинать полноценную разработку.

**Отказ:** В некоторых ситуациях (например, когда требования к проекту хорошо известны) PoC может быть избыточным, и разработку стоит начинать сразу с основного проекта.

**Проект:** В рамках проекта избыточен, работаем по водопаду, требования хорошо изучены и известны + нет времени оценивать эффективность, из-за сжатых сроков.
