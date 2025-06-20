# Notion → n8n Trigger

Простые HTML страницы для запуска n8n workflows из Notion через ссылки.

## ⚠️ ВАЖНО: Проблема с закрытием окна

**Браузеры отменяют запросы, если окно закрывается слишком быстро!**

## Рекомендуемые страницы

### 1. manual.html - Ручное закрытие (САМЫЙ НАДЕЖНЫЙ)
```
https://alexeykalinin.github.io/notion-n8n-trigger/manual.html?name=Alexey&task=Test
```
✅ Показывает статус и позволяет закрыть окно вручную

### 2. simple.html - Автозакрытие через 2 секунды
```
https://alexeykalinin.github.io/notion-n8n-trigger/simple.html?name=Alexey&task=Test
```
✅ Ждет 2 секунды перед закрытием для гарантии доставки

### 3. instant.html - Быстрое закрытие (1 секунда)
```
https://alexeykalinin.github.io/notion-n8n-trigger/instant.html?name=Alexey&task=Test
```
⚠️ Может не работать если соединение медленное

## Production режим

Добавьте `?mode=prod` для использования production webhook:
```
https://alexeykalinin.github.io/notion-n8n-trigger/manual.html?mode=prod&name=Test
```

## Отключение автозакрытия

Для основной страницы можно отключить автозакрытие:
```
https://alexeykalinin.github.io/notion-n8n-trigger/?autoclose=false&name=Test
```

## Технические детали

Страницы используют три метода отправки для надежности:
1. **navigator.sendBeacon** - переживает закрытие окна
2. **Image beacon** - самый совместимый метод
3. **fetch с keepalive** - современный метод

## Webhook URLs

- **Test**: `https://n8n.wefiftytwo.com/webhook-test/ats-score`
- **Production**: `https://n8n.wefiftytwo.com/webhook/ats-score`

## Примеры для Notion

**Простая ссылка:**
```
https://alexeykalinin.github.io/notion-n8n-trigger/manual.html?action=analyze&doc=resume
```

**С формулой Notion:**
```
"https://alexeykalinin.github.io/notion-n8n-trigger/simple.html?id=" + prop("ID") + "&name=" + prop("Name")
```

## Отладка

### debug.html - Полная диагностика
```
https://alexeykalinin.github.io/notion-n8n-trigger/debug.html?name=Test
```
Позволяет тестировать каждый метод отдельно

### test.html - Автоматический тест всех методов
```
https://alexeykalinin.github.io/notion-n8n-trigger/test.html?name=Test
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

## Решение проблем

1. **Параметры не передаются** → Используйте `manual.html` или `simple.html`
2. **Webhook не срабатывает** → Проверьте что webhook активен в n8n
3. **Большая задержка** → Первый запуск может быть медленным из-за GitHub Pages