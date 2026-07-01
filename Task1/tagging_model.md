# Модель тегирования данных

## Цель

Ввести единый механизм тегирования данных, чтобы контролировать доступ, хранение, передачу, логирование и использование данных в BI/ML/AI.

## Базовые теги

| Тег | Значение |
|---|---|
| PUBLIC | Не чувствительные данные |
| INTERNAL | Внутренние данные компании |
| PII | Персональные данные |
| PII_EXTENDED | Расширенные персональные данные |
| MEDICAL | Медицинские данные |
| PAYMENT | Платёжные данные |
| LEGAL | Договоры, согласия, подписи |
| HR | Данные сотрудников |
| SECRET | Секреты, ключи, пароли |
| ANONYMIZED | Обезличенные данные |
| PSEUDONYMIZED | Псевдонимизированные данные |

## Дополнительные атрибуты

| Атрибут | Пример |
|---|---|
| data_owner | medical_department |
| system_owner | crm_team |
| region | ru |
| branch_id | msk-01 |
| retention_period | 5y |
| legal_basis | contract / consent / law |
| access_model | RBAC / ABAC |
| masking_required | true / false |
| audit_required | true / false |
| export_allowed | true / false |

## Пример тегирования

```yaml
field: patient.phone
tags:
  - PII
attributes:
  data_owner: reception
  region: ru
  retention_period: 5y
  masking_required: true
  audit_required: true
  export_allowed: false
```

```yaml
field: medical_record.diagnosis
tags:
  - MEDICAL
attributes:
  data_owner: medical_department
  region: ru
  retention_period: 10y
  masking_required: true
  audit_required: true
  export_allowed: false
  access_model: ABAC
```

## Правила использования тегов

1. Данные с тегами `PII`, `PII_EXTENDED`, `MEDICAL`, `PAYMENT`, `LEGAL`, `HR` нельзя передавать без проверки политики доступа.
2. Данные с тегом `MEDICAL` доступны только врачу, связанному с пациентом, и ограниченному набору ролей.
3. Для BI/ML/AI используются только `ANONYMIZED` или `PSEUDONYMIZED` данные.
4. Логи не должны содержать значения полей с тегами `PII` и `MEDICAL`.
5. Экспорт данных разрешён только при `export_allowed: true`.
6. Все операции чтения и выгрузки данных с тегами `PII` и `MEDICAL` должны попадать в audit log.

## Инструменты тегирования

- Data Catalog: OpenMetadata / DataHub.
- Data Lineage: OpenLineage / Marquez.
- DLP: контроль файлового сервера, почты и выгрузок.
- Policy Engine: OPA / собственный PDP.
- Data Quality / Validation: Great Expectations.
- SIEM: сбор событий доступа и алерты.
