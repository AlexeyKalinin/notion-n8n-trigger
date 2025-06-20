# Notion → n8n Trigger

Простые HTML страницы для запуска n8n workflows из Notion через ссылки.

## Использование

### 1. Основная страница (с анимацией)
```
https://alexeykalinin.github.io/notion-n8n-trigger/?param1=value1&param2=value2
```

### 2. Мгновенный триггер (без UI)
```
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?param1=value1&param2=value2
```

### 3. Тестовая страница (простая)
```
https://alexeykalinin.github.io/notion-n8n-trigger/test.html?param1=value1&param2=value2
```

## Примеры для Notion

**Простая ссылка:**
```
https://alexeykalinin.github.io/notion-n8n-trigger/?action=send-email&to=test@mail.com
```

**С формулой Notion:**
```
"https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?id=" + prop("ID") + "&status=" + prop("Status") + "&name=" + prop("Name")
```

**С кодированием русского текста:**
```
"https://alexeykalinin.github.io/notion-n8n-trigger/?task=" + replaceAll(replaceAll(replaceAll(prop("Задача"), " ", "%20"), "а", "%D0%B0"), "я", "%D1%8F")
```

## Как это работает

1. Notion открывает ссылку в браузере
2. JavaScript отправляет GET запрос на n8n webhook
3. Все параметры из URL передаются в n8n в поле `query`
4. Страница закрывается автоматически

## В n8n

Данные приходят в Webhook node в формате:
```json
{
  "query": {
    "param1": "value1",
    "param2": "value2"
  }
}
```

Используйте `{{ $json.query.param1 }}` для доступа к параметрам.