# .gitignore-va-tarix-tahlili
GitHub'da Pull Request (PR) bilan professional darajada ishlash, loyiha ustida jamoaviy kod yozish va review (ko'rib chiqish) jarayonining yuragi hisoblanadi.

Keling, barcha buyruqlar va GitHub interfeysidagi harakatlarni qadamma-qadam ko'rib chiqamiz.

1. Feature Branch va Birinchi Commitlar
Avval lokal kompyuterimizda yangi branch ochib, bir nechta commit qilamiz. Commit xabarlarini tushunarli va standart formatda (Conventional Commits) yozamiz.

Bash
# Yangi branch ochish va unga o'tish
git switch -c feature/user-profile

# 1-commit: Profil sahifasi strukturasi
echo "<div>Profil Sahifasi</div>" > profile.html
git add profile.html
git commit -m "feat(profile): foydalanuvchi profili uchun asosiy sahifa yaratildi"

# 2-commit: Avatar yuklash qismi
echo "<input type='file' />" >> profile.html
git add profile.html
git commit -m "feat(profile): foydalanuvchiga avatar rasm yuklash imkoniyati qo'shildi"
2. Branch'ni GitHub'ga Push qilish
Branch faqat sizning kompyuteringizda turibdi. Uni GitHub serverida ham yaratib, kodni yuborish uchun:

Bash
git push -u origin feature/user-profile
3. GitHub UI orqali Pull Request (PR) Yaratish
GitHub sahifangizga kirsangiz, tepada sariq rangda "Compare & pull request" tugmasi paydo bo'ladi. Uni bosing va quyidagilarni to'ldiring:

PR Title (Sarlavha): feat(profile): add user profile page with avatar upload (Conventional Commit formatida).

PR Description (Tavsif): PR nima ish qilishi va qaysi masalani (Issue) yopishi haqida yoziladi.

Markdown
### Nima ish qilindi?
- Foydalanuvchi ma'lumotlarini ko'rsatuvchi sahifa yaratildi.
- Avatar yuklash uchun input elementi qo'shildi.

### Skrinshotlar (Screenshots)
![Profil Sahifasi](https://github-storage.com/rasm.png)

Closes #12
Muhim: Closes #12 (yoki Fixes #12) yozuvi PR asosiy branchga merge bo'lishi bilan 12-raqamli Issue'ni avtomatik ravishda yopib yuboradi.

4. gh CLI (Terminal) orqali PR Yaratish
Agar ishingizni brauzerga o'tmasdan, terminalning o'zida bitirmoqchi bo'lsangiz, GitHub CLI (gh) vositasidan foydalanishingiz mumkin:

Bash
# Terminal orqali to'g'ridan-to'g'ri PR ochish
gh pr create --title "feat(profile): add user profile page" --body "Closes #12" --web
--web flagi sizga tayyor PR sahifasini brauzerda ochib beradi.

5. Draft PR (Xomaki PR) nima?
Agar kodingiz hali to'liq tayyor bo'lmasa, lekin boshqa hamkasblaringizga hozircha qanday kod yozayotganingizni ko'rsatib turmoqchi bo'lsangiz, Draft PR ochasiz.

Qanday ochiladi? GitHub UI'da "Create pull request" tugmasining yonidagi strelkani bosib, "Create draft pull request" tanlanadi.

Xususiyati: Uni hech kim tasodifan main branchga merge qilib yubora olmaydi. Tayyor bo'lganidan keyin "Ready for review" tugmasini bosib, uni oddiy PR holatiga o'tkazish mumkin.

6. PR'larni ko'rish va boshqarish (CLI commands)
Terminal orqali barcha faol PR'larni ko'rish va tekshirish:

Bash
# Loyihadagi barcha ochiq PR'lar ro'yxatini ko'rish
gh pr list

# Joriy PR'ni brauzerda ochib ko'rish
gh pr view --web
7. Kodni Tasdiqlash (Approve) va 3 xil Merge Strategiyasi
Odatda jamoada boshqa dasturchi sizning kodingizni tekshirib, Approve bosadi. Agar loyiha egasi o'zingiz bo'lsangiz, to'g'ridan-to'g'ri merge qilishga o'tasiz. GitHub merge qilish uchun 3 xil tugma taklif qiladi:

Strategiya nomi	Qanday ishlaydi?	Qachon ishlatiladi?
Create a merge commit	Feature branchdagi barcha commitlarni va alohida "Merge commit"ni tarixga qo'shadi.	Tarmoqlar tarixi to'liq saqlanib qolishi kerak bo'lganda.
Squash and merge 🌟	Feature branchdagi 2-3 ta mayda commitlarni bitta yagona commitga birlashtirib mainga qo'shadi.	Tavsiya etiladi! main branch tarixi toza va tushunarli bo'lib qoladi.
Rebase and merge	Feature branchdagi commitlarni main branchning eng uchiga bittalab ko'chirib o'tkazadi (merge commit yaratmaydi).	Tarix chiziqli (linear) bo'lishi talab etilganda.
8. Branchlarni Butunlay O'chirish
PR muvaffaqiyatli merge bo'lgandan keyin, endi u branchga ehtiyoj qolmaydi. Uni har ikki joydan ham o'chirib tashlaymiz:

Bash
# 1. Masofaviy serverdagi (GitHub) branchni o'chirish
git push origin --delete feature/user-profile

# 2. Lokal kompyuterimizdagi branchni o'chirish (avval main'ga o'tamiz)
git switch main
git pull origin main  # Yangilangan main kodini olish
git branch -d feature/user-profile
