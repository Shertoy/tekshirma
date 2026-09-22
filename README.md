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

---

## 1-qadam. Vercel'ga joylash

### Variant A — brauzer orqali (eng tez, 2 daqiqa)

1. [vercel.com](https://vercel.com) → **Sign Up** (GitHub yoki email bilan). Hobby tarifi bepul.
2. [vercel.com/new](https://vercel.com/new) sahifasini oching.
3. **Deploy** maydoniga shu papkani (zip ichidagi fayllarni) sudrab tashlang.
4. Framework Preset: **Other**. Build Command va Output Directory — **bo'sh qoldiring**.
5. **Deploy** tugmasini bosing.

30–60 soniyada sayt `tekshirma-xxxx.vercel.app` manzilida ochiladi.

### Variant B — GitHub orqali (tavsiya etiladi)

Keyingi yangilanishlar avtomatik chiqadi — faylni tahrirlab push qilsangiz kifoya.

1. GitHub'da yangi repozitoriy oching (masalan `tekshirma`).
2. Shu papkadagi fayllarni yuklang.
3. Vercel → **Add New → Project** → repozitoriyni tanlang → **Import**.
4. Framework Preset: **Other**. Boshqa hech narsa o'zgartirmang → **Deploy**.

---

## 2-qadam. tekshirma.uz domenini ulash

### Vercel tomonida

1. Loyihani oching → **Settings** → **Domains** → **Add Domain**.
2. `tekshirma.uz` deb yozing va **Add** bosing.
3. Vercel `www.tekshirma.uz` ni ham qo'shishni taklif qiladi — **rozi bo'ling**.
4. Vercel ekranda kerakli DNS yozuvlarini ko'rsatadi. **Shu ekrandagi qiymatlarni yozib oling** — pastdagi jadval faqat namuna.

### Domen registratori panelida (domenni sotib olgan joyda)

DNS bo'limiga o'ting va ikkita yozuv qo'shing:

| Turi | Nomi (Host) | Qiymati |
|------|-------------|---------|
| **A** | `@` (yoki bo'sh) | `76.76.21.21` |
| **CNAME** | `www` | Vercel ekranidagi qiymat, masalan `d1d4fc829fe7bc7c.vercel-dns-017.com` |

> **Diqqat.** CNAME qiymati endi har bir loyiha uchun alohida bo'ladi. Eski qo'llanmalarda uchraydigan
> umumiy `cname.vercel-dns.com` qiymatini ishlatmang — Vercel panelidagi aniq qiymatni ko'chiring.

### Muqobil yo'l — Vercel nameserverlari

Agar DNS yozuvlari bilan ovora bo'lishni istamasangiz, registrator panelida nameserverlarni Vercel
bergan qiymatlarga almashtiring. Shunda barcha DNS'ni Vercel boshqaradi.

Bu yo'lni tanlasangiz, eski DNS provayderidagi saqlab qolmoqchi bo'lgan yozuvlarni (masalan pochta
uchun MX) Vercel'ga qo'lda ko'chirish kerak.

### Kutish

DNS tarqalishi odatda 10 daqiqadan bir necha soatgacha. Vercel panelidagi domen holati o'zi
yangilanadi. SSL sertifikat avtomatik beriladi — hech narsa qilish shart emas.

Tekshirish uchun: `nslookup tekshirma.uz` yoki [dnschecker.org](https://dnschecker.org).

---

## 3-qadam. Saytni yangilash

`index.html` — yagona fayl. Uni tahrirlash uchun ichidagi uchta blok muhim:

| Blok | Qayerda | Nima uchun |
|------|---------|------------|
| `:root{...}` | `<style>` boshida | Barcha ranglar. Chop etish ranglari `@media print` ichida alohida. |
| `const SRC = {...}` | `<script>` boshida | Manbalar reyestri |
| `const SECTORS`, `const B` | SRC dan keyin | Soha etalonlari va benchmark qiymatlari |

Bozor koeffitsientini o'zgartirish: `const MARKET = { uz: {k:0.12} ... }`.
Namuna hisobot ma'lumotlari: `const DEMO = {...}`.

**GitHub orqali joylagan bo'lsangiz:** faylni tahrirlab push qiling — Vercel o'zi qayta joylaydi.
**Sudrab tashlash orqali joylagan bo'lsangiz:** yangi faylni yana sudrab tashlang.

---

## Sahifalar

| Sahifa | Qanday ochiladi | Nima uchun |
|--------|-----------------|------------|
| Audit oqimi | «Auditni boshlash» | 5 bosqichli anketa → hisobot |
| Namuna hisobot | «Namuna hisobot — demo» | O'ylab topilgan raqamlar bilan to'liq hisobot namunasi |
| Ma'lumot yig'ish varaqasi | «Ma'lumot yig'ish varaqasi» | Auditga borishdan oldin chop etiladigan ro'yxat — qaysi raqamni kimdan so'rash |

---

## Texnik xususiyatlar

- Bitta HTML fayl, ~190 KB. Tashqi kutubxona yo'q.
- Shriftlar Google Fonts'dan yuklanadi; internet bo'lmasa tizim shriftlariga tushadi va sayt baribir ishlaydi.
- Yagona to'q dizayn. Chop etishda avtomatik oq qog'ozga aylanadi — hisobotdan va varaqadan to'g'ridan-to'g'ri PDF chiqadi.
- Mobil: 390px kenglikda gorizontal siljish yo'q, tugmalar 44px+, pastda doimiy navigatsiya paneli.
- `prefers-reduced-motion` hurmat qilinadi.
- Foydalanuvchi ma'lumoti hech qanday serverga yuborilmaydi. Brauzerda ham saqlanmaydi.
