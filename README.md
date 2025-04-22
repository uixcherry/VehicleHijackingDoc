# Forge Vehicle Hijacking

![Version](https://img.shields.io/badge/Version-1.0.0-brightgreen)
![RocketMod](https://img.shields.io/badge/RocketMod-Compatible-blue)
![Unturned](https://img.shields.io/badge/Unturned-3.0+-yellow)

Реалистичная система угона транспортных средств для вашего Unturned сервера. Добавляет игрокам возможность угонять транспортные средства, а полиции - выслеживать и конфисковать их.

## 📋 Содержание

- [Функциональность](#-функциональность)
- [Установка](#-установка)
- [Команды](#-команды)
- [Разрешения](#-разрешения)
- [Конфигурация](#-конфигурация)
- [Механика работы](#-механика-работы)
- [FAQ](#-faq)

## 🚗 Функциональность

- Система миссий по угону транспортных средств
- Полицейские могут получать уведомления о угонах и конфисковать транспорт
- Настраиваемые точки спавна и доставки транспортных средств
- Гибкая система наград за угон
- Маркеры на карте для угонщиков и полицейских
- Реалистичный геймплей с элементами RP

## 💾 Установка

1. Скачайте последнюю версию плагина из [релизов](https://github.com/yourname/Forge.VehicleHijacking/releases)
2. Поместите `Forge.VehicleHijacking.dll` в папку `Plugins` вашего RocketMod сервера
3. Перезапустите сервер или используйте команду `/rocket reload`
4. Настройте плагин, используя файл конфигурации `Plugins/Forge.VehicleHijacking/config.xml`
5. Установите точки спавна и доставки с помощью команд `/setpoint`

## 💬 Команды

| Команда | Алиас | Синтаксис | Описание | Разрешение |
|---------|-------|-----------|----------|------------|
| `/hijack` | `/hj` | `/hijack` | Начать миссию по угону транспортного средства | `forge.hijacking.use` |
| `/confiscate` | `/conf` | `/confiscate` | Конфисковать угнанное транспортное средство (нужно находиться рядом) | `forge.hijacking.confiscate` |
| `/setpoint` | `/sp` | `/setpoint <spawn\|delivery> <название>` | Установить точку спавна или доставки на текущей позиции | `forge.hijacking.admin` |
| `/deletepoint` | `/dp` | `/deletepoint <spawn\|delivery> <id>` | Удалить точку по указанному ID | `forge.hijacking.admin` |
| `/listpoints` | `/lp` | `/listpoints <spawn\|delivery\|all>` | Показать список всех точек | `forge.hijacking.admin` |

## 🔒 Разрешения

| Разрешение | Описание |
|------------|----------|
| `forge.hijacking.use` | Доступ к команде `/hijack` для начала миссий по угону |
| `forge.hijacking.confiscate` | Доступ к команде `/confiscate` для конфискации угнанных транспортных средств |
| `forge.hijacking.admin` | Доступ к административным командам плагина (`/setpoint`, `/deletepoint`, `/listpoints`) |
| `hijacking.notification` | Получение уведомлений о начале угона и маркеров на карте (для полиции) |

## ⚙️ Конфигурация

```xml
<?xml version="1.0" encoding="utf-8"?>
<Configuration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Интервал обновления маркеров на карте (в секундах) -->
  <MarkerUpdateInterval>10</MarkerUpdateInterval>
  
  <!-- Задержка между миссиями по угону (в секундах) -->
  <HijackingCooldown>600</HijackingCooldown>
  
  <!-- Разрешения для получения уведомлений о угонах -->
  <NotificationPermissions>
    <string>hijacking.notification</string>
  </NotificationPermissions>
  
  <!-- Разрешения для конфискации транспортных средств -->
  <ConfiscationPermissions>
    <string>hijacking.confiscate</string>
  </ConfiscationPermissions>
  
  <!-- Точки спавна угоняемых транспортных средств -->
  <SpawnLocations>
    <SpawnLocation>
      <Id>1</Id>
      <Name>Автосалон</Name>
      <Position>
        <x>100</x>
        <y>50</y>
        <z>100</z>
      </Position>
      <Rotation>
        <x>0</x>
        <y>0</y>
        <z>0</z>
        <w>1</w>
      </Rotation>
    </SpawnLocation>
  </SpawnLocations>
  
  <!-- Точки доставки угнанных транспортных средств -->
  <DeliveryLocations>
    <DeliveryLocation>
      <Id>1</Id>
      <Name>Гараж скупщика</Name>
      <Position>
        <x>500</x>
        <y>50</y>
        <z>500</z>
      </Position>
    </DeliveryLocation>
  </DeliveryLocations>
  
  <!-- Награды за транспортные средства (ID транспорта и опыт) -->
  <VehicleRewards>
    <VehicleReward>
      <VehicleId>1</VehicleId>
      <ExperienceReward>100</ExperienceReward>
    </VehicleReward>
    <VehicleReward>
      <VehicleId>2</VehicleId>
      <ExperienceReward>200</ExperienceReward>
    </VehicleReward>
  </VehicleRewards>
</Configuration>
```

### Параметры конфигурации

- **MarkerUpdateInterval**: Частота обновления маркеров на карте (в секундах)
- **HijackingCooldown**: Время, которое игрок должен ждать между миссиями по угону (в секундах)
- **NotificationPermissions**: Список разрешений, обладатели которых получают уведомления о угонах
- **ConfiscationPermissions**: Список разрешений для конфискации угнанных транспортных средств
- **SpawnLocations**: Точки спавна транспортных средств для угона
- **DeliveryLocations**: Точки, куда нужно доставлять угнанные транспортные средства
- **VehicleRewards**: ID транспортных средств и награды за их успешную доставку

## 🎮 Механика работы

### Для угонщиков:

1. Используйте команду `/hijack` для получения миссии
2. Следуйте за маркером на карте к транспортному средству
3. Взломайте транспортное средство (стандартный механизм взлома в Unturned)
4. После взлома получите новый маркер с местом доставки
5. Доставьте транспортное средство в указанное место
6. Получите награду за успешную доставку

### Для полиции:

1. При взломе транспортного средства угонщиком, все игроки с разрешением `hijacking.notification` получат оповещение
2. На карте полицейских появится маркер с местоположением угнанного транспортного средства
3. Найдите угнанное транспортное средство и используйте команду `/confiscate`, находясь рядом с ним
4. При успешной конфискации получите половину награды, которую мог бы получить угонщик

## ❓ FAQ

**В: Как добавить новые точки спавна или доставки?**  
О: Используйте команду `/setpoint spawn <название>` или `/setpoint delivery <название>`, находясь в нужном месте.

**В: Как изменить время перезарядки между угонами?**  
О: Измените параметр `HijackingCooldown` в файле конфигурации.

**В: Могут ли другие игроки взаимодействовать с угнанным транспортным средством?**  
О: До взлома - нет, после взлома - только полиция с соответствующими разрешениями может конфисковать его.

**В: Что происходит, если угнанное транспортное средство уничтожается?**  
О: Миссия отменяется, и игрок получает двойное время перезарядки перед следующей миссией.

---

## 📄 Лицензия

Copyright © 2025 Forge Plugins. Все права защищены.

---

Сделано с ❤️ Forge Plugins
