# .gitignore-va-tarix-tahlili
Lokal kompyuterdagi Git omborini GitHub masofaviy (remote) serveri bilan bog'lash, xavfsiz ulanish (SSH) o'rnatish va kodlarni sinxronizatsiya qilish bo'yicha to'liq va ketma-ket qo'llanma.

1. SSH Kalit Yaratish va GitHub'ga Qo'shish
Parol kiritib o'tirmaslik va xavfsiz aloqa o'rnatish uchun SSH kalitidan foydalanamiz.

SSH kalit yaratish
Terminalingizni oching va quyidagi buyruqni kiriting (elektron pochtangizni yozing):

Bash
ssh-keygen -t ed25519 -C "sizning_pochtangiz@example.com"
Tizim sizdan kalitni qayerga saqlashni va parol (passphrase) qo'yishni so'raydi. Hammasiga shunchaki Enter bosing.

Public key (ommaviy kalit)ni nusxalash
Yaratilgan maxfiy kalitning ommaviy qismini GitHub'ga berishimiz kerak. Uni ko'rish uchun:

Bash
# Mac/Linux foydalanuvchilari uchun:
cat ~/.ssh/id_ed25519.pub

# Windows (Git Bash) foydalanuvchilari uchun:
cat ~/.ssh/id_ed25519.pub
Ekrandagi ssh-ed25519 ... bilan boshlanadigan barcha matnni nusxalab oling (Copy).

GitHub'ga qo'shish
GitHub saytiga kiring va profil rasmingizni bosib, Settings bo'limiga o'ting.

Chap menyudan SSH and GPG keys bo'limini tanlang.

New SSH key tugmasini bosing.

Title qismiga kompyuteringiz nomini yozing (masalan: Dasturchi-Noutbuki).

Key qismiga nusxalangan matnni joylashtiring (Paste) va Add SSH key tugmasini bosing.

Aloqani tasdiqlash
Ulanish muvaffaqiyatli bo'lganini tekshirish uchun terminalda quyidagini ishlating:

Bash
ssh -T git@github.com
Sizdan so'rov so'ralsa yes deb yozing. Agar hammasi to'g'ri bo'lsa, quyidagi xabarni ko'rasiz:

Hi [Sizning-Loginingiz]! You've successfully authenticated, but GitHub does not provide shell access.

2. GitHub'da Yangi Repo ochish va Lokal Reponi Ulash
GitHub bosh sahifasiga o'ting va New (yoki Create repository) tugmasini bosing.

Repository nomini yozing (masalan: kundalik).

DIQQAT: Add a README file, Add .gitignore bo'limlariga mutlaqo tegib o'tirmang (ular belgilangan bo'lsa, olib tashlang). Repo butunlay bo'sh bo'lishi kerak.

Create repository tugmasini bosing.

Sizga GitHub tomonidan SSH manzili beriladi (u git@github.com:login/repo.git ko'rinishida bo'ladi).

Lokal reponi GitHub'ga bog'lash
O'zingizning kompyuteringizdagi loyiha papkasiga (kundalik/) kirib, masofaviy server manzilini qo'shing:

Bash
# Masofaviy server manzilini 'origin' nomi bilan saqlash
git remote add origin git@github.com:SIZNING_LOGIN/REPOS_NOMI.git

# Birinchi marta push qilish (Lokal main branchini GitHub'ga bog'lash)
git push -u origin main
-u (upstream) flagi bir marta yoziladi. Keyingi safar Git qayerga push qilishni o'zi eslab qoladi.

3. Kundalik Ish Oqimi (Workflow) va Qisqartirilgan Push
Endi loyihada biror o'zgarish qilamiz:

Bash
echo "- Bugun GitHub bilan ishlashni o'rgandim" >> README.md
git add README.md
git commit -m "docs: bugungi o'rganishlar yozildi"
Endi -u flagisiz, shunchaki qisqa buyruq orqali kodni GitHub'ga yuboramiz:

Bash
git push
4. Loyihani Boshqa Joyga Clone Qilish va Pull Olish
Tasavvur qiling, siz uydagi kompyuterda ishni tugatdingiz va ofisdagi boshqa kompyuterda loyihani davom ettirmoqchisiz.

Clone (Nusxa olish)
Boshqa ixtiyoriy papkaga o'tib, loyihani butunlay ko'chirib olasiz:

Bash
git clone git@github.com:SIZNING_LOGIN/REPOS_NOMI.git
Bu buyruq loyihaning barcha fayllari va Git tarixini yangi papka qilib yuklab beradi.

Pull (Yangiliklarni olish)
Agar loyiha kompyuteringizda allaqachon bor bo'lsa-yu, lekin GitHub'da kimdir (yoki o'zingiz boshqa joydan) yangi commit qo'shgan bo'lsa, o'sha o'zgarishlarni kompyuterga yuklash uchun foydalaniladi:

Bash
git pull
5. Feature Branch Yaratish va Masofaviy Serverga Push Qilish
Yangi vazifa ustida ishlash uchun lokal kompyuterda yangi branch ochamiz:

Bash
# Yangi feature branch yaratish va unga o'tish
git switch -c feature/profile

# Biror o'zgarish qilish
echo "Foydalanuvchi profili bo'limi" > profile.md
git add profile.md
git commit -m "feat: profil sahifasi asosi yaratildi"
Ushbu branch faqat bizning kompyuterimizda mavjud. Uni GitHub serverida ham ochish va kodni yuborish uchun quyidagi buyruqni bajaramiz:

Bash
git push -u origin feature/profile
Endi GitHub saytiga kirsangiz, u yerda ikkita branch (main va feature/profile) paydo bo'lganini va jamoangiz siz yozgan kodni ko'rib chiqishi (Pull Request) mumkinligini ko'rasiz.
