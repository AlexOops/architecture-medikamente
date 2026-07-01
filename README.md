# architecture-medikamente

Проектная работа 10 спринта.

Кейс: компания «Медикаменте».

## Цель проекта

Подготовить архитектурные решения для автоматизации процессов компании «Медикаменте» с учётом:

- защиты конфиденциальных данных и PII;
- соответствия требованиям законодательства РФ;
- масштабирования под рост филиалов, сотрудников и клиентов;
- перехода от Excel/файлового хранения к единой системе управления данными;
- подготовки решений для интеграций, BI/ML/AI и новых клиентских сервисов.

## Структура проекта

```text
architecture-medikamente/
├── Task1/
│   ├── diagrams/
│   └── screenshots/
├── Task2/
│   ├── diagrams/
│   └── screenshots/
├── Task3/
│   ├── diagrams/
│   └── screenshots/
├── docs/
├── scripts/
├── .gitignore
└── README.md
```

## Подход к выполнению заданий

Решение каждого задания будет находиться в отдельной директории:

- `Task1` — решение первого задания;
- `Task2` — решение второго задания;
- `Task3` — решение третьего задания.

Для каждого задания могут быть добавлены:

- `README.md` с описанием решения;
- диаграммы в формате PlantUML;
- сгенерированные PNG-версии диаграмм;
- скриншоты проверок, если они нужны для сдачи.

## Диаграммы

Диаграммы выполняются в формате PlantUML.

Исходные файлы:

```text
*.puml
```

Сгенерированные изображения:

```text
*.png
```

Проверить диаграммы:

```bash
plantuml -checkonly Task1/diagrams/*.puml
```

Сгенерировать PNG:

```bash
plantuml -tpng Task1/diagrams/*.puml
```

Также можно использовать скрипт:

```bash
./scripts/render-puml.sh Task1/diagrams
```

## Инструменты

Для работы нужны:

- Git;
- Docker;
- Docker Compose;
- Java Runtime;
- Graphviz;
- PlantUML.

Проверка окружения:

```bash
docker --version
docker compose version
git --version
java -version
dot -V
plantuml -version
```

## Git workflow

Ветка `main` содержит initial setup проекта.

Рабочая ветка для заданий:

```text
tasks
```

План коммитов:

```text
main
└── chore: initial project setup

tasks
├── task 1 
├── task 2 
└── task 3 
```

Создать рабочую ветку:

```bash
git checkout -b tasks
git push -u origin tasks
```

Коммит задания:

```bash
git status --short
git add Task1
git diff --cached --name-status
git commit -m "feat: add task 1 solution"
git push
```

## Что не коммитить

В репозиторий не должны попадать локальные runtime-данные:

- Docker volumes;
- локальные базы данных;
- логи;
- временные файлы;
- `node_modules`;
- `.env` с секретами;
- IDE-файлы.

Эти файлы и директории должны быть описаны в `.gitignore`.

## Проверка перед сдачей

Перед созданием pull request нужно проверить:

```bash
git status --short
```

Проверить staged-файлы:

```bash
git diff --cached --name-status
```

Проверить диаграммы:

```bash
./scripts/render-puml.sh Task1/diagrams
```

После выполнения заданий на ревью отправляется ссылка на pull request из ветки `tasks`.
