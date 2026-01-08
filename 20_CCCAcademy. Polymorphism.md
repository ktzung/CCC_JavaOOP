# Bài 20: Tính đa hình (Polymorphism) trong Java

> **Mục tiêu**: Hiểu được tính đa hình trong Java, phân biệt method overloading (compile-time) và method overriding (runtime), và áp dụng đa hình vào các ví dụ thực tế.

## I. Giới thiệu về tính đa hình

### Polymorphism là gì?

**Polymorphism** (Tính đa hình) là một trong bốn tính chất cơ bản của OOP, cho phép các đối tượng thuộc các lớp khác nhau có thể phản ứng **khác nhau** với cùng một thông điệp (method call).

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có ba con vật: **chó**, **mèo**, và **chim**:

- **Thông điệp**: "Hãy kêu!"
- **Con chó** → Kêu "Gâu gâu"
- **Con mèo** → Kêu "Meo meo"
- **Con chim** → Kêu "Chíp chíp"

Cùng một thông điệp ("kêu"), nhưng mỗi con vật phản ứng khác nhau → **Đa hình**!

**Trong Java**:
- Cùng một phương thức `makeSound()`
- Mỗi lớp (Dog, Cat, Bird) thực hiện khác nhau
- Gọi `animal.makeSound()` → Mỗi đối tượng tự biết cách kêu của mình

### Định nghĩa

**Tính đa hình** có nghĩa là "nhiều hình dạng". Trong lập trình, nó cho phép:
- Cùng một **tên phương thức** có thể được sử dụng cho các kiểu khác nhau
- Cùng một **giao diện** có thể được triển khai khác nhau
- Cùng một **thông điệp** có thể được xử lý khác nhau tùy vào đối tượng

## II. Các loại Polymorphism trong Java

Java có **2 loại đa hình**:

1. **Static Polymorphism (Compile-time)** - Đa hình tĩnh (thời gian biên dịch)
   - **Method Overloading** (Nạp chồng phương thức)
   
2. **Dynamic Polymorphism (Runtime)** - Đa hình động (thời gian chạy)
   - **Method Overriding** (Ghi đè phương thức)

## III. Static Polymorphism - Method Overloading

### Method Overloading là gì?

**Method Overloading** (Nạp chồng phương thức) là khả năng định nghĩa **nhiều phương thức** trong cùng một lớp với **cùng tên** nhưng **khác tham số** (số lượng, kiểu dữ liệu, hoặc thứ tự).

### Đặc điểm

- ✅ **Cùng tên** phương thức
- ✅ **Khác tham số**: Số lượng, kiểu dữ liệu, hoặc thứ tự
- ✅ **Khác kiểu trả về** (nếu có) - nhưng phải khác tham số
- ✅ **Compile-time**: Trình biên dịch quyết định phương thức nào được gọi

### Ví dụ Method Overloading

```java
public class MethodOverloading {
    // Overloaded methods - Cùng tên, khác tham số
    
    // Method 1: Không tham số
    public void display() {
        System.out.println("Không có tham số");
    }
    
    // Method 2: Một tham số int
    public void display(int number) {
        System.out.println("Số nguyên: " + number);
    }
    
    // Method 3: Một tham số String
    public void display(String message) {
        System.out.println("Chuỗi: " + message);
    }
    
    // Method 4: Hai tham số int
    public void display(int a, int b) {
        System.out.println("Hai số: " + a + ", " + b);
    }
    
    // Method 5: Hai tham số String
    public void display(String name, int age) {
        System.out.println("Tên: " + name + ", Tuổi: " + age);
    }
    
    // Method 6: Tham số khác kiểu (double)
    public void display(double number) {
        System.out.println("Số thực: " + number);
    }
    
    public static void main(String[] args) {
        MethodOverloading obj = new MethodOverloading();
        
        // Compiler chọn phương thức phù hợp dựa trên tham số
        obj.display();                      // Method 1
        obj.display(10);                    // Method 2 (int)
        obj.display("Hello");               // Method 3 (String)
        obj.display(10, 20);                // Method 4 (int, int)
        obj.display("Nguyễn Văn A", 20);   // Method 5 (String, int)
        obj.display(3.14);                  // Method 6 (double)
    }
}
```

**Kết quả**:
```
Không có tham số
Số nguyên: 10
Chuỗi: Hello
Hai số: 10, 20
Tên: Nguyễn Văn A, Tuổi: 20
Số thực: 3.14
```

### Ví dụ thực tế: Lớp Calculator

```java
public class Calculator {
    // Overloaded methods: add()
    
    // Cộng 2 số int
    public int add(int a, int b) {
        return a + b;
    }
    
    // Cộng 2 số double
    public double add(double a, double b) {
        return a + b;
    }
    
    // Cộng 3 số int
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Cộng mảng số
    public int add(int[] numbers) {
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        return sum;
    }
    
    // Cộng nhiều số (varargs - Java 5+)
    public int add(int... numbers) {
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        return sum;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        System.out.println("2 số int: " + calc.add(10, 20));           // 30
        System.out.println("2 số double: " + calc.add(10.5, 20.5));   // 31.0
        System.out.println("3 số int: " + calc.add(10, 20, 30));      // 60
        System.out.println("Mảng: " + calc.add(new int[]{10, 20, 30, 40})); // 100
        System.out.println("Varargs: " + calc.add(1, 2, 3, 4, 5));    // 15
    }
}
```

### Lưu ý về Method Overloading

**1. Không thể overload chỉ khác kiểu trả về**:
```java
public class InvalidOverloading {
    // ❌ LỖI: Không thể overload chỉ khác return type
    // public int method(int a) { return a; }
    // public String method(int a) { return "" + a; }  // Lỗi!
    
    // ✅ OK: Khác tham số
    public int method(int a) { return a; }
    public String method(String a) { return a; }  // OK
}
```

**2. Thứ tự tham số cũng tạo overload**:
```java
public class ParameterOrder {
    // ✅ OK: Khác thứ tự tham số
    public void method(int a, String b) {
        System.out.println("int, String");
    }
    
    public void method(String a, int b) {
        System.out.println("String, int");
    }
    
    public static void main(String[] args) {
        ParameterOrder obj = new ParameterOrder();
        obj.method(10, "Hello");   // int, String
        obj.method("Hello", 10);   // String, int
    }
}
```

## IV. Dynamic Polymorphism - Method Overriding

### Method Overriding là gì?

**Method Overriding** (Ghi đè phương thức) là khả năng định nghĩa lại một phương thức trong lớp con với **cùng tên, cùng tham số, cùng kiểu trả về** như phương thức trong lớp cha.

### Đặc điểm

- ✅ **Cùng tên** phương thức
- ✅ **Cùng tham số** (số lượng, kiểu, thứ tự)
- ✅ **Cùng kiểu trả về** (hoặc subclass)
- ✅ **Runtime**: JVM quyết định phương thức nào được gọi dựa trên **loại đối tượng thực tế**
- ✅ **Annotation `@Override`**: Đánh dấu phương thức được override (khuyến nghị)

### Ví dụ Method Overriding

```java
// Lớp cha
public class Animal {
    // Phương thức sẽ được override
    public void makeSound() {
        System.out.println("Động vật kêu...");
    }
    
    public void eat() {
        System.out.println("Động vật đang ăn...");
    }
}

// Lớp con 1
public class Dog extends Animal {
    @Override  // Annotation đánh dấu override
    public void makeSound() {
        System.out.println("Gâu gâu!");
    }
}

// Lớp con 2
public class Cat extends Animal {
    @Override  // Annotation đánh dấu override
    public void makeSound() {
        System.out.println("Meo meo!");
    }
}

// Lớp con 3
public class Bird extends Animal {
    @Override  // Annotation đánh dấu override
    public void makeSound() {
        System.out.println("Chíp chíp!");
    }
    
    // Phương thức riêng của Bird
    public void fly() {
        System.out.println("Chim đang bay...");
    }
}

// Sử dụng
public class PolymorphismExample {
    public static void main(String[] args) {
        // Tạo các đối tượng
        Animal dog = new Dog();     // Animal reference, Dog object
        Animal cat = new Cat();     // Animal reference, Cat object
        Animal bird = new Bird();   // Animal reference, Bird object
        
        // Runtime polymorphism - JVM quyết định phương thức nào được gọi
        dog.makeSound();   // "Gâu gâu!" - Gọi makeSound() của Dog
        cat.makeSound();   // "Meo meo!" - Gọi makeSound() của Cat
        bird.makeSound();  // "Chíp chíp!" - Gọi makeSound() của Bird
        
        // Phương thức không override - Gọi từ lớp cha
        dog.eat();   // "Động vật đang ăn..."
        cat.eat();   // "Động vật đang ăn..."
        bird.eat();  // "Động vật đang ăn..."
        
        // ❌ KHÔNG THỂ: Gọi phương thức riêng của Bird qua Animal reference
        // bird.fly();  // Lỗi! fly() không có trong Animal
        
        // ✅ PHẢI: Downcast để gọi phương thức riêng
        if (bird instanceof Bird) {
            Bird birdObj = (Bird) bird;
            birdObj.fly();  // OK
        }
    }
}
```

**Kết quả**:
```
Gâu gâu!
Meo meo!
Chíp chíp!
Động vật đang ăn...
Động vật đang ăn...
Động vật đang ăn...
Chim đang bay...
```

### Ví dụ thực tế: Hệ thống thanh toán

```java
// Lớp cơ sở - PaymentMethod
public abstract class PaymentMethod {
    protected double amount;
    
    public PaymentMethod(double amount) {
        this.amount = amount;
    }
    
    // Phương thức abstract - Phải override
    public abstract void processPayment();
    
    // Phương thức cụ thể - Có thể override
    public void displayAmount() {
        System.out.println("Số tiền: " + amount);
    }
}

// Lớp con 1 - CreditCard
public class CreditCard extends PaymentMethod {
    private String cardNumber;
    
    public CreditCard(double amount, String cardNumber) {
        super(amount);
        this.cardNumber = cardNumber;
    }
    
    @Override
    public void processPayment() {
        System.out.println("=== THANH TOÁN BẰNG THẺ TÍN DỤNG ===");
        System.out.println("Số thẻ: " + maskCardNumber(cardNumber));
        System.out.println("Số tiền: " + amount);
        System.out.println("Đang xử lý thanh toán...");
        System.out.println("✅ Thanh toán thành công!");
    }
    
    private String maskCardNumber(String cardNumber) {
        if (cardNumber == null || cardNumber.length() < 4) {
            return "****";
        }
        return "****-****-****-" + cardNumber.substring(cardNumber.length() - 4);
    }
}

// Lớp con 2 - PayPal
public class PayPal extends PaymentMethod {
    private String email;
    
    public PayPal(double amount, String email) {
        super(amount);
        this.email = email;
    }
    
    @Override
    public void processPayment() {
        System.out.println("=== THANH TOÁN BẰNG PAYPAL ===");
        System.out.println("Email: " + email);
        System.out.println("Số tiền: " + amount);
        System.out.println("Đang chuyển hướng đến PayPal...");
        System.out.println("✅ Thanh toán thành công!");
    }
}

// Lớp con 3 - BankTransfer
public class BankTransfer extends PaymentMethod {
    private String accountNumber;
    
    public BankTransfer(double amount, String accountNumber) {
        super(amount);
        this.accountNumber = accountNumber;
    }
    
    @Override
    public void processPayment() {
        System.out.println("=== CHUYỂN KHOẢN NGÂN HÀNG ===");
        System.out.println("Số TK: " + accountNumber);
        System.out.println("Số tiền: " + amount);
        System.out.println("Đang xử lý chuyển khoản...");
        System.out.println("✅ Chuyển khoản thành công!");
    }
}

// Sử dụng
public class PaymentSystem {
    public static void processPayment(PaymentMethod payment) {
        // Runtime polymorphism - Mỗi loại thanh toán tự xử lý khác nhau
        payment.displayAmount();
        payment.processPayment();
        System.out.println();
    }
    
    public static void main(String[] args) {
        // Cùng một phương thức processPayment(), nhưng mỗi lớp xử lý khác nhau
        PaymentMethod payment1 = new CreditCard(1000000, "1234567890123456");
        PaymentMethod payment2 = new PayPal(2000000, "user@example.com");
        PaymentMethod payment3 = new BankTransfer(3000000, "ACC123456");
        
        // Đa hình - Cùng một phương thức, kết quả khác nhau
        processPayment(payment1);
        processPayment(payment2);
        processPayment(payment3);
    }
}
```

**Kết quả**:
```
Số tiền: 1000000.0
=== THANH TOÁN BẰNG THẺ TÍN DỤNG ===
Số thẻ: ****-****-****-3456
Số tiền: 1000000.0
Đang xử lý thanh toán...
✅ Thanh toán thành công!

Số tiền: 2000000.0
=== THANH TOÁN BẰNG PAYPAL ===
Email: user@example.com
Số tiền: 2000000.0
Đang chuyển hướng đến PayPal...
✅ Thanh toán thành công!

Số tiền: 3000000.0
=== CHUYỂN KHOẢN NGÂN HÀNG ===
Số TK: ACC123456
Số tiền: 3000000.0
Đang xử lý chuyển khoản...
✅ Chuyển khoản thành công!
```

## V. So sánh Overloading và Overriding

### Bảng so sánh

| Đặc điểm | Method Overloading | Method Overriding |
|----------|-------------------|-------------------|
| **Tên** | Cùng tên | Cùng tên |
| **Tham số** | ✅ Phải khác (số lượng, kiểu, thứ tự) | ✅ Phải giống (số lượng, kiểu, thứ tự) |
| **Kiểu trả về** | ✅ Có thể khác | ✅ Phải giống (hoặc subclass) |
| **Phạm vi** | ✅ Cùng lớp | ✅ Lớp con override lớp cha |
| **Thời gian quyết định** | ⚡ Compile-time | 🎯 Runtime |
| **Annotation** | ❌ Không cần | ✅ `@Override` (khuyến nghị) |
| **Access modifier** | ✅ Có thể khác | ✅ Phải cùng hoặc mở rộng (protected → public) |

### Ví dụ so sánh

```java
// Lớp cha
public class Parent {
    // Method sẽ được override
    public void method(int a) {
        System.out.println("Parent: " + a);
    }
    
    // Method sẽ được overload
    public void method(String s) {
        System.out.println("Parent: " + s);
    }
}

// Lớp con
public class Child extends Parent {
    // ✅ OVERRIDE: Cùng tên, cùng tham số, cùng return type
    @Override
    public void method(int a) {
        System.out.println("Child: " + a);
    }
    
    // ✅ OVERLOAD: Cùng tên, khác tham số (thêm tham số)
    public void method(int a, int b) {
        System.out.println("Child: " + a + ", " + b);
    }
    
    public static void main(String[] args) {
        Child child = new Child();
        
        // Override - Gọi từ Child
        child.method(10);          // "Child: 10" (override)
        
        // Overload - Gọi từ Child (nếu có) hoặc Parent
        child.method("Hello");     // "Parent: Hello" (kế thừa từ Parent)
        child.method(10, 20);      // "Child: 10, 20" (overload)
        
        // Polymorphism với Parent reference
        Parent parent = new Child();
        parent.method(10);         // "Child: 10" (runtime - override)
        parent.method("Hello");    // "Parent: Hello" (compile-time)
    }
}
```

## VI. @Override Annotation

### @Override là gì?

**`@Override`** là một annotation đánh dấu rằng phương thức này **ghi đè** phương thức của lớp cha.

### Lợi ích của @Override

1. **Kiểm tra lỗi**: Trình biên dịch cảnh báo nếu không có phương thức để override
2. **Dễ đọc**: Code rõ ràng hơn - người đọc biết ngay đây là override
3. **Tránh lỗi**: Phát hiện lỗi typo hoặc thay đổi signature không đúng

### Ví dụ

```java
public class Parent {
    public void display() {
        System.out.println("Parent");
    }
}

public class Child extends Parent {
    // ✅ Có @Override - An toàn
    @Override
    public void display() {
        System.out.println("Child");
    }
    
    // ❌ Không có @Override - Có thể là typo
    // public void displa() {  // Lỗi typo nhưng compiler không cảnh báo nếu không có @Override
    //     System.out.println("Typo");
    // }
    
    // ⚠️ Với @Override - Compiler sẽ cảnh báo lỗi
    // @Override
    // public void displa() {  // Compiler error: method does not override from supertype
    //     System.out.println("Typo");
    // }
}
```

## VII. Upcasting và Downcasting trong Polymorphism

### Upcasting (Ép kiểu lên)

**Upcasting** là gán đối tượng của lớp con cho reference của lớp cha (tự động).

```java
public class UpcastingExample {
    public static void main(String[] args) {
        // Upcasting - Tự động và an toàn
        Animal dog = new Dog();      // ✅ OK - Upcast tự động
        Animal cat = new Cat();      // ✅ OK - Upcast tự động
        
        // Gọi phương thức - Runtime polymorphism
        dog.makeSound();  // "Gâu gâu!" (Dog's method)
        cat.makeSound();  // "Meo meo!" (Cat's method)
        
        // ❌ KHÔNG THỂ: Gọi phương thức riêng của Dog qua Animal reference
        // dog.bark();  // Lỗi! bark() không có trong Animal
    }
}
```

### Downcasting (Ép kiểu xuống)

**Downcasting** là gán đối tượng của lớp cha cho reference của lớp con (cần ép kiểu tường minh).

```java
public class DowncastingExample {
    public static void main(String[] args) {
        // Upcast trước
        Animal animal = new Dog();  // Animal reference, Dog object
        
        // Downcast - Cần kiểm tra với instanceof
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;  // ✅ Downcast
            dog.bark();              // ✅ OK - Gọi phương thức riêng
        }
        
        // ❌ NGUY HIỂM: Downcast không kiểm tra
        // Dog dog2 = (Dog) new Cat();  // ClassCastException!
        
        // ✅ AN TOÀN: Kiểm tra trước
        Animal animal2 = new Cat();
        if (animal2 instanceof Dog) {
            Dog dog3 = (Dog) animal2;  // Không vào đây vì animal2 là Cat
        } else {
            System.out.println("animal2 không phải là Dog!");
        }
    }
}
```

### Ví dụ sử dụng instanceof

```java
public class InstanceofExample {
    public static void processAnimal(Animal animal) {
        animal.makeSound();  // Runtime polymorphism
        
        // Kiểm tra loại thực tế để xử lý đặc biệt
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;
            System.out.println("Đây là chó");
            dog.bark();  // Phương thức riêng của Dog
        } else if (animal instanceof Cat) {
            Cat cat = (Cat) animal;
            System.out.println("Đây là mèo");
            cat.meow();  // Phương thức riêng của Cat
        } else if (animal instanceof Bird) {
            Bird bird = (Bird) animal;
            System.out.println("Đây là chim");
            bird.fly();  // Phương thức riêng của Bird
        }
    }
    
    public static void main(String[] args) {
        processAnimal(new Dog());   // Chó
        processAnimal(new Cat());   // Mèo
        processAnimal(new Bird());  // Chim
    }
}
```

## VIII. Lợi ích của Polymorphism

### 1. Tính linh hoạt (Flexibility)

Cùng một giao diện, nhiều triển khai khác nhau:

```java
public class ShapeDemo {
    public static void drawShape(Shape shape) {
        // Không cần biết loại hình cụ thể
        shape.draw();  // Mỗi hình tự vẽ theo cách của mình
    }
    
    public static void main(String[] args) {
        Shape circle = new Circle();
        Shape rectangle = new Rectangle();
        Shape triangle = new Triangle();
        
        // Cùng một phương thức, kết quả khác nhau
        drawShape(circle);      // Vẽ hình tròn
        drawShape(rectangle);   // Vẽ hình chữ nhật
        drawShape(triangle);    // Vẽ tam giác
    }
}
```

### 2. Dễ mở rộng (Extensibility)

Thêm lớp mới không cần sửa code cũ:

```java
// Code cũ vẫn hoạt động
public void processPayment(PaymentMethod payment) {
    payment.processPayment();  // Không cần sửa khi thêm loại thanh toán mới
}

// Thêm lớp mới - Không cần sửa code trên
public class CryptoPayment extends PaymentMethod {
    @Override
    public void processPayment() {
        // Xử lý thanh toán bằng crypto
    }
}
```

### 3. Giảm coupling (Loosely Coupled)

Code phụ thuộc vào abstraction, không phụ thuộc vào implementation cụ thể:

```java
// ✅ TỐT: Phụ thuộc vào abstraction (Animal)
public void feedAnimal(Animal animal) {
    animal.eat();  // Không cần biết loại động vật cụ thể
}

// ❌ KHÔNG TỐT: Phụ thuộc vào implementation cụ thể
public void feedDog(Dog dog) {
    dog.eat();  // Chỉ có thể cho chó ăn
}
```

## IX. Ví dụ thực tế: Hệ thống quản lý nhân viên

```java
// Lớp cơ sở
public abstract class Employee {
    protected String name;
    protected double baseSalary;
    
    public Employee(String name, double baseSalary) {
        this.name = name;
        this.baseSalary = baseSalary;
    }
    
    // Phương thức abstract - Phải override
    public abstract double calculateSalary();
    
    // Phương thức cụ thể - Có thể override
    public void displayInfo() {
        System.out.println("Tên: " + name);
        System.out.println("Lương cơ bản: " + baseSalary);
        System.out.println("Lương thực tế: " + calculateSalary());
    }
}

// Lớp con 1 - FullTimeEmployee
public class FullTimeEmployee extends Employee {
    private double bonus;
    
    public FullTimeEmployee(String name, double baseSalary, double bonus) {
        super(name, baseSalary);
        this.bonus = bonus;
    }
    
    @Override
    public double calculateSalary() {
        return baseSalary + bonus;  // Lương cơ bản + thưởng
    }
}

// Lớp con 2 - PartTimeEmployee
public class PartTimeEmployee extends Employee {
    private double hoursWorked;
    private double hourlyRate;
    
    public PartTimeEmployee(String name, double baseSalary, double hoursWorked, double hourlyRate) {
        super(name, baseSalary);
        this.hoursWorked = hoursWorked;
        this.hourlyRate = hourlyRate;
    }
    
    @Override
    public double calculateSalary() {
        return hoursWorked * hourlyRate;  // Số giờ × Giá giờ
    }
}

// Lớp con 3 - Contractor
public class Contractor extends Employee {
    private double projectFee;
    
    public Contractor(String name, double baseSalary, double projectFee) {
        super(name, baseSalary);
        this.projectFee = projectFee;
    }
    
    @Override
    public double calculateSalary() {
        return projectFee;  // Phí dự án
    }
}

// Sử dụng
public class EmployeeManagement {
    public static void calculateAndDisplay(Employee employee) {
        // Runtime polymorphism - Mỗi loại nhân viên tự tính lương khác nhau
        employee.displayInfo();
        System.out.println();
    }
    
    public static double calculateTotalPayroll(Employee[] employees) {
        double total = 0;
        for (Employee emp : employees) {
            total += emp.calculateSalary();  // Polymorphism - Mỗi loại tính khác nhau
        }
        return total;
    }
    
    public static void main(String[] args) {
        Employee[] employees = {
            new FullTimeEmployee("Nguyễn Văn A", 10000000, 2000000),
            new PartTimeEmployee("Trần Thị B", 0, 40, 250000),
            new Contractor("Lê Văn C", 0, 5000000)
        };
        
        System.out.println("=== THÔNG TIN NHÂN VIÊN ===\n");
        for (Employee emp : employees) {
            calculateAndDisplay(emp);
        }
        
        System.out.println("=== TỔNG QUỸ LƯƠNG ===");
        double total = calculateTotalPayroll(employees);
        System.out.println("Tổng quỹ lương: " + total);
    }
}
```

**Kết quả**:
```
=== THÔNG TIN NHÂN VIÊN ===

Tên: Nguyễn Văn A
Lương cơ bản: 10000000.0
Lương thực tế: 12000000.0

Tên: Trần Thị B
Lương cơ bản: 0.0
Lương thực tế: 10000000.0

Tên: Lê Văn C
Lương cơ bản: 0.0
Lương thực tế: 5000000.0

=== TỔNG QUỸ LƯƠNG ===
Tổng quỹ lương: 27000000.0
```

## X. Lưu ý quan trọng

### 1. Static methods không thể override

```java
public class Parent {
    public static void staticMethod() {
        System.out.println("Parent static");
    }
}

public class Child extends Parent {
    // Không phải override - Chỉ là hide (ẩn)
    public static void staticMethod() {
        System.out.println("Child static");
    }
    
    public static void main(String[] args) {
        Parent parent = new Child();
        parent.staticMethod();  // "Parent static" - Không phải polymorphism!
        
        Child.staticMethod();   // "Child static"
    }
}
```

### 2. Final methods không thể override

```java
public class Parent {
    public final void finalMethod() {
        System.out.println("Cannot override");
    }
}

public class Child extends Parent {
    // ❌ LỖI: Không thể override final method
    // @Override
    // public void finalMethod() { }  // Compiler error!
}
```

### 3. Private methods không thể override

```java
public class Parent {
    private void privateMethod() {
        System.out.println("Private");
    }
}

public class Child extends Parent {
    // Không phải override - Đây là method mới (vì private không thể truy cập)
    public void privateMethod() {
        System.out.println("This is a new method, not override");
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu tính đa hình là gì và tại sao nó quan trọng
- ✅ Phân biệt được static polymorphism (overloading) và dynamic polymorphism (overriding)
- ✅ Nắm được method overloading (compile-time)
- ✅ Nắm được method overriding (runtime)
- ✅ Hiểu về upcasting và downcasting
- ✅ Sử dụng `@Override` annotation đúng cách
- ✅ Áp dụng đa hình vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo hệ thống hình học với đa hình**:
   - Lớp cha: `Shape` với phương thức `calculateArea()`
   - Lớp con: `Circle`, `Rectangle`, `Triangle`
   - Mỗi lớp override `calculateArea()` theo cách riêng

2. **Tạo hệ thống động vật với đa hình**:
   - Lớp cha: `Animal` với phương thức `makeSound()`, `move()`
   - Lớp con: `Dog`, `Cat`, `Bird`, `Fish`
   - Mỗi lớp override các phương thức theo cách riêng

3. **Tạo hệ thống thanh toán với đa hình**:
   - Lớp cha: `PaymentMethod` với phương thức `processPayment()`
   - Lớp con: `CreditCard`, `PayPal`, `BankTransfer`
   - Sử dụng đa hình để xử lý thanh toán

## Tài liệu tham khảo

- [Oracle Java Tutorial - Polymorphism](https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html)
- [Java Method Overloading](https://www.javatpoint.com/method-overloading-in-java)
- [Java Method Overriding](https://www.javatpoint.com/method-overriding-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
