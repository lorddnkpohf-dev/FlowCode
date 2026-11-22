# FlowCode

[Русский](#русский) | [English](#english)

FlowCode — настольный AI-агент для разработки. Он работает с выбранной папкой проекта: читает и редактирует файлы, выполняет команды, запускает проверки и подключается к дополнительным инструментам.

## Русский

### Возможности

- Подключение моделей Kilo, Moonshot/Kimi, Ollama, LM Studio, OpenRouter и совместимых API.
- Работа с локальными моделями через Ollama и LM Studio.
- Редактирование файлов, запуск команд, поиск по проекту и проверка изменений.
- Кнопка **Test & fix** для поиска ошибок, исправления и повторного запуска проверок.
- Три стиля системного промпта: **Safe**, **Normal** и **Anti**.
- Поддержка MCP-серверов, плагинов и мастер-промптов `.Flow`.
- Дополнительный SuperGram-плагин для работы с Telegram.
- Управление с телефона по локальной сети.

### Запуск для авторизованных разработчиков

FlowCode — закрытый проприетарный проект. Исходный код доступен только лицам, которым владелец проекта предоставил доступ. Не клонируйте публичный репозиторий: исходники не распространяются как open source.

Для разработки требуются Windows x64, Node.js и npm. В авторизованной копии проекта выполните:

```powershell
npm ci
npm start
```

Для быстрой smoke-проверки:

```powershell
npm start -- --smoke
```

При первом запуске откройте папку проекта через **Open project folder** и настройте провайдера и модель в **Settings → Model**. Для провайдеров с авторизацией укажите API key. Для Ollama или LM Studio сначала запустите соответствующий локальный сервер.

### Режимы

**Системный промпт**

- **Safe** — более осторожный подход к изменениям и потенциальным побочным эффектам.
- **Normal** — сбалансированный режим по умолчанию.
- **Anti** — прямой и творческий стиль с меньшим количеством лишних отказов.

Режимы меняют инструкции и стиль агента, но не отключают обязательные требования безопасности.

**Подтверждение действий**

- **Ask every time** — агент запрашивает подтверждение для действий, требующих разрешения.
- **Auto approve** и **Full access** — в текущей реализации оба режима пропускают подтверждения для вызовов инструментов и функционально не различаются.

Режим можно переключить в настройках или прямо в строке чата, в том числе во время выполнения. При выборе Auto approve или Full access уже ожидающие подтверждения в текущем запуске разрешаются.

### Сборка Windows EXE

Только для авторизованных разработчиков с доступом к исходному коду:

```powershell
npm ci
npm run build:win
```

Установщик NSIS появится в `dist/FlowCode Setup 0.1.0.exe`. Portable-версия будет в `dist/win-unpacked/FlowCode.exe`. Сборка не подписывается сертификатом разработчика, поэтому Windows может показать предупреждение SmartScreen.

### Мастер-промпт `.Flow`

В **Settings → Master prompt** можно задать инструкции вручную или загрузить `.Flow`-файл. Поддерживаются секции с заголовками `@section`; строки, начинающиеся с `//`, `;` или `#`, считаются комментариями.

### MCP и плагины

MCP-серверы настраиваются в **Settings → MCP tools**. Плагины размещаются в отдельных папках внутри `plugins/` и описываются файлом `plugin.json`.

SuperGram предоставляет инструменты для работы с Telegram. Подключайте аккаунт только на доверенном компьютере и учитывайте, что разрешённые действия могут читать и отправлять сообщения от имени аккаунта.

### Конфиденциальность и безопасность

- Агент получает доступ к выбранной папке и выполняет доступные ему инструменты и команды.
- Запросы и переданный контекст обрабатываются выбранным провайдером модели; ознакомьтесь с его правилами хранения данных.
- API-ключи и настройки сохраняются локально на компьютере. Не добавляйте конфигурацию с секретами в Git.
- Auto approve и Full access отключают подтверждения действий — используйте их осознанно.
- Управление с телефона использует локальный сетевой сервер. Не передавайте ссылку управления посторонним и используйте её только в доверенной сети.

### Лицензия и права

FlowCode не является open-source программой. Исходный код, приложение и связанные материалы являются проприетарными. Этот README не предоставляет лицензию на использование, копирование, изменение или распространение. Для разрешений обратитесь к владельцу проекта.

## English

FlowCode is a desktop AI coding agent. It works with a selected project folder to read and edit files, run commands and checks, and connect to additional tools.

### Features

- Connects to Kilo, Moonshot/Kimi, Ollama, LM Studio, OpenRouter, and compatible APIs.
- Supports local models through Ollama and LM Studio.
- Edits files, runs commands, searches projects, and checks changes.
- **Test & fix** can find issues, apply fixes, and rerun checks.
- Includes three system-prompt styles: **Safe**, **Normal**, and **Anti**.
- Supports MCP servers, plugins, and `.Flow` master prompts.
- Includes the optional SuperGram plugin for Telegram.
- Supports phone control over a local network.

### Running from an authorized checkout

FlowCode is proprietary closed-source software. Source code is available only to people granted access by the project owner. Do not clone a public repository expecting open-source source code.

Development requires Windows x64, Node.js, and npm. From an authorized project checkout, run:

```powershell
npm ci
npm start
```

To run a smoke check:

```powershell
npm start -- --smoke
```

On first launch, open a project folder with **Open project folder** and configure a provider and model under **Settings → Model**. Enter an API key for providers that require authentication. Start the relevant local server before using Ollama or LM Studio.

### Modes

**System prompt**

- **Safe** takes a more cautious approach to changes and potential side effects.
- **Normal** is the balanced default.
- **Anti** uses a more direct, creative style with fewer unnecessary refusals.

These modes change the agent's instructions and style; they do not disable required safety rules.

**Action approvals**

- **Ask every time** asks for approval for actions that require permission.
- **Auto approve** and **Full access** currently both skip approval for tool calls and do not differ functionally.

You can change the mode in Settings or directly in the chat input, including while a task is running. Selecting Auto approve or Full access also resolves approvals already waiting in the current run.

### Building the Windows EXE

For authorized developers with access to the source code only:

```powershell
npm ci
npm run build:win
```

The NSIS installer is generated at `dist/FlowCode Setup 0.1.0.exe`. The portable build is generated at `dist/win-unpacked/FlowCode.exe`. The build is not signed with a developer certificate, so Windows SmartScreen may show a warning.

### `.Flow` master prompt

Use **Settings → Master prompt** to enter instructions or load a `.Flow` file. The parser supports `@section` headers; lines beginning with `//`, `;`, or `#` are treated as comments.

### MCP and plugins

Configure MCP servers in **Settings → MCP tools**. Plugins live in separate folders under `plugins/` and are described by a `plugin.json` file.

SuperGram provides Telegram tools. Connect an account only on a trusted computer and note that permitted actions may read and send messages on that account's behalf.

### Privacy and security

- The agent can access the selected folder and run the tools and commands available to it.
- Prompts and context sent to the model are processed by the selected provider; review that provider's data-retention policies.
- API keys and settings are stored locally. Do not commit configuration containing secrets to Git.
- Auto approve and Full access disable action confirmations; use them carefully.
- Phone control uses a local network server. Do not share its control link and use it only on a trusted network.

### License and rights

FlowCode is not open-source software. Its source code, application, and related materials are proprietary. This README does not grant a license to use, copy, modify, or distribute them. Contact the project owner for permission.