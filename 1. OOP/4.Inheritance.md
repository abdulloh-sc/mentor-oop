# Java'da Inheritance (Vorislik)

## Inheritance nima?
Inheritance — bu bir classning boshqa classdan xususiyatlari (fields) va metodlarini meros sifatida olish jarayoni. Bu orqali yangi class o'z superklassidan umumiy xususiyatlarni oladi va o'ziga xos xususiyatlar yoki metodlarni qo'shishi mumkin. Java'da inheritance `extends` kalit so'zi yordamida amalga oshiriladi.

### Asosiy tushunchalar:
- **Superclass (Ota class):** Meros beruvchi class.
- **Subclass (Bola class):** Meros oluvchi class.
- **extends:** Subclass'ni superclass bilan bog'laydigan kalit so'z.
- **Single Inheritance:** Java faqat bitta classdan meros olishni qo'llab-quvvatlaydi (multiple inheritance classlar uchun mavjud emas, lekin interfeyslar orqali amalga oshirilishi mumkin).
- **super:** Superclassning konstruktorini yoki metodlarini chaqirish uchun ishlatiladi.

## Inheritance turlari
Java'da quyidagi inheritance turlari mavjud:
1. **Single Inheritance:** Bir class boshqa bitta classdan meros oladi.
2. **Multilevel Inheritance:** Bir class boshqa classdan meros olsa, u class esa boshqa classdan meros oladi.
3. **Hierarchical Inheritance:** Bir superclassdan bir nechta subclass meros oladi.
4. **Multiple Inheritance:** Java classlar orqali multiple inheritance'ni qo'llab-quvvatlamaydi, lekin interfeyslar orqali bu imkoniyat ta'minlanadi.
5. **Hybrid Inheritance:** Turli inheritance turlarining kombinatsiyasi (interfeyslar orqali amalga oshiriladi).

**Eslatma:** Java'da `final` kalit so'zi bilan belgilangan class meros qilib olinmaydi.

## Inheritancening afzalliklari
- **Kodning qayta ishlatilishi:** Umumiy kodni superclassda yozib, uni bir nechta subclasslarda ishlatish mumkin.
- **Modullilik:** Kodni tashkil qilish va boshqarish osonlashadi.
- **Polimorfizm:** Superclass tipidagi o'zgaruvchilar orqali subclass ob'ektlarini ishlatish imkoniyati.

## Inheritancening cheklovlari
- **Murakkablik:** Katta ierarxiyalarda kodni tushunish qiyinlashishi mumkin.
- **Bog'lanish:** Subclass superklassga qattiq bog'lanadi, bu moslashuvchanlikni kamaytirishi mumkin.

## Misollar

### 1. Single Inheritance
Bitta class boshqa classdan meros oladi.

```java
// Superclass
class Animal {
    String name;

    void eat() {
        System.out.println(name + " is eating.");
    }
}

// Subclass
class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking.");
    }
}

// Test classi
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.name = "Rex";
        dog.eat(); // Superclassdan meros qilingan metod
        dog.bark(); // Subclassning o'ziga xos metodi
    }
}
```

**Natija:**
```
Rex is eating.
Rex is barking.
```

**Tushuntirish:** `Dog` classi `Animal` classidan meros olib, uning `name` xususiyati va `eat` metodini ishlatadi. Shu bilan birga, `Dog` classi o'ziga xos `bark` metodini qo'shadi.

### 2. Multilevel Inheritance
Bir class boshqa classdan meros olsa, u class esa boshqa classdan meros oladi.

```java
// Superclass
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Intermediate class
class Mammal extends Animal {
    void walk() {
        System.out.println("This mammal walks.");
    }
}

// Subclass
class Dog extends Mammal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

// Test classi
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // Animal classidan meros
        dog.walk(); // Mammal classidan meros
        dog.bark(); // Dog classining o'z metodi
    }
}
```

**Natija:**
```
This animal eats food.
This mammal walks.
The dog barks.
```

**Tushuntirish:** `Dog` classi `Mammal` classidan meros oladi, `Mammal` esa `Animal` classidan meros oladi. Natijada, `Dog` ob'ekti barcha uchta classning metodlariga ega bo'ladi.

### 3. Hierarchical Inheritance
Bir superclassdan bir nechta subclass meros oladi.

```java
// Superclass
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass 1
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

// Subclass 2
class Cat extends Animal {
    void meow() {
        System.out.println("The cat meows.");
    }
}

// Test classi
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Cat cat = new Cat();
        
        dog.eat();  // Animal classidan meros
        dog.bark(); // Dog classining o'z metodi
        cat.eat();  // Animal classidan meros
        cat.meow(); // Cat classining o'z metodi
    }
}
```

**Natija:**
```
This animal eats food.
The dog barks.
This animal eats food.
The cat meows.
```

**Tushuntirish:** `Dog` va `Cat` classlari `Animal` classidan meros oladi. Har bir subclass o'ziga xos metodlarga ega, lekin umumiy `eat` metodini `Animal` classidan oladi.

### 4. super kalit so'zi
`super` kalit so'zi superclassning konstruktorini yoki metodlarini chaqirish uchun ishlatiladi.

```java
// Superclass
class Vehicle {
    String brand;

    Vehicle(String brand) {
        this.brand = brand;
        System.out.println("Vehicle brand: " + brand);
    }
}

// Subclass
class Car extends Vehicle {
    String model;

    Car(String brand, String model) {
        super(brand); // Superclass konstruktorini chaqirish
        this.model = model;
        System.out.println("Car model: " + model);
    }
}

// Test classi
public class Main {
    public static void main(String[] args) {
        Car car = new Car("Toyota", "Camry");
    }
}
```

**Natija:**
```
Vehicle brand: Toyota
Car model: Camry
```

**Tushuntirish:** `Car` classi `Vehicle` classidan meros oladi va `super` kalit so'zi orqali superclassning konstruktorini chaqiradi.

## E'tibor berilishi kerak bo'lgan jihatlar
1. **Access Modifiers:** `private` xususiyatlar va metodlar meros qilib olinmaydi. `protected` va `public` modifikatorlari meros qilinadi.
2. **Overriding:** Subclass superklassning metodini qayta aniqlab (override) berishi mumkin.
3. **final class:** `final` bilan belgilangan class meros qilib olinmaydi.
4. **Multiple Inheritance:** Java'da classlar orqali multiple inheritance qo'llab-quvvatlanmaydi, lekin interfeyslar orqali amalga oshirilishi mumkin.

## Xulosa
Inheritance Java'da kodni tashkil qilish va qayta ishlatish uchun muhim vositadir. U classlar o'rtasida ierarxik aloqalarni yaratadi va polimorfizm kabi boshqa OOP konsepsiyalarini qo'llab-quvvatlaydi. Yuqoridagi misollar orqali single, multilevel va hierarchical inheritance turlari tushuntirildi.
