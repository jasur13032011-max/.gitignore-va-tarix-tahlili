# .gitignore-va-tarix-tahlili
  Mana Git-ning eng foydali va amaliy buyruqlari bo'yicha qulay qo'llanma. Bu buyruqlar kunlik ish unumdorligingizni sezilarli darajada oshiradi.

1. git stash — Ishni Vaqtincha Saqlash
git stash sizning joriy o'zgarishlaringizni (commit qilmasdan) alohida xotiraga olib qo'yadi va ishchi katalogni toza (clean) holatga qaytaradi.

Uchta Asosiy Vaziyat:
Yarim qolgan ish (Work in Progress): Biror funksiya ustida ishlayapsiz, lekin u hali bitmadi. Shu payt shoshilinch boshqa bug-ni to'g'rilashingiz kerak bo'lib qoldi. Kodni chala holatda commit qilmaslik uchun uni git stash qilib turasiz.

Pull Conflict (To'qnashuv) oldini olish: Masofaviy serverdan (main branchdan) oxirgi kodlarni tortib olmoqchisiz (git pull), lekin siz joriy fayllarni o'zgartirgansiz. Git sizga pull qilishga ruxsat bermaydi. Shunda kodni stash qilib, pull qilasiz va keyin stash-ni qaytarib olasiz.

Eksperiment (Tajriba): Kodga biror yangilik qo'shib ko'rmoqchisiz, lekin u o'xshamasligi mumkin. Uni vaqtincha stash-ga olib, toza kodda boshqa narsani sinab ko'rsangiz bo'ladi.

Boshqarish Buyruqlari:
git stash list — Saqlangan barcha stash-lar ro'yxatini ko'rsatadi (masalan: stash@{0}, stash@{1}).

git stash apply — Eng oxirgi saqlangan stash-ni ishchi katalogga qaytaradi, lekin uni stash ro'yxatidan o'chirib tashlamaydi.

git stash pop — Eng oxirgi stash-ni qaytaradi va uni ro'yxatdan o'chirib yuboradi (eng ko'p ishlatiladigan usul).

git stash drop — Keraksiz bo'lgan stash-ni ro'yxatdan butunlay o'chirib tashlaydi.

Maxsus Holatlar:
git stash -u (yoki --include-untracked) — Git hali kuzatishni boshlamagan (yangi yaratilgan, git add qilinmagan) untracked fayllarni ham stash ichiga qo'shib saqlaydi. Oddiy git stash bularni saqlamaydi.

git stash branch <branch_nomi> — Stash ichidagi o'zgarishlar bilan to'g'ridan-to'g'ri yangi branch ochadi va stash-ni o'chiradi. Bu stash-ni qaytarganda juda ko'p konflikt chiqsa juda asqotadi.

2. git cherry-pick — Kerakli Commit-ni Ko'chirib O'tish
Boshqa bir branch-dagi tayyor commit-ni o'zingiz turgan joriy branch-ga nusxalab o'tkazish uchun ishlatiladi.

Bitta commit-ni olish:

Bash
git cherry-pick <commit_hash>
Bir nechta commit-larni olish:

Bash
git cherry-pick <commit_hash1> <commit_hash2> <commit_hash3>
Ketma-ket kelgan commit-lar oralig'ini olish uchun: git cherry-pick <eski_hash>..<yangi_hash>

Cherry-pick Conflict Yechish:
Agar nusxalanayotgan commit joriy branch kodi bilan to'qnashsa (conflict), Git jarayonni to'xtatadi. Uni yechish tartibi:

Konflikt bor fayllarni ochib, kodni tartibga soling.

Fayllarni saqlab, git add <fayl_nomi> qiling.

Jarayonni davom ettirish uchun quyidagini yozing:

Bash
git cherry-pick --continue
(Agar cherry-pick-ni bekor qilmoqchi bo'lsangiz: git cherry-pick --abort)

3. git commit --amend — Oxirgi Commit-ni O'zgartirish
Eng oxirgi qilingan commit-ga tuzatish kiritish uchun ishlatiladi.

Commit xabarini tahrirlash: Oxirgi commit xabarida xato qilib qo'ysangiz, uni qayta yozish imkonini beradi:

Bash
git commit --amend -m "Yangi va to'g'ri commit xabari"
Yangi fayl qo'shish (--no-edit): Biror fayl commit-ga qo'shilmay qolib ketgan bo'lsa, uni git add qilib, so'ng commit xabarini o'zgartirmasdan oxirgi commit-ga qo'shib yuborish mumkin:

Bash
git add unutilgan_fayl.txt
git commit --amend --no-edit
⚠️ Push Qilingan Commit-da Amend Xavfi:
Muhim qoida: Agar siz commit-ni masofaviy serverga (git push qilib) yuborgan bo'lsangiz, uni lokalda --amend qilmaslik kerak.

--amend buyrug'i eski commit-ni shunchaki tahrirlamaydi, balki uni o'chirib, yangi ID (hash) bilan yangi commit yaratadi. Agar buni push qilsangiz, Git tarix buzilgani haqida xato beradi. Uni majburlab push qilish (git push --force) esa jamoadagi boshqa dasturchilarning kodlarida jiddiy chalkashlik va to'qnashuvlarga (conflict) olib keladi.

4. 6 ta Foydali Git Alias (Tezkor Buyruqlar)
Git-da uzoq buyruqlarni qisqartirish uchun quyidagi alias-larni terminalda bir marta ishga tushirib sozlab oling:

git st — Holatni qisqa va tushunarli ko'rish:

Bash
git config --global alias.st "status -s"
git co — Branch-lar aro tez almashish:

Bash
git config --global alias.co checkout
git cm — Xabar bilan tezkor commit qilish:

Bash
git config --global alias.cm "commit -m"
git br — Branch-lar ro'yxatini ko'rish:

Bash
git config --global alias.br branch
git lg — Commit-lar tarixini chiroyli, rangli va grafik shaklda ko'rish (juda foydali!):

Bash
git config --global alias.lg "log --oneline --graph --decorate --all"
git unstage — git add qilingan faylni commit ro'yxatidan qaytarib chiqarish:

Bash
git config --global alias.unstage "restore --staged"
Endi siz git status o'rniga shunchaki git st, yoki chiroyli log ko'rish uchun git lg buyruqlaridan foydalanishingiz mumkin.
