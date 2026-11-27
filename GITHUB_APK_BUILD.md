# Бесплатная сборка APK с телефона

В проект добавлен `.github/workflows/build-apk.yml`. Expo/EAS-аккаунт для этого workflow не нужен.

## Что сделать на телефоне

1. Открой GitHub и создай аккаунт или войди в существующий.
2. Создай новый репозиторий `claucode`. Для самого простого варианта выбери Public.
3. Открой репозиторий → **Add file** → **Upload files**.
4. Распакуй архив проекта на телефоне и загрузи содержимое проекта. Вместе с файлами должен попасть каталог `.github/workflows/build-apk.yml`. Если GitHub не показывает скрытые каталоги, загружай через ZIP всего проекта или включи отображение скрытых файлов.
5. Нажми **Commit changes**.
6. Открой вкладку **Actions** → **Build ClauCode APK** → **Run workflow** → выбери `main` → **Run workflow**.
7. Дождись зелёного статуса. Открой запуск workflow, прокрути вниз до **Artifacts** и скачай `claucode-debug-apk`.
8. Распакуй скачанный архив и установи `app-debug.apk` на Android.

Workflow автоматически устанавливает Java 17, Node.js, pnpm, зависимости Expo, генерирует Android-проект через `expo prebuild` и выполняет `./gradlew assembleDebug`.

Это debug APK: он подходит для установки и проверки на телефоне, но не для публикации в Google Play. Для Play Store позже добавим отдельный release workflow с личным keystore, который нельзя загружать в репозиторий.
