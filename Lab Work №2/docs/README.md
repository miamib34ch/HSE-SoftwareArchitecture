# Диаграмма системного контекста

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/8ef95985-a143-4089-81f7-9bddc226a523)

```PlantUML
@startuml "messagebus"
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
' uncomment the following line and comment the first to use locally
' !include C4_Container.puml

AddElementTag("microService", $shape=EightSidedShape(), $bgColor="CornflowerBlue", $fontColor="white", $legendText="micro service\neight sided")
AddElementTag("storage", $shape=RoundedBoxShape(), $bgColor="lightSkyBlue", $fontColor="white")

SHOW_PERSON_OUTLINE()

Person(tourAgencies, Турфирмы/Экскурсоводы, "Создают маршруты и делятся ими с туристами")
Person(tourist, Туристы, "Получают маршруты и просматривают их")
Container(c1, "Система экскурсий с дополненной реальностью", "System")
Container_Ext(link, "Сторонняя система создания ссылок", "System", "Сторонняя система позволящая создавать ссылки и qr-коды")
Rel_D(tourAgencies, c1, "Создаёт маршрут, загружает материалы по маршруту, настраивает дополненную реальность, формирует ссылку для маршрута")
Rel_D(c1, link, "Создаёт ссылку на маршрут")
Rel_D(link, c1, "Передаёт ссылку на маршрут")
Rel_D(tourAgencies, tourist, "Передаёт ссылку на маршрут")
Rel_D(tourist, c1, "Открывает ссылку на маршрут, Просматривает маршрут, Просматривает дополненную реальность")

SHOW_LEGEND()
@enduml
```

# Диаграмма контейнеров с пояснениями по выбору базового архитектурного стиля / архитектуры уровня приложений

## Выбор архитектурного стиля:  
Выбранный стиль: Клиент-Серверная архитектура.  
Обоснование:  
* **Мобильная ориентация:** Клиент-Серверная архитектура подходит для мобильных приложений, где мобильные клиенты взаимодействуют с центральным сервером для получения данных и обновлений.
* **Управление данными на сервере:** Так как необходимо управлять маршрутами и материалами экскурсоводов, центральный сервер является естественным местом для хранения и обработки этих данных.
* **Обновления в реальном времени:** Клиент-Серверная архитектура обеспечивает эффективный механизм для обновления/получения данных в реальном времени, что важно для туристов во время маршрута.
* **Простота масштабирования:** Этот стиль облегчает масштабирование системы, так как сервер может быть масштабирован отдельно от клиентов.

## Выбор архитектуры уровня приложений: 
Выбранная архитектура: MVVM (Model-View-ViewModel).  
Обоснование:
* **Сложность пользовательского интерфейса:** MVVM обеспечивает четкое разделение данных и логики отображения, что особенно полезно для приложения, где могут быть сложные пользовательские интерфейсы с множеством взаимодействующих элементов.
* **Связывание данных:** MVVM обладает механизмами для эффективного связывания данных между пользовательским интерфейсом и данными, что важно для отображения материалов экскурсовода и маршрутов туриста.
* **Тестируемость:** MVVM упрощает тестирование, так как бизнес-логика лежит в ViewModel, которую можно тестировать независимо от пользовательского интерфейса.
* **Поддержка адаптации интерфейса:** Эта архитектура позволяет легко адаптировать пользовательский интерфейс под разные разрешения экранов, что важно для поддержки разных устройств iOS.

## Диаграмма контейнеров

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/4da868e7-ac45-4c44-b14f-b9cf9d5c0092)

```PlantUML
@startuml "messagebus"
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
' uncomment the following line and comment the first to use locally
' !include C4_Container.puml

AddElementTag("microService", $shape=EightSidedShape(), $bgColor="CornflowerBlue", $fontColor="white", $legendText="micro service\neight sided")
AddElementTag("storage", $shape=RoundedBoxShape(), $bgColor="lightSkyBlue", $fontColor="white")

SHOW_PERSON_OUTLINE()

Person(tourAgencies, Турфирмы/Экскурсоводы, "Создают маршруты и делятся ими с туристами")
Person(tourist, Туристы, "Получают маршруты и просматривают их")
System_Boundary(c1, "Система экскурсий с дополненной реальностью") {
    Container(clientTourAgencies, "Клиент экскурсоводов", "iOS, Swift", "Позволяет создавать маршруты и отправлять их туристам")
    Container(clientTourist, "Клиент туристов", "iOS, Swift", "Позволяет получать маршруты и просматривать их")
    Container(server, "Сервер", "C#, .NET", "Ответственен за обработку и передачу данных")
    ContainerDb(db, "База данных", "Microsoft SQL", "Хранит маршруты и материалы связанные с маршрутами", $sprite="msql_server")
}
Container_Ext(link, "Сторонняя система создания ссылок", "System", "Сторонняя система позволящая создавать ссылки и qr-коды")
Rel_D(tourAgencies, clientTourAgencies, "Создаёт маршрут, загружает материалы по маршруту, настраивает дополненную реальность, формирует ссылку для маршрута")
Rel_D(clientTourAgencies, server, "Получает созданные маршруты с настройками дополненной реальности, загруженные материалы")
Rel_D(server, db, "Сохраняет маршруты и связанные материалы (настройки ar, ссылку, медиа)")
Rel_U(db, server, "Получает сохранённые маршруты и связанные материалы (настройки ar, ссылку, медиа)")
Rel_D(server, link, "Создаёт ссылку на маршрут")
Rel_D(link, server, "Передаёт ссылку на маршрут")
Rel_D(server, clientTourAgencies, "Передаёт ссылку на маршрут")
Rel_D(tourAgencies, tourist, "Передаёт ссылку на маршрут")
Rel_D(tourist, clientTourist, "Открывает ссылку на маршрут, Просматривает маршрут, Просматривает дополненную реальность")
Rel_D(clientTourist, server, "Передаёт ссылку на маршрут")
Rel_D(server, clientTourist, "Получает маршрут и связанные материалы (настройки ar, медиа)")

SHOW_LEGEND()
@enduml
```

# Диаграмма компонентов

## Мобильное приложение туристов 

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/76582c09-d036-4133-9c0d-610f9ea71001)

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

## Мобильное приложение экскурсоводов

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/f265637b-0a63-4d1e-81b4-aad4e03e3d30)

```PlantUML
@startuml "messagebus"
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
' uncomment the following line and comment the first to use locally
' !include C4_Container.puml

AddElementTag("microService", $shape=EightSidedShape(), $bgColor="CornflowerBlue", $fontColor="white", $legendText="micro service\neight sided")
AddElementTag("storage", $shape=RoundedBoxShape(), $bgColor="lightSkyBlue", $fontColor="white")

SHOW_PERSON_OUTLINE()

Person(mt, Турфирмы/Экскурсоводы, "Создают маршруты и делятся ими с туристами")
System(s, "Сервер", "Ответственен за обработку и передачу данных", $type="Container / C#, .NET")
Boundary(c, "Клиент экскурсоводов", "Container / iOS, Swift") {
Container(v, "Карта", "Component: UI View", "Экраны для составления маршрутов. Формы для добавления точек на карте. Интерфейс для загрузки текстовых, изображений и видео материалов.")
Container(vm, "ViewModel", "Component: Controller", "Логика, управляющая данными и взаимодействием с View.")
Container(m, "Model", "Component: Model", "Хранит и передаёт данные о маршрутах и материалах. Обрабатывает запросы от ViewModel.")
Container(ar, "Дополненная реальность", "Component: UI View", "Компонент, реализующий взаимодействие с технологией дополненной реальности. Виртуальное размещение материалов на реальных объектах.")
}
Rel_D(mt, v, "Нажатие кнопок (пользовательское взаимодействие)")
Rel_D(mt, ar, "Нажатие кнопок (пользовательское взаимодействие)")
Rel_D(v, vm, "Отправка пользовательского взаимодействия")
Rel_D(vm, v, "Уведомление об обновлении данных")
BiRel(vm, m, "Получение и обновления данных о маршрутах и материалах")
Rel_D(vm, ar, "Уведомление об обновлении данных")
BiRel(m, s, "Получение и передача данных о маршрутах и материалах")
Rel_D(ar, vm, "Отправка пользовательского взаимодействия")

SHOW_LEGEND()
@enduml
```

## Сервер

![image](https://github.com/miamib34ch/HSE-SoftwareArchitecture/assets/77894393/afaeaff4-96ca-4473-a504-622b965bba51)

```PlantUML
@startuml "messagebus"
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
' uncomment the following line and comment the first to use locally
' !include C4_Container.puml

AddElementTag("microService", $shape=EightSidedShape(), $bgColor="CornflowerBlue", $fontColor="white", $legendText="micro service\neight sided")
AddElementTag("storage", $shape=RoundedBoxShape(), $bgColor="lightSkyBlue", $fontColor="white")

SHOW_PERSON_OUTLINE()

Person(mt, Турфирмы/Экскурсоводы, "Создают маршруты и делятся ими с туристами")
System(s, "Сервер", "Ответственен за обработку и передачу данных", $type="Container / C#, .NET")
Boundary(c, "Клиент экскурсоводов", "Container / iOS, Swift") {
Container(v, "Карта", "Component: UI View", "Экраны для составления маршрутов. Формы для добавления точек на карте. Интерфейс для загрузки текстовых, изображений и видео материалов.")
Container(vm, "ViewModel", "Component: Controller", "Логика, управляющая данными и взаимодействием с View.")
Container(m, "Model", "Component: Model", "Хранит и передаёт данные о маршрутах и материалах. Обрабатывает запросы от ViewModel.")
Container(ar, "Дополненная реальность", "Component: UI View", "Компонент, реализующий взаимодействие с технологией дополненной реальности. Виртуальное размещение материалов на реальных объектах.")
}
Rel_D(mt, v, "Нажатие кнопок (пользовательское взаимодействие)")
Rel_D(mt, ar, "Нажатие кнопок (пользовательское взаимодействие)")
Rel_D(v, vm, "Отправка пользовательского взаимодействия")
Rel_D(vm, v, "Уведомление об обновлении данных")
BiRel(vm, m, "Получение и обновления данных о маршрутах и материалах")
Rel_D(vm, ar, "Уведомление об обновлении данных")
BiRel(m, s, "Получение и передача данных о маршрутах и материалах")
Rel_D(ar, vm, "Отправка пользовательского взаимодействия")

SHOW_LEGEND()
@enduml
```

