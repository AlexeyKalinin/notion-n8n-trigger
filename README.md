# Notion → n8n Trigger

Простые HTML страницы для запуска n8n workflows из Notion через ссылки.

## Webhook URLs

- **Test**: `https://n8n.wefiftytwo.com/webhook-test/ats-score`
- **Production**: `https://n8n.wefiftytwo.com/webhook/ats-score`

## ⚠️ Известные проблемы

1. **Задержка GitHub Pages** - первый запуск может занять 20-30 секунд из-за кэширования
2. **Параметры могут не передаваться** - используйте `simple.html` или `debug.html` для диагностики

## Страницы

### simple.html - Самая простая версия (рекомендуется)
```
https://alexeykalinin.github.io/notion-n8n-trigger/simple.html?name=Alexey&task=Test
```
Использует только image beacon - максимально надежно.

### instant.html - Быстрая версия
```
# Test mode
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?name=Alexey&task=Test

# Production mode  
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?mode=prod&name=Alexey&task=Test
```

### debug.html - Отладочная версия
```
https://alexeykalinin.github.io/notion-n8n-trigger/debug.html?name=Alexey&task=Test
```
Показывает все URL и позволяет тестировать разные методы отправки.

### redirect.html - Прямой редирект
```
https://alexeykalinin.github.io/notion-n8n-trigger/redirect.html?mode=test&name=Alexey&task=Test
```
Делает прямой редирект на webhook URL.

### test.html - Тестирование всех методов
```
https://alexeykalinin.github.io/notion-n8n-trigger/test.html?name=Alexey&task=Test
```

## Если не работает

1. **Используйте `simple.html`** - самый надежный вариант
2. **Откройте `debug.html`** и проверьте что URL формируется правильно
3. **Проверьте в n8n**:
   - Webhook активен
   - Принимает GET запросы
   - Смотрите execution history

4. **Попробуйте прямую ссылку** в браузере:
   ```
   https://n8n.wefiftytwo.com/webhook-test/ats-score?test=123
   ```

## Примеры для Notion

**Простая ссылка:**
```
https://alexeykalinin.github.io/notion-n8n-trigger/simple.html?action=analyze&doc=resume
```

**С формулой Notion:**
```
"https://alexeykalinin.github.io/notion-n8n-trigger/simple.html?id=" + prop("ID") + "&name=" + prop("Name")
```

## В n8n

Данные приходят в Webhook node:
```json
{
  "query": {
    "name": "Alexey",
    "task": "Test"
  }
}
```

Используйте `{{ $json.query.name }}` для доступа к параметрам.