# Реестр программных и аппаратных средств защиты данных

## Программные средства

| Средство | Назначение | Какие данные защищает | Этап внедрения |
|---|---|---|---|
| IAM / SSO | единая аутентификация, роли, MFA | все системы | MVP |
| Policy Decision Point | RBAC/ABAC и проверка политик | PII, MEDICAL, PAYMENT | MVP |
| API Gateway | защита API и внешних интеграций | данные в передаче | MVP |
| KMS / Vault | хранение ключей и секретов | SECRET, ключи шифрования | MVP |
| Database Encryption | шифрование данных в БД | PII, MEDICAL, PAYMENT, HR | MVP |
| Encrypted Object Storage | защищённое хранение документов | LEGAL, MEDICAL files | MVP |
| Audit Log Service | журналирование операций | PII, MEDICAL, PAYMENT | MVP |
| SIEM | корреляция событий и алерты | события доступа | MVP |
| DLP | контроль утечек через файлы, почту, выгрузки | PII, MEDICAL, LEGAL | MVP |
| Data Catalog | каталог данных, владельцы, теги | все классы данных | To-Be |
| Data Lineage | путь данных от источника до витрины | analytics datasets | To-Be |
| Anonymization Service | обезличивание данных | BI/ML/AI datasets | To-Be |
| Pseudonymization Service | замена идентификаторов | лаборатория, аналитика | To-Be |
| Retention Service | сроки хранения и удаление | PII, MEDICAL, LEGAL | To-Be |
| Secrets Scanner | поиск секретов в коде | SECRET | MVP |
| Log Masking Processor | очистка логов от PII и токенов | logs | MVP |
| Vulnerability Scanner | поиск уязвимостей | приложения и контейнеры | To-Be |
| Backup System | резервное копирование и restore | все критичные данные | MVP |

## Аппаратные и инфраструктурные средства

| Средство | Назначение | Какие данные защищает | Этап внедрения |
|---|---|---|---|
| HSM | аппаратное хранение критичных ключей | master keys, KMS keys | To-Be |
| Firewall / NGFW | сегментация сети и контроль трафика | все сетевые потоки | MVP |
| VPN | защищённый админский доступ | админские подключения | MVP |
| Isolated Backup Storage | изолированные резервные копии | backup | MVP |
| Immutable Storage | защита backup от изменения | backup | To-Be |
| Disk Encryption | защита физических дисков | data at rest | MVP |
| Network Segmentation | разделение офисной, серверной и гостевой сети | внутренние системы | MVP |
| PAM jump host | контролируемый доступ администраторов | production-системы | To-Be |
| EDR на рабочих станциях | защита endpoint сотрудников | локальные файлы и доступы | To-Be |

## Минимальный набор для первого этапа

Для MVP необходимо внедрить:

1. IAM / SSO + MFA.
2. RBAC для всех сотрудников.
3. ABAC для медицинских данных.
4. TLS для всех API.
5. API Gateway для внешних интеграций.
6. Шифрование БД, файлов и backup.
7. Vault/KMS для секретов и ключей.
8. Audit Log для операций с PII/MEDICAL.
9. DLP для файлового сервера и почты.
10. SIEM для событий доступа и алертов.

## Целевой набор

Для To-Be состояния дополнительно внедрить:

1. Data Catalog.
2. Data Lineage.
3. Anonymization / Pseudonymization Service.
4. Retention & Deletion Service.
5. HSM для критичных ключей.
6. PAM для администраторов.
7. EDR на рабочих станциях.
8. Автоматические policy checks в CI/CD.
