# Claude Design — prompt to'plami (web-platform dizayn tizimi asosida)

> Ishlatish tartibi: har Claude Design sessiyasida **avval 0-bo'limdagi bazaviy promptni** yuboring,
> keyin kerakli sahifaning promptini. Natija mavjud frontend (Vue 3 + Quasar) bilan bir xil
> vizual tilda chiqadi — keyin dasturchi uni Quasar komponentlariga o'girishi oson bo'ladi.

---

## 0. BAZAVIY DIZAYN-TIZIM PROMPTI (har sessiyada birinchi yuboriladi)

```
Sen korporativ CRM tizimining UI dizaynerisan. Quyidagi dizayn tizimiga QAT'IY rioya qil —
bu mavjud ishlab turgan mahsulotning tizimi, undan chetga chiqma.

RANGLAR (light theme — asosiy):
- Primary: #2563eb (yorqin ko'k) — asosiy tugmalar, aktiv holatlar, linklar, fokus
- Sahifa foni: #f5f7fa; Karta/panel foni: #ffffff
- Matn: asosiy #1e293b, ikkilamchi #64748b; Chegara: #e2e8f0
- Semantik: muvaffaqiyat #22c55e, xato/o'chirish #e31e24 (brend qizil — FAQAT delete va xatolar),
  ogohlantirish #f59e0b, info #3b82f6
- Secondary/muted ko'k: #6b85a8; Chuqur slate (aksent matnlar/aktiv sidebar): #394769
- Dark rejim (agar so'ralsa): fon #141824, karta #1e2535, matn #f1f5f9/#94a3b8, chegara #2d3748

TIPOGRAFIKA:
- Asosiy shrift: 'Sora', sans-serif (kirill matnlarda 'Noto Sans' fallback)
- Raqamlar/kodlar/statistik qiymatlar: 'JetBrains Mono' monospace
- Jadval sarlavhalari: 14px, weight 600; jadval matni 14px
- Sahifa sarlavhasi: 18-20px semibold; bo'lim sarlavhalari 15-16px semibold
- Kichik yorliqlar (stat label, badge): 11-12.5px, weight 600, ba'zan uppercase + letter-spacing

SHAKL:
- Border-radius: kartalar 12px, tugmalar 8px, umumiy 10px, modallar 16px, chiplar 999px
- Soyalar yumshoq: 0 2px 6px rgba(0,0,0,.05) / 0 4px 12px rgba(0,0,0,.08) / 0 8px 24px rgba(0,0,0,.12)
- Spacing shkalasi: 4 / 8 / 16 / 24 / 32px (baza 16px)

LAYOUT:
- Chapda oq sidebar (kengligi 300px): tepada logo, bo'lim sarlavhalari (kichik, kulrang,
  uppercase), menyu elementlari icon + label (Material Icons), guruhlar ochilib-yopiladi,
  aktiv element #394769 rangda, hover juda yengil kulrang-ko'k fon
- Tepada oq topbar (balandligi 64px, pastki chegarasi nozik): o'ng tomonda til tanlash,
  dark-mode toggle, bildirishnomalar qo'ng'irog'i, foydalanuvchi avatari/menyusi
- Kontent maydoni: 16px padding, fon #f5f7fa

JADVAL NAQSHI (barcha ro'yxat sahifalari shu naqshda):
- Oq karta ichida jadval: flat, bordered, cell separator (barcha katak chegaralari nozik)
- Toolbar (jadval tepasida): chapda sahifa sarlavhasi; o'ngda ketma-ket —
  qidiruv inputi (outlined, dense, 220px, lupa ikonka, placeholder "Qidiruv..."),
  faol filtrlar tugmasi (filter ikonka + qizil badge son bilan),
  ustun sozlamalari tugmasi, yangilash (refresh) tugmasi,
  va PRIMARY "Yaratish" tugmasi (add_circle ikonka, unelevated, #2563eb)
- Amallar ustuni o'ngda sticky (soyali), har qatorda 3 icon-tugma: ko'rish (visibility),
  tahrirlash (edit), o'chirish (delete — qizil)
- Oxirgi amal bajarilgan qator: fon #e3edf7 + chap chetida 3px #2563eb chiziq
- Pastda pagination: sahifa raqamlari + sahifadagi qatorlar soni tanlash
- Status ustunlarida StatusBadge (quyida)

KOMPONENTLAR:
- StatusBadge: pill chip (radius 999px), ichida pulsli rangli nuqta + matn.
  Tonlar: pos (yashil #5bd49a), neg (qizil #ff8a73), warn (sariq #f2c14e), neutral (kulrang).
  Rangli headerlar ustida yarim shaffof oq fon bilan.
- StatStrip: KPI ko'rsatkichlar qatori — har element: kichik uppercase yorliq (icon bilan),
  katta MONO qiymat, ixtiyoriy progress-bar va sub-izoh. Ikki variant: chiziq bilan
  ajratilgan qator (strip) yoki alohida kartalar to'ri (grid).
- Form-modal (AppFormShell naqshi): radius 16px; PRIMARY ko'k header (oq sarlavha + yopish X);
  body — bo'limlarga (section) ajratilgan, har bo'limda 2 ustunli grid: yorliq + input;
  inputlar outlined, balandligi 46px, majburiylar yulduzcha bilan;
  footer: chapda "* majburiy maydonlar" izohi, o'ngda "Bekor qilish" (flat) va
  "Yaratish/Yangilash" (primary, check_circle ikonka). Kengliklar: 820px (oddiy) / 1040px (keng).
- Detail-modal: xuddi shu qobiq, lekin o'qish rejimida — ma'lumotlar yorliq-qiymat juftliklarida.
- Delete-modal: kichik, qizil urg'uli tasdiqlash.
- EmptyState: markazda katta yengil ikonka + izoh matni + (ixtiyoriy) yaratish tugmasi.
- Loading: gears spinner, primary rang.
- Grafiklar: ApexCharts uslubi — yumshoq, primary/semantik ranglarda.

UMUMIY QOIDALAR:
- Til: interfeys matnlari o'zbekcha (tizim 5 tilli, dizaynda o'zbekcha yoz)
- Ikonkalar: Material Icons (outlined uslub)
- Zichlik: korporativ-ixcham (dense), lekin havo bor — 16px ritm
- Hech qanday gradient-og'ir, neon yoki "startup" uslub emas — sokin, professional bank-korporativ til
- Har sahifa responsive: <768px da sticky ustunlar oddiy bo'ladi, toolbar elementlari o'raladi
```

---

## 1. LEAD MODULI

### 1.1 Lead pipeline (kanban ko'rinish)
```
Bazaviy dizayn tizimida "Leadlar — Pipeline" sahifasini chiz.
Toolbar: sarlavha "Leadlar", o'ngda pipeline tanlovchi select (masalan "Asosiy voronka"),
qidiruv, filtr, "Yaratish" primary tugma.
Asosiy maydon: gorizontal kanban — ustunlar pipeline bosqichlari:
"Yangi" → "Aloqa qilindi" → "Taklif yuborildi" → "Muzokara" → "Yutildi" / "Yo'qotildi".
Har ustun tepasida: nom + leadlar soni + umumiy summa (mono shriftda, masalan "84.5 mln UZS").
Lead kartasi (radius 10px, oq, yengil soya): sarlavha (lead nomi), mijoz nomi kichik kulrang,
summa mono qalin, pastda: manba chipi (masalan "Instagram" kichik badge), mas'ul avatari,
sana. Yutilgan ustun kartalarida yashil urg'u, yo'qotilganda kulrang-so'nik.
Kartalar sudralayotgan holatni ham ko'rsat (bitta karta ko'tarilgan, ustun hover holatda).
```

### 1.2 Lead ro'yxati va mijozlar
```
Bazaviy jadval naqshida "Mijozlar" sahifasini chiz. Ustunlar: ID, Mijoz nomi, Turi
(StatusBadge: "Jismoniy" neutral / "Yuridik" pos), Telefon (mono), Region, Mas'ul,
Yaratilgan sana, Amallar (sticky). Bitta qator row-actioned holatda. Toolbar to'liq naqshda.
```

---

## 2. PROJECT MODULI (task management)

### 2.1 Loyihalar ro'yxati
```
Bazaviy jadval naqshida "Loyihalar" sahifasi. Ustunlar: Kod (mono, masalan "CRM"),
Nomi, Shartnomalar soni, A'zolar (avatar stack — 3 ta avatar + "+4"), Ochiq vazifalar,
Status (StatusBadge), Amallar. Toolbarda qo'shimcha: "Arxiv" toggle.
```

### 2.2 Board sahifasi (eng muhim ekran)
```
Bazaviy tizimda loyiha board sahifasini chiz: "Mobil ilova · Development boardi".
Sahifa tepasida board konteksti: loyiha nomi + board tanlovchi tablar
("Development" aktiv, "Maintenance", "+ Board"), o'ngda: sprint indikatori
("Sprint 14 · 5 kun qoldi" — faqat scrum boardda), a'zolar avatar stack,
board sozlamalari tugmasi, "Vazifa qo'shish" primary tugma.
Kanban ustunlari (loyiha statuslaridan): "To Do", "In Progress" (tepasida WIP 4/5 chip),
"Code Review", "QA Testing", "Blocked" (sariq-qizg'ish urg'uli ustun), "Done".
Vazifa kartasi: tepada mono kod "MOB-142" + turi ikonkasi (Story yashil / Bug qizil /
Task ko'k), sarlavha 2 qatorgacha, pastda: priority chip (rangli), baholash badge
(mono "5 pt" yoki "90 min"), assignee avatari, subtask hisobi "2/4".
Blocked ustunidagi kartada qo'shimcha: qizg'ish "blocked" belgisi + sabab tooltip ko'rinishi.
Bitta karta drag holatida. Done ustuni kartalari biroz so'nik.
```

### 2.3 Vazifa detail modali
```
Detail-modal naqshida (keng, 1040px) vazifa sahifasi: "MOB-142 · OAuth integratsiyasi".
Header primary ko'k: mono kod + sarlavha + StatusBadge (status nomi) + yopish X.
Body ikki ustun: chapda (70%) — tavsif bloki, subtasklar ro'yxati (checkbox uslubida,
har birida status badge), izohlar lentasi (avatar + ism + vaqt + matn, oxirida izoh yozish
inputi), faylar qatori (file-preview chiplar). O'ngda (30%) yon panel yorliq-qiymat:
Status (select ko'rinishida), Board, Sprint, Priority (rangli chip), Baholash (mono,
tahrirlanadigan), Assignee (avatar+ism), Watcherlar (avatar stack), Muddat, Teglar (chiplar),
Bog'lanishlar ("relates_to: MOB-99"), Blocker bo'limi (agar bor: sabab matni + hal qiluvchi
issue havolasi qizg'ish kartada). Pastda tarix (history) qismidan 2-3 qator kulrang.
```

### 2.4 Sprint planning (scrum board uchun)
```
"Sprint rejalashtirish" sahifasi: ikki ustunli. Chapda "Backlog" ro'yxati (vazifa qatorlari:
kod, sarlavha, priority, baholash pt), o'ngda "Sprint 15" paneli (sana oralig'i, sig'im
indikatori: "34 / 40 pt" progress-bar bilan, tanlangan vazifalar). Orada sudrash strelkasi.
Tepada StatStrip: "Backlog: 46 vazifa · 182 pt", "O'tgan sprint velocity: 38 pt".
Pastda "Sprintni boshlash" primary tugma.
```

### 2.5 Handover ekrani
```
"Topshirish (Handover)" sahifasi — xodim almashganda vazifalarni o'tkazish.
Tepada ogohlantirish banner (warning rang): "A. Karimov tayinlovi tugadi — 12 ta ochiq
vazifa taqsimlanishi kerak". StatStrip: ochiq vazifalar, jami baholash, kutilayotgan kunlar.
Asosiy jadval: vazifa kodi, sarlavha, status, baholash, "Yangi mas'ul" ustuni — har qatorda
select (default taklif: voris B. Toshev avatari bilan). Tepa o'ngda "Hammasini vorisga"
tezkor tugma + "Tasdiqlash" primary. Bitta qator boshqa a'zoga o'zgartirilgan holatda.
```

---

## 3. SUPPORT MODULI

### 3.1 Ticketlar ro'yxati
```
Bazaviy jadval naqshida "Support so'rovlari". Ustunlar: № (mono), Mavzu, Loyiha,
Mijoz, Priority (rangli chip: low kulrang / medium ko'k / high sariq / critical qizil),
Status (StatusBadge), SLA (qolgan vaqt — mono, muddati yaqinlarida sariq, o'tganlarida
qizil "SLA buzildi"), Operator (avatar+ism), Ochilgan vaqt, Amallar.
Toolbar tepasida StatStrip: "Ochiq: 23", "Bugun yopildi: 17", "SLA xavfda: 3" (neg),
"O'rtacha javob: 14 min".
```

### 3.2 Telegram inbox (operator ish stoli)
```
Uch panelli messenjer ekrani (bazaviy ranglarda):
Chap panel (280px): chatlar ro'yxati — tepada qidiruv va filtr tablar ("Hammasi /
Guruhlar / Shaxsiy / Javobsiz"); har chat qatori: bot/loyiha logosi (dumaloq), nomi,
oxirgi xabar bir qator kulrang, vaqt, o'qilmagan hisoblagich (primary badge).
Markaz: tanlangan chat — tepada header (guruh nomi + loyiha chipi + "Ticket ochish" tugma),
xabarlar lentasi (mijoz xabarlari chapda oq kartalarda, operator javoblari o'ngda och
ko'k #e3edf7 kartalarda, vaqtlar mono kichik), pastda javob yozish paneli (input +
biriktirma + yuborish primary tugma).
O'ng panel (300px): kontekst — mijoz ma'lumoti, loyiha, bog'langan ticketlar ro'yxati
(№ + status badge), oxirgi feedback bahosi (yulduzchalar).
```

---

## 4. CONTRACT MODULI
```
Bazaviy jadval naqshida "Shartnomalar". Ustunlar: № (mono), Mijoz, Mavzu, Summa
(mono, o'ngga tekislangan), Valyuta, Loyiha, Imzolangan sana, Status (StatusBadge:
draft neutral / signed pos / cancelled neg), To'lov holati (mini progress-bar:
"2/4 to'lov"), Amallar.
Detail-modalda qo'shimcha ko'rsat: to'lov jadvali bo'limi (kichik ichki jadval:
muddat, summa, status — muddati o'tganlar qizil), hujjatlar bo'limi (file-preview
kartalar versiya raqami bilan).
```

---

## 5. CALL CENTER MODULI
```
"Qo'ng'iroqlar" sahifasi. Tepada StatStrip grid variantda: "Bugun: 142 qo'ng'iroq",
"Javob berilgan: 96%", "O'rtacha davomiylik: 4:32" (mono), "AI o'rtacha baho: 87".
Jadval: Vaqt (mono), Yo'nalish (ikonka: kiruvchi yashil ↓ / chiquvchi ko'k ↑),
Raqam (mono), Mijoz/Lead, Operator, Davomiylik (mono), Holat (answered pos /
missed neg), AI baho (raqam + mini rangli halqa: >80 yashil, 60-80 sariq, <60 qizil),
Yozuv (play tugmasi), Amallar.
Yon drawer (bitta qator tanlangan): audio pleer chizig'i + AI tahlil kartasi —
umumiy ball katta mono raqamda + mezonlar ro'yxati progress-barlar bilan
(salomlashish 92, muammoni hal qilish 78, xushmuomalalik 95).
```

---

## 6. INVENTORY MODULI
```
"Inventar" sahifasi ikki tab bilan: "Jihozlar" va "Ombor harakati".
Jihozlar jadvali: Inventar № (mono), Nomi, Kategoriya, Seriya № (mono), Holat
(StatusBadge: omborda neutral / biriktirilgan pos / ta'mirda warn / hisobdan
chiqarilgan neg), Kimda (avatar + ism, bo'sh bo'lsa "—"), Berilgan sana, Amallar.
Qo'shimcha amal ikonkasi: "topshirish/qaytarish" (swap_horiz).
Biriktirish modali: xodim tanlash (qidiruvli select, avatar bilan), holat izohi
textarea, sana.
```

---

## 7. KPI MODULI

### 7.1 KPI dashboard (davr natijalari)
```
"KPI natijalar — 2026 Iyul" sahifasi. Tepada davr tanlovchi (oy navigatsiyasi ← →),
status chip ("Yakunlangan" pos), qayta hisoblash tugmasi.
StatStrip: "Xodimlar: 48", "O'rtacha KPI: 82.4" (mono), "Eng yuqori: 96.8", "80 dan past: 7" (neg).
Asosiy jadval: Xodim (avatar+ism+lavozim ikki qatorda), Profil, kriteriyalar ustunlari
(Vazifalar / Feedback / Intizom / ...) — har katakda mono ball + kichik progress-bar,
Yakuniy ball (katta mono, rangli: >85 yashil, 70-85 ko'k, <70 sariq/qizil), Amallar.
O'ng tomonda kichik ApexCharts ustunli grafik: bo'limlar bo'yicha o'rtacha KPI.
```

### 7.2 KPI profil sozlamalari
```
"KPI profillari" sahifasi: chapda profillar ro'yxati (Dasturchi, Support operatori,
Sotuvchi... — har birida lavozim va kriteriya soni), o'ngda tanlangan profil tahriri:
kriteriyalar ro'yxati — har qatorda kriteriya nomi + manba chipi (project/support/
callcenter/turniket) + vazn % inputi + slider. Pastda vaznlar yig'indisi indikatori:
"Jami: 100%" (yashil; 100 bo'lmasa qizil ogohlantirish). "Saqlash" primary tugma.
```

---

## 8. NOTIFICATION MARKAZI
```
Topbar qo'ng'irog'i bosilgandagi dropdown panel (360px): tepada "Bildirishnomalar" +
"Hammasini o'qilgan qilish" havolasi; ro'yxat elementlari: rangli dumaloq ikonka
(turi bo'yicha: vazifa ko'k, SLA qizil, KPI yashil), sarlavha + bir qator matn,
vaqt mono kichik; o'qilmaganlar och ko'k fonda chap primary chiziq bilan.
Pastda "Barchasini ko'rish" havolasi.
```

---

## Qo'shimcha ko'rsatma (har prompt oxirida ishlatsa bo'ladi)

```
Natijani bitta to'liq HTML sahifa sifatida ber (sidebar + topbar + kontent),
real ko'rinadigan namunaviy ma'lumotlar bilan (lorem emas — o'zbekcha real nomlar,
raqamlar mono shriftda). Interaktivlik shart emas, holatlarni statik ko'rsat.
```
