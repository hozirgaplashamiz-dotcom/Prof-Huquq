import logging
from telegram import Update, ReplyKeyboardMarkup, KeyboardButton, ReplyKeyboardRemove, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import (
    Application,
    CommandHandler,
    MessageHandler,
    CallbackQueryHandler,
    ContextTypes,
    filters,
)

# Logging
logging.basicConfig(
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s", level=logging.INFO
)

TOKEN = "8887155834:AAEbMAfo75G22A2n3r3sOmhbmvwlDIE7Wz8"
ADMIN_USERNAME = "obulen"
ADMIN_CHAT_ID = 6106446622

# TEST BAZASI
QUIZ_DATA = {
    # ------------------ 1-TEST ------------------
    1: [
        {
            "question": "1-savol:\nQuyidagilardan noto’g’ri mulohazani toping.\n\nA) Oʻzbekiston Respublikasi Davlat gerbi Oʻzbekiston Respublikasi davlat mustaqilligining ramzidir.\nB) Davlat organlari va boshqa tashkilotlar Oʻzbekiston Respublikasi Davlat gerbining boʻrtma tasviridan foydalanishi mumkin.\nC) Nodavlat notijorat tashkilotlarining ramzlari Oʻzbekiston Respublikasining Davlat gerbiga oʻxshash boʻlishi mumkin .\nD) Nodavlat notijorat tashkilotlarining ramzlari Oʻzbekiston Respublikasining Davlat gerbiga oʻxshash boʻlishi mumkin emas.",
            "correct": "C"
        },
        {
            "question": "2-savol:\nQuyidagilaar orasidan tog’ri mulohaza keltirilgan javobni toping.\n\nA) ‘’Davlat gerbi to’g’risidagi’’ Qonunning Oʻzbekiston Respublikasi diplomatik vakolatxonalari, konsullik muassasalari, shuningdek xalqaro tashkilotlar huzuridagi vakolatxonalari tomonidan ijro etilishi ustidan nazorat Oʻzbekiston Respublikasi Tashqi ishlar vazirligi, boshqa davlat organlari va boshqa tashkilotlar tomonidan ijro etilishi ustidan nazorat esa davlat xavfsizlik xizmati tomonidan amalga oshiriladi.\nB) Oʻzbekiston Respublikasining fuqarolari, shuningdek Oʻzbekistonda turgan boshqa shaxslar Oʻzbekiston Respublikasining Davlat gerbini hurmat qilishlari shart.\nC) Oʻzbekiston Respublikasi Davlat gerbining takrorlanayotgan tasviri, uning katta-kichikligidan qatʼi nazar, ushbu Qonunga ilova qilinayotgan rangli va oq-qora tasviriga aniq mos boʻlishi shatrt emas.\nD) Oʻzbekiston Respublikasining Davlat megaralarida oʻrnatiladigan sarhad ustunlarida bolishi mumkin emas.",
            "correct": "B"
        },
        {
            "question": "3-savol:\nQuyidagilar orasidan davlatning belgilari xató keltirilgan javobni toping.\n\nA) Aholi va hudud\nB) Armiya\nC) Davlat apparati\nD) Budjet/Soliq tizimi",
            "correct": "B"
        },
        {
            "question": "4-savol:\nBOSHQARUV SHAKLI haqida noto’g’ri mulohaza keltirilgan javobni toping.\n\nA) Monarxiya turlari: Mutlaq, Cheklangan, Noananviy , teokratik.\nB) Respublika turlari : Aralash , prezidentlik , parlamentar\nC) Respublika lotincha umumiy ish degan manoni bildiradi\nD) Monarxiya lotincha yakka hokimyat",
            "correct": "D"
        },
        {
            "question": "5-savol:\n“Ma’lum bir axloqiy sifatlarga ega bo‘lmasdan, munosib inson bo‘lmay turib, ijtimoiy hayotda harakat qilib bo‘lmaydi.” Muallifni aniqlang.\n\nA) Alisher Navoiy\nB) Aflotun\nC) Arastu\nD) Amir Temur",
            "correct": "C"
        },
        {
            "question": "6-savol:\nIjtimoiy davlatga togri tarif berilgan javobni toping .\n\nA) Huquq ustuvorligi taminlangan davlat.\nB) Ijtimoiy davlat — har bir inson uchun farovon turmush darajasi, sifatli taʼlim, kafolatli tibbiy xizmat, munosib mehnat sharoiti va adolatli ish haqi, pensiya va nafaqalar, ijtimoiy yordam va xizmatlar tizimi yaratilgan, uy-joyli boʻlish sharoiti mavjud boʻlgan, ijtimoiy tafovutlarni yumshatishga qaratilgan davlat modelidir.\nC) Vijdon erkinligi tamoinlangan davlat\nD) To’la qonli mustqalikka ega , tashqi va ichki siyosatda erkin davlat",
            "correct": "B"
        },
        {
            "question": "7-savol:\nShaxsga oid notogri malumotni aniqlang.\n\nA) Huquqshunoslik fanida shaxs tushunchasi ikki ma’noda, ya’ni jismoniy va yuridik shaxs sifatida ifodalanadi.\nB) Muassa va jamoat fondi tijorat tashkiloti hisoblanadi.\nC) Jismoniy shaxslar deganda O‘zbekiston Respublikasining fuqarolari, boshqa davlatlarning fuqarolari, shuningdek, fuqaroligi bo‘lmagan shaxslar tushuniladi\nD) Tijorat tashkilotlari (foyda olishni o‘z faoliyatining asosiy maqsadi qilib olgan kor xona va tashkilotlar: sotuv bo‘limlari, quruvchi tashkilotlar, ulgurji savdo do‘konlari va v.b )",
            "correct": "B"
        },
        {
            "question": "8-savol:\nTo’g’ri mulohaza keltirilgan malumotni toping.\n\nA) Tijorat tashkilotlari (foyda olishni o‘z faoliyatining asosiy maqsadi qilib olgan kor xona va tashkilotlar: sotuv bo‘limlari, quruvchi tashkilotlar, ulgurji savdo do‘konlari v.b )\nB) Jismoniy shaxs alohida mol-mulkka ega bo‘lgan hamda o‘z majburiyatlari yuzasidan ushbu mol mulk bilan javob beradigan, majburiyatlarni bajara oladigan, sudda da’vogar va javobgar bo‘la oladigan tashkilot\nC) Jamiyat — davlating shakllangan siyosiy institutidir.\nD) O‘zbekiston — boshqaruvning respublika shakliga ega bo‘lgan suveren, demokratik, huquqiy, ijtimoiy va diniy davlat.",
            "correct": "A"
        },
        {
            "question": "9-savol:\nNotogri keltirilgan mulozani toping .\n\nA) Davlat shakllari deyilganda, davlatning boshqaruv, hududiy tuzilishi va siyosiy tartiboti jihatidan qanday shakllarga bo‘lini shi tushuniladi.\nB) Respublika - oliy hokimiyat yakka davlat boshlig'ining qo'lida bo'lgan va bu hokimiyat avloddan avlodga meros qilib beriladigan davlat boshqaruv shakli.\nC) Respublika davlat boshqaruvining shunday shakliki, unda hokimiyat oliy idoralari ma'lum muddatga saylanadi\nD) Respublika shaklidagi boshqaruvga ega bo'l gan davlatning asosiy belgilari quyidagilardan iborat: - hokimiyat oliy idoralarining saylab qo'yilishi; - hokimiyat vakolatlari qat'iy ravishda qonun chi qa ruvchi, ijro etuvchi va sud hokimiyatiga bo'linishi; hokimiyat oliy idoralarining o'z qarorlarini saylangan muddati davomida qabul qilishi; fuqarolarning davlat ishlarini boshqarishda ishtirok eta olishi.",
            "correct": "B"
        },
        {
            "question": "10-savol:\nParlamentar Respublika davlatlari korsatilgan javobni toping.\n\nA) Germaniya, Italiya, O`zbekiston\nB) Buyuk Britaniya, Germaniya, Italiya\nC) Italiya, Gretsiya, AQSH\nD) Germaniya, Italiya, Gretsiya",
            "correct": "D"
        },
        {
            "question": "11-savol:\nQuyidagilardan notogri malumot berilgan javobni toping.\n\nA) Demokratiya lotincha \"xalq hokimiyati\" degan ma'noni anglatadi.\nB) Federativ davlat bir necha davlatlarning birlashuvidan hosil boʻlgan murakkab, ittifoqdosh davlat.\nC) Davlat hokimiyatini amalga oshirish usullari va uslublari tizimiga \"siyosiy tartibot\" deyiladi\nD) Demokratik tartibot sharoitida insonning siyosiy va fuqarolik huquqlari hurmat qilinadi. Fuqarolar davlat hokimiyati idoralarini tuzishda va ularning faoliyatida faol ishtirok etadilar. Demokratik hokimiyatning yagona manbai xalq irodasi hisoblanadi.",
            "correct": "A"
        },
        {
            "question": "12-savol:\nSiyosiy tartbotga oid notogri malumotni toping.\n\nA) Demokratiyaga zid tartibot \"nodemokratik tartibot\" deb ataladi\nB) Totalitar tartibotda har qanday hukmron muxolifat yakson etiladi. Biron-bir irq ning hukmronligi e'lon qilinadi. Va nihoyat, boshqa hududlarni bosib olishga harakat kuchayadi.\nC) Demokratik davlatda g'oyaviy va siyosiy pluralizm konstitutsiya tomonidan qo'llab quvvatlanib, siyosiy partiyalarning faoliyatiga ruxsat etiladi.\nD) Totalitar davlat misoli sifatida sobiq Sovet Ittifoqini keltirish mumkin.",
            "correct": "B"
        },
        {
            "question": "13-savol:\n.... bu davlat tomonidan belgilanadigan, muhofaza qilinadigan, oʻzida erkinlik, tenglik va adolat tamoyillarini ifodalaydigan, ijtimoiy munosabatlarni tartibga solishga qaratilgan, umum majburiy xulq-atvor qoidalari yig'indisidir.\nNuqtalar orasiga mos keluvchi javobni aniqlang.\n\nA) Huquq normasi\nB) Huquq\nC) Axloq\nD) Huquq instituti",
            "correct": "B"
        },
        {
            "question": "14-savol:\nQuyidagilar orasidan notog’ri malumotni toping.\n\nA) Huquq — kishining jamiyatdagi xulqatvorini tartibga soluvchi talab va qoidalar yig’indisi.\nB) “Huquq” atamasi ikki — obyektiv hamda subyektiv huquq ma’nosida qo‘llaniladi\nC) Obyektiv huquq — huquq normalarining yig‘indisi\nD) Subyektiv huquq esa ma’lum bir shaxs yoki guruhga tegishli bo‘lgan huquq",
            "correct": "A"
        },
        {
            "question": "15-savol:\nO‘zbekiston Respublikasi Konstitutsiyasi O‘zbekiston Respublikasining qonunlari O‘zbekiston Respublikasi Oliy Majlisi palatalarining qarorlari O‘zbekiston Respublikasi Prezidentining farmonlari, qarorlari O‘zbekiston Respublikasi Vazirlar Mahkamasining qarorlari Vazirliklar va idoralarning buyruqlari hamda qarorlari Mahalliy davlat hokimiyati organlarining qarorlari.\nYuqoridagilar huquq manbasining qaysi turiga mansub? \n\nA) Huquq normasi\nB) Normativ huquqiy hujjat\nC) Yuridik pretsedent \nD) Huquqiy odat",
            "correct": "B"
        },
        {
            "question": "16-savol:\nQuyidalar orasidan noto’g’ri malumotni toping . \n\nA) Huquq manbasi — huquqning ifoda etilish shakli. Huquq manbasi o‘zida huquq normasining paydo bo‘lishi va amal qilinishiga imkon beruvchi manbalarni ifodalaydi\nB) Pretsedent” so‘zi yunon tilidan kelib chiqqan bo‘lib, “avvalgisi”, “oldingisi” degan maʼno larni anglatadi.\nC) Yuridik pretsedent sud yoki maʼmuriy organning qaroridir\nD) Yuridik pretsedent Aqsh , Kanada , Avstraliya va Buyuk Britaniya kabi davlatlarda mavjud.",
            "correct": "B"
        },
        {
            "question": "17-savol:\n…. — ikki yoki undan ortiq davlatlar o‘rtasida tuziladigan, ular ning huquq va majburiyatlarini o‘rnatadigan, o‘zgartiradigan yoki bekor qiladigan bitim hisoblanadi.\n\nA) Xalqaro odat\nB) Xalqaro tashkilot \nC) Xalqaro shartnoma\nD) Normativ hujjat",
            "correct": "C"
        },
        {
            "question": "18-savol:\n… bu huquq normalariga mos keladigan, yuridik oqibatlarni keltirib chiqaradigan, ijtimoiy foydali ahamiyatga ega bo‘lgan, huquq subyektlarining ongli xatti-harakati (harakatsizligi) hisoblanadi.\n\nA) Huquqiy ong\nB) Huquqiy madaniyat\nC) Huquqiy xulq atvor\nD) Huquqiy shaxs",
            "correct": "C"
        },
        {
            "question": "19-savol:\nXULQ-ATVOR TURLARI xató korsatilgan javobni toping.\n\nA) G'ayriijtimoiy xulq-atvor\nB) Betaraf huquqiy xulq-atvor\nC) Huquqqa mos\nD) Sust",
            "correct": "C"
        },
        {
            "question": "20-savol:\nDavlat madhiyasi (a) yilda, davlat gerbi esa.(b) yilda qabul qilingan.\n\nA) a-1992 yil 10-dekabr, b-1991-yil 18-noyabr\nB) a-1991 yil 10-dekabr, b-1991-yil 2-iyul\nC) a-1992 yil 10-dekabr, b-1992-yil 2-iyul\nD) a-1991 yil 10-dekabr, b-1992-yil 18-noyabr",
            "correct": "C"
        },
        {
            "question": "21-savol:\nQuyidagilar noto'g'ri malumot ko'rsatilgan javobni toping.\n\nA) Oʻzbekiston Respublikasining Davlat madhiyasiga zo'r ehtirom bilan qarash Oʻzbekiston Respublikasi har bir fuqarosining vatanparvarlik burchidir.\nB) Oʻzbekiston Respublikasi Prezidenti lavozimiga kirishish chog'ida u qasamyod qabul qilishidan oldin ijro etiladi.\nC) Davlat televideniye va radioeshittirish kompaniyalari tomonidan har kuni koʻrsatuv va eshittirishlar boshlanishidan avval va tugaganidan so'ng, koʻrsatuv va eshittirishlar kechayu kunduz olib borilganida esa soat 6 da va soat 24 da, yangi yil kechasida soat 24 da ijro etiladi.\nD) O'zbekiston Respublikasi Prezidenti, O'zbekiston Respublikasi Oliy Majlisi Qonunchilik palatasi deputatlari, xalq deputatlari Kengashlari deputatlari saylovlari yoki referendum kunlari ovoz berish o'tkaziladigan binolarda soat 8.00 da ijro etiladi.",
            "correct": "B"
        },
        {
            "question": "22-savol:\nQuyidagilar orasidan to'g'ri keltirilgan javobni toping.\n\nA) Oʻzbekiston Respublikasining Davlat madhiyasi unga nisbatan lozim darajadagi hurmat ta'minlangan holda umummilliy bayramlar va tantanali tadbirlar vaqtida ijro etilishi mumkin emas.\nB) Madhiya ijro etilganda ovoz yozib olish vositalaridan foydalanilishi mumkin.\nC) O'zbekiston Respublikasining Davlat madhiyasi koʻpchilik huzurida ijro etilganda, agar qonunchilikda boshqacha qoida belgilanmagan boʻlsa, hozir boʻlgan kishilar madhiyani tik turib va chap qo'l kaftini ko'krakning chap tomoniga qo'yib, harbiy yoki davlatning boshqa xizmatidagi maxsus kiyimdagi shaxslar esa qo'lini bosh kiyimiga qo'yib tinglaydi.\nD) Agar O'zbekiston Respublikasi Davlat madhiyasining ijro etilishi O'zbekiston Respublikasi Davlat bayrogʻining ko'tarilishi bilan birgalikda amalga oshirilsa, hozir bo'lgan kishilar unga orqasini o'girib turadi.",
            "correct": "B"
        },
        {
            "question": "23-savol:\nOʻzbekiston Respublikasi hududida respublika va xalqaro sport musobaqalarini oʻtkazish vaqtida Oʻzbekiston Respublikasining Davlat madhiyasi…….manfaatdor tashkilotlar bilan kelishib turib belgilab qoʻyadigan qoidalarga muvofiq ijro etiladi.\nNuqtalarni o’rnini to’ldiring.\n\nA) Oʻzbekiston Respublikasi tashqi ishlar vazirligi \nB) Oʻzbekiston Respublikasi sport vazirligi\nC) Oʻzbekiston Respublikasi ichki ishlar \nD) Oʻzbekiston Respublikasi Vazirlar Mahkamasi",
            "correct": "B"
        },
        {
            "question": "24-savol:\nOʻzbekiston Respublikasining Davlat madhiyasi toʻgʻrisidagi qonunchiligini buzganlikda aybdor shaxslar belgilangan tartibda ……javobgarlikka tortiladi.\n\nA) Jinoiy \nB) Intizomiy\nC) Ma’muriy\nD) Fuqaroviy",
            "correct": "C"
        },
        {
            "question": "25-savol:\n“Madhiya to’g’risidagi “ qonunning ijro etilishi ustidan nazorat …….tomonidan amalga oshiriladi.\nNuqtala o’rniga mos javobni tanlang.\n\nA) ichki ishlar organlari \nB) tashqi ishlar vazirligi \nC) DXX\nD) Sud",
            "correct": "A"
        },
        {
            "question": "26-savol:\nQuyidagilardan noto’g’ri mulohaza keltirilgan javobni toping.\n\nA) Oʻzbekiston Respublikasi Davlat bayrogʻining uzunligi 250 santimetrga, kengligi 125 santimetrga teng. Moviy rang, oq rang va yashil rangli enlarning kengligi bir xil. Har bir en 40 santimetrga tengdir.\nB) Oq rangli yangi oy va oʻn ikkita oq rangli besh qirrali yulduzning tasviri moviy rangli yuqori enning oʻrtasidan 70x35 santimetrga teng toʻgʻri toʻrtburchakka sigʻadigan qilib joylashtirilgan.\nC) Oq rangli yangi oy vertikal holatda doʻng tomoni dastaga qaratilgan, dastadan 20 santimetr masofada joylashtirilgan boʻlib, diametri 30 santimetrli doiraga sigʻadi.\nD) Oʻzbekiston Respublikasining Davlat bayrogʻi xalqaro munosabatlarda Oʻzbekiston Respublikasining timsoli boʻladi",
            "correct": "B"
        },
        {
            "question": "27-savol:\nUshbu Qonunning Oʻzbekiston Respublikasi diplomatik vakolatxonalari, konsullik muassasalari, shuningdek xalqaro tashkilotlar huzuridagi vakolatxonalari tomonidan ijro etilishi ustidan nazorat …..(a).… boshqa davlat organlari va boshqa tashkilotlar tomonidan ijro etilishi ustidan nazorat esa ....(b)... tomonidan amalga oshiriladi.\n\nA) a- Oʻzbekiston Respublikasi Prezidenti, b-ichki ishlar organlari\nB) a- Oʻzbekiston Respublikasi Tashqi ishlar vazirligi, b-ichki ishlar organlari\nC) a- Oʻzbekiston Respublikasi Tashqi ishlar vazirligi, b- DXX\nD) a- O'zbekiston Respublikasi Prezidenti, b- DXX",
            "correct": "B"
        },
        {
            "question": "28-savol:\nO'zbekiston Respublikasining Davlat bayrog'ini tayyorlash, saqlash va yo'q qilish tartibi kim tomonidan belgilanadi?\n\nA) Vazirlar Mahkamasi\nB) Ichki ishlar\nC) DXX\nD) TIV",
            "correct": "A"
        },
        {
            "question": "29-savol:\nQuyidagilar orasidan noto'g'ri keltirilgan malumotni aniqlang.\n\nA) Ko'tarib qo'yilgan O'zbekiston Respublikasi Davlat bayrogʻining matosi yer sathidan kamida 2,5 metr balandlikda bo'lishi kerak.\nB) O'zbekiston Respublikasining Davlat bayrog'i binolarning asosiy kirish joyida yoki buning uchun maqbul bo'lgan boshqa joyda, yoxud tegishli tutqichi bo'lgan dastada, yo bo'lmasa flagshtokda bayroqning dastasi binoning old tomoni bilan koʻpi bilan 90 gradusli burchak hosil qiladigan tarzda ko'tariladi.\nC) Oʻzbekiston Respublikasining Davlat bayrog'i bilan bir vaqtda xorijiy davlatlar va (yoki) xalqaro tashkilotlar bayroqlari ko'tarilganda Oʻzbekiston Respublikasining Davlat bayrogʻi xalqaro huquq normalariga va diplomatik protokol qoidalariga muvofiq ko'tariladi.\nD) O'zbekiston Respublikasining Davlat bayrogʻi xorijiy davlatlar va (yoki) xalqaro tashkilotlar bayroqlari bilan bir xil balandlikda joylashtirilishi hamda bir xil o'lchamga ega bo'lishi kerak.",
            "correct": "B"
        },
        {
            "question": "30-savol:\nQuyidagilar orasidan notog'ri malumotni aniqlang.\n\nA) Oʻzbekiston Respublikasi Qurolli Kuchlarining harbiy birlashmalarida, qo'shilmalarida va qismlarida, shuningdek boshqa harbiy tuzilmalarida O'zbekiston Respublikasi Prezidentining farmoniga muvofiq bayroq ko'tariladi.\nB) Oʻzbekiston Respublikasining Davlat bayrogʻiga nisbatan hurmatni ta'minlagan holda, undan jamoat joylarida, binolar va boshqa obyektlarda, yashash yoki ish joylarida, shuningdek ularga tutash boʻlgan hududlarda, transport vositalarining salonida foydalanilishi mumkin.\nC) Harbiy yoki boshqa davlat xizmatida bo'lgan shaxslarning kiyim-boshida va farqlovchi nishonlarida Oʻzbekiston Respublikasi Davlat bayrogʻining tasviri tushirilgan belgilardan foydalanilishi mumkin.\nD) O'zbekiston Respublikasi Davlat bayrogʻining elementlarini nodavlat tashkilotlari hujjatlarining rekvizitlari yoki reklama materiallariga kiritilishiga yo'l qo'yilmaydi.",
            "correct": "A"
        }
    ],

    # ------------------ 2-TEST ------------------
    2: [
        {
            "question": "1-savol:\nQuyidagilar orasidan HUQUQ NORMAsiga oid tog’ri mulohaza keltirilgan javobni toping.\n\nA) U davlat tomonidan o‘rnatiladigan umumajburiy bo’lgan, ijtimoiy munosabatlarni tartibga soluvchi qoida\nB) Uning turlari 4 xil bo’ladi :vakolat beruvchi, man etuvchi, majburiyat yuklovchi va himoyalovchi.\nC) U davlat tomonidan o’rnatilgan, umumajburiy tusga ega bo’lgan hamda davlat tomonidan muhofaza etiladigan davlatning umumajburiy qoidalar yig’indisi\nD) Jamiyatda insonlarning xatti-harakatlarini tartibga soladigan xulq-atvor qoidalar yig’indisi",
            "correct": "A"
        },
        {
            "question": "2-savol:\nQuyidagilarni moslashtiring\na) huquq b) huquq normasi c) huquq tizimi d) huquq instituti g) huquq sohasi\n\n1. davlat tomonidan o‘rnatiladigan umumajburiy bo’lgan, ijtimoiy munosabatlarni tartibga soluvchi qoida\n2. davlat tomonidan o’rnatilgan, umumajburiy tusga ega bo’lgan hamda davlat tomonidan muhofaza etiladigan davlatning umumajburiy qoidalar yig’indisi\n3. bu o‘zaro bog‘liq bo‘lgan bir turdagi ijtimoiy munosabatlarni tartibga soluvchi huquq normalari guruhi\n4. huquqning ichki tuzilishi bo‘lib, huquq normalari, huquq institutlari va huquq sohalarining qat’iy izchillikda joylashgan tartibidir.\n5. bu ijtimoiy munosabatlarning muayyan sohasini tartibga soluvchi huquq normalari va huquq institutlarining yig‘indisi.\n\nA) a-1, b-2, c-3, d-4, g-5\nB) a-2, b-3, c-1, d-5, g-4\nC) a-2, b-1, c-4, d-3, g-5\nD) a-1, b-2, c-3, d-5, g-4",
            "correct": "C"
        },
        {
            "question": "3-savol:\nHuquq normasi elementlariga oid notog'ri malumotni aniqlang.\n\nA) Huquq normasi elementlari uchga; gipoteza, dispozitsiya va sanksiya\nB) Gipoteza lotinchadan, \"faraz qilish\" degan manoni bildiradi.\nC) Dispozitsiya lotinchadan \"joylashuv\", \"bayon qilish\" degan manoni bildirib, o'zida huquq va majburiyatlarni ko'rsatish vazifasini bajaradi.\nD) Sanksiya lotinchadan, \"majburiy chora\" degan manoni bildirib, norma bajarmaganligi uchun majburlov choralarini o'zida aks ettiradi.",
            "correct": "A"
        },
        {
            "question": "4-savol:\nQuyidagi huquq normasi qaysi elementlaridan iboratligini aniqlang.\n\"Davlat nodavlat notijorat tashkilotlarining huquqlari va qonuniy manfaatlariga rioya etilishini ta'minlaydi, ularga jamiyat hayotida ishtirok etish uchun teng huquqiy imkoniyatlar yaratadi\".\n\nA) Gipoteza va dispozitsiyadan\nB) Faqat dispozitsiyadan\nC) Faqat gipotezadan\nD) Gipoteza, dispozitsiya va sanksiyadan",
            "correct": "B"
        },
        {
            "question": "5-savol:\nQuyidagi normaning ta'riflangan qismi huquq normasining qaysi turiga mansub?\n\"Voyaga yetmagan shaxsni ma'muriy huquqbuzarlik sodir etishga jalb qilish bazaviy hisoblash miqdorining oʻn baravaridan o'ttiz baravarigacha miqdorda jarima solishga sabab bo'ladi\". (MJTK 188¹-modda)\n\nA) Sanksiya\nB) Promulgatsiya\nC) Gipoteza\nD) Dispozitsiya",
            "correct": "A"
        },
        {
            "question": "6-savol:\nQuyidagi normaning ta'riflangan qismi huquq normasining qaysi turiga mansub?\n\"Yer berish tartibini buzish, shunday harakat uchun ma'muriy jazo qo'llanilganidan keyin sodir etilgan boʻlsa...\"\n\nA) Sanksiya\nB) Promulgatsiya\nC) Gipoteza\nD) Dispozitsiya",
            "correct": "C"
        },
        {
            "question": "7-savol:\nNotog’ri malumot keltirilgan javobni aniqlang.\n\nA) Ichki huquq tizimi ikkiga; Moddiy va Protsessual huquq sohalariga ajratiladi.\nB) Moddiy huquq sohasi - huquqiy munosabat ishtirokchilarining huquq va majburiyatlarini belgilab beradi.\nC) Protsessual huquq sohasi huquq va majburiyatlarni amalga oshirish tartibini belgilab beradi.\nD) Iqtisodiy protsessual huquqi normalari sudlarning fuqarolik, oilaviy, mehnat, yer bilan bog‘liq va moliyaviy munosabatlar kabi bir qator sohalardagi faoliyatini tartibga soladi. Iqtisodiy protsessual huquqi ishtirokchilari, asosan, jismoniy shaxslar hisoblanadi.",
            "correct": "D"
        },
        {
            "question": "8-savol:\nQuyidagilar orasidan HUQUQBUZARLIK belgilari xató korsatilganini toping.\n\nA) Ayblilik\nB) Subyektiv tomon\nC) Ijtimoiy xavflilik\nD) Jazoga loyiqlik",
            "correct": "B"
        },
        {
            "question": "9-savol:\nMulk bilan aloqador hamda nomulkiy munosabatlarni tartibga soladi. Ushbu qoida qaysi huquq sohasining tarifi?\n\nA) Mehnat\nB) Iqtisodiy\nC) Oilaviy\nD) Fuqaroviy",
            "correct": "D"
        },
        {
            "question": "10-savol:\nXalqaro huquqning fan sifatidagi rivojlanishiga golland huquqshunosi, davlat arbobi va adib….. katta hissa qo‘shgan. U “Urush va tinchlik huquqi” asarida xalqaro huquqning asos lari va prinsiplarini ishlab chiqqan. Nutqalar o’rniga mos keluvchi shaxsni aniqlang.\n\nA) Jan Boden\nB) Lev Tolstoy\nC) Hyugo Grotiyus\nD) Robin Gud",
            "correct": "C"
        },
        {
            "question": "11-savol:\nXalqning o‘zi to‘g‘ridan to‘g‘ri tasdiqlamagan qonun — haqiqiy emas. Ushbu jumlaning muallifi kim ?\n\nA) Jan Jak Russo\nB) Ulpian\nC) Lev Tolstoy\nD) Arastu",
            "correct": "A"
        },
        {
            "question": "12-savol:\nHuquqiy xulq-atvor shakliga oid bo’lmagan javobni aniqlang.\n\nA) Sust\nB) Odatiy\nC) Befarq\nD) Faol",
            "correct": "C"
        },
        {
            "question": "13-savol:\nMulohazalarning yakuniy xulosasidan kelib chiqib mos keluvchi variantni aniqlang. (tog’ri/noto’g’ri)\n\nI- Emansipatsiyalanish uchun kamida 14 yoshga to’lgan va mehnat shartnomasi bilan ishlayotgan yok ota-onasining roziligi bilan biznes faoliyatini amalga oshirayotgan bolishi kerak.\nII- Muassa notijorat tashkiloti hisoblanadi\nIII- Agar shaxs o‘z qilmishining ijtimoiy xavfli xususiyatini anglagan, uning ijtimoiy xavfli oqibatlariga ko‘zi yetgan va ularning yuz berishini istagan bo‘lsa, bunday huquqbuzarlik egri qasddan sodir etilgan deb topiladi.\nIV- Huquqbuzarlik obyekti — bu huquq bilan tartibga solinadigan va muhofaza qilinadigan ijtimoiy munosabatlardir.\nV- Huquqbuzarlikning subyektiv tomoni - bu huquqqa zid xatti-harakatning tashqi belgisidir.\n\nA) I-notogri, II-togri, III-togri, IV-togri, V-notogri\nB) I-togri, II-togri, III-togri, IV-notogri, V-togri\nC) I-notogri, II-togri, III-notogri, IV-notogri, V-notogri\nD) I-notogri, II-togri, III-notogri, IV-togri, V-notogri",
            "correct": "D"
        },
        {
            "question": "14-savol:\nQuyidagilar Togri keltirilgan variantni toping.\n\nA) Monarxiya davlatlar; AQSH, Daniya, Angliya\nB) Parlamentar Respublika davlatlari- Portugaliya, Gretsiya, Italiya, Qatar\nC) Aralash Respublika davlatlari- J Korea, Fransiya\nD) Noanaviy monarxiya - Buyuk Britaniya va Malayziya",
            "correct": "C"
        },
        {
            "question": "15-savol:\nTogri tarif keltirilgan variatni toping.\na- Mamuriy Huquqbuzarlik\nb- Jinoiy huquqbuzarlik\n\nA) a- insonlarning mulkiga yoki shaxsiga qarshi qonunga xilof harakat natijasida yetkazilgan zarar.\nb- xizmat burchini bajarib turganda mehnat tartib-qoidalarining buzilishi.\nB) a- xizmat burchini bajarib turganda mehnat tartib-qoidalarining buzilishi.\nb- Jinoyat kodeksi bilan taqiqlangan, aybli ijtimoiy xavfli qilmish jazo qo‘llash tahdidi bilan jinoyat deb topiladi.\nC) a- shaxsga, fuqarolarning huquqlari va erkinliklariga, mulkchilikka tajovuz qiluvchi g‘ayrihuquqiy, aybli sodir etilgan harakat yoki harakatsizlik.\nb- shaxsga, uning huquq va erkinliklariga, jamiyat va davlat manfaatlariga qarshi sodir etilgan huquqbuzarlik\nD) a- Jinoyat kodeksi bilan taqiqlangan qilmish.\nb- insonlarning mulkiga yoki shaxsiga qarshi qonunga xilof harakat.",
            "correct": "C"
        },
        {
            "question": "16-savol:\nHuquqbuzarlikning tarkibi nimalardan iborat?\n\nA) Subyekt, obyekt, subyektiv huquq, obyektiv majburiyat\nB) Subyekt, obyekt, subyektiv tomon, obyektiv tomon\nC) Ijtimoiy xavflilik, ayb, huquqqa zidlik, jazoga loyiqlik\nD) Ijtimoiy xavflilik, qonunga zidlik, subyekt, obyekt",
            "correct": "B"
        },
        {
            "question": "17-savol:\nTeshavoy aka 2026-yil 12-avgust kuni 23:00 atrofida Afsona savdo majmuasiga Azamat akaning \"Alpha\" nomli oyoq kiyim do'koniga og'irlikka tushdi.\nYuqoridagi holatga ko'ra Jinoyatning tarkibi togri keltirilgan javobni toping.\n\nA) Subyektiv tomondan ehtiyotsizlik natijasida sodir etilgan\nB) Obyekti Teshavoy aka va Azamat aka\nC) Subyektiv tomondan egri qasd asosida sodir etilgan\nD) Obyektiv tomondan Afsona savdo majmuasidagi \"Alpha\" dokoniga yashirincha kirib sodir etilgan",
            "correct": "D"
        },
        {
            "question": "18-savol:\nFuqaroviy huquqbuzarlikka oid togri mulohazani aniqlang.\n\nA) xizmat burchini bajarib turganda har qanday mehnatda majburiy bo'lgan mehnat tartib-qoidalarining va rahbarlikka bo'ysunish tamoyillarining buzilishi. Masalan, ishga, oʻqishga kech qolish...\nB) insonlarning mulkiga yoki shaxsiga qarshi qonunga xilof harakat (yoki harakatsizlik) natijasida yetkazilgan zarar. Masalan, bir shaxsdan qarz olib, uni vaqtida qaytarmaslik; shartnomalarni, majburiyatlarni bajarmaslik va boshqalar\nC) Jinoyat kodeksi bilan taqiqlangan, aybli ijtimoiy xavfli qilmish (harakat yoki harakatsizlik) jazo qoʻllash tahdidi bilan Fuqaroviy huquqbuzarlik deb topiladi.\nD) qonun hujjatlariga binoan ma'muriy javobgarlikka tortish nazarda tutilgan, shaxsga, fuqarolarning huquqlari va erkinliklariga tajovuz qiluvchi sodir etilgan harakat yoki harakatsizlik",
            "correct": "B"
        },
        {
            "question": "19-savol:\nYuridik javobgarlik turlarini xató korsatilgan javobni aniqlang.\n\nA) Intizomiy\nB) Harbiy\nC) Fuqaroviy\nD) Mamuriy",
            "correct": "B"
        },
        {
            "question": "20-savol:\nMamuriy jazolarga kirmaydiganini aniqlang.\n\nA) Jarima\nB) Musodara qilish\nC) Maxsus huquqdan mahrum qilish\nD) Muayyan huquqdan mahrum qilish",
            "correct": "D"
        },
        {
            "question": "21-savol:\nMamuriy qamoq muddatini aniqlang.\n\nA) 3 sutkadan 15 sutkagacha , ayrim hollarda 1 yilgacha\nB) 1 sutkadan 15 sutkagacha, ayrim hollarda 30 sutkagacha\nC) 3 sutkadan 15 sutkagacha, ayrim hollarda 30 sutkagacha\nD) 1 sutkadan 15 sutkchagacha, ayrim hollarda 60 kungacha",
            "correct": "C"
        },
        {
            "question": "22-savol:\nO’lim jazosi O’zbekistonda qachon rasman bekor qilindi va qonunchilik hujjatlaridan olib tashlandi.\n\nA) 2008-yil 1-avgust\nB) 2005-yil 1-avgust\nC) 2005-yil 1-yanvar\nD) 2008-yil 1-yanvar",
            "correct": "D"
        },
        {
            "question": "23-savol:\nJinoiy jazolar togri korsatilgan qatorni aniqlang.\n\nA) Umrbod ozodlikdan mahrum qilish , Jarima , Axloq tuzatish ishlari\nB) Majburiy jamoat ishlari, Qamoq, Jarima\nC) Muayyan huquqdan mahrum etish, Jarima, Qamoq\nD) Maxsus huquqdan mahrum etish , Jarima, Qamoq",
            "correct": "A"
        },
        {
            "question": "24-savol:\nUmrbod ozodlikdan mahrum etish jazosi kimlarga tayinlanmaydi?\n\nA) 18 yoshga to’lmaganlarga, I va II guruh nogironlariga , harbiy xizmatchilarga\nB) Homilador ayollarga , 16 yoshga tolmaganlarga , chet el fuqarolariga\nC) 60 yoshdan oshgan erkaklarga , ayollarga, 18 yoshga to’lmaganlarga\nD) Ayollarga , harbiy xizmatchilarga, 16 yoshga to’lmaganlarga",
            "correct": "C"
        },
        {
            "question": "25-savol:\nIntizomiy jazolar xató korsatilgan javobni aniqlang.\n\nA) Hayfsan\nB) Ogohlantirish\nC) Jarima ( oyligining 30 %igacha) agr mehnat shartnomasida korsatildan bolsa 50%\nD) Mehnat shartnomasini bekor qilish",
            "correct": "B"
        },
        {
            "question": "26-savol:\nMamuriy ogohlantirish qancha muddat davomida eng kopi bir marta qollaniladi?\n\nA) Bir oyda\nB) Olti oyda\nC) Ikki yilda\nD) Bir yilda",
            "correct": "D"
        },
        {
            "question": "27-savol:\nIntizomiy javobgarlikka oid notogri malumot korsatilgan javobni aniqlang.\n\nA) Agar intizomiy jazo qoʻllanilgan kundan eʼtiboran olti oy ichida xodimga yangi intizomiy jazo qoʻllanilmasa, u intizomiy jazoga tortilmagan deb hisoblanadi.\nB) Oʻziga nisbatan intizomiy jazo chorasini qoʻllash haqidagi buyruq bilan tanishtirilmagan xodim intizomiy jazosi boʻlmagan deb hisoblanadi.\nC) Intizomiy qilmish deganda xodim tomonidan oʻz mehnat majburiyatlarini aybli tarzda, gʻayriqonuniy ravishda bajarmaganligi yoki lozim darajada bajarmaganligi (mehnat (lavozim) majburiyatlarining buzilishi) tushuniladi.\nD) Barchasi to'g'ri",
            "correct": "D"
        },
        {
            "question": "28-savol:\nMamuriy jazolarga oid notogri mulohazani toping.\n\nA) Oʻqotar ov qurolini, pnevmatik ov qurolini hamda uning oʻq-dorilarini haqini toʻlash sharti bilan olib qoʻyish asosiy tirikchilik manbai ovchilik boʻlgan shaxslarga nisbatan qoʻllanilishi mumkin emas.\nB) Maxsus huquqdan mahrum qilish muddati uch kundan kam boʻlmasligi kerak.\nC) Haq toʻlanadigan jamoat ishlariga jalb etiladigan shaxslar ish haqining ellik foizi aliment majburiyatlari boʻyicha qarzni toʻlashga yoʻnaltiriladi.\nD) Maʼmuriy qamoqqa olish chorasi homilador ayollarga, uch yoshgacha bolasi boʻlgan ayollarga, oʻn toʻrt yoshgacha boʻlgan bolasini yakka oʻzi tarbiyalayotgan shaxslarga, oʻn sakkiz yoshga toʻlmagan shaxslarga, birinchi va ikkinchi guruh nogironligi boʻlgan shaxslarga nisbatan qoʻllanilishi mumkin emas.",
            "correct": "B"
        },
        {
            "question": "29-savol:\nJinoiy javobgarlikka oid notogri malumotni toping.\n\nA) Majburiy jamoat ishlari pensiya yoshiga yetgan shaxslarga, oʻn olti yoshga toʻlmagan shaxslarga, homilador ayollarga, uch yoshga toʻlmagan bolalari bor ayollarga, birinchi va ikkinchi guruh nogironligi boʻlgan shaxslarga, harbiy xizmatchilarga, chet el fuqarolariga va Oʻzbekiston Respublikasida doimiy yashamaydigan shaxslarga nisbatan qoʻllanilmaydi.\nB) Maxsus huquqdan mahrum qilish aybdorning mansabi yoki ish faoliyati bilan bevosita bogʻliq boʻlgan jinoyatni sodir etganligi uchun asosiy jazo tariqasida tayinlanganda — bir yildan besh yilgacha muddatga, qoʻshimcha jazo tariqasida tayinlanganda — bir yildan uch yilgacha muddatga belgilanadi.\nC) Jarima aybdordan davlat daromadiga ushbu Kodeksda belgilangan miqdorda pul undirishdir.\nD) Jarima bazaviy hisoblash miqdorining besh baravaridan olti yuz baravarigacha miqdorda belgilanadi.",
            "correct": "D"
        },
        {
            "question": "30-savol:\nVoyaga yetmaganlarning Jinoiy javobgarligiga oid notogri malumotni aniqlang.\n\nA) Oʻn sakkiz yoshga toʻlmasdan jinoyat sodir etgan shaxslarga quyidagi asosiy jazolar qoʻllanilishi mumkin: jarima, majburiy jamoat ishlari, axloq tuzatish ishlari, ozodlikni cheklash, ozodlikdan mahrum qilish.\nB) Oʻn sakkiz yoshga toʻlmasdan jinoyat sodir etgan shaxslarga nisbatan qoʻshimcha jazolar tayinlanishi mumkin emas.\nC) Ozodlikni cheklash voyaga yetmagan mahkumlarga nisbatan asosiy jazo chorasi sifatida bir oydan uch yilgacha muddatga tayinlanadi\nD) Jinoyat sodir etish paytida oʻn toʻrt yoshdan oʻn sakkiz yoshgacha boʻlgan shaxslarga nisbatan bir necha hukm yuzasidan tayinlanadigan ozodlikdan mahrum qilish jazosining muddati oʻn besh yildan oshmasligi kerak",
            "correct": "B"
        }
    ],

    # ------------------ 3-TEST ------------------
    3: [
        {
            "question": "1-savol:\nQuyidagilar orasidan HUQUQ NORMAsiga oid tog’ri mulohaza keltirilgan javobni toping.\n\nA) U davlat tomonidan o‘rnatiladigan umumajburiy bo’lgan, ijtimoiy munosabatlarni tartibga soluvchi qoida\nB) Uning turlari 4 xil bo’ladi :vakolat beruvchi, man etuvchi, majburiyat yuklovchi va himoyalovchi.\nC) U davlat tomonidan o’rnatilgan, umumajburiy tusga ega bo’lgan hamda davlat tomonidan muhofaza etiladigan davlatning umumajburiy qoidalar yig’indisi\nD) Jamiyatda insonlarning xatti-harakatlarini tartibga soladigan xulq-atvor qoidalar yig’indisi",
            "correct": "A"
        },
        {
            "question": "2-savol:\nQuyidagilarni moslashtiring\na) huquq b) huquq normasi c) huquq tizimi d) huquq instituti g) huquq sohasi\n\n1. davlat tomonidan o‘rnatiladigan umumajburiy bo’lgan, ijtimoiy munosabatlarni tartibga soluvchi qoida\n2. davlat tomonidan o’rnatilgan, umumajburiy tusga ega bo’lgan hamda davlat tomonidan muhofaza etiladigan davlatning umumajburiy qoidalar yig’indisi\n3. bu o‘zaro bog‘liq bo‘lgan bir turdagi ijtimoiy munosabatlarni tartibga soluvchi huquq normalari guruhi\n4. huquqning ichki tuzilishi bo‘lib, huquq normalari, huquq institutlari va huquq sohalarining qat’iy izchillikda joylashgan tartibidir.\n5. bu ijtimoiy munosabatlarning muayyan sohasini tartibga soluvchi huquq normalari va huquq institutlarining yig‘indisi.\n\nA) a-1, b-2, c-3, d-4, g-5\nB) a-2, b-3, c-1, d-5, g-4\nC) a-2, b-1, c-4, d-3, g-5\nD) a-1, b-2, c-3, d-5, g-4",
            "correct": "C"
        },
        {
            "question": "3-savol:\nHuquq normasi elementlariga oid notog'ri malumotni aniqlang.\n\nA) Huquq normasi elementlari uchga; gipoteza, dispozitsiya va sanksiya\nB) Gipoteza lotinchadan, \"faraz qilish\" degan manoni bildiradi.\nC) Dispozitsiya lotinchadan \"joylashuv\", \"bayon qilish\" degan manoni bildirib, o'zida huquq va majburiyatlarni ko'rsatish vazifasini bajaradi.\nD) Sanksiya lotinchadan, \"majburiy chora\" degan manoni bildirib, norma bajarmaganligi uchun majburlov choralarini o'zida aks ettiradi.",
            "correct": "A"
        },
        {
            "question": "4-savol:\nQuyidagi huquq normasi qaysi elementlaridan iboratligini aniqlang.\n\"Davlat nodavlat notijorat tashkilotlarining huquqlari va qonuniy manfaatlariga rioya etilishini ta'minlaydi, ularga jamiyat hayotida ishtirok etish uchun teng huquqiy imkoniyatlar yaratadi\".\n\nA) Gipoteza va dispozitsiyadan\nB) Faqat dispozitsiyadan\nC) Faqat gipotezadan\nD) Gipoteza, dispozitsiya va sanksiyadan",
            "correct": "B"
        },
        {
            "question": "5-savol:\nQuyidagi normaning ta'riflangan qismi huquq normasining qaysi turiga mansub?\n\"Voyaga yetmagan shaxsni ma'muriy huquqbuzarlik sodir etishga jalb qilish bazaviy hisoblash miqdorining oʻn baravaridan o'ttiz baravarigacha miqdorda jarima solishga sabab bo'ladi\". (MJTK 188¹-modda)\n\nA) Sanksiya\nB) Promulgatsiya\nC) Gipoteza\nD) Dispozitsiya",
            "correct": "A"
        },
        {
            "question": "6-savol:\nQuyidagi normaning ta'riflangan qismi huquq normasining qaysi turiga mansub?\n\"Yer berish tartibini buzish, shunday harakat uchun ma'muriy jazo qo'llanilganidan keyin sodir etilgan boʻlsa...\"\n\nA) Sanksiya\nB) Promulgatsiya\nC) Gipoteza\nD) Dispozitsiya",
            "correct": "C"
        },
        {
            "question": "7-savol:\nNotog’ri malumot keltirilgan javobni aniqlang.\n\nA) Ichki huquq tizimi ikkiga; Moddiy va Protsessual huquq sohalariga ajratiladi.\nB) Moddiy huquq sohasi - huquqiy munosabat ishtirokchilarining huquq va majburiyatlarini belgilab beradi.\nC) Protsessual huquq sohasi huquq va majburiyatlarni amalga oshirish tartibini belgilab beradi.\nD) Iqtisodiy protsessual huquqi normalari sudlarning fuqarolik, oilaviy, mehnat, yer bilan bog‘liq va moliyaviy munosabatlar kabi bir qator sohalardagi faoliyatini tartibga soladi. Iqtisodiy protsessual huquqi ishtirokchilari, asosan, jismoniy shaxslar hisoblanadi.",
            "correct": "D"
        },
        {
            "question": "8-savol:\nQuyidagilar orasidan HUQUQBUZARLIK belgilari xató korsatilganini toping.\n\nA) Ayblilik\nB) Subyektiv tomon\nC) Ijtimoiy xavflilik\nD) Jazoga loyiqlik",
            "correct": "B"
        },
        {
            "question": "9-savol:\nMulk bilan aloqador hamda nomulkiy munosabatlarni tartibga soladi. Ushbu qoida qaysi huquq sohasining tarifi?\n\nA) Mehnat\nB) Iqtisodiy\nC) Oilaviy\nD) Fuqaroviy",
            "correct": "D"
        },
        {
            "question": "10-savol:\nXalqaro huquqning fan sifatidagi rivojlanishiga golland huquqshunosi, davlat arbobi va adib….. katta hissa qo‘shgan. U “Urush va tinchlik huquqi” asarida xalqaro huquqning asos lari va prinsiplarini ishlab chiqqan. Nutqalar o’rniga mos keluvchi shaxsni aniqlang.\n\nA) Jan Boden\nB) Lev Tolstoy\nC) Hyugo Grotiyus\nD) Robin Gud",
            "correct": "C"
        },
        {
            "question": "11-savol:\nXalqning o‘zi to‘g‘ridan to‘g‘ri tasdiqlamagan qonun — haqiqiy emas. Ushbu jumlaning muallifi kim ?\n\nA) Jan Jak Russo\nB) Ulpian\nC) Lev Tolstoy\nD) Arastu",
            "correct": "A"
        },
        {
            "question": "12-savol:\nHuquqiy xulq-atvor shakliga oid bo’lmagan javobni aniqlang.\n\nA) Sust\nB) Odatiy\nC) Befarq\nD) Faol",
            "correct": "C"
        },
        {
            "question": "13-savol:\nMulohazalarning yakuniy xulosasidan kelib chiqib mos keluvchi variantni aniqlang. (tog’ri/noto’g’ri)\n\nI- Emansipatsiyalanish uchun kamida 14 yoshga to’lgan va mehnat shartnomasi bilan ishlayotgan yok ota-onasining roziligi bilan biznes faoliyatini amalga oshirayotgan bolishi kerak.\nII- Muassa notijorat tashkiloti hisoblanadi\nIII- Agar shaxs o‘z qilmishining ijtimoiy xavfli xususiyatini anglagan, uning ijtimoiy xavfli oqibatlariga ko‘zi yetgan va ularning yuz berishini istagan bo‘lsa, bunday huquqbuzarlik egri qasddan sodir etilgan deb topiladi.\nIV- Huquqbuzarlik obyekti — bu huquq bilan tartibga solinadigan va muhofaza qilinadigan ijtimoiy munosabatlardir.\nV- Huquqbuzarlikning subyektiv tomoni - bu huquqqa zid xatti-harakatning tashqi belgisidir.\n\nA) I-notogri, II-togri, III-togri, IV-togri, V-notogri\nB) I-togri, II-togri, III-togri, IV-notogri, V-togri\nC) I-notogri, II-togri, III-notogri, IV-notogri, V-notogri\nD) I-notogri, II-togri, III-notogri, IV-togri, V-notogri",
            "correct": "D"
        },
        {
            "question": "14-savol:\nQuyidagilar Togri keltirilgan variantni toping.\n\nA) Monarxiya davlatlar; AQSH, Daniya, Angliya\nB) Parlamentar Respublika davlatlari- Portugaliya, Gretsiya, Italiya, Qatar\nC) Aralash Respublika davlatlari- J Korea, Fransiya\nD) Noanaviy monarxiya - Buyuk Britaniya va Malayziya",
            "correct": "C"
        },
        {
            "question": "15-savol:\nTogri tarif keltirilgan variatni toping.\na- Mamuriy Huquqbuzarlik\nb- Jinoiy huquqbuzarlik\n\nA) a- insonlarning mulkiga yoki shaxsiga qarshi qonunga xilof harakat natijasida yetkazilgan zarar.\nb- xizmat burchini bajarib turganda mehnat tartib-qoidalarining buzilishi.\nB) a- xizmat burchini bajarib turganda mehnat tartib-qoidalarining buzilishi.\nb- Jinoyat kodeksi bilan taqiqlangan, aybli ijtimoiy xavfli qilmish jazo qo‘llash tahdidi bilan jinoyat deb topiladi.\nC) a- shaxsga, fuqarolarning huquqlari va erkinliklariga, mulkchilikka tajovuz qiluvchi g‘ayrihuquqiy, aybli sodir etilgan harakat yoki harakatsizlik.\nb- shaxsga, uning huquq va erkinliklariga, jamiyat va davlat manfaatlariga qarshi sodir etilgan huquqbuzarlik\nD) a- Jinoyat kodeksi bilan taqiqlangan qilmish.\nb- insonlarning mulkiga yoki shaxsiga qarshi qonunga xilof harakat.",
            "correct": "C"
        },
        {
            "question": "16-savol:\nHuquqbuzarlikning tarkibi nimalardan iborat?\n\nA) Subyekt, obyekt, subyektiv huquq, obyektiv majburiyat\nB) Subyekt, obyekt, subyektiv tomon, obyektiv tomon\nC) Ijtimoiy xavflilik, ayb, huquqqa zidlik, jazoga loyiqlik\nD) Ijtimoiy xavflilik, qonunga zidlik, subyekt, obyekt",
            "correct": "B"
        },
        {
            "question": "17-savol:\nTeshavoy aka 2026-yil 12-avgust kuni 23:00 atrofida Afsona savdo majmuasiga Azamat akaning \"Alpha\" nomli oyoq kiyim do'koniga og'irlikka tushdi.\nYuqoridagi holatga ko'ra Jinoyatning tarkibi togri keltirilgan javobni toping.\n\nA) Subyektiv tomondan ehtiyotsizlik natijasida sodir etilgan\nB) Obyekti Teshavoy aka va Azamat aka\nC) Subyektiv tomondan egri qasd asosida sodir etilgan\nD) Obyektiv tomondan Afsona savdo majmuasidagi \"Alpha\" dokoniga yashirincha kirib sodir etilgan",
            "correct": "D"
        },
        {
            "question": "18-savol:\nFuqaroviy huquqbuzarlikka oid togri mulohazani aniqlang.\n\nA) xizmat burchini bajarib turganda har qanday mehnatda majburiy bo'lgan mehnat tartib-qoidalarining va rahbarlikka bo'ysunish tamoyillarining buzilishi. Masalan, ishga, oʻqishga kech qolish...\nB) insonlarning mulkiga yoki shaxsiga qarshi qonunga xilof harakat (yoki harakatsizlik) natijasida yetkazilgan zarar. Masalan, bir shaxsdan qarz olib, uni vaqtida qaytarmaslik; shartnomalarni, majburiyatlarni bajarmaslik va boshqalar\nC) Jinoyat kodeksi bilan taqiqlangan, aybli ijtimoiy xavfli qilmish (harakat yoki harakatsizlik) jazo qoʻllash tahdidi bilan Fuqaroviy huquqbuzarlik deb topiladi.\nD) qonun hujjatlariga binoan ma'muriy javobgarlikka tortish nazarda tutilgan, shaxsga, fuqarolarning huquqlari va erkinliklariga tajovuz qiluvchi sodir etilgan harakat yoki harakatsizlik",
            "correct": "B"
        },
        {
            "question": "19-savol:\nYuridik javobgarlik turlarini xató korsatilgan javobni aniqlang.\n\nA) Intizomiy\nB) Harbiy\nC) Fuqaroviy\nD) Mamuriy",
            "correct": "B"
        },
        {
            "question": "20-savol:\nMamuriy jazolarga kirmaydiganini aniqlang.\n\nA) Jarima\nB) Musodara qilish\nC) Maxsus huquqdan mahrum qilish\nD) Muayyan huquqdan mahrum qilish",
            "correct": "D"
        },
        {
            "question": "21-savol:\nMamuriy qamoq muddatini aniqlang.\n\nA) 3 sutkadan 15 sutkagacha , ayrim hollarda 1 yilgacha\nB) 1 sutkadan 15 sutkagacha, ayrim hollarda 30 sutkagacha\nC) 3 sutkadan 15 sutkagacha, ayrim hollarda 30 sutkagacha\nD) 1 sutkadan 15 sutkchagacha, ayrim hollarda 60 kungacha",
            "correct": "C"
        },
        {
            "question": "22-savol:\nO’lim jazosi O’zbekistonda qachon rasman bekor qilindi va qonunchilik hujjatlaridan olib tashlandi.\n\nA) 2008-yil 1-avgust\nB) 2005-yil 1-avgust\nC) 2005-yil 1-yanvar\nD) 2008-yil 1-yanvar",
            "correct": "D"
        },
        {
            "question": "23-savol:\nJinoiy jazolar togri korsatilgan qatorni aniqlang.\n\nA) Umrbod ozodlikdan mahrum qilish , Jarima , Axloq tuzatish ishlari\nB) Majburiy jamoat ishlari, Qamoq, Jarima\nC) Muayyan huquqdan mahrum etish, Jarima, Qamoq\nD) Maxsus huquqdan mahrum etish , Jarima, Qamoq",
            "correct": "A"
        },
        {
            "question": "24-savol:\nUmrbod ozodlikdan mahrum etish jazosi kimlarga tayinlanmaydi?\n\nA) 18 yoshga to’lmaganlarga, I va II guruh nogironlariga , harbiy xizmatchilarga\nB) Homilador ayollarga , 16 yoshga tolmaganlarga , chet el fuqarolariga\nC) 60 yoshdan oshgan erkaklarga , ayollarga, 18 yoshga to’lmaganlarga\nD) Ayollarga , harbiy xizmatchilarga, 16 yoshga to’lmaganlarga",
            "correct": "C"
        },
        {
            "question": "25-savol:\nIntizomiy jazolar xató korsatilgan javobni aniqlang.\n\nA) Hayfsan\nB) Ogohlantirish\nC) Jarima ( oyligining 30 %igacha) agr mehnat shartnomasida korsatildan bolsa 50%\nD) Mehnat shartnomasini bekor qilish",
            "correct": "B"
        },
        {
            "question": "26-savol:\nMamuriy ogohlantirish qancha muddat davomida eng kopi bir marta qollaniladi?\n\nA) Bir oyda\nB) Olti oyda\nC) Ikki yilda\nD) Bir yilda",
            "correct": "D"
        },
        {
            "question": "27-savol:\nIntizomiy javobgarlikka oid notogri malumot korsatilgan javobni aniqlang.\n\nA) Agar intizomiy jazo qoʻllanilgan kundan eʼtiboran olti oy ichida xodimga yangi intizomiy jazo qoʻllanilmasa, u intizomiy jazoga tortilmagan deb hisoblanadi.\nB) Oʻziga nisbatan intizomiy jazo chorasini qoʻllash haqidagi buyruq bilan tanishtirilmagan xodim intizomiy jazosi boʻlmagan deb hisoblanadi.\nC) Intizomiy qilmish deganda xodim tomonidan oʻz mehnat majburiyatlarini aybli tarzda, gʻayriqonuniy ravishda bajarmaganligi yoki lozim darajada bajarmaganligi (mehnat (lavozim) majburiyatlarining buzilishi) tushuniladi.\nD) Barchasi to'g'ri",
            "correct": "D"
        },
        {
            "question": "28-savol:\nMamuriy jazolarga oid notogri mulohazani toping.\n\nA) Oʻqotar ov qurolini, pnevmatik ov qurolini hamda uning oʻq-dorilarini haqini toʻlash sharti bilan olib qoʻyish asosiy tirikchilik manbai ovchilik boʻlgan shaxslarga nisbatan qoʻllanilishi mumkin emas.\nB) Maxsus huquqdan mahrum qilish muddati uch kundan kam boʻlmasligi kerak.\nC) Haq toʻlanadigan jamoat ishlariga jalb etiladigan shaxslar ish haqining ellik foizi aliment majburiyatlari boʻyicha qarzni toʻlashga yoʻnaltiriladi.\nD) Maʼmuriy qamoqqa olish chorasi homilador ayollarga, uch yoshgacha bolasi boʻlgan ayollarga, oʻn toʻrt yoshgacha boʻlgan bolasini yakka oʻzi tarbiyalayotgan shaxslarga, oʻn sakkiz yoshga toʻlmagan shaxslarga, birinchi va ikkinchi guruh nogironligi boʻlgan shaxslarga nisbatan qoʻllanilishi mumkin emas.",
            "correct": "B"
        },
        {
            "question": "29-savol:\nJinoiy javobgarlikka oid notogri malumotni toping.\n\nA) Majburiy jamoat ishlari pensiya yoshiga yetgan shaxslarga, oʻn olti yoshga toʻlmagan shaxslarga, homilador ayollarga, uch yoshga toʻlmagan bolalari bor ayollarga, birinchi va ikkinchi guruh nogironligi boʻlgan shaxslarga, harbiy xizmatchilarga, chet el fuqarolariga va Oʻzbekiston Respublikasida doimiy yashamaydigan shaxslarga nisbatan qoʻllanilmaydi.\nB) Maxsus huquqdan mahrum qilish aybdorning mansabi yoki ish faoliyati bilan bevosita bogʻliq boʻlgan jinoyatni sodir etganligi uchun asosiy jazo tariqasida tayinlanganda — bir yildan besh yilgacha muddatga, qoʻshimcha jazo tariqasida tayinlanganda — bir yildan uch yilgacha muddatga belgilanadi.\nC) Jarima aybdordan davlat daromadiga ushbu Kodeksda belgilangan miqdorda pul undirishdir.\nD) Jarima bazaviy hisoblash miqdorining besh baravaridan olti yuz baravarigacha miqdorda belgilanadi.",
            "correct": "D"
        },
        {
            "question": "30-savol:\nVoyaga yetmaganlarning Jinoiy javobgarligiga oid notogri malumotni aniqlang.\n\nA) Oʻn sakkiz yoshga toʻlmasdan jinoyat sodir etgan shaxslarga quyidagi asosiy jazolar qoʻllanilishi mumkin: jarima, majburiy jamoat ishlari, axloq tuzatish ishlari, ozodlikni cheklash, ozodlikdan mahrum qilish.\nB) Oʻn sakkiz yoshga toʻlmasdan jinoyat sodir etgan shaxslarga nisbatan qoʻshimcha jazolar tayinlanishi mumkin emas.\nC) Ozodlikni cheklash voyaga yetmagan mahkumlarga nisbatan asosiy jazo chorasi sifatida bir oydan uch yilgacha muddatga tayinlanadi\nD) Jinoyat sodir etish paytida oʻn toʻrt yoshdan oʻn sakkiz yoshgacha boʻlgan shaxslarga nisbatan bir necha hukm yuzasidan tayinlanadigan ozodlikdan mahrum qilish jazosining muddati oʻn besh yildan oshmasligi kerak",
            "correct": "B"
        }
    ]
}

USERS = {}

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    global ADMIN_CHAT_ID
    user = update.effective_user
    user_id = user.id

    if user.username and user.username.lower() == ADMIN_USERNAME.lower():
        ADMIN_CHAT_ID = user_id

    context.user_data.clear()

    if user_id not in USERS or "phone" not in USERS[user_id]:
        button = KeyboardButton("📱 Telefon raqamni yuborish", request_contact=True)
        keyboard = ReplyKeyboardMarkup([[button]], resize_keyboard=True, one_time_keyboard=True)
        text = (
            "⚖️ **Prof Huquq** botiga xush kelibsiz!\n\n"
            "📲 Tizimdan foydalanish uchun quyidagi tugma orqali telefon raqamingizni yuboring."
        )
        await update.message.reply_text(text, reply_markup=keyboard, parse_mode="Markdown")
        return

    if "name" not in USERS[user_id]:
        await update.message.reply_text(
            "✍️ Ism va familiyangizni kiriting:\n_(Masalan: Ali Valiyev)_",
            reply_markup=ReplyKeyboardRemove(),
            parse_mode="Markdown"
        )
        return

    await show_test_selection(update, context)

async def show_test_selection(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    user_id = update.effective_user.id
    context.user_data.clear()
    
    text = (
        f"👋 Xush kelibsiz, **{USERS[user_id]['name']}**!\n\n"
        "📅 Test topshirmoqchi bo'lgan test raqamini kiriting (1–100):"
    )
    await update.message.reply_text(text, reply_markup=ReplyKeyboardRemove(), parse_mode="Markdown")

async def handle_contact(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    user_id = update.effective_user.id

    contact = update.message.contact
    if user_id not in USERS:
        USERS[user_id] = {"completed_tests": {}}
    
    USERS[user_id]["phone"] = contact.phone_number
    
    await update.message.reply_text(
        "✅ Telefon raqamingiz qabul qilindi.\n\n✍️ Endi ism va familiyangizni kiriting:",
        reply_markup=ReplyKeyboardRemove(),
        parse_mode="Markdown"
    )

async def send_question(update: Update, context: ContextTypes.DEFAULT_TYPE, q_index: int) -> None:
    selected_test = context.user_data.get("selected_test")
    context.user_data["current_question"] = q_index
    
    keyboard = [
        ["A", "B"],
        ["C", "D"],
        ["🔙 Ortga qaytish"]
    ]
    reply_markup = ReplyKeyboardMarkup(keyboard, resize_keyboard=True)
    q_text = QUIZ_DATA[selected_test][q_index]["question"]
    await update.message.reply_text(q_text, reply_markup=reply_markup)

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    user = update.effective_user
    user_id = user.id
    text = update.message.text.strip()

    global ADMIN_CHAT_ID
    if user.username and user.username.lower() == ADMIN_USERNAME.lower():
        ADMIN_CHAT_ID = user_id

    if user_id not in USERS or "phone" not in USERS[user_id]:
        await start(update, context)
        return

    if "name" not in USERS[user_id]:
        USERS[user_id]["name"] = text
        await start(update, context)
        return

    if text == "🔙 Ortga qaytish":
        await show_test_selection(update, context)
        return

    completed_tests = USERS[user_id].get("completed_tests", {})
    selected_test = context.user_data.get("selected_test")

    if text.isdigit() and selected_test is None:
        target_test = int(text)
        
        if target_test < 1 or target_test > 100:
            await update.message.reply_text("⚠️ Iltimos, 1 dan 100 gacha bo'lgan raqam kiriting.")
            return

        if target_test not in QUIZ_DATA:
            await update.message.reply_text(f"📌 {target_test}-test hali kiritilmagan.")
            return
        
        if target_test in completed_tests:
            saved_text = completed_tests[target_test]
            await update.message.reply_text(
                f"ℹ️ Siz {target_test}-testni allaqachon topshirgansiz.\n\n{saved_text}",
                parse_mode="Markdown"
            )
            return
        
        context.user_data["selected_test"] = target_test
        keyboard = [
            ["1", "2", "3", "4", "5"],
            ["6", "7", "8", "9", "10"],
            ["11", "12", "13", "14", "15"],
            ["16", "17", "18", "19", "20"],
            ["21", "22", "23", "24", "25"],
            ["26", "27", "28", "29", "30"],
            ["🔙 Ortga qaytish"]
        ]
        reply_markup = ReplyKeyboardMarkup(keyboard, resize_keyboard=True)
        await update.message.reply_text(
            f"📖 **{target_test}-test.**\n❓ Boshlamoqchi bo'lgan savol raqamini tanlang:",
            reply_markup=reply_markup,
            parse_mode="Markdown"
        )
        return

    if selected_test is not None:
        test_quiz = QUIZ_DATA.get(selected_test, [])

        if text.isdigit() and 1 <= int(text) <= len(test_quiz) and "current_question" not in context.user_data:
            start_idx = int(text) - 1
            context.user_data["user_answers"] = {}
            await send_question(update, context, start_idx)
            return

        clean_text = text.upper().strip()
        
        if clean_text in ["A", "B", "C", "D"]:
            current_q = context.user_data.get("current_question")
            if current_q is not None:
                if "user_answers" not in context.user_data:
                    context.user_data["user_answers"] = {}
                context.user_data["user_answers"][current_q] = clean_text

                next_q = current_q + 1

                if next_q < len(test_quiz):
                    await send_question(update, context, next_q)
                else:
                    answers = context.user_data.get("user_answers", {})
                    correct_count = 0
                    total_count = len(test_quiz)
                    details = []

                    for idx, item in enumerate(test_quiz):
                        user_ans = answers.get(idx, "-")
                        correct_ans = item["correct"]
                        if user_ans == correct_ans:
                            correct_count += 1
                            details.append(f"{idx + 1}. ✅ (Siz: {user_ans})")
                        else:
                            details.append(f"{idx + 1}. ❌ (Siz: {user_ans} | To'g'ri: {correct_ans})")

                    wrong_count = total_count - correct_count
                    percentage = int((correct_count / total_count) * 100)

                    results_summary = (
                        f"📊 **{selected_test}-TEST NATIJALARI**\n\n"
                        f"👤 Foydalanuvchi: **{USERS[user_id]['name']}**\n"
                        f"📞 Telefon: **+{USERS[user_id]['phone']}**\n\n"
                        f"✅ To'g'ri javoblar: **{correct_count}**\n"
                        f"❌ Noto'g'ri javoblar: **{wrong_count}**\n"
                        f"🎯 Natija: **{percentage}%**\n\n"
                        f"📋 **Batafsil:**\n" + "\n".join(details)
                    )

                    USERS[user_id]["completed_tests"][selected_test] = results_summary

                    await update.message.reply_text(results_summary, reply_markup=ReplyKeyboardRemove(), parse_mode="Markdown")

                    if ADMIN_CHAT_ID:
                        admin_notification = (
                            f"🔔 **Yangi natija:**\n\n{results_summary}"
                        )
                        try:
                            await context.bot.send_message(
                                chat_id=ADMIN_CHAT_ID,
                                text=admin_notification,
                                parse_mode="Markdown"
                            )
                        except Exception as e:
                            logging.error(f"Adminga yuborishda xatolik: {e}")

                    context.user_data.clear()

def main() -> None:
    application = Application.builder().token(TOKEN).build()

    application.add_handler(CommandHandler("start", start))
    application.add_handler(MessageHandler(filters.CONTACT, handle_contact))
    application.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    print("⚙️ Bot ishga tushdi...")
    application.run_polling()

if __name__ == "__main__":
    main()
