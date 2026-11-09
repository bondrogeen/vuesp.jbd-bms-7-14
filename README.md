# vuesp.jbd-bms-7-14

Мониторинг BMS **JBD / Xiaoxiang** на 7–14 ячеек: напряжение, ток, ёмкости, циклы, температуры и напряжения ячеек в локальном веб-интерфейсе.

Проект собран на базе шаблона [Vuesp](https://github.com/bondrogeen/vuesp): прошивка PlatformIO + web UI на Vue 3 и `vuesp-components`.

## Документация

Подробное описание платы, распиновка, протокол кадров, ScriptRunner и ограничения — в [DOCS.md](./DOCS.md).

## Особенности

- UART 9600 8N1: RX GPIO5, TX GPIO6.
- Запросы `DD A5 03 …` (basic) и `DD A5 04 …` (ячейки), проверка CRC.
- До 14 ячеек, 1–3 NTC, RSOC, циклы и статусы защиты.

## Плата и окружение

- PlatformIO env: `esp32-c3-devkitm-1`
- Прошивка: `platformio.ini`
- Web UI: `vue/`
- Файловая система: LittleFS, веб-сборка попадает в `data/www`

## Сборка

```bash
cd vue
npm ci
npm run build-web
```

Полная сборка (web + прошивка):

```bash
cd vue
npm run build
```

Либо отдельно:

```bash
~/.platformio/penv/bin/pio run
~/.platformio/penv/bin/pio run -t buildfs
```

Прошивка: `build/esp32-c3-devkitm-1/firmware.bin`, FS: `build/esp32-c3-devkitm-1/littlefs.bin`.

## Возможности

- локальный веб-интерфейс без облака;
- настройка Wi-Fi, безопасности, GPIO и файловой системы;
- dashboard с плитками ячеек и температур;
- сценарии и автоматизация;
- обновление прошивки и файловой системы через веб-интерфейс.

## CI

GitHub Actions собирает web UI, прошивку и LittleFS для указанных env, запускает тесты ScriptRunner и публикует артефакты в релиз при пуше тега.

## Version History

### 4.2.0 (2026-11-09)

- Поддержка JBD BMS 7–14S, разбор basic и pack кадров.
- Плитки ячеек, температур и статусов в dashboard.
- Release workflow публикует `esp32-c3-devkitm-1` прошивку и LittleFS.

### 4.0.0 (2026-11-08)

- V4.0 device UI with the shared glass theme and light/dark modes.
- Updated web dependencies and regenerated screenshots.

## Репозиторий

<https://github.com/bondrogeen/vuesp.jbd-bms-7-14>

## Лицензия

MIT — см. [LICENSE](./LICENSE).
