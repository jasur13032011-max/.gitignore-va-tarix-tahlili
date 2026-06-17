# .gitignore-va-tarix-tahlili
1. Loyiha turi uchun moslangan .gitignore
Loyiha papkasida keraksiz fayllar (masalan, virtual muhitlar, yuklab olingan modullar yoki maxfiy kalitlar) Git-ga yuklanib ketmasligi uchun .gitignore faylidan foydalaniladi.

Python loyihalar uchun .gitignore tarkibi:
Plaintext
# Virtual muhitlar
venv/
.venv/
env/

# Python kesh fayllari
__pycache__/
*.py[cod]
*$py.class

# Maxfiy ma'lumotlar
.env
Node.js loyihalar uchun .gitignore tarkibi:
Plaintext
# Yuklab olingan kutubxonalar
node_modules/

# Log fayllar
*.log
npm-debug.log*

# Qurilish (build) natijalari
dist/
build/

# Maxfiy ma'lumotlar
.env
2. .env faylini yaratish va ignore qilish
Maxfiy kalitlar va parollarni saqlash uchun .env fayli yaratiladi. Uni Git ko'rmasligi (kuzatmasligi) uchun quyidagi qadamlar bajariladi:

Loyiha papkasida .env faylini yarating va ichiga ma'lumot yozing:

Bash
echo "DB_PASSWORD=secret123" > .env
.gitignore fayliga .env satrini qo'shing.

Holatni tekshiring:

Bash
git status
Natija: git status buyrug'i chiqqanda, Untracked files bo'limida .env fayli ko'rinmasligi kerak. Faqat .gitignore faylining o'zi ko'rinadi.

3. Global .gitignore_global sozlash
Kompyuterdagi barcha Git loyihalari uchun umumiy amal qiladigan qoidalarni (masalan, operatsion tizim yaratadigan keraksiz fayllarni) global sozlash mumkin.

Kompyuterning foydalanuvchi papkasida global ignore faylini yarating:

Bash
git config --global core.excludesfile ~/.gitignore_global
Fayl ichiga hamma loyihalarda ignore qilinishi kerak bo'lgan tizim fayllarini yozing (masalan, macOS yoki Windows fayllari):

Plaintext
.DS_Store
Thumbs.db
.vscode/
4. git diff 3 ta variantda
git diff buyrug'i kod dagi o'zgarishlarni solishtirish uchun ishlatiladi.

1-variant: Ishchi katalog va Sahna (Working Directory vs Staged Index)
Siz kodni o'zgartirdingiz, lekin hali git add buyrug'ini bermadingiz. Shundagi o'zgarishlarni ko'rish:

Bash
git diff
2-variant: Sahna va Oxirgi commit (Staged Index vs HEAD)
Siz git add qilib sahnalashtirgan, lekin hali git commit qilmagan o'zgarishlarni ko'rish:

Bash
git diff --staged
3-variant: Ishchi katalog va Oxirgi commit (Working Directory vs HEAD)
Oxirgi commit-dan keyin kiritilgan barcha o'zgarishlarni (sahnalashtirilganidan qat'i nazar) ko'rish:

Bash
git diff HEAD
5. Chiroyli tarmoqlar logi uchun Alias yaratish
Git tarixini chiroyli, grafik ko'rinishda va bir qatorda ko'rish uchun maxsus qisqartma (alias) yaratamiz:

Bash
git config --global alias.tree "log --oneline --graph --all"
Endi loyiha tarixini ko'rish uchun shunchaki quyidagi qisqa buyruqni yozish kifoya:

Bash
git tree
6. git blame bilan qatorlar tarixi
Fayldagi har bir qatorni kim, qachon va qaysi commit ID bilan o'zgartirganini aniqlash uchun ishlatiladi:

Bash
git blame main.py
(Bu yerda main.py o'rniga o'zingiz tekshirmoqchi bo'lgan fayl nomini yozasiz).

7. git log -S 'soz' bilan qidirish
Kodni ichidan biror bir so'z, o'zgaruvchi nomi yoki funksiya qachon qo'shilgani yoki o'chirilganini qidirish (bunga Git-da "pickaxe" deyiladi):

Bash
git log -S 'secret_key' --oneline
Bu buyruq kod tarkibida secret_key so'zi qatnashgan barcha commit'lar ro'yxatini chiqarib beradi.

8. Kuzatilgan faylni git rm --cached bilan ignore qilish
Agar loyihada biror fayl (masalan, .env yoki config.json) allaqachon Git tomonidan kuzatuvga olingan (commit qilingan) bo'lsa, uni shunchaki .gitignorega qo'shish foyda bermaydi. Uni keshdan o'chirish kerak:

Faylni Git keshidan o'chiring (kompyuterdan o'chib ketmaydi, faqat Git kuzatishni to'xtatadi):

Bash
git rm --cached .env
Ushbu fayl nomini .gitignore ichiga yozib qo'ying.

O'zgarishni saqlash uchun commit qiling:

Bash
git commit -m "Kuzatuvdagi .env fayli keshdan olib tashlandi"
