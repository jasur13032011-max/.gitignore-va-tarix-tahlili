# .gitignore-va-tarix-tahlili
1. Muhitni sozlash va Git init
Dastlab, kundalik/ papkasini ochamiz, ichiga kirib Git omborini yaratamiz va asosiy sozlamalarni qilamiz.

Bash
mkdir kundalik && cd kundalik
git init

# README faylini yaratish
echo "# Mening Shaxsiy Kundaligim" > README.md

# .gitignore yaratish (va vaqtinchalik .tmp fayllarni ignore qilish)
echo "*.tmp" > .gitignore

# Ilk commitni amalga oshirish
git add README.md .gitignore
git commit -m "chore: loyiha boshlang'ich nuqtasi (.gitignore va README)"
2. Shablon yaratish va Feature Branch bilan ishlash
Kundalik yozuvlari bir xil strukturada bo'lishi uchun shablon yaratamiz.

Bash
mkdir shablonlar
cat << 'EOF' > shablonlar/kun-shabloni.md
## 🎯 Kunlik Maqsadlar
- 

## 🐛 Bugun duch kelgan muammolar va xatolar
- 

## 💡 Yangi g'oyalar va o'rganilgan narsalar
- 

## 📋 Ertangi kun rejalari
- 
EOF

git add shablonlar/kun-shabloni.md
git commit -m "feat: kunlik yozuvlar uchun shablon qo'shildi"
feature/teglar branchida ishlash
Kundalikda teglardan foydalanish qoidasini README.mdga qo'shish uchun yangi branch ochamiz:

Bash
# Yangi branch ochish va unga o'tish
git switch -c feature/teglar

# README.md fayliga teglar bo'limini qo'shish
cat << 'EOF' >> README.md

## 🏷 Teglar Tizimi
Yozuvlarda quyidagi teglardan foydalaniladi:
- `#shaxsiy` - Shaxsiy hayot va fikrlar
- `#kodlash` - Dasturlashga oid o'rganishlar
- `#sport` - Sog'lom turmush tarzi
EOF

# O'zgarishni saqlash
git add README.md
git commit -m "docs: README fayliga teglar tizimi qo'shildi"
Branch'ni merge qilish va o'chirish
Endi qilgan ishimizni asosiy (main) branchga birlashtiramiz va ortiqcha branchni o'chiramiz:

Bash
git switch main

# Merj qilish (Bu yerda Fast-forward sodir bo'ladi)
git merge feature/teglar

# Branch o'chirildi
git branch -d feature/teglar
3. 5 kunlik yozuvlar (8-12 iyun, 2026) va individual commitlar
Har bir kun uchun alohida fayl yaratamiz va ularni alohida commit qilamiz:

Bash
# 8-iyun yozuvi
cp shablonlar/kun-shabloni.md 2026-06-08.md
echo "- Bugun Git laboratoriyasini boshladim #kodlash" >> 2026-06-08.md
git add 2026-06-08.md && git commit -m "docs(daily): 8-iyun yozuvi"

# 9-iyun yozuvi
cp shablonlar/kun-shabloni.md 2026-06-09.md
echo "- Merge va Branchlar bilan ishladim #kodlash" >> 2026-06-09.md
git add 2026-06-09.md && git commit -m "docs(daily): 9-iyun yozuvi"

# 10-iyun yozuvi
cp shablonlar/kun-shabloni.md 2026-06-10.md
echo "- Bugun faqat dam oldim va kitob o'qidim #shaxsiy" >> 2026-06-10.md
git add 2026-06-10.md && git commit -m "docs(daily): 10-iyun yozuvi"

# 11-iyun yozuvi
cp shablonlar/kun-shabloni.md 2026-06-11.md
echo "- Ertalab 5 km yugurdim #sport" >> 2026-06-11.md
git add 2026-06-11.md && git commit -m "docs(daily): 11-iyun yozuvi"

# 12-iyun yozuvi
cp shablonlar/kun-shabloni.md 2026-06-12.md
echo "- Git tarixi tahlili ustida ishlayapman #kodlash" >> 2026-06-12.md
git add 2026-06-12.md && git commit -m "docs(daily): 12-iyun yozuvi"
4. git diff bilan o'zgarishlarni tekshirish
Keling, 8-iyun kundaligiga qo'shimcha kiritamiz va hali commit qilinmagan o'zgarish qanday ko'rinishini tekshiramiz:

Bash
echo "- Kechki payt Git bo'yicha qo'shimcha maqola o'qidim" >> 2026-06-08.md

# O'zgarishlarni ko'rish
git diff 2026-06-08.md
Natija konsolda quyidagicha ko'rinadi:

Diff
diff --git a/2026-06-08.md b/2026-06-08.md
index 4b5c6d7..8e9f0a1 100644
--- a/2026-06-08.md
+++ b/2026-06-08.md
@@ -9,3 +9,4 @@
 ## 📋 Ertangi kun rejalari
 - 
 - Bugun Git laboratoriyasini boshladim #kodlash
++ - Kechki payt Git bo'yicha qo'shimcha maqola o'qidim
(Yashil rangdagi + belgisi yangi qo'shilgan qatorni anglatadi. Keling, buni ham saqlab qo'yamiz):

Bash
git add 2026-06-08.md
git commit -m "docs(daily): 8-iyun yozuviga qo'shimcha"
5. Tarix Tahlili (Statistics & Blame)
Loyihamizning umumiy holatini tahlil qilamiz.

Jami commitlar sonini aniqlash:
Bash
git rev-list --count HEAD
Hozirgi holatda natija: 9 chiqishi kerak.

Eng katta o'zgarish (qaysi commitda eng ko'p qator qo'shilgan):
Bizda shablon fayli yaratilganda yoki README tahrirlanganda katta o'zgarish bo'ldi. Statisikani qisqa ko'rish uchun:

Bash
git log --stat --oneline
git blame natijasi:
README.md faylining har bir qatorini kim va qachon yozganini ko'rish uchun:

Bash
git blame README.md
Bu buyruq sizga har bir qator yonida commit ID'si va muallif ismini chiqarib beradi.

6. .tmp Ignore Tizimi Ishlashini Tasdiqlash
.gitignore faylimizga yozilgan *.tmp qoidasi to'g'ri ishlayotganini tekshirish uchun vaqtinchalik fayl yaratib ko'ramiz:

Bash
echo "Maxfiy yoki keraksiz kesh ma'lumotlar" > kesh-fayli.tmp

# Git holatini tekshiramiz
git status
Natija:
git status buyrug'ini berganingizda, kesh-fayli.tmp fayli "Untracked files" ro'yxatida ko'rinmaydi. Bu .gitignore qoidasi muvaffaqiyatli ishlayotganini va Git uni ataylab hisobga olmayotganini tasdiqlaydi.
