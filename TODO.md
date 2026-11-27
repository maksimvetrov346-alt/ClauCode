# ClauCode — full workspace acceptance

- [x] Рабочий AI-чат ClauCode на русском языке с аккуратными ответами и лёгким юмором.
- [x] MCP Connector `/mcp` с initialize/tools/list/tools/call.
- [x] `create_project(name, type)` для html/love2d/godot/android-web.
- [x] `write_file`, `edit_file`, `read_file`, `list_files`, `delete_file` с безопасными относительными путями.
- [x] Постоянное серверное хранение в `data/projects`, project manifest, атомарная запись и лимит размера файла.
- [x] `run_check` с HTML/JSON/JavaScript логом.
- [x] tRPC workspace API для мобильного экрана Projects.
- [x] AI tool-calling: чат может вызвать workspace-инструменты и возвращает список фактически выполненных действий.
- [x] Projects UI: реальные проекты, список файлов, Run check и Build APK actions.
- [x] `get_build_status` с persistent JSON build record и полным логом.
- [x] `project_status` со списком проектов и Android toolchain status.
- [x] Smoke test `create_project → write_file → run_check` пройден на HTML clicker.
- [x] Smoke test `build_apk` выполнен честно: returned failed status; APK/link не заявлены.
- [ ] Подключить Android SDK + Gradle build worker; без этого нельзя легитимно выдать APK.
- [ ] Capacitor/WebView packaging, keystore signing, icon, orientation и публичный artifact URL на 24 часа.
- [ ] Полноценный mobile editor с просмотром/редактированием содержимого файлов и live logs.
- [ ] Durable DB/object storage для сохранности проектов между redeploy.
