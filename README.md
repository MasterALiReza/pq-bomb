# 💣 PQ Bomb (Advanced DPI Evasion Tunnel)

<div align="center">
  <h3>
    <a href="#-معرفی-پروژه-pq-bomb">🇮🇷 راهنمای فارسی</a> 
    &nbsp;&nbsp;|&nbsp;&nbsp; 
    <a href="#-about-pq-bomb">🇬🇧 English Guide</a>
  </h3>
</div>

<div align="center">
  <img src="https://img.shields.io/badge/Status-Active-success" alt="Status">
  <img src="https://img.shields.io/badge/Platform-Linux-blue" alt="Platform">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
</div>

<br>

<div dir="rtl">

## 🌟 معرفی پروژه (PQ Bomb)

پروژه **PQ Bomb** یک راهکار تانلینگ بسیار پیشرفته و به شدت ارتقا یافته است که برای مقابله با سیستم‌های فیلترینگ پیچیده (DPI) طراحی شده است. این سیستم با بهره‌گیری از **Raw Sockets** و پروتکل انتقال **KCP**، ترافیک شما را از لایه‌های معمول سیستم‌عامل مخفی می‌کند و به صورت یک ترافیک نامشخص و امن از سد فایروال‌ها عبور می‌دهد.

سیستم فیلترینگ ایران با استفاده از تحلیل آماری (Statistical Analysis)، فایروال‌های هوشمند، تشخیص الگوهای زمانی (Timing Analysis) و کاوشگرهای فعال (Active Probing) تانل‌های معمول را در کمتر از چند ساعت مسدود می‌کند. **PQ Bomb** دقیقاً برای خنثی کردن تمامی این تکنیک‌ها توسعه یافته است.

### 🛡️ قابلیت‌های پیشرفته و ویژگی‌های کلیدی

- **دور زدن تشخیص هوشمند (DPI Evasion):** عدم استفاده از پروتکل‌های استاندارد TCP/IP در لایه کاربرد و انتقال داده‌ها به صورت خام.
- **تغییر شکل ترافیک (Traffic Morphing):** تصادفی‌سازی داینامیک `MTU` و فلگ‌های `TCP` به گونه‌ای که هرگز دو پکت کاملاً شبیه به هم (Signature) ارسال نشوند. این تغییرات بر اساس کلید رمزنگاری شما انجام می‌شود.
- **محافظت در برابر کاوشگرها (Active Probing Protection):** سرور خارج شما مجهز به یک دیوار آتش قدرتمند می‌شود که **فقط و فقط** به IP سرور ایران شما پاسخ می‌دهد. تمامی درخواست‌های ناشناس و ربات‌های اسکنر سیستم فیلترینگ به صورت کاملاً بی‌صدا مسدود (Drop) می‌شوند تا سرور شما کاملاً نامرئی بماند.
- **تغییر الگوهای زمانی (Anti-Timing Analysis):** حذف ری‌استارت‌های قابل پیش‌بینی (مثل ۳۰ دقیقه یکبار) و استفاده از تاخیرهای فزاینده (Exponential Backoff) برای اتصال مجدد، تا رفتار تانل کاملاً شبیه به یک ترافیک عادی و انسانی به نظر برسد.
- **تولید پورت‌های تصادفی:** جلوگیری از شناسایی پورت‌های پیش‌فرض با اختصاص پورت‌های رندوم (بین 10000 تا 60000) در هنگام نصب.
- **معماری مقیاس‌پذیر برای Load Balancing:** پیکربندی شده برای بافرهای عظیم هسته لینوکس (256MB) و محدودیت اتصال ۲ میلیونی. این تانل به راحتی می‌تواند ترافیک بیش از **۱۰۰۰ کاربر همزمان** را مدیریت کند و انتخابی ایده‌آل برای اتصال به پنل‌های Xray است.

---

## 🚀 آموزش نصب و راه‌اندازی

برای اجرای این تانل به دو سرور مجازی (VPS) نیاز دارید: **سرور ایران (Client)** و **سرور خارج (Server)**.

### گام اول: راه‌اندازی سرور خارج
این دستور را در ترمینال سرور خارج (Kharej) کپی و اجرا کنید:
```bash
curl -fsSL https://raw.githubusercontent.com/MasterALiReza/pq-bomb/master/deploy-tunnel.sh -o deploy.sh && chmod +x deploy.sh && sudo ./deploy.sh
```
1. از منوی باز شده گزینه **Server** را انتخاب کنید.
2. اسکریپت یک پورت تصادفی تولید می‌کند، با زدن دکمه Enter آن را تایید کنید (پورت را یادداشت کنید).
3. **بسیار مهم:** اسکریپت از شما `IP سرور ایران` را می‌خواهد. حتماً آن را وارد کنید تا سپر Active Probing فعال شود.
4. در نهایت یک **Encryption Key (کلید رمزنگاری)** به شما نمایش داده می‌شود. آن را با دقت کپی کنید.

### گام دوم: راه‌اندازی سرور ایران
این دستور را مجدداً روی سرور ایران (Iran) خود اجرا کنید:
1. گزینه **Client** را انتخاب کنید.
2. آی‌پی سرور خارج و پورتی که در مرحله قبل ثبت کردید را وارد کنید.
3. دقیقاً همان **Encryption Key** سرور خارج را وارد کنید.
4. تانل لوکال شما (معمولاً SOCKS5 روی پورت `127.0.0.1:1080`) آماده است! می‌توانید این پورت را به عنوان `Outbound` در پنل Xray خود تنظیم کنید.

---

## 🛠️ دستورات مدیریت تانل

اسکریپت پس از نصب به عنوان یک دستور سیستم در دسترس است. شما می‌توانید در هر زمان از دستور `paqet` استفاده کنید:
```bash
sudo paqet              # باز کردن منوی گرافیکی مدیریت
sudo paqet --status     # مشاهده وضعیت تانل‌های در حال اجرا
sudo paqet --manage     # متوقف کردن یا حذف تانل‌ها
sudo paqet --help       # مشاهده راهنمای دستورات
```

---

## 💖 حمایت مالی (Donation)

اگر این پروژه به شما در دور زدن محدودیت‌ها و داشتن یک اینترنت آزاد کمک کرده است، می‌توانید با دونیت کردن از توسعه آن حمایت کنید. 

**Wallet Address (USDT):**
```text
0xee5219f316878cf531a9a1d638c9f2d85f09c598
```
*(Networks: **BEP20** & **Polygon**)*

سپاس فراوان از حمایت شما! 🙏

---

## 📚 تقدیر و تشکر

- **Created by:** [MasterALiReza](https://github.com/MasterALiReza)
- **Based on original fork by:** [ChownYourLife/paqet-tunnel](https://github.com/ChownYourLife/paqet-tunnel)

</div>

<br><hr><br>

<div dir="ltr">

## 🌟 About PQ Bomb

**PQ Bomb** is a heavily modified, high-security tunneling solution engineered to bypass the most advanced Deep Packet Inspection (DPI) systems and state firewalls. By utilizing **Raw Sockets** combined with the **KCP protocol**, PQ Bomb transmits data entirely outside the operating system's standard TCP/IP stack (`conntrack`), rendering traditional traffic analysis tools useless.

Advanced firewalls aggressively block traditional tunnels through statistical analysis, timing patterns, and active probing. PQ Bomb counters these techniques with state-of-the-art obfuscation methods.

### 🛡️ Core Capabilities & Features

- **Deep Packet Inspection (DPI) Evasion:** Raw socket transmission ensures packets do not follow predictable protocol handshakes.
- **Dynamic Traffic Morphing:** Packet MTU sizes and TCP flags are deterministically randomized based on your unique encryption key. Changing the key entirely morphs the traffic signature.
- **Active Probing Protection:** The server side implements a zero-trust `iptables` firewall. It **only** replies to your specified client IP address. All unsolicited connections and censorship scanner bots are silently dropped, keeping your server completely invisible.
- **Anti-Timing Analysis:** Eradicates predictable `systemd` restart loops (e.g., rigid 30-minute cycles) and implements Exponential Backoff delays for reconnections to mimic human networking behavior.
- **Randomized Port Generation:** Defaults to generating random high ports (10000-60000) during setup to avoid well-known port fingerprinting.
- **High Concurrency for Load Balancing:** Pre-configured with aggressive kernel tuning (256MB buffers, 2M conntrack limit). Optimized to handle **1000+ simultaneous users**, making it the perfect backend tunnel for Xray/V2ray panels.

---

## 🚀 Quick Install (Linux)

You will need two servers: one internal (Client) and one external (Server).

Run the following command on **both** servers:

```bash
curl -fsSL https://raw.githubusercontent.com/MasterALiReza/pq-bomb/master/deploy-tunnel.sh -o deploy.sh && chmod +x deploy.sh && sudo ./deploy.sh
```

**Setup Flow:**
1. **On External Server:** Select `Server` mode. Approve the random port, input your Internal Server's IP (for Active Probing Protection), and copy the generated Encryption Key.
2. **On Internal Server:** Select `Client` mode. Input the External Server's IP and port, paste the exact Encryption Key, and choose your proxy mode (e.g., SOCKS5).
3. Connect your Xray panel to the local SOCKS5 port (default `127.0.0.1:1080`).

---

## 💖 Donate

If you found this project helpful for bypassing censorship, consider supporting the development!

**Wallet Address (USDT):**
```text
0xee5219f316878cf531a9a1d638c9f2d85f09c598
```
*(Networks: **BEP20** & **Polygon**)*

Thank you for your support! 🙏

---

## 📚 Credits

- **Created by:** [MasterALiReza](https://github.com/MasterALiReza)
- **Based on original fork by:** [ChownYourLife/paqet-tunnel](https://github.com/ChownYourLife/paqet-tunnel)

</div>
