# Чекліст перед запуском у продакшн

> **Статус: прототип.** Сайт опубліковано безкоштовно на GitHub Pages —
> <https://royalstudio-ua.github.io/>. Якщо проєкт викуплять і сайт стане
> офіційним сайтом салону, виконайте пункти нижче. Нічого з цього не блокує
> демонстрацію прототипу.

## 1. Доступ і акаунт — найвищий пріоритет

Весь сайт контролюється одним GitHub-акаунтом, тому це головний ризик.

- [ ] Увімкнути двофакторну автентифікацію: <https://github.com/settings/security>
      (краще passkey або застосунок-автентифікатор, не SMS).
- [ ] Перевірити активні сесії та SSH/GPG-ключі, прибрати зайві.
- [ ] Додати другого власника в організацію `royalstudio-ua` (Settings → People),
      щоб сайт не залежав від одного акаунта.
- [ ] Organization settings → Authentication security → *Require two-factor
      authentication*.
- [ ] **Не видаляти й не перейменовувати** організацію `royalstudio-ua` та
      репозиторій `royalstudio-ua.github.io`, поки адреса використовується.
      Інакше ім'я звільняється, і стороння людина може зайняти його й отримати
      **точно таку саму адресу** — готовий майданчик для фішингу від імені салону.
- [ ] Увімкнути в репозиторії Settings → Code security: secret scanning,
      Dependabot alerts (безкоштовно для публічних репозиторіїв).

## 2. Домен

> **Рішення (листопад 2026): поки що без власного домену.** Сайт живе на
> безкоштовному `https://royalstudio-ua.github.io/`, поки проєкт не викуплено.
> Перевірено як вільні: `royalstudio.pp.ua`, `royal-studio.pp.ua`,
> `royalstudiokrasy.pp.ua`. Коли салон викупить сайт — брати `.com.ua`
> (~712 ₴/рік); `.pp.ua` безкоштовний, але делегується лише на 1 рік і потребує
> щорічної активації кодом із SMS. Переїзд на домен займає ~10 хвилин — пункти нижче.

- [ ] Купити домен (наприклад `royalstudio.com.ua`) і ввімкнути в реєстратора
      2FA, блокування перенесення (transfer lock) та автопродовження.
- [ ] Додати файл `CNAME` з доменом, налаштувати DNS (`A`-записи на GitHub Pages
      або `CNAME` → `royalstudio-ua.github.io`).
- [ ] Settings → Pages → Custom domain + *Enforce HTTPS*.
- [ ] Оновити `og:url`, `og:image` і додати `<link rel="canonical">`.
- [ ] У реєстратора ввімкнути DNSSEC, якщо підтримується.
- [ ] **Правило проти захоплення піддомену:** якщо сайт колись переїде з GitHub,
      спочатку приберіть DNS-записи, які вказують на GitHub, і лише потім
      видаляйте репозиторій/Pages.

## 3. Заголовки безпеки

GitHub Pages не дозволяє керувати HTTP-заголовками (CSP, `X-Frame-Options`,
`Referrer-Policy`, `Permissions-Policy`, `X-Content-Type-Options`).

- [ ] Перенести хостинг на Cloudflare Pages або Netlify (безкоштовні тарифи,
      той самий статичний `index.html`) і задати заголовки через `_headers`.
- [ ] Мінімальний набір:

      Content-Security-Policy: default-src 'self'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; img-src 'self' data:; script-src 'self' 'unsafe-inline'; frame-ancestors 'none'; base-uri 'self'; form-action 'self'
      X-Content-Type-Options: nosniff
      Referrer-Policy: strict-origin-when-cross-origin
      Permissions-Policy: geolocation=(), microphone=(), camera=()
      X-Frame-Options: DENY

- [ ] Перевірити результат на <https://securityheaders.com>.
- [ ] Якщо лишаємось на GitHub Pages — додати хоча б `<meta http-equiv=
      "Content-Security-Policy">` і `<meta name="referrer">` (часткова заміна;
      `frame-ancestors` у `<meta>` не працює).

## 4. Приватність і сторонні запити

- [ ] Перенести Cormorant Garamond та Inter у `assets/` (self-host), як уже
      зроблено з Great Vibes — зараз IP відвідувачів іде в Google Fonts.
- [ ] Карту Google Maps вантажити лише після кліку («двоклікове рішення») або
      замінити статичним зображенням із посиланням на Google Maps.
- [ ] Аналітика без cookie (Plausible, Umami) або взагалі без аналітики.
- [ ] Не додавати сторонніх скриптів (чати, пікселі) без потреби.

## 5. Контент і право

- [ ] Відгуки — лише за письмовою згодою клієнтів; імена публікувати за згодою.
- [ ] Фото — переконатися, що права належать салону або фотографу.
- [ ] Замінити всі плейсхолдери (`[ФОТО САЛОНУ]`, `[ФОТО]`, `[Ім’я майстра]`,
      `[ВІДГУК КЛІЄНТА]`, `[ГОДИНИ РОБОТИ]`, `[КАРТА GOOGLE MAPS]` тощо).
- [ ] Перевірити актуальність цін, графіка, адреси й телефону.
- [ ] Якщо з'явиться форма запису — додати сторінку політики конфіденційності
      та захист від спаму.

## 6. Надійність

- [ ] Дзеркало на Cloudflare Pages / Netlify (безкоштовно) — на випадок блокування
      GitHub-акаунта чи збою Pages.
- [ ] Бекап: репозиторій + локальна копія папки `royal-studio/`.
- [ ] Uptime-моніторинг (UptimeRobot, безкоштовний тариф) зі сповіщенням на email.

## 7. Індексація

- [ ] Поки це прототип — за бажанням тимчасово закрити від пошуку:
      `<meta name="robots" content="noindex">`. **Прибрати перед запуском.**
- [ ] Додати `robots.txt` і `sitemap.xml`.
- [ ] Google Search Console: підтвердити домен, надіслати sitemap.
- [ ] Перевірити прев'ю посилання (Telegram/Viber) після зміни `og:`-тегів.

---

*Оновлено: листопад 2026. Цей файл — нагадування, а не блокер: прототип
працює й без цих пунктів.*
