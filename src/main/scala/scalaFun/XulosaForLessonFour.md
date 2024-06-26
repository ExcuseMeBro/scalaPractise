Sinf -> o'zgaruvchilar, qiymati o'zgarmas o'zgaruvchilarlar hamda ma'lum bir vazifa bajaruvchi kod 
bloklari ya'ni metodlar to'plamidir.

Konstruktor - bu ma'lum bir sinfning namunasini ya'ni obyektini yaratuvchi metod yoki funksiya. Bu metodga murojaat
qilish uchun xuddi sinfni namunasini yaratganimizdek new kalit so'zi yordamida murojaat qilamiz.
class Apple(color: String, count: Int){
    def printInfo(): Unit = println(s"Yashikda $count ta $color olma bor!")
}
Bu sinfning namunasini yanatishda biz new kalit so'zi bilan asosiy konstruktor Apple metodiga quyidagicha
murojaat qilamiz:
val yashik1 = new Apple("Qizil", 15)
                    |
         bu metod Asosiy (primary) konstruktor

Yuqorida biz Sinf e'lon qilganimizda uni parameterlar bilan e'lon qildik. Biz shu sinfni parametersiz ifodalasak,
uning asosiy konstruktorini ham () (Qavs)siz yoki qavs bilan murojaat qilgan bo'lar edik.
class Orange {
    def printInfo():Unit = println(s"Mandarin juda shirin meva hisoblanadi!")
}
Orange sinfining namunasi ya'ni obyektini e'lon qilamiz
val orange1 = new Orange
val orange2 = new Orange()

Yordamchi konstruktorlar - bu asosiy konstruktorning qismlaridan tashkil topgan ikkinchi darajali konstruktorlardir.
Ular sinf ichida this kalit so'zi yordamida e'lon qilinadi. Masalan:
val defaultColor:String = "Qizil"
val defaultCount:Int = 5
class Apple(color: String, count: Int){
   def this(color: String) = {
     this(color, defaultCount)
   }
   def this(count: Int) = {
     this(defaultColor, count)
   }
   def this() = {
     this(defaultColor, defaultCount)
   }
   override def toString():String = s"Yashikda $count ta $color olma bor!"
}

Ikkinchi darajali konstruktorlarni e'lon qilish uchun quyidagi qoidalarga amal qilish lozim:
1. Biz yaratayotgan har bir konstruktor bir biridan farq qilishi kerak
2. Har bir konstruktor asosiy konstruktorga murojaat qilishi kerak

Yordamchi konstruktorlar bizga parametr bilan berilgan sinfning namunalarini ya'ni obyektlarini turli ko'rinishlarda
ya'ni asosiy konstruktorga bir argument bilan, bir nechta argument bilan hamda ummuman argument bermasdan yaratish
imkonini beradi. Bunda biz bermagan argument sifatida oldindan belgilangan qiymatlarni oladi.

Bir argument bergan holda Apple sinfining namumasi ya'ni obyektini yaratish:
val apple1 = new Apple(45)
bu holatda kod avtomatik sinfning ushbu qismiga tushadi:
   ........
   def this(count: Int) = {
     this(defaultColor, count)
   }
   ........
Bir nechta argument bergan holda Apple sinfining namumasi ya'ni obyektini yaratish:
val apple2 = new Apple("Yashil", 45)
bu holatda kod avtomatik sinfning ushbu qismiga tushadi:
   ........
   def this(color: String) = {
     this(color, defaultCount)
   }
   ........
Argument bermagan holda Apple sinfining namumasi ya'ni obyektini yaratish:
val apple3 = new Apple()
val apple4 = new Apple
bu holatda kod avtomatik sinfning ushbu qismiga tushadi:
   ........
   def this() = {
     this(defaultColor, defaultCount)
   }
   ........

Obyekt -> Sinflarning namunasi hisoblanadi. Ko'z bilan ko'rib, qo'l bilan ushlab bo'ladigan ixtiyoriy
narsa yoki buyumni obyekt deb tushunish mumkin.

Sinf bilan Obyektlarni farqi: Sinflarni biror bir mashinani ishlab chiqish loyihasi deb qarasak,
Obyektlarni esa shu loyiha yordamida yaratilgan avtomobil deb tushunish mumkin.

Singleton obyekt - sinf (class) kalit so'zi o'rniga obyekt (object) kalit ishlatgan holda yaratiluvchi obyektdir.
Bu obyekt bo'lgani uchun uning a'zolarini "." (nuqta) bilan chaqira olamiz. Sinflarda esa a'zolarga murojaat qilish
uchun uning new kalit so'zi obyektini yaratishimiz kerak edi.

Sinflar parameter oladi, Singleton obyektlar bo'lsa parameter qabul qilmaydi.
Sinf namunasi (instance) new kalit so'zi yordamida yaratiladi.
-> Sinf
class Follower(login: String, password: String){
    def thankYou(username: String): Unit = println(s"Xush kelibsiz, $username, Tashrifingizdan minnatdormiz!")
}
-> Sinf namunasi (instance)
val newFollower1 = new Follower("jack0777", "noP@ssword4567")

Sinfdagi maydonlarga murojaat qilish uchun uni oldin namunasi (instance)ni yaratib olishimiz kerak bo'ladi.
val newFollower2 = new Follower("mark0999", "noP@ssword1234")
Keyin sinf namuna (instance)sidagi ya'ni, obyektidagi ixtiyoriy maydonga "." (nuqta) bilan murojaat qilish mumkin 
bo'ladi
newFollower2.thankYou("Mark")
Yuqoridagi sinfda biz login va password degan parameterlarni e'lon qilgan edik, lekin ularni biz sinf namunasi
(isntance) bo'lgan newFollower1 va newFolloer2 da "." (nuqta) yordamida, maydonlarga ya'ni, sinf a'zolariga murojaat
qila olmaymiz. Biz shu parameterlarga murojaat qilishimiz uchun o'sha parameterlarni var yoki val kalit so'zlari
bilan yaratishimiz kerak edi.
-> Sinf
class Follower(login: String, password: String){
    def thankYou(username: String): Unit = println(s"Xush kelibsiz, $username, Tashrifingizdan minnatdormiz!")
}
-> Sinf namunasi (instance)
val newFollower3 = new Follower("jack0777", "noP@ssword4567")

println(newFollower3.login)
println(newFollower3.password)

Sinflarda maydonlarni ya'ni sinf a'zolarini 3 xil ko'rinishda e'lon qilishimiz mumkin. Bular:
1. public -> Scalada bunday zaxiralangan so'z yo'q, ya'ni public metodisiz o'zgaruvchilarni to'g'ridan to'g'ri e'lon
qilamiz. Masalan:
class Follower(login: String, password: String){
    def thankYou(username: String): Unit = println(s"Xush kelibsiz, $username, Tashrifingizdan minnatdormiz!")
}
-> Bu yerda thankYou() metodini public qilib e'lon qildik.
Bu maydonga ya'ni, metodga biz Follow sinfining namunasi (instance) da "." (nuqta) bilan murajaat qila olmaymiz.
Sinfdagi bu maydonga biz uning ixtiyoriy sinf namunasi (instance) da ruxsat (access) olishimiz mumkin.
2. private -> Shaxsiy sinf a'zolari. Biz private kalit so'zi bilan e'lon qilingan sinf a'zolariga faqat Sinf
ichidagi maydonlardan yoki hamroh obyektlardan (Companion Object) ruxsat olishimiz mumkin.

Hamroh obyektlar (Companion Object) - bular sinf bilan bir faylda yaratilgan sinf nomi bilan bir xil nom
bilan yaratilgan obyekt.

class Follower {
    private val secretKey: String = "jhsaoihwaejbHJKHhdajksldhkjqweq313"
    def thankYou(username: String): Unit = println(s"Xush kelibsiz, $username, Tashrifingizdan minnatdormiz!")
    def showSecretKey(username: String): Unit = println(s"Sizning maxsus kodingiz: $secretKey")
}

Hamroh obyekt (Companion object)
class Test {
    private val login:String = "jack2345"
}
object Test {
    def printLogin():Unit = println((new Test).login)
}
Test.printLogin()

3. protected -> Himoyalangan sinf maydonlaridan ya'ni, a'zolaridan Follower sinfining ichki sinf (subclass) larida
a'zolarga murojaat qilish va ushbu a'zolarni qayta e'lon qilish mumkin va shu bilan birga foydalanish Follower
sinfining hamroh obyekti (companion object) dan turib murojaat qilish ham mumkin.

class Follower(){
    private val secretKey: String = "jhsaoihwaejbHJKHhdajksldhkjqweq313"
    protected val login: String = "Hello4567"
    def thankYou(username: String): Unit = println(s"Xush kelibsiz, $username, Tashrifingizdan minnatdormiz!")
    def showSecretKey(username: String): Unit = println(s"Sizning maxsus kodingiz: $secretKey")
}
class NewFollower extends Follower {
    def printLogin():Unit = println(s"Sizning loginingiz: $login")
}
val newUser = new NewFollower
newUser.printLogin()


