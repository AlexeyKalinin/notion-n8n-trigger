# Notion → n8n Trigger

Простые HTML страницы для запуска n8n workflows из Notion через ссылки.

## Webhook URLs

- **Test**: `https://n8n.wefiftytwo.com/webhook-test/ats-score`
- **Production**: `https://n8n.wefiftytwo.com/webhook/ats-score`

## Использование

### Основная страница (с анимацией)
```
# Test mode (по умолчанию)
https://alexeykalinin.github.io/notion-n8n-trigger/?param1=value1&param2=value2

# Production mode
https://alexeykalinin.github.io/notion-n8n-trigger/?mode=prod&param1=value1&param2=value2

# С отладкой (не закрывает окно)
https://alexeykalinin.github.io/notion-n8n-trigger/?debug=true&param1=value1
```

### Мгновенный триггер (без UI)
```
# Test mode
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?param1=value1

# Production mode  
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?mode=prod&param1=value1
```

## Примеры для Notion

**Простая ссылка (test):**
```
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?action=analyze&doc=resume
```

**Production с параметрами:**
```
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?mode=prod&action=process&id=12345
```

**С формулой Notion:**
```
"https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?mode=prod&id=" + prop("ID") + "&name=" + prop("Name")
```

## Как это работает

1. Страница отправляет запрос тремя способами для надежности:
   - fetch с mode: 'no-cors'
   - Image beacon
   - POST запрос

2. Параметр `mode` определяет какой webhook использовать (test/prod)

3. Все остальные параметры передаются в n8n

## В n8n

Данные приходят в Webhook node:
```json
{
  "query": {
    "param1": "value1",
    "param2": "value2"
  }
}
```

Используйте `{{ $json.query.param1 }}` для доступа к параметрам.

## Отладка

Если webhook не срабатывает:

1. Добавьте `?debug=true` к URL чтобы увидеть какой webhook используется
2. Проверьте что webhook в n8n активен и настроен на GET/POST
3. Проверьте логи n8n для входящих запросов