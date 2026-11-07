# Маршрутизация для роутера: OpenWrt + SSClash-Go (mihomo)

Профиль mihomo для роутера с [SSClash-Go](https://github.com/zerolabnet/SSClash-Go): российские сайты — напрямую, остальное — через VPN, нейросети — через отдельный узел, выбранный вручную.

**Профиль:** [`router-mihomo.yaml`](router-mihomo.yaml) — шаблон для Remnawave на основе RoscomVPN. Строка `proxies: # LEAVE THIS LINE!` заполняется панелью.

## Группы

| Группа | Что делает |
|---|---|
| 🛡️ VPN | весь зарубежный трафик, по умолчанию ⚡️ Авто (узел с наименьшей задержкой) |
| 🤖 Нейросети | ChatGPT, Claude, Gemini, Copilot, Perplexity, Grok, Cursor и др. — только ручной выбор узла, без РФ |
| 📺 Youtube | YouTube отдельно, можно выбрать свой узел |
| 🎮 Игры | Steam, Epic, Riot, Xbox, Microsoft — по умолчанию без VPN |

Вместе с нейросетями в ту же страну идут их вспомогательные сервисы: капча Cloudflare, аналитика, вход через Google/Apple, оплата Stripe, весь Google и Google Play. Сервис видит один IP и не ругается на регион.

## Настройки SSClash-Go — обязательно

В режиме fake-ip SSClash отправляет в mihomo только трафик на адреса `198.18.x.x` и на IP из fake-ip whitelist. Соединения на настоящие IP идут мимо VPN — с российского адреса. Отсюда «периодически» ломающиеся нейросети. В **Настройках** SSClash-Go включите:

1. **DNS → Firewall redirect** — перехват DNS, «зашитого» в устройство (например `8.8.8.8:53`).
2. **DNS → Block DoT** и **Block known DoH (dibdot)** — Android «Частный DNS», DoH в браузерах и Windows. С устройств в сети перестанут открываться `https://8.8.8.8` и `https://1.1.1.1`.
3. **Options → Drop forwarded IPv6** — IPv6 SSClash не перехватывает.
4. **Options → Kill switch** — без интернета, пока mihomo перезапускается, вместо утечки мимо VPN.

## Если нейросеть снова пишет про регион

До переключения узла откройте на этом устройстве `https://chatgpt.com/cdn-cgi/trace` (или `https://claude.ai/cdn-cgi/trace`) и посмотрите строку `loc=`:

- `loc=RU` — трафик идёт мимо VPN: проверьте настройки выше, DNS и IPv6 на устройстве;
- другая страна, не та, что выбрана в 🤖 Нейросети — домен не попал в правила, его нужно добавить в `ai-extra`;
- нужная страна — дело не в маршруте, а в аккаунте или репутации IP узла.

## Copilot

Вход в аккаунт Microsoft по умолчанию идёт через 🎮 Игры (без VPN). Если пользуетесь Copilot, раскомментируйте в `rules:` три строки `login.microsoftonline.com`, `login.live.com`, `msauth.net` → 🤖 Нейросети.

## Прежняя версия

[`roscomvpn-ssclash-old.yaml`](roscomvpn-ssclash-old.yaml) — первая версия профиля (RoscomVPN + SSClash, с `proxy-providers`).
