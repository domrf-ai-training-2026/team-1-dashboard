# Контракт API — команда 1

GET https://domrf-ai-training-2026.github.io/team-1-dashboard/data.json

Все данные вымышлены. Публичный read-only JSON, без ключа. CORS не требуется между проектами одной организации, поскольку их origin одинаков: https://domrf-ai-training-2026.github.io. Для форков на другом origin проверьте CORS в браузере. Не используйте режим no-cors: он не даёт читать JSON.

## Общий формат

schema_version: строка 1.0; team_id: число 1; synthetic: true; updated_at: ISO UTC; units: единицы; records: массив записей. Ключ строки: period + office_id + product.

- period — Неделя до
- office_id — Код офиса
- office — Офис
- city — Город
- product — Продукт
- plan_mln — План, млн ₽ (млн RUB)
- fact_mln — Факт, млн ₽ (млн RUB)

Суммируйте план и факт; выполнение = сумма факта / сумма плана × 100%. Не усредняйте проценты строк.

## Пример чтения

```js
const response = await fetch(API_URL, {cache: 'no-store'});
if (!response.ok) throw new Error('HTTP ' + response.status);
const payload = await response.json();
if (payload.schema_version !== '1.0' || !Array.isArray(payload.records))
  throw new Error('Неверный формат API');
```

Держите видимыми источник, updated_at и время успешного чтения. При ошибке не подменяйте результат нулями и не оставляйте старые цифры без отметки. Публикация коммита и распространение кэша Pages занимают время; проверяйте успешный deploy и updated_at.

## Принимаемый источник

Команда 2: https://domrf-ai-training-2026.github.io/team-2-dashboard/data.json

Сравните выполнение плана с конверсией воронки по офису и неделе.
