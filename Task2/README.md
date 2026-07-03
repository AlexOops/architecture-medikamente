# Task2 — Проектирование решения Privacy by Design

## Цель

Спроектировать целевое состояние системы «Медикаменте» с учётом принципов Privacy by Design.

Задание фокусируется на том, какие архитектурные блоки нужно добавить до реализации новых сервисов, чтобы снизить риски утечки, неправомерного доступа и неконтролируемой обработки конфиденциальных данных.

## Что подготовлено

- C4 Context диаграмма целевого состояния.
- Описание новых архитектурных блоков.
- Описание слоя аналитической работы с данными.
- Краткая матрица Privacy by Design механизмов.

## Структура

```text
Task2/
├── README.md
├── architecture_decisions.md
├── privacy_controls.md
└── diagrams/
    ├── medikamente_target_context_c4.puml
    └── pictures/
        └── medikamente_target_context_c4.png
```

## Диаграмма

Исходник:

```text
Task2/diagrams/medikamente_target_context_c4.puml
```

## Ключевые решения

В целевую архитектуру добавлены блоки:

- IAM / SSO;
- Policy Decision Point;
- Data Classification & Tagging;
- Consent Management;
- Data Catalog & Lineage;
- Audit Log;
- DLP;
- SIEM / Monitoring;
- API Gateway;
- Secure Data Platform для аналитики;
- Anonymization / Pseudonymization Service;
- Retention & Deletion Service.

## Основной принцип

Конфиденциальные данные не должны свободно перемещаться между системами.

Любой доступ к данным должен проходить через:

1. идентификацию пользователя или системы;
2. проверку роли и атрибутов;
3. проверку тегов данных;
4. аудит действия;
5. минимизацию состава передаваемых данных.

## Аналитический слой

Для BI, ML и AI выделяется отдельный слой Secure Data Platform.

В него данные попадают только через контролируемый ingestion pipeline:

```text
Source Systems -> Data Classification -> Anonymization/Pseudonymization -> Data Lake -> DWH/Data Marts -> BI/ML/AI
```

В аналитический слой нельзя передавать сырые PII и MEDICAL данные без тегирования, политики доступа и обезличивания.
