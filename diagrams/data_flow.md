# Data Flow Diagram (DFD) — Level 1

На данной диаграмме представлен первый уровень декомпозиции потоков данных системы удаленного доступа. 
Здесь отражены основные функциональные компоненты и их взаимодействие.

```mermaid
graph LR
    User((Пользователь)) -- "1. Запрос доступа (Auth Data)" --> Gateway[VPN Gateway]
    Gateway -- "2. Проверка прав (Request)" --> AD[(Active Directory)]
    AD -- "3. Статус пользователя (Response)" --> Gateway
    Gateway -- "4. Запрос 2-го фактора" --> MFA[MFA Provider]
    MFA -- "5. Подтверждение (Token)" --> Gateway
    Gateway -- "6. Шифрованный туннель" --> Intranet[Внутренняя сеть]
    
    subgraph "DMZ Zone"
    Gateway
    end
    
    subgraph "Internal Zone"
    AD
    Intranet
    end
```
