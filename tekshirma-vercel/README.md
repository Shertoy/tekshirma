# Tekshirma — tekshirma.uz

Biznes va klinika auditi dvigateli. Statik sayt: build qadami yo'q, server yo'q, ma'lumotlar bazasi yo'q.
Barcha hisob-kitob brauzerda bajariladi — kiritilgan raqamlar hech qayerga yuborilmaydi.

## Fayllar

```
index.html     — butun sayt (HTML + CSS + JS ichida)
vercel.json    — sarlavhalar va clean URL sozlamalari
robots.txt
sitemap.xml
```

## Vercel'ga joylash (bepul tarif)

### Variant A — brauzer orqali, 2 daqiqa

1. [vercel.com/new](https://vercel.com/new) → **Deploy** → papkani sudrab tashlang.
2. Framework Preset: **Other**. Build Command va Output Directory — bo'sh qoldiring.
3. **Deploy** tugmasini bosing.

### Variant B — GitHub orqali (tavsiya etiladi, keyingi yangilanishlar oson bo'ladi)

1. Yangi GitHub repozitoriy oching va shu papkadagi fayllarni yuklang.
2. Vercel → **Add New → Project** → repozitoriyni tanlang.
3. Framework Preset: **Other**. Boshqa hech narsa o'zgartirmang → **Deploy**.

Keyin `index.html` ni tahrirlab GitHub'ga push qilsangiz, sayt avtomatik yangilanadi.

## tekshirma.uz domenini ulash

1. Vercel loyihasida: **Settings → Domains → Add** → `tekshirma.uz` yozing.
2. Vercel sizga ikkita yozuv beradi. Domen registratoringiz panelida DNS ga qo'shing:

| Turi | Nomi | Qiymati |
|------|------|---------|
| A | `@` | `76.76.21.21` |
| CNAME | `www` | `cname.vercel-dns.com` |

3. `www.tekshirma.uz` ni ham qo'shing va uni asosiy domenga yo'naltiring (Vercel buni o'zi taklif qiladi).
4. DNS tarqalishini kuting — odatda 10 daqiqadan 2 soatgacha. SSL sertifikat avtomatik beriladi.

> Vercel ba'zan A yozuvi uchun boshqa IP ko'rsatishi mumkin. **Har doim Vercel panelidagi qiymatni ishlating**, yuqoridagi jadval faqat namuna.

## Yangilash

`index.html` yagona fayl. Uni tahrirlash uchun ichidagi uchta blok muhim:

| Blok | Qayerda | Nima uchun |
|------|---------|------------|
| `:root{...}` | `<style>` boshida | Ranglar (light va dark rejim tokenlari) |
| `const SRC = {...}` | `<script>` boshida | Manbalar reyestri |
| `const SECTORS`, `const B` | SRC dan keyin | Soha etalonlari va benchmark qiymatlari |

Bozor koeffitsientini o'zgartirish: `const MARKET = { uz: {k:0.12} ...}`.

## Texnik xususiyatlar

- Bitta HTML fayl, ~170 KB. Tashqi kutubxona yo'q.
- Shriftlar Google Fonts'dan yuklanadi; internet bo'lmasa tizim shriftlariga tushadi va sayt baribir ishlaydi.
- Light va dark rejim: tizim sozlamasiga moslashadi, foydalanuvchi tanlovi `localStorage` da saqlanadi.
- Mobil: 390px kenglikda gorizontal siljish yo'q, tugmalar 44px balandlikda, pastda doimiy navigatsiya paneli.
- Chop etish: hisobot sahifasidan to'g'ridan-to'g'ri PDF chiqadi (`@page` va `break-inside` sozlangan).
- Foydalanuvchi ma'lumoti hech qanday serverga yuborilmaydi.
