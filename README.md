# 💣 PQ Bomb

<div align="center">
  <h3>
    <a href="#-quick-start">🇬🇧 English</a> 
    &nbsp;|&nbsp; 
    <a href="#-راهنمای-سریع">🇮🇷 فارسی</a>
  </h3>

  ![Status](https://img.shields.io/badge/status-active-success)
  ![Platform](https://img.shields.io/badge/platform-linux-blue)
  ![License](https://img.shields.io/badge/license-MIT-green)
</div>

---

## What is this?

A hardened tunnel script built on top of [paqet](https://github.com/hanselime/paqet). It creates an encrypted raw-socket tunnel between two Linux servers using the KCP protocol — invisible to standard DPI systems.

**Key differences from vanilla paqet:**
- 🛡 **Active Probing Protection** — server only responds to your whitelisted IP, everything else is silently dropped
- 🎲 **Traffic Morphing** — MTU & TCP flags are randomized per encryption key (change key = change fingerprint)
- ⏱ **Anti-Timing** — no predictable restart patterns, exponential backoff on reconnect  
- 📡 **Smart Setup** — auto-detects server resources and suggests optimal config for your user count
- 🌐 **Iran DNS Finder** — auto-benchmarks Iranian DNS servers on client setup
- 🔄 **Mirror Selector** — finds fastest apt mirror for Iran servers

---

## 🚀 Quick Start

Run on **both** servers (Iran + Kharej):

```bash
curl -fsSL https://raw.githubusercontent.com/MasterALiReza/pq-bomb/master/deploy-tunnel.sh -o deploy.sh && chmod +x deploy.sh && sudo ./deploy.sh
```

### Setup in 3 steps:

**1. Kharej (External Server)** → choose `Server` → copy the encryption key  
**2. Iran (Client Server)** → choose `Client` → paste the key + enter Kharej IP  
**3. Done** — SOCKS5 proxy ready at `127.0.0.1:1080`, or use port forwarding

### Example: Port forwarding for Xray

```
Enter port mappings: 443=443, 8443=8443
  ✓ Forward: :443 -> 87.120.106.55:443
  ✓ Forward: :8443 -> 87.120.106.55:8443
```

Now point your Xray inbound to `127.0.0.1:443`.

---

## 🛠 Management

After first run, `paqet` command is available system-wide:

```bash
sudo paqet              # main menu
sudo paqet --status     # tunnel status
sudo paqet --manage     # start/stop/remove tunnels
sudo paqet --update-core # update paqet binary
```

---

## 📊 Smart Configuration

The script detects your server's RAM and CPU, then suggests optimal settings:

```
Smart Configuration (based on server resources):
  RAM: 4096 MB | CPU: 2 cores

  #   Users       Conn  Mode    MTU
  ─── ────────── ───── ─────── ────
  1)  1-50        2     fast    1350
  2)  50-200      3     fast    1350  (Recommended)
  3)  200-500     4     fast2   1280
  4)  500-1000    6     fast2   1280
  5)  1000+       8     fast3   1200
  6)  Custom (set each value manually)
```

---

## 💖 Donate

If this helped you bypass censorship:

**USDT (BEP20 & Polygon):**
```
0xee5219f316878cf531a9a1d638c9f2d85f09c598
```

---

## 📚 Credits

Built by [MasterALiReza](https://github.com/MasterALiReza)  
Based on [ChownYourLife/paqet-tunnel](https://github.com/ChownYourLife/paqet-tunnel)  
Core binary: [hanselime/paqet](https://github.com/hanselime/paqet)

---

<div dir="rtl">

## 🇮🇷 راهنمای سریع

این اسکریپت یک تانل رمزنگاری‌شده بین دو سرور لینوکس (ایران و خارج) ایجاد می‌کند. از Raw Socket و پروتکل KCP استفاده می‌کند و برای مقابله با DPI پیشرفته طراحی شده.

### نصب (روی هر دو سرور):

```bash
curl -fsSL https://raw.githubusercontent.com/MasterALiReza/pq-bomb/master/deploy-tunnel.sh -o deploy.sh && chmod +x deploy.sh && sudo ./deploy.sh
```

### مراحل:

**۱.** روی سرور خارج → گزینه `Server` → کلید رمزنگاری را کپی کنید  
**۲.** روی سرور ایران → گزینه `Client` → کلید و IP سرور خارج را وارد کنید  
**۳.** تمام! پروکسی SOCKS5 روی `127.0.0.1:1080` آماده است

### ویژگی‌های کلیدی:

- تشخیص هوشمند منابع سرور و پیشنهاد تنظیمات بهینه
- محافظت در برابر Active Probing (فقط IP ایران اجازه اتصال دارد)
- تغییر شکل ترافیک بر اساس کلید رمزنگاری
- یافتگر DNS ایران (تست خودکار سرعت DNS های ایرانی)
- یافتگر Mirror (تست سرعت مخازن اوبونتو/دبیان)

### حمایت مالی:

**USDT (شبکه BEP20 و Polygon):**
```
0xee5219f316878cf531a9a1d638c9f2d85f09c598
```

</div>
