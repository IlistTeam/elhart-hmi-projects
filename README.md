# ELHART HMI Projects

Навык Codex для создания, адаптации и исправления нативных проектов
**ELHART HMI Soft** для панелей ECP. Включает пример ECP-10, безопасное
редактирование XML и проверки состояний, размеров, подписей и числовых полей.

## Установка в Codex

Скопируйте в чат Codex на нужном компьютере:

```text
$skill-installer Установи навык elhart-hmi-projects из https://github.com/IlistTeam/elhart-hmi-projects. SKILL.md находится в корне репозитория; имя устанавливаемого навыка — elhart-hmi-projects. Установи вместе с scripts, references, agents и assets.
```

Репозиторий публичный; доступ к приватному `IlistTeam/Skills` не требуется.
После установки используйте `$elhart-hmi-projects`. Если навык не появился,
перезапустите Codex.

Целевая среда нативных проверок — Windows с установленным ELHART HMI Soft 3.x
и Windows PowerShell 5.1/.NET Framework. Python-инструменты требуют Python 3.10+.
Проверенные версии и особенности формата описаны в
[инструкции навыка](SKILL.md) и [native-format.md](references/native-format.md).
ELHART HMI Soft и библиотеки производителя в этот репозиторий не входят.

## Что входит

- `SKILL.md` — инструкции и выбор рабочего процесса.
- `references/` — формат DTO, логика демо, известные ошибки и способы проверки.
- `scripts/native_xml.py` — XML-редактор с сохранением областей QName.
- `scripts/project_tool.py` — извлечение примера и проверка XML.
- `scripts/validate_native.ps1` — проверки установленными библиотеками Elhart.
- `scripts/slm_checks/` — дополнительные проверки конкретного примера SLM.
- `assets/slm-ecp10-starter.zip` — редактируемый пример 1024×768, пять экранов,
  внутренняя память HMI и обновление демо каждые 100 мс.

## Быстрая проверка

Из корня копии репозитория:

```powershell
python scripts/test_helpers.py
python scripts/project_tool.py starter --out C:\Projects\ElhartDemo --name ElhartDemo
python scripts/project_tool.py xml-check --project C:\Projects\ElhartDemo
powershell.exe -NoProfile -ExecutionPolicy Bypass -File scripts/validate_native.ps1 -ProjectRoot C:\Projects\ElhartDemo
```

Для извлечения выберите новую папку: существующий проект не перезаписывается.
Проверка нативного формата требует Elhart. Тесты системных настроек и порядка
полей кнопок: `scripts/test_system_validation.py` и
`scripts/test_control_validation.py`. Подробнее — [verification.md](references/verification.md).

Пример SLM использует демонстрационную карту регистров и свои блокировки;
это не схема подключения произвольного оборудования. Он содержит известное
ограничение точности дробной части таймера, описанное в
[demo-runtime.md](references/demo-runtime.md).
Проверки XML, DTO и макроса не заменяют полную компиляцию проекта и проверку
в симуляторе целевой версии. Подробности примера — [slm-example.md](references/slm-example.md).

## Основное место разработки

Этот репозиторий — основное место разработки `elhart-hmi-projects`.
Навык выделен из приватного каталога `IlistTeam/Skills`; другие навыки и история
исходного репозитория сюда не перенесены.
