```puml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml

LAYOUT_LEFT_RIGHT()

title [Component] Scenario Service

Container_Boundary(scenario_service, "Scenario Service") {
    Component(scenario_api, "Scenario API", "Go / HTTP", "Обработка запросов к сценариям")
    Component(rule_engine, "Rule Engine", "Go", "Проверка условий и запуск действий")
    Component(scenario_repository, "Scenario Repository", "Go / SQL", "Доступ к данным сценариев")
    Component(telemetry_adapter, "Telemetry Adapter", "Go / gRPC", "Получение данных телеметрии")
    Component(device_adapter, "Device Adapter", "Go / gRPC", "Передача команд устройствам")
}

ContainerDb(scenario_db, "Scenario DB", "PostgreSQL", "Сценарии, условия, действия")

Container_Ext(telemetry_service, "Telemetry Service", "Сбор данных и выдача")
Container_Ext(device_service, "Device Service", "Устройства и команды")


Rel(scenario_api, scenario_repository, "CRUD")
Rel(scenario_api, rule_engine, "Инициация выполнения сценариев")

Rel(rule_engine, scenario_repository, "Получение правил, условий и действий сценария")
Rel(rule_engine, telemetry_adapter, "Получение телеметрических данных для проверки условий")
Rel(rule_engine, device_adapter, "Передача команд для выполнения действий сценария")

Rel(scenario_repository, scenario_db, "Чтение и запись", "SQL")
Rel(telemetry_adapter, telemetry_service, "", "gRPC")
Rel(device_adapter, device_service, "", "gRPC")

@enduml

```
