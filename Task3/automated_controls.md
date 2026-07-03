# Автоматизированный контроль данных

## Цель

Обеспечить постоянный контроль за тем, где находятся конфиденциальные данные, кто к ним обращается и как они используются.

## Контроль доступа

| Контроль | Что проверяет | Инструмент |
|---|---|---|
| RBAC | роль пользователя | IAM / SSO |
| ABAC | филиал, пациент, врач, цель доступа | Policy Decision Point |
| Ownership check | пациент видит только свои данные | Backend policy checks |
| MFA | усиленный вход сотрудников | IAM |
| Session control | время жизни сессий | IAM / API Gateway |

## Контроль потоков данных

| Контроль | Что проверяет | Инструмент |
|---|---|---|
| API schema validation | состав request/response | API Gateway |
| Data minimization | отсутствие лишних PII в API | API Gateway / Data contracts |
| mTLS check | доверенность внешней системы | API Gateway |
| Rate limit | аномальная активность API | API Gateway |
| DLP scan | PII/MEDICAL в файлах и почте | DLP |

## Контроль хранения

| Контроль | Что проверяет | Инструмент |
|---|---|---|
| Encryption at rest | шифрование БД и storage | DB/KMS/Object Storage |
| Backup encryption | шифрование резервных копий | Backup system / KMS |
| Access review | кто имеет доступ к данным | IAM / PAM |
| Retention check | срок хранения данных | Retention Service |
| Secrets scan | секреты в репозитории | Git hooks / CI scanner |

## Контроль аналитики

| Контроль | Что проверяет | Инструмент |
|---|---|---|
| Tag validation | наличие тегов у датасета | Data Catalog |
| Lineage check | источник и путь данных | OpenLineage / DataHub |
| Anonymization check | отсутствие прямых идентификаторов | Data Quality checks |
| Dataset policy | можно ли использовать датасет в ML/AI | Policy Engine |
| Export control | выгрузка датасета наружу | DLP / Audit Log |

## Контроль логов и мониторинга

| Контроль | Что проверяет | Инструмент |
|---|---|---|
| Log masking | отсутствие PII в логах | Log processor |
| Token redaction | отсутствие JWT/API tokens в логах | Log processor |
| Audit events | чтение/изменение/экспорт данных | Audit Log |
| Anomaly detection | массовые выгрузки, доступ вне роли | SIEM |
| Alerting | уведомления ИБ-команды | SIEM / Alertmanager |

## События, которые нужно отправлять в SIEM

- вход сотрудника в систему;
- неуспешные попытки входа;
- просмотр медицинской карты;
- изменение медицинской записи;
- выгрузка отчёта;
- массовое скачивание файлов;
- доступ к данным вне филиала;
- попытка доступа к чужому пациенту;
- передача данных во внешнюю систему;
- изменение ролей;
- изменение политик доступа;
- чтение секретов;
- восстановление из backup.

## Автоматические проверки в CI/CD

Перед релизом проверять:

- наличие data tags у новых полей;
- отсутствие PII/MEDICAL в логах;
- отсутствие секретов в коде;
- корректность OpenAPI contracts;
- запрет PII в URL query parameters;
- наличие audit events для операций с PII/MEDICAL;
- наличие policy checks для новых endpoint;
- отсутствие прямого доступа к medical data без PDP.
