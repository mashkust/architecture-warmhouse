```puml
@startuml

entity Device <<Entity>>

record DeviceDto <<Record>>
record DeviceCommandDto <<Record>>
record DeviceSettingsDto <<Record>>

class DeviceController <<REST Controller>>
class DeviceService <<Service>> {
    + getDevices(): List<DeviceDto>
    + getDeviceById(id: int): DeviceDto
    + createDevice(device: DeviceDto): DeviceDto
    + updateDevice(id: int, device: DeviceDto): DeviceDto
    + deleteDevice(id: int): void
    + sendCommand(command: DeviceCommandDto): void
    + updateSettings(id: int, settings: DeviceSettingsDto): void
}

class DeviceRepository <<Repository>>
interface DeviceConnector <<Interface>>

DeviceController ..> DeviceDto : receives / sends
DeviceController ..> DeviceCommandDto : receives
DeviceController ..> DeviceSettingsDto : receives
DeviceController --> DeviceService : uses

DeviceService ..> DeviceDto : processes
DeviceService ..> DeviceCommandDto : processes
DeviceService ..> DeviceSettingsDto : processes
DeviceService --> DeviceRepository : uses
DeviceService --> DeviceConnector : uses

DeviceRepository ..> Device : reads / writes
DeviceConnector ..> DeviceCommandDto : sends
DeviceConnector ..> DeviceSettingsDto : applies

@enduml

```
