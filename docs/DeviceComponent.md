```puml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml

LAYOUT_LEFT_RIGHT()

title [Component] Device Service

Container_Boundary(device_service, "Device Service") {
    Component(device_api, "Device API", "Go / HTTP", "Обработка запросов к устройствам и командам")
    Component(device_registry, "Device Registry", "Go", "Управление устройствами и настройками")
    Component(command_manager, "Command Manager", "Go", "Подготовка и передача команд устройствам")
    Component(device_repository, "Device Repository", "Go / SQL", "Доступ к данным устройств")
}

ContainerDb(device_db, "Device DB", "PostgreSQL", "Устройства, типы, настройки")
System_Ext(devices, "Умные устройства", "Физические устройства")

Rel(device_api, device_registry, "CRUD")
Rel(device_api, command_manager, "Инициация отправки управляющих команд")

Rel(device_registry, device_repository, "Доступ к данным устройств и их конфигурации")
Rel(command_manager, device_repository, "Получение данных устройств и параметров конфигурации")

Rel(command_manager, devices, "Передача управляющих команд устройствам")
Rel(device_repository, device_db, "Чтение и запись", "SQL")

@enduml

```
