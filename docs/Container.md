```puml
@startuml
top to bottom direction
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

LAYOUT_LEFT_RIGHT()

title [Container] Система «Умный дом» — микросервисная архитектура

Person(user, "Пользователь", "Клиент системы «Умный дом»")

System_Ext(devices, "Умные устройства", "Датчики и исполнительные устройства в доме")

System_Boundary(smart_home, "Система «Умный дом»") {

  Container(web_app, "Web application", "React + TypeScript", "Интерфейс пользователей и администраторов")

  Container(api_gateway, "API Gateway", "Nginx", "Единая точка входа и маршрутизация запросов")

Container(user_service, "User Service", "Go", "Регистрация, аутентификация и управление домами")
Container(device_service, "Device Service", "Go", "Реестр устройств, типы устройств и передача команд")
Container(telemetry_service, "Telemetry Service", "Go", "Сбор данных, хранение истории и выдача значений")
Container(scenario_service, "Scenario Service", "Go", "Управление сценариями, проверка условий и инициация действий")

ContainerDb(user_db, "User DB", "PostgreSQL", "Пользователи, дома, учётные данные")
ContainerDb(device_db, "Device DB", "PostgreSQL", "Устройства, типы, настройки")
ContainerDb(telemetry_db, "Telemetry DB", "PostgreSQL", "Текущие значения и история")
ContainerDb(scenario_db, "Scenario DB", "PostgreSQL", "Сценарии, условия, действия")
}

Rel(user, web_app, "Управление домом и устройствами")

Rel(web_app, api_gateway, "Передача запросов", "HTTPS/JSON")

Rel(api_gateway, user_service, "Запросы пользователей и домов", "REST")
Rel(api_gateway, device_service, "Запросы устройств и команд", "REST")
Rel(api_gateway, telemetry_service, "Запросы телеметрии и истории", "REST")
Rel(api_gateway, scenario_service, "Запросы сценариев", "REST")

Rel(user_service, user_db, "Чтение и запись", "SQL")
Rel(device_service, device_db, "Чтение и запись", "SQL")
Rel(telemetry_service, telemetry_db, "Чтение и запись", "SQL")
Rel(scenario_service, scenario_db, "Чтение и запись", "SQL")

Rel(devices, telemetry_service, "Передача данных")
Rel(device_service, devices, "Передача команд")

Rel(scenario_service, telemetry_service, "Получение данных для условий", "gRPC")
Rel(scenario_service, device_service, "Передача команд сценариев", "gRPC")

@enduml


```
