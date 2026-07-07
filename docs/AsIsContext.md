```puml
@startuml
title Умный дом Диаграмма Контекста (As-Is)

top to bottom direction


!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Context.puml

Person(installer, "Специалист", "Устанавливает\nустройства")

Person(user, "Пользователь")

System(smartHome, "Smart Home System", "Домен 1: Управление устройствами\nДомен 2: Телеметрия")

System_Ext(sensors, "Датчики")

System_Ext(actuators, "Исполнительные устройства", "Реле")

Rel(installer, smartHome, "Регистрация\nустройств")
Rel(installer, sensors, "Установка")
Rel(installer, actuators, "Установка")

Rel(user, smartHome, "Управление\nумным\nдомом")

Rel(smartHome, sensors, "Получение\nпоказаний")
Rel(smartHome, actuators, "Отправка\nкоманд")

@enduml

```
