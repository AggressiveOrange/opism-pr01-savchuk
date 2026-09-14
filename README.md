# Практична робота № 1

**Дисципліна:** Основи побудови інформаційних систем та мереж

**Тема:** Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії


|                                             |                                                                                                           |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Прізвище, ім'я**               | Савчук Костянтин                                                                           |
| **Група**                              | ІПЗ-2.01                                                                                               |
| **Номер варіанта**             | 29                                                                                                        |
| **Домен варіанта**             | nbuv.gov.ua                                                                                               |
| **Середовище виконання** | *Windows*                                                                                                 |
| **Версія curl**                       | *curl 8.4.0 (Windows) libcurl/8.4.0 Schannel WinIDN* |
| **Дата виконання**             | 09.09.2026                                                                                                          |

---

## Частина A. Збір експериментальних даних

### A.1. Запит із діагностичним виводом

**Команда:**

```
curl -v https://nbuv.gov.ua
```

**Вивід:**

```
*   Trying 194.44.11.136:443...
* Connected to nbuv.gov.ua (194.44.11.136) port 443
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* using HTTP/1.1
> GET / HTTP/1.1
> Host: nbuv.gov.ua
> User-Agent: curl/8.4.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Server: nginx/1.30.1
< Date: Mon, 14 Sep 2026 16:23:38 GMT
< Content-Type: text/html; charset=utf-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< X-Powered-By: PHP/5.4.45
< Expires: Sun, 19 Nov 1978 05:00:00 GMT
< Cache-Control: no-cache, must-revalidate
< X-Content-Type-Options: nosniff
< Content-Language: uk
< X-Frame-Options: SAMEORIGIN
< X-Generator: Drupal 7 (http://drupal.org)
< Strict-Transport-Security: max-age=604800
```

---

### A.2. Запит без захисту з'єднання

**Команда:**

```
curl -v http://neverssl.com
```

**Вивід:**

```
*   Trying 34.223.124.45:80...
* Connected to neverssl.com (34.223.124.45) port 80
> GET / HTTP/1.1
> Host: neverssl.com
> User-Agent: curl/8.4.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Date: Mon, 14 Sep 2026 16:26:01 GMT
< Server: Apache/2.4.68 ()
< Upgrade: h2,h2c
< Connection: Upgrade
< Last-Modified: Wed, 29 Jun 2022 00:23:33 GMT
< ETag: "f79-5e28b29d38e93"
< Accept-Ranges: bytes
< Content-Length: 3961
< Vary: Accept-Encoding
< Content-Type: text/html; charset=UTF-8
```

---

### A.3. Запит до служби доменних імен

*Windows: `Resolve-DnsName ВАШ_ДОМЕН`*

**Команда (перше виконання):**

```
Resolve-DnsName nbuv.gov.ua
```

**Вивід:**

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
nbuv.gov.ua                                    A      108   Answer     194.44.11.136

Name      : nbuv.gov.ua
QueryType : NS
TTL       : 28069
Section   : Authority
NameHost  : robin.ns.cloudflare.com


Name      : nbuv.gov.ua
QueryType : NS
TTL       : 28069
Section   : Authority
NameHost  : skip.ns.cloudflare.com

skip.ns.cloudflare.com                         A      85524 Additional 173.245.59.233
skip.ns.cloudflare.com                         A      85524 Additional 108.162.193.233
skip.ns.cloudflare.com                         A      85524 Additional 172.64.33.233
robin.ns.cloudflare.com                        A      17192 Additional 108.162.192.218
                                                      7
robin.ns.cloudflare.com                        A      17192 Additional 172.64.32.218
                                                      7
robin.ns.cloudflare.com                        A      17192 Additional 173.245.58.218
                                                      7
skip.ns.cloudflare.com                         AAAA   85524 Additional 2803:f800:50::6ca2:c1e9
skip.ns.cloudflare.com                         AAAA   85524 Additional 2a06:98c1:50::ac40:21e9
skip.ns.cloudflare.com                         AAAA   85524 Additional 2606:4700:58::adf5:3be9
robin.ns.cloudflare.com                        AAAA   17192 Additional 2803:f800:50::6ca2:c0da
                                                      7
robin.ns.cloudflare.com                        AAAA   17192 Additional 2a06:98c1:50::ac40:20da
                                                      7
robin.ns.cloudflare.com                        AAAA   17192 Additional 2606:4700:50::adf5:3ada
                                                      7
```

**Команда (повторне виконання через 5–7 хвилин):**

```
Resolve-DnsName nbuv.gov.ua
```

**Вивід:**

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
nbuv.gov.ua                                    A      300   Answer     194.44.11.136

Name      : nbuv.gov.ua
QueryType : NS
TTL       : 27808
Section   : Authority
NameHost  : robin.ns.cloudflare.com


Name      : nbuv.gov.ua
QueryType : NS
TTL       : 27808
Section   : Authority
NameHost  : skip.ns.cloudflare.com

skip.ns.cloudflare.com                         A      85263 Additional 172.64.33.233
skip.ns.cloudflare.com                         A      85263 Additional 173.245.59.233
skip.ns.cloudflare.com                         A      85263 Additional 108.162.193.233
robin.ns.cloudflare.com                        A      17166 Additional 172.64.32.218
                                                      6
robin.ns.cloudflare.com                        A      17166 Additional 173.245.58.218
                                                      6
robin.ns.cloudflare.com                        A      17166 Additional 108.162.192.218
                                                      6
skip.ns.cloudflare.com                         AAAA   85263 Additional 2606:4700:58::adf5:3be9
skip.ns.cloudflare.com                         AAAA   85263 Additional 2803:f800:50::6ca2:c1e9
skip.ns.cloudflare.com                         AAAA   85263 Additional 2a06:98c1:50::ac40:21e9
robin.ns.cloudflare.com                        AAAA   17166 Additional 2a06:98c1:50::ac40:20da
                                                      6
robin.ns.cloudflare.com                        AAAA   17166 Additional 2606:4700:50::adf5:3ada
                                                      6
robin.ns.cloudflare.com                        AAAA   17166 Additional 2803:f800:50::6ca2:c0da
                                                      6
```

**Зафіксовані значення:**


| Параметр                        | Перше виконання | Повторне виконання |
| --------------------------------------- | ----------------------------- | ----------------------------------- |
| Час виконання (год:хв) | 12:15                              | 12:20                                    |
| IP-адреса                         | 194.44.11.136                              | 194.44.11.136                                    |
| Значення TTL                    | 108                              | 300                                    |

> Якщо друге значення TTL виявилося більшим за перше — це нормально: кеш резолвера встиг оновитися. Зафіксуйте як є.

---

### A.4. Контрольний ресурс

**Команда:**

```
curl -v https://google.com
```

**Вивід:**

```
*   Trying 142.250.130.102:443...
* Connected to google.com (142.250.130.102) port 443
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* using HTTP/1.1
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/8.4.0
> Accept: */*
>
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-C_3Js-KdWGrv0e2XGCuTMg' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Date: Mon, 14 Sep 2026 16:27:50 GMT
< Expires: Wed, 14 Oct 2026 16:27:50 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
```

---

### A.5. Ресурси з некоректною конфігурацією сертифіката

**Випадок 1**

```
curl -v https://expired.badssl.com
```

```
*   Trying 104.154.89.105:443...
* Connected to expired.badssl.com (104.154.89.105) port 443
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
* Closing connection
* schannel: shutting down SSL/TLS connection with expired.badssl.com port 443
curl: (35) schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
```

**Випадок 2**

```
curl -v https://wrong.host.badssl.com
```

```
*   Trying 104.154.89.105:443...
* Connected to wrong.host.badssl.com (104.154.89.105) port 443
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
* Closing connection
* schannel: shutting down SSL/TLS connection with wrong.host.badssl.com port 443
curl: (60) schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
```

**Випадок 3**

```
curl -v https://self-signed.badssl.com
```

```
*   Trying 104.154.89.105:443...
* Connected to self-signed.badssl.com (104.154.89.105) port 443
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
* Closing connection
* schannel: shutting down SSL/TLS connection with self-signed.badssl.com port 443
curl: (60) schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
```

> Якщо використано альтернативний спосіб із параметром `--resolve` — зазначити це та навести фактичну команду.

---

## Частина B. Власна модель рівнів

**Кількість виділених груп:** 3


| № | Назва групи (власне формулювання) | Рядки виводу, віднесені до групи | Обґрунтування |
|---|-----------------------------------|----------------------------------|---------------|
| 1 | Рівень програмного забезпечення | > GET / HTTP/1.1<br>> Host: nbuv.gov.ua<br>> User-Agent: curl/8.4.0<br>> Accept: */* <br>< Content-Type: text/html; charset=utf-8| Взаємодію програмного забезпечення клієнта із сервером |
| 2 | Рівень захисту | * schannel: disabled automatic use of client certificate<br>schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.<br>* schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.<br><* schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.><br>curl: (60) schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect. | Захищення з'єднання HTTPS/TLS та перевірка цифрових сертифікатів. |
| 3 | Рівень мережевого підключення | * Trying 194.44.11.136:443...<br>Connected to nbuv.gov.ua (194.44.11.136) port 443<br>* Trying 34.223.124.45:80...<br>* Connected to neverssl.com (34.223.124.45) port 80<br>* Connected to google.com (142.250.130.102) port 443 | Встановлення мережевого з'єднання між клієнтом і сервером |

*Групи впорядковано від найближчої до користувача (№ 1) до найближчої до апаратного забезпечення. Зайві рядки вилучити, за потреби — додати.*

**Рядки, які не вдалося віднести до жодної групи:**


| Рядок виводу | Причина утруднення |
| ----------------------- | ----------------------------------- |
|                         |                                     |
|                         |                                     |
|                         |                                     |

---

## Контрольні питання

**1. Скільки рядків діагностичного виводу передує отриманню даних сторінки (завдання A.1)?**
```
24 рядки діагностичного виводу передує отриманню даних сторінки завдання A.1.
```

**2. Які рядки наявні у виводі A.1 і відсутні у виводі A.2? Чим це зумовлено?**
```
У виводі А.1 наявний рядок HTTPS на відміну від виводу А.2 рядок HTTP. Це зумовлено тим, що перший запит здійснюється через захищений порт 443, а в другому — не захищений 80.
```

**3. Звідки у виводі з'явилося значення `443`, якщо його не було вказано в адресі?**
```
Значення `443` це порт, який належить протоколу `https`.
```

**4. Як змінилося значення TTL між двома запитами (A.3)? Що означає це число?**
```
Значення TTL (Time To Live) це час у секундах, протягом якого резолвер може зберігати DNS-запис перед тим, як видалити його. Резолвер це пристрій, який перетворює інформацію у відповідь на запит. Перші п'ять хвилин резолвер віддає дані зі свого швидкого локального кешу. Через п'ять хвилин термін дії кешу закінчується і резолвер змушений знову йти в мережу до авторитетних серверів імен, щоб оновити дані. Це викликає раптове збільшення часу відповіді або сплеск трафіку. Саме тому в завданні А.3 через п'ять хвилин значення резолвера збільшилося втричі.
```

**5. Чим відрізняються між собою три причини помилок із завдання A.5? Сформулювати кожну однією фразою.**

| Випадок | Причина недовіри |
| -------------- | ------------------------------- |
| `expired`      | `дедлайн` |
| `wrong.host`   | `недостовірність` |
| `self-signed`  | `самопідпсаний` |

**6. Три рядки з власних виводів, про які не йшлося на лекції 1:**


| № | Рядок виводу | Джерело (номер завдання) |
| -- | ----------------------- | -------------------------------------------- |
| 1  | Server: nginx/1.30.1 | А.1 |
| 2  | Transfer-Encoding: chunked | А.1 |
| 3  | Strict-Transport-Security: max-age=604800 | А.1 |

*Пояснення до цих рядків не потрібне.*

---

## Висновки

*150–300 слів. Спиратися на власні спостереження, а не на матеріал лекції.*

**D.1. Що виявилося неочевидним або несподіваним**

*В завданні А.1 стало несподіванкою, те що після виконання команди запиту	із	діагностичним	виводом crl у виводі з'явились не лише основні налаштування і параметри доменного імені, а також html розмітка разом з стилями і скриптами з сайту з доменним ім'ям даним за варіантом.*

**D.2. Чому саме така кількість груп у частині B**

*У частині В, на мою думку, буде достатньо трьох груп тому, що створювати більше груп немає необхідності, всі виводи із завдань чітко розділені по своїх категоріях та обґрунтовані базуючись на моїх висновках в ході роботи даної практичної роботи.*

**D.3. Питання, яке залишилося без відповіді**

*Як працює блокування реклами після налаштування на телефоні DNS-сервера dns.AdGuard.com? Чи перенаправляється при цьому трафік через сервер AdGuard?*

---

## Використання штучного інтелекту

*Розділ обов'язковий. Заповнюється незалежно від того, чи використовувався ШІ. Детальні вимоги — у документі «Політика використання технологій штучного інтелекту».*

**Факт використання:** використано *(потрібно залишити)*

**Установлений рівень для цієї роботи:** Р3 — ШІ як співвиконавець

**Фактичний рівень використання:** Р3

### Використані системи


| Система | Версія або модель | Період використання |
| -------------- | -------------------------------- | ------------------------------------- |
| ChatGPT | GPT-5.6 Luna | одне завдання |

### Промпти

*Наводити дослівно, у тому вигляді, у якому запит було надано системі. Переказ не приймається.*


| № | Розділ роботи | Текст промпта |
| -- | ------------------------- | ------------------------- |
| 1  | Частина B. Власна модель рівнів | Як в GitHub інструментом Markdown перенести текст на новий ряд в таблиці? |
| 2  |                           |                           |
| 3  |                           |                           |

### Дії з отриманим результатом


| № промпта | Що перевірено | Що змінено  | Що відхилено і чому |
|---| ------------- | ------------------- | ----------------------------------- |
| 1 | Частина B. Власна модель рівнів     | застосування тегу `<br>` для переносу коду в таблиці на новий ряд | |
| 2 |               |                     |                                     |
| 3 |               |                     |                                     |

### Підтвердження

Підтверджую, що всі наведені в цьому звіті виводи команд отримано мною особисто внаслідок фактичного виконання відповідних дій, а відомості цього розділу є повними та достовірними.

> Виводи `curl`, `dig` та інші артефакти не можуть бути згенеровані. Це стосується будь-якого рівня використання ШІ.

---

## Примітки виконавця

*(необов'язковий розділ: що не спрацювало, які команди довелося змінити, які виникли труднощі)*
