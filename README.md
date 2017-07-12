# Java Exception

Exceptionlar programın normal akısını bozan hatalardır.

Javada 3 çeşit hata türü vardır:

* **Checked**
* **Unchecked**
* **Error**

### Checked Exceptions

Derleme zamanında kontrol edildiklerinden bu ismi alırlar. Kontrol edilmiş bir hataya sebep olabilecek bir işlem yapıyorsak bunun mutlaka **try-catch** bloğuna alınması ya da ilgili metot da **throws** anahtar kelimesiyle hatanın meydana gelebileceğini belirtmemiz gerekir. **JVM** derleme zamanında bizi bu konuda uyarır. **Try Catch** bloğuna alınmamış ya da **throws** edilmemiş **checked exceptionlar** derleme zamanında hata verir.

### Unchecked Exceptions

Çalışma zamanı hatalarıdır. Derleme zamanında kontrol edilmezler, bu yüzden çalışma zamanında karşımıza çıkar. **Try Catch** bloğu kullanarak hatayı handle etmek kullanıcıya bırakılmıştır zorunlu değildir. **RunTimeException** sınıfı altındaki tüm hata türleri kontrol edilmemiş hatadır.

### Error

Çok büyük bir problemden ötürü java programının durması ya da çalıştırılamamasıdır. Bu hataları handle etme gibi bir seçenek yoktur. Program direk olarak çöker.

### Try Catch Finally

* **Try**: Hataya sebep olabilecek kodlarımızı yazdığımız bölümdür.
* **Catch**: Hatanın yakalandığı kısımdır.
* **Finally**: Hata meydana gelse bile her zaman çalıştırılmasını istediğimiz kodlar buraya yazılır. Finaly bloğu her zaman çalışır(Try bloğu içerisinde process sonlandırılmamışsa ya da process bir hatadan dolayı kendisi sonlanmamışsa).

Kullanılabilecek syntax yapıları:

* **try-catch blokları:**
```java

try {

} catch (Exception_Class_Name referance){

}
```

* **try-finally blokları**: Programda sadece bu blokların kullanılması hatanın handle edilmesine yeterli değildir. Eğer **try** içerisindeki kodlar hata fırlatacak olursa **JVM** hatayı konsola yazdıracak ve **finally** içerisinde ki kodları işletip programı sonlandıracaktır.

```java
try {

} finally {
            
}
```

* **try-catch-finally**:

```java
try {

} catch (Exception_Class_Name referance){

}finally {
            
}
```

* **try-catch-catch…**: Bir çok **catch** bloğunu kullanmamız münkündür. Bu yapının **finally** bloklu halide kullanılabilir.

```java
try {

} catch (Exception_Class_Name_1 referance){

}catch (Exception_Class_Name_2 referance){

}catch (Exception_Class_Name_3 referance){

}
```
* **try-try … catch-catch**: İç içe geçmiş **try-catch** blokları kullanabiliriz. Bunlara **finally** bloklarıda eklenebilir.
```java
 try {

    try {
                
    }catch (Exception_Class_Name referance){
                
    }
            
} catch (Exception_Class_Name referance){

}

```

### Throw/Throws

Bu anahtar kelimeler hatanın yönetimi için önemlidir.

* **Throw**: Hatalar her zaman **JVM** tarafından üretilmek zorunda değildir. Hata olduğunu düşündüğümüz durumda hatayı kendimizde fırlatabiliriz. Bunu yapabilmek için **throw** anahtar kelimesinden yararlanırız. Metot içerisinde, normal kod akışında kullanılır. Aynı anda birden fazla hata fırlatılamaz. Kontrol edilmiş hatalar için direkt olarak throw kullanılamaz. Ya throw ile metodun hata üretebileceği bildirilir ya da **try-catch** bloğuna alınır.

```java
...
if (userInput == null) {
   throw new NullPointerException("User Input Cannot Be Empty");
}
...
```

* **Throws**: Bu anahtar kelime ile bir hatanın meydana gelebileceği bildirilir. Metotlarda kullanılır. Bir çok hatanın meydana gelebileceği bildirilebilir. Çağrı zincirinde hataların üst katmanlara iletilmesi sağlanır.
```java
public void run() throws IOException {
        ...
        if(file == null){
            throw new IOException("File Not Found");
        }
        ...
    }
```
### Override Metotlar ve Hata Yönetimi


* Eğer üst sınıf metodu bir hata meydana gelebileceğini bildirmemişse, kalıtım alan sınıf metodu kontrol edilmiş bir hata bildiremez fakat kontrol edilmemiş bir hata bildirebilir.

```java
class A {
    void run() {

    }
}

class B extends A {
    @Override
    void run() throws NullPointerException {

    }
}
```

* Eğer üst sınıf metodu bir hata bildirirse, kalıtım alan sınıf metodu bildirilen hatadan daha büyük bir hata bildiremez. Örneğin üst sınıf metodu **NullPointerException** bildirmişse kalıtım alan sınıf metodu **Exception** hatasının meydana gelebileceğini bildiremez. Ama tam tersi olabilir ya da kalıtım alan sınıf hiçbir hata bildirmeyebilir.

```java
class A {
    void run() throws Exception {

    }
}

class B extends A {
    @Override
    void run() throws NullPointerException {

    }
}

//yada

class B extends A {
    @Override
    void run(){

    }
}
```
### Kullanıcı Tanımlı Hata Sınıfları

Herhangi bir hata sınıfından kalıtım alınarak gerçekleştirilebilir.

```java
class B {
    void run() throws UserExceptionClass {
        
        throw new UserExceptionClass();
    }
}

class UserExceptionClass extends Exception {

}
```
