# ClauCode — план full workspace

## Цель
Мобильная command center в стиле Claude Code: чат с AI, который умеет вызывать workspace-инструменты, постоянные проекты и файлы, проверки, MCP Connector для Claude и прозрачный APK build pipeline.

## Реализовано в текущем слое
- `server/_core/projectManager.ts`: постоянный серверный каталог `data/projects`, manifest `.claucode.json`, атомарная запись UTF-8 файлов, лимиты и защита от path traversal.
- MCP `/mcp`: `create_project`, `write_file`, `edit_file`, `read_file`, `list_files`, `delete_file`, `run_check`, `build_apk`, `get_build_status`, `project_status` и совместимый `claucode_chat`.
- tRPC `workspace.*`: тот же контракт для мобильного UI.
- AI chat: модель получает workspace function tools, выполняет до четырёх раундов tool-calling и возвращает `executed` с фактическими результатами.
- Projects UI: серверный список проектов, просмотр файлов, запуск проверки и запуск build с понятным логом.
- `run_check`: базовые HTML/JSON проверки и `node --check` для JS.
- `build_apk`: записывает build record/log и никогда не создаёт фиктивную ссылку. В текущем Sandbox отсутствуют Gradle и Android SDK, поэтому возвращается `android_toolchain_unavailable`-подобная подробная ошибка.

## Архитектура
- `app/(tabs)/` — Expo Router tab shell.
- `app/(tabs)/projects.tsx` — workspace list, files, checks, build action.
- `server/routers.ts` — assistant tool-calling и workspace tRPC API.
- `server/_core/mcp.ts` — Streamable HTTP JSON-RPC endpoint.
- `server/_core/projectManager.ts` — общий безопасный слой операций.
- `server/_core/llm.ts` — OpenAI-compatible LLM client с поддержкой `tool_calls`.

## Контракт APK
Для HTML/android-web нужен отдельный Android build worker с Java, Gradle, Android SDK, keystore, Capacitor/WebView packaging и публикацией артефакта минимум на сутки. До подключения такого worker ClauCode показывает полный failed log и не выдаёт URL.

## Дальнейшие этапы
1. Подключить managed/persistent Android build worker и реализовать Capacitor packaging, signing, icon/orientation и artifact storage.
2. Вынести project metadata/build records в durable DB/object storage для сохранности между redeploy, а не только между перезапусками процесса.
3. Добавить полноценный редактор файлов и live preview в mobile UI.
4. Добавить Git, asset/texture pipeline и 2D/3D generators с отдельными permission limits.

## Дизайн
Выбран Claude Ember / industrial calm: тёплый фон, чёрные поверхности, ember-orange `#F97316`, плотная типографика и моноширинные технические метки. UI остаётся mobile-first и адаптивным.
