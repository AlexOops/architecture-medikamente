# Классификация данных

## Матрица данных для защиты

| Данные | Чувствительность | Состояние | В чём необходимость защиты | Инструменты защиты |
|---|---|---|---|---|
| ФИО, дата рождения, телефон, email пациента | PII | хранение, передача, использование | Позволяют идентифицировать пациента | TLS, encryption at rest, RBAC, masking, audit log |
| Адрес, место работы/учёбы пациента | PII_EXTENDED | хранение, передача | Повышают ущерб при утечке | encryption at rest, ABAC, data minimization |
| Диагнозы, назначения, хронические заболевания | MEDICAL | хранение, передача, использование | Врачебная тайна, высокий репутационный и юридический риск | encryption at rest, ABAC, audit log, DLP, SIEM |
| Результаты анализов | MEDICAL | передача, хранение | Могут раскрыть состояние здоровья пациента | TLS/mTLS, API Gateway, pseudonymization, audit log |
| Медицинские документы, заключения, сканы | MEDICAL / LEGAL | хранение, архив | Содержат PII и медицинские сведения | encrypted object storage, access control, DLP, retention |
| Договоры, согласия, подписи | LEGAL / PII | хранение, архив | Юридически значимые документы | encryption, versioning, audit log, retention policy |
| Платежи, чеки, статусы оплаты | PAYMENT | хранение, передача | Финансовые и договорные риски | RBAC, TLS, audit log, backup encryption |
| Данные сотрудников, зарплата, кадровые данные | HR | хранение | Конфиденциальные данные персонала | RBAC, encryption, restricted access, audit |
| Учётные записи, роли, группы | IDENTITY | хранение, использование | Захват доступа ко всей системе | IAM, MFA, password policy, secrets rotation |
| Логи приложений | INTERNAL / PII risk | хранение | В логах могут оказаться PII и токены | log masking, secrets scanning, SIEM |
| BI-отчёты и витрины | ANALYTICS | хранение, использование | Возможна повторная идентификация пациента | anonymization, pseudonymization, RBAC, data catalog |
| ML/AI датасеты | ANALYTICS / MEDICAL risk | хранение, использование | Риск обучения на сырых PII/MEDICAL данных | anonymization, synthetic data, lineage, policy checks |
| Резервные копии | BACKUP | хранение, передача | Полная копия критичных данных | backup encryption, immutable backup, access control |
| Секреты, ключи, пароли, API tokens | SECRET | хранение, использование | Компрометация инфраструктуры | Vault/KMS/HSM, rotation, no secrets in repo |

## Классы чувствительности

| Класс | Описание | Примеры | Базовая защита |
|---|---|---|---|
| PUBLIC | Открытые данные | публичное расписание, справочная информация | контроль целостности |
| INTERNAL | Внутренние данные | регламенты, внутренние справочники | RBAC |
| PII | Персональные данные | ФИО, телефон, email | encryption, masking, audit |
| PII_EXTENDED | Расширенные персональные данные | адрес, место работы | encryption, ABAC, minimization |
| MEDICAL | Медицинские данные | диагнозы, анализы, назначения | encryption, ABAC, DLP, SIEM, audit |
| PAYMENT | Платёжные данные | чеки, статусы оплат | RBAC, audit, encryption |
| LEGAL | Юридические документы | договоры, согласия | encryption, retention, audit |
| HR | Данные сотрудников | зарплата, кадровые документы | RBAC, encryption, audit |
| SECRET | Секреты и ключи | пароли, токены, ключи | Vault/KMS/HSM, rotation |

## Классификация по состоянию

| Состояние | Примеры | Риски | Защита |
|---|---|---|---|
| Data at rest | БД, файлы, архивы, backup | кража диска, несанкционированный доступ | encryption at rest, KMS, RBAC, backup encryption |
| Data in transit | API, интеграции, почта, синхронизации | перехват, MITM, подмена | TLS 1.2+, mTLS, VPN, API Gateway |
| Data in use | UI, backend processing, BI notebooks | избыточный доступ, выгрузки, скриншоты | ABAC, masking, DLP, audit |
| Data in logs | backend logs, gateway logs, SIEM | утечка через логи | log masking, token redaction, retention |
| Data in analytics | Data Lake, DWH, ML datasets | повторная идентификация | anonymization, pseudonymization, lineage |
| Data in backup | backup БД и файлов | полная утечка системы | encrypted backup, immutable storage, restricted restore |

## Профиль риска

| Уровень риска | Критерии | Примеры |
|---|---|---|
| Low | Нет PII и medical data | публичные справочники |
| Medium | Внутренние данные без PII | внутренние регламенты |
| High | PII, PAYMENT, LEGAL | договоры, контакты, платежи |
| Critical | MEDICAL, SECRET, полные backup | медкарты, анализы, ключи, резервные копии |
