# .gitignore-va-tarix-tahlili
1. Muhitni tayyorlash va Feature Branchlar yaratish
Avval yangi git ombori (repository) ochamiz va asosiy branchda boshlang'ich nuqtani yaratamiz:

Bash
mkdir git-mashq && cd git-mashq
git init
echo "Loyiha boshlandi" > readme.md
git add readme.md
git commit -m "Initial commit"
Endi shart bo'yicha 3-4 ta feature branch yaratamiz va ularning ichida 2-3 tadan commit qilamiz.

feature/auth branchini yaratish va commitlar:
Bash
git switch -c feature/auth # Yangi branchga o'tish

echo "Login funksiyasi" > auth.txt && git add auth.txt && git commit -m "feat: login qo'shildi"
echo "Register funksiyasi" >> auth.txt && git add auth.txt && git commit -m "feat: register qo'shildi"
feature/payment branchini yaratish va commitlar:
main branchga qaytib, yangi branch ochamiz:

Bash
git switch main
git switch -c feature/payment

echo "Payme integratsiyasi" > payment.txt && git add payment.txt && git commit -m "feat: payme qo'shildi"
echo "Click integratsiyasi" >> payment.txt && git add payment.txt && git commit -m "feat: click qo'shildi"
feature/ui va feature/chat branchlarini yaratish:
Bash
git switch main
git switch -c feature/ui
echo "Navbar yaratildi" > ui.txt && git add ui.txt && git commit -m "style: navbar"
echo "Sidebar yaratildi" >> ui.txt && git add ui.txt && git commit -m "style: sidebar"

git switch main
git switch -c feature/chat
echo "Telegram bot ulash" > chat.txt && git add chat.txt && git commit -m "feat: tg bot"
2. Fast-Forward Merge misoli
Fast-forward merge — bu main branchda siz feature branch ochganingizdan beri hech qanday o'zgarish bo'lmagan vaziyatda sodir bo'ladi. Git shunchaki main branch ko'rsatkichini oldinga surib qo'yadi.

Keling, feature/auth branchini mainga fast-forward merge qilamiz:

Bash
git switch main
git merge feature/auth
Konsolda Fast-forward yozuvini ko'rasiz. Hech qanday yangi merge-commit yaratilmaydi.

3. 3-Way Merge (Merge Commit) misoli
Endi vaziyat boshqacha: main branchda o'zgarish bor (chunki boya feature/authni qo'shdik). Lekin biz parallel ravishda yaratilgan feature/payment branchini ham mainga qo'shishimiz kerak. Bu yerda Git tarixlarni solishtirib, 3-way merge algoritmidan foydalanadi va yangi Merge Commit yaratadi.

Bash
git switch main
git merge feature/payment -m "Merge branch 'feature/payment' into main"
Bu yerda Git ikkala branch tarixini birlashtirib, yangi maxsus commit yaratadi.

4. Branch nomini o'zgartirish (-m)
Aytaylik, biz ochgan feature/ui branchining nomini standartga moslab feature/design qilib o'zgartirmoqchimiz.

Bash
# Agar o'sha branchning ichida bo'lsangiz:
git switch feature/ui
git branch -m feature/design

# Agar boshqa branchda (masalan, main'da) turgan bo'lsangiz:
# git branch -m feature/ui feature/design
5. Ataylab xato: Commit qilinmagan o'zgarishlar bilan branch o'zgartirish
Siz so'ragan o'sha mashhur xatolikni ataylab keltirib chiqaramiz. feature/design branchida turib, faylga o'zgarish kiritamiz lekin uni commit qilmaymiz:

Bash
echo "Yangi tugma" >> ui.txt
# git add yoki commit QILMAYMIZ!

# Endi boshqa branchga o'tishga urinamiz:
git switch main
Git beradigan xatolik (Error):

error: Your local changes to the following files would be overwritten by checkout: ui.txt
Please commit your changes or stash them before you switch branches.

(Buni tuzatish yo'llarini boya aytib o'tganimdek git stash yoki git commit orqali hal qilinadi. Hozircha buni shunday qoldiramiz yoki git stash qilib qo'yamiz).

Bash
git stash # Xatolikdan qutulish va davom etish uchun
6. Branch o'chirish (-d xavfsiz va -D majburiy)
-d (Xavfsiz o'chirish):
Bu buyruq faqatgina main branchga to'liq merge qilingan (birlashtirilgan) branchlarni o'chirishga ruxsat beradi.

Bash
git switch main

# feature/auth allaqachon merge bo'lgan, shuning uchun muammosiz o'chadi:
git branch -d feature/auth
-D (Majburiy o'chirish):
Agar branch mainga merge qilinmagan bo'lsa (masalan, undagi kodlardan voz kechmoqchisiz), Git -d buyrug'i bilan uni o'chirishga yo'l qo'ymaydi. Uni majburlab o'chirish uchun katta -D ishlatiladi.

Boya biz feature/chat branchini yaratgan edik, lekin uni merge qilmadik. Uni majburiy o'chiramiz:

Bash
git branch -D feature/chat
7. git log --graph --all bilan branchlar grafigi
Loyihamizda hozirgacha nimalar bo'lganini chiroyli va tushunarli grafik ko'rinishida ko'rish uchun quyidagi buyruqni kiritamiz:

Bash
git log --graph --oneline --all
Terminalda taxminan quyidagicha grafik hosil bo'ladi:

Plaintext
* e7b2a3f (HEAD -> main) Merge branch 'feature/payment' into main
|\  
| * 9a1c4d2 (feature/payment) feat: click qo'shildi
| * 4f3b2a1 feat: payme qo'shildi
* | 8c7b6a5 feat: register qo'shildi
* | 2b1a0f9 feat: login qo'shildi
|/  
* a1b2c3d Initial commit
|
| * 5e6f7d8 (feature/design) style: sidebar
| * 1a2b3c4 style: navbar
Bu grafik tarmoqlar qayerda ajralganini, qayerda qaytadan birlashganini (merge) juda aniq ko'rsatib beradi.
