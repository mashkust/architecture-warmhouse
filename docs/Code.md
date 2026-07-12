```puml
@startuml
title Device Service Code Diagram

skinparam backgroundColor #1E1E1E
skinparam defaultFontColor white
skinparam shadowing false
skinparam titleFontColor white

skinparam class {
    BackgroundColor #2B2B2B
    BorderColor #BFBFBF
    FontColor white
    AttributeFontColor white
    StereotypeFontColor white
}

skinparam ArrowColor #D9D9D9

entity Device <<Entity>>

record DeviceDto <<Record>>
record DeviceCommandDto <<Record>>

class DeviceController <<REST Controller>>
class DeviceService <<Service>> {
  + getDeviceById(id: long): DeviceDto
  + getDevices(): List<DeviceDto>
  + createDevice(device: DeviceDto): DeviceDto
  + sendCommand(id: long, command: DeviceCommandDto): void
}

class DeviceRepository <<Repository>>

DeviceController ..> DeviceDto : returns
DeviceController ..> DeviceCommandDto : receives
DeviceController --> DeviceService : uses

DeviceService ..> DeviceDto : processes
DeviceService ..> DeviceCommandDto : processes
DeviceService --> DeviceRepository : uses

DeviceRepository ..> Device : reads / writes

@enduml

```
