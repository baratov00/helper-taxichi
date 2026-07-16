# TaxiChi Admin

Полноценная панель управления TaxiChi: активность водителей, подписки, рефералы, рейтинг, чат, выплаты и живая карта.

## Подключение Supabase

1. Открыть Supabase → SQL Editor и выполнить `supabase/schema.sql`.
2. Установить Supabase CLI и войти в проект.
3. Создать длинный случайный пароль и сохранить его как секрет:
   `supabase secrets set ADMIN_DASHBOARD_TOKEN=ВАШ_ДЛИННЫЙ_СЕКРЕТ`
4. Добавить серверные ключи Яндекс API (значения брать из `TaxiChi5/maps.local.properties`):
   `supabase secrets set YANDEX_GEOCODER_API_KEY=... YANDEX_MATRIX_API_KEY=... YANDEX_ROUTER_API_KEY=...`
   Для тестирования оставить подписку необязательной:
   `supabase secrets set ENFORCE_SUBSCRIPTIONS=false`
   После подключения оплаты заменить значение на `true`.
5. Развернуть функции без проверки Supabase JWT, потому что функции самостоятельно проверяют токен Яндекс ID:
   `supabase functions deploy telemetry --no-verify-jwt`
   `supabase functions deploy admin-stats --no-verify-jwt`
   `supabase functions deploy route-estimate --no-verify-jwt`
   `supabase functions deploy fare-feedback --no-verify-jwt`
6. Опубликовать `index.html`, `app.js`, `styles.css`, `config.js` на любом HTTPS-хостинге либо открыть локально.

## Разделы панели

- Обзор: водители, онлайн, день/неделя/месяц, Premium и выручка.
- Водители: поиск, подписка, рефералы и последняя активность.
- Карта: свежие GPS-точки не старше 10 минут.
- Подписки: покупки и обработка заявок на вывод по СБП.
- Рефералы и ТОП водителей.
- Чат: текст, фото, голосовые и удаление сообщений.
- Система: версии приложения и средняя ошибка прогноза цены.

Никогда не добавляйте `SUPABASE_SERVICE_ROLE_KEY` или `ADMIN_DASHBOARD_TOKEN` в Android-приложение и `config.js`.
