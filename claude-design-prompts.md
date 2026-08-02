# Claude Design — prompt to'plami (web-platform dizayn tizimi asosida)

> Ishlatish tartibi: har Claude Design sessiyasida **avval 0-bo'limdagi bazaviy promptni** yuboring,
> keyin kerakli sahifaning promptini. Natija mavjud frontend (Vue 3 + Quasar) bilan bir xil
> vizual tilda chiqadi — keyin dasturchi uni Quasar komponentlariga o'girishi oson bo'ladi.

---

## 0. BAZAVIY DIZAYN-TIZIM PROMPTI (har sessiyada birinchi yuboriladi)

```
Sen korporativ CRM tizimining UI dizaynerisan. Quyidagi dizayn tizimiga QAT'IY rioya qil —
bu mavjud ishlab turgan mahsulotning tizimi (koddan olingan), undan chetga chiqma.

═══ GLOBAL RANGLAR (light) ═══
- Primary: #2563eb — asosiy tugmalar, aktiv menyu matni, fokus, linklar
- Sahifa foni: #f3f4f6; Karta/panel: #ffffff; Chegara: #e2e8f0 / #eaecf0
- Matn: asosiy #1e293b (#0f172a sarlavhalarda), ikkilamchi #64748b, xira #94a3b8
- Yorqin semantik (jadval/sahifa darajasida): pos #22c55e, neg #e31e24 (FAQAT delete/xato),
  warn #f59e0b, info #3b82f6

═══ MODAL ICHKI PALITRA (muted — modallar sahifadan farq qiladi!) ═══
- Modal body foni: #f4f7fb; karta: #ffffff; chegaralar: #d5dee8 / #e9eef4
- Matn shkalasi: #182634 / #5c6e80 / #93a2b2
- SO'NIK semantik: pos #1b7a4d (fon #e0f0e8), neg #b83d2e (fon #f7e3df),
  accent #1f66a8 (fon #e3edf7), warn #976a14 (fon #f8f0dc)
- OLTIN aksent: #c9a227 — modal header ikonka belgisi (mark) rangida
- Dark rejim modallari: surface #161f29, body #101820, matn #e6ecf2/#9aabbb, chegara #2a3744

═══ TIPOGRAFIKA ═══
- Asosiy: 'Sora' (kirillda 'Noto Sans' fallback); raqam/kod/qiymat/sana/vaqt: 'JetBrains Mono'
  (tabular-nums bilan)
- Sahifa sarlavha 18-20px semibold; jadval th 14px/600; body 13-14px
- Mikro-sarlavhalar (section, stat label, ledger th): 10-13px, 700, UPPERCASE,
  letter-spacing 0.07-0.12em, rang #8b9aa9/#94a3b8

═══ SHAKL ═══
- Radius: input/karta-kichik 10px, karta 12px, tugma 8-9px, modal/sidebar 16px, chip 999px
- Soyalar juda yumshoq: 0 1px 4px .04 (header) / 0 2px 6px .05 / 0 4px 12px .08;
  menyular: 0 12-16px 40px .12-.22
- Spacing: 4/8/16/24/32

═══ LAYOUT ═══
- TOPBAR (64px, oq, soya 0 1px 4px): chapda 284px brand-zona — logo 40px (radius 11,
  ko'k soya) + wordmark (17px/800 #0f172a, ostida 10px uppercase #94a3b8 sub), hamburger,
  breadcrumb (14px/600 #94a3b8, joriy #0f172a/700, ajratkich chevron #cbd5e1).
  O'ngda: jonli sana-soat (mono, ko'k ikonka), 1px ajratkich chiziqlar, icon-tugmalar
  (radius 10, hover #f3f4f6), til, dark toggle, bildirishnoma qo'ng'irog'i,
  USER-PILL: #f3f4f6 fon, radius 22, gradient avatar (#667eea→#764ba2) + ism 13px/600 + chevron
- SIDEBAR — SUZUVCHI KARTA: sahifa fonidan 16px chekingan oq karta, radius 16,
  yengil soya, pastki qismida juda nozik mesh-gradient (shaftoli-binafsha radial dog'lar).
  Bo'lim yorlig'i 11px/700 uppercase #94a3b8. Menyu elementi: radius 8, balandlik 48px
  (bolalar 42/38px), matn 15-16px/500 #4b5563, ikonka #64748b.
  HOVER: #f3f4f6. AKTIV: OQ fon + #2563eb matn/ikonka + 1px rgba(0,0,0,.06) chegara +
  nozik soya. Bolalar chap tomondan 1.5px chiziq bilan ichkariga surilgan (sub'lar dashed +
  nuqta marker). Badge: qizil gradient pill. Sidebar pastida PROMO-KARTA: ko'k-binafsha
  gradient (#2563eb→#4f46e5→#7c3aed), radius 16, pulsli glow, hover'da shine, oq CTA tugma.
- Kontent: 16px padding.

═══ JADVAL NAQSHI (ro'yxat sahifalari) ═══
- Oq karta ichida flat bordered jadval, cell separator
- Toolbar: chapda sarlavha (text-h6); o'ngda: qidiruv (outlined dense 220px, lupa),
  faol filtrlar tugmasi (qizil badge son), ustun sozlash, refresh, "Yaratish" PRIMARY
  (add_circle, unelevated)
- Amallar ustuni o'ngda STICKY (chapga soya): ko'rish/tahrirlash/o'chirish(qizil) icon-tugmalar
- Oxirgi amal qatori: fon #e3edf7 + chapda inset 3px #2563eb; hover #d6e4f2
- Har ustun sarlavhasida filter-input ochilishi mumkin; pastda pagination (tugma min 28px)

═══ MODALLAR (uch qobiq) ═══
Barchasi: radius 16, max-height 92vh, header rangli + oq matn, body scroll (thin scrollbar).
1) FORM (820px / keng 1040 / tor 560): PRIMARY ko'k header; body oq, bo'limlarga ajratilgan —
   bo'lim sarlavhasi: 24px ikonka-chip (primary 12% fon) + 12px uppercase matn + cho'ziluvchi
   chiziq; 2 ustunli grid (gap 24/16); yorliq 12.5px/600, majburiy * qizil #d23f31;
   INPUT: 46px, radius 10, 1px #d5dee8 chegara, hover #93a2b2, fokus primary + 3px 16% halqa,
   xato matni input ostida absolute (layoutni siljitmaydi); checkbox — karta-qator uslubida.
   Footer #f4f7fb: chapda "* majburiy" izoh, o'ngda Bekor (flat) + Yaratish/Yangilash
   (primary, check_circle, ko'k soya).
2) DETAIL (720px): primary header, body #f4f7fb ichida DescriptionCard'lar; footer: chapda
   Yopish, o'ngda Tahrirlash (primary) + O'chirish (matnli, muted qizil #b83d2e).
3) DELETE (480px): header MUTED qizil #b83d2e; qo'shimcha tasdiqlash popover (260px).
MODAL SARLAVHASI (ModalTitle): 38px kvadrat mark (oq 8% fon, 16% chegara, radius 9,
OLTIN #c9a227 ikonka) + sarlavha 16px/600 oq + ostida mono ID (oq 62%) + copy tugma.

═══ KOMPONENTLAR ═══
- DescriptionCard (detail'larning yuragi, "ledger" uslubi): karta radius 10, headerda
  uppercase 13px sarlavha + o'ngda mono izoh; ichida KV qatorlar:
  "yorliq ·············· qiymat" — orasi NUQTALI chiziq (dotted leader), qiymat o'ngda
  13.5px/500, xavfli qiymat muted qizil; qator orasi 1px chiziq; hoverda copy tugma.
  Ledger jadval varianti: th 10px uppercase fon #eff3f8, qator hover #e3edf7,
  JAMI qator (2px ust chiziq, qalin, fon #eff3f8), mono kataklar nowrap,
  score-pill chiplar (mono, hit=ko'k / pos / neg yumshoq fonlarda).
- StatusBadge: pill chip, pulsli nuqta (halo soya bilan): pos #5bd49a / neg #ff8a73 /
  warn #f2c14e / neutral #cbd5e1; rangli header ustida yarim shaffof oq fon.
- StatusBanner (kontekst banner, to'liq kenglik): yumshoq fon + to'q matn
  (neg #faeae7/#b83d2e, warn #f8f0dc/#976a14, pos #e2f1e9/#1b7a4d), 30px doira ikonka
  to'ldirilgan rangda, ostida sabab-chiplar (oq fon, rangli chegara).
- StatStrip: label 10px uppercase (ikonka accent rangda) + qiymat 16.5px/600 MONO +
  ixtiyoriy 3px progress-bar (120px) + sub 11px. Variantlar: strip (1px chiziq bilan
  ajratilgan qator, min 130px) / grid (kartalar 210px+).
- PersonSummary: 44px avatar (radius 10, navy #15395c fon + OLTIN harflar), ism 14.5/600,
  meta qatori mono + copy.
- EmptyState: 52px doira ikonka (#eff3f8 fon), sarlavha 14.5/600, izoh 12px, min 240px.
- Fayl kartasi: 56px thumb (radius 8), nom 13px/500 ellipsis, meta 11px, hoverda zoom
  overlay; grid varianti 4:3 media + footer. Fullscreen preview: to'q #1a1a2e fon,
  blur headerli.
- Loading: gears spinner primary.
- Grafiklar: ApexCharts, yumshoq, primary/semantik ranglar.

═══ UMUMIY QOIDALAR ═══
- Interfeys matni o'zbekcha; ikonkalar Material Icons
- Raqam/sana/ID/summa HAR DOIM mono (tabular-nums)
- Zichlik korporativ-ixcham, 16px ritm; sokin professional til — gradient faqat
  promo-karta va avatarlarda, boshqa joyda yo'q
- Responsive: <768px sticky o'chadi, <640px breadcrumb yashirinadi, form grid 1 ustun
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
