# Bài 21: Tính trừu tượng (Abstraction) trong Java

> **Mục tiêu**: Hiểu được tính trừu tượng trong Java, phân biệt Abstract Classes và Interfaces, cách sử dụng chúng, và áp dụng vào các ví dụ thực tế.

## I. Giới thiệu về tính trừu tượng

### Abstraction là gì?

**Abstraction** (Tính trừu tượng) là một trong bốn tính chất cơ bản của OOP, cho phép **ẩn giấu chi tiết triển khai** và chỉ hiển thị những gì cần thiết cho người dùng.

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **chiếc xe ô tô**:

- **Người lái** (User) chỉ cần biết:
  - Bàn đạp ga → Xe tăng tốc (cái gì - WHAT)
  - Vô lăng → Xe rẽ trái/phải (cái gì - WHAT)
  - Phanh → Xe dừng lại (cái gì - WHAT)
  
- **Người lái KHÔNG CẦN biết**:
  - Động cơ hoạt động như thế nào (làm thế nào - HOW)
  - Hộp số chuyển số ra sao (làm thế nào - HOW)
  - Hệ thống phanh hoạt động như thế nào (làm thế nào - HOW)

**Trong Java**:
- **Interface/Abstract Class** = Bảng điều khiển (WHAT - Cái gì)
- **Concrete Class** = Động cơ, hộp số, hệ thống phanh (HOW - Làm thế nào)

### Định nghĩa

**Tính trừu tượng** là quá trình **ẩn giấu chi tiết triển khai** và chỉ hiển thị **giao diện công khai** (public interface) cho người dùng. Người dùng chỉ cần biết "cái gì" (what), không cần biết "làm thế nào" (how).

### Mục đích

- ✅ **Tập trung vào cốt lõi**: Chỉ quan tâm đến những gì cần thiết
- ✅ **Ẩn giấu chi tiết**: Giấu đi những phần phức tạp không cần thiết
- ✅ **Dễ sử dụng**: Người dùng chỉ cần biết cách sử dụng, không cần hiểu chi tiết
- ✅ **Dễ bảo trì**: Thay đổi implementation không ảnh hưởng đến người dùng

## II. Cách thực hiện Abstraction trong Java

Java cung cấp **2 cách** để thực hiện abstraction:

1. **Abstract Classes** (Lớp trừu tượng)
2. **Interfaces** (Giao diện)

## III. Abstract Classes (Lớp trừu tượng)

### Abstract Class là gì?

**Abstract Class** (Lớp trừu tượng) là lớp được khai báo với từ khóa `abstract`, **không thể tạo đối tượng** trực tiếp, nhưng có thể chứa cả phương thức **abstract** (không có implementation) và phương thức **concrete** (có implementation).

### Đặc điểm

- ✅ Được khai báo với từ khóa `abstract`
- ❌ **Không thể tạo đối tượng** trực tiếp (`new AbstractClass()` sẽ lỗi)
- ✅ Có thể chứa **abstract methods** (không có code)
- ✅ Có thể chứa **concrete methods** (có code)
- ✅ Có thể chứa **constructors** (được gọi bởi lớp con)
- ✅ Có thể chứa **fields** (instance và static)
- ✅ Có thể có **access modifiers** (public, private, protected)
- ✅ Lớp con **phải override** tất cả abstract methods (trừ khi lớp con cũng abstract)

### Ví dụ Abstract Class

```java
// Abstract class - Không thể tạo đối tượng
public abstract class Animal {
    // Fields
    protected String name;
    protected int age;
    
    // Constructor
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Concrete method - Có implementation
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ...");
    }
    
    // Abstract method - KHÔNG có implementation
    public abstract void makeSound();
    
    public abstract void move();
    
    // Getters
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
}

// Lớp con 1 - Phải override tất cả abstract methods
public class Dog extends Animal {
    public Dog(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " sủa: Gâu gâu!");
    }
    
    @Override
    public void move() {
        System.out.println(name + " chạy bằng 4 chân");
    }
}

// Lớp con 2
public class Bird extends Animal {
    public Bird(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " hót: Chíp chíp!");
    }
    
    @Override
    public void move() {
        System.out.println(name + " bay bằng cánh");
    }
}

// Sử dụng
public class AbstractExample {
    public static void main(String[] args) {
        // ❌ LỖI: Không thể tạo đối tượng từ abstract class
        // Animal animal = new Animal("Test", 0);  // Compiler error!
        
        // ✅ OK: Tạo đối tượng từ lớp con
        Animal dog = new Dog("Buddy", 3);
        Animal bird = new Bird("Tweety", 1);
        
        // Polymorphism - Mỗi đối tượng tự biết cách thực hiện
        dog.makeSound();   // "Buddy sủa: Gâu gâu!"
        dog.move();        // "Buddy chạy bằng 4 chân"
        dog.eat();         // "Buddy đang ăn..." (kế thừa từ Animal)
        
        System.out.println();
        
        bird.makeSound();  // "Tweety hót: Chíp chíp!"
        bird.move();       // "Tweety bay bằng cánh"
        bird.eat();        // "Tweety đang ăn..." (kế thừa từ Animal)
    }
}
```

### Abstract Methods (Phương thức trừu tượng)

**Abstract methods** là phương thức được khai báo với từ khóa `abstract`, **không có implementation** (không có code trong `{ }`).

**Đặc điểm**:
- ✅ Được khai báo với từ khóa `abstract`
- ✅ **Không có code** (không có body `{ }`)
- ✅ **Phải** được override bởi lớp con (trừ khi lớp con cũng abstract)
- ✅ Chỉ có thể khai báo trong abstract class hoặc interface

**Cú pháp**:
```java
public abstract void methodName();
public abstract ReturnType methodName(Parameters);
```

**Ví dụ**:
```java
public abstract class Shape {
    // Abstract method - Không có implementation
    public abstract double calculateArea();
    
    public abstract double calculatePerimeter();
    
    // Concrete method - Có implementation
    public void displayInfo() {
        System.out.println("Diện tích: " + calculateArea());
        System.out.println("Chu vi: " + calculatePerimeter());
    }
}
```

## IV. Interfaces (Giao diện)

### Interface là gì?

**Interface** (Giao diện) là một kiểu dữ liệu đặc biệt trong Java, định nghĩa một **hợp đồng** (contract) về các phương thức mà lớp implement phải cung cấp. Interface chỉ định nghĩa **"cái gì"** (what), không định nghĩa **"làm thế nào"** (how).

### Đặc điểm

- ✅ Được khai báo với từ khóa `interface`
- ❌ **Không thể tạo đối tượng** trực tiếp
- ✅ Tất cả methods là **public abstract** (mặc định, từ Java 8 có thể có default methods)
- ✅ Tất cả fields là **public static final** (constants)
- ❌ **Không có constructors**
- ✅ Lớp implement **phải override** tất cả methods (trừ default methods)
- ✅ Một lớp có thể **implement nhiều interfaces** (multiple inheritance)

### Cú pháp Interface

```java
[access modifier] interface InterfaceName {
    // Constants (public static final)
    int CONSTANT = 100;
    
    // Abstract methods (public abstract - mặc định)
    void method1();
    ReturnType method2(Parameters);
    
    // Default methods (Java 8+)
    default void defaultMethod() {
        // Code
    }
    
    // Static methods (Java 8+)
    static void staticMethod() {
        // Code
    }
}
```

### Ví dụ Interface

```java
// Interface - Định nghĩa contract
public interface Drawable {
    // Constant (public static final)
    String DEFAULT_COLOR = "Black";
    
    // Abstract method (public abstract - mặc định)
    void draw();
    
    // Abstract method
    String getColor();
    
    // Abstract method
    void setColor(String color);
}

// Lớp implement interface
public class Circle implements Drawable {
    private String color;
    private double radius;
    
    public Circle(double radius, String color) {
        this.radius = radius;
        this.color = color;
    }
    
    // Phải override tất cả abstract methods
    @Override
    public void draw() {
        System.out.println("Vẽ hình tròn màu " + color + " với bán kính " + radius);
    }
    
    @Override
    public String getColor() {
        return color;
    }
    
    @Override
    public void setColor(String color) {
        this.color = color;
    }
}

// Lớp khác implement cùng interface
public class Rectangle implements Drawable {
    private String color;
    private double width;
    private double height;
    
    public Rectangle(double width, double height, String color) {
        this.width = width;
        this.height = height;
        this.color = color;
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ hình chữ nhật màu " + color + " " + width + "x" + height);
    }
    
    @Override
    public String getColor() {
        return color;
    }
    
    @Override
    public void setColor(String color) {
        this.color = color;
    }
}

// Sử dụng
public class InterfaceExample {
    public static void drawShape(Drawable shape) {
        // Polymorphism - Không cần biết loại hình cụ thể
        shape.draw();
    }
    
    public static void main(String[] args) {
        Drawable circle = new Circle(5.0, "Red");
        Drawable rectangle = new Rectangle(10.0, 5.0, "Blue");
        
        // Cùng một phương thức, kết quả khác nhau
        drawShape(circle);      // Vẽ hình tròn
        drawShape(rectangle);   // Vẽ hình chữ nhật
        
        // Sử dụng constant từ interface
        System.out.println("Màu mặc định: " + Drawable.DEFAULT_COLOR);
    }
}
```

## V. Default Methods trong Interfaces (Java 8+)

### Default Methods là gì?

**Default methods** (Java 8+) là các phương thức trong interface có **implementation** (có code), được đánh dấu bằng từ khóa `default`.

### Tại sao cần Default Methods?

**Vấn đề**: Nếu thêm method mới vào interface, tất cả các lớp đã implement phải override method đó → **Rất tốn thời gian** nếu có nhiều lớp.

**Giải pháp**: Default methods cho phép thêm implementation mặc định, các lớp implement **không bắt buộc** phải override.

### Ví dụ Default Methods

```java
// Interface với default method
public interface Vehicle {
    // Abstract method - Phải override
    void start();
    
    void stop();
    
    // Default method - Có implementation mặc định, không bắt buộc override
    default void honk() {
        System.out.println("Bíp bíp!");
    }
    
    // Default method với logic phức tạp
    default void displayInfo() {
        System.out.println("=== THÔNG TIN XE ===");
        start();
        stop();
        honk();
    }
}

// Lớp implement - Có thể override default method hoặc không
public class Car implements Vehicle {
    private String brand;
    
    public Car(String brand) {
        this.brand = brand;
    }
    
    @Override
    public void start() {
        System.out.println(brand + " khởi động...");
    }
    
    @Override
    public void stop() {
        System.out.println(brand + " dừng lại.");
    }
    
    // ✅ Tùy chọn: Override default method
    @Override
    public void honk() {
        System.out.println(brand + " còi: BEEP BEEP!");
    }
}

// Lớp khác - Không override default method
public class Bicycle implements Vehicle {
    @Override
    public void start() {
        System.out.println("Đạp xe...");
    }
    
    @Override
    public void stop() {
        System.out.println("Dừng lại.");
    }
    
    // ❌ Không override honk() → Dùng implementation mặc định
}

// Sử dụng
public class DefaultMethodExample {
    public static void main(String[] args) {
        Vehicle car = new Car("Toyota");
        Vehicle bike = new Bicycle();
        
        car.start();   // "Toyota khởi động..."
        car.honk();    // "Toyota còi: BEEP BEEP!" (override)
        car.stop();    // "Toyota dừng lại."
        
        System.out.println();
        
        bike.start();  // "Đạp xe..."
        bike.honk();   // "Bíp bíp!" (default method)
        bike.stop();   // "Dừng lại."
    }
}
```

## VI. Static Methods trong Interfaces (Java 8+)

### Static Methods trong Interfaces

**Static methods** (Java 8+) là các phương thức static trong interface, có implementation và được gọi qua **tên interface**.

### Ví dụ

```java
public interface MathUtils {
    // Constant
    double PI = 3.14159;
    
    // Abstract method
    double calculate();
    
    // Static method - Java 8+
    static double add(double a, double b) {
        return a + b;
    }
    
    static double multiply(double a, double b) {
        return a * b;
    }
}

// Sử dụng
public class StaticMethodExample {
    public static void main(String[] args) {
        // Gọi static method qua tên interface
        double sum = MathUtils.add(10.5, 20.3);
        double product = MathUtils.multiply(5.0, 3.0);
        
        System.out.println("Sum: " + sum);        // 30.8
        System.out.println("Product: " + product); // 15.0
        System.out.println("PI: " + MathUtils.PI); // 3.14159
    }
}
```

## VII. Private Methods trong Interfaces (Java 9+)

### Private Methods là gì?

**Private methods** (Java 9+) là các phương thức private trong interface, dùng để **chia nhỏ** các default methods hoặc static methods lớn.

### Ví dụ

```java
public interface Calculator {
    // Default method - Sử dụng private method
    default double calculateTotal(double... numbers) {
        if (numbers.length == 0) {
            return 0;
        }
        
        double sum = sumNumbers(numbers);
        return applyTax(sum);  // Gọi private method
    }
    
    // Private method - Java 9+ (chỉ dùng trong interface)
    private double sumNumbers(double[] numbers) {
        double sum = 0;
        for (double num : numbers) {
            sum += num;
        }
        return sum;
    }
    
    private double applyTax(double amount) {
        return amount * 1.1;  // Thêm 10% thuế
    }
    
    // Static method với private method
    static double calculateAverage(double... numbers) {
        if (numbers.length == 0) {
            return 0;
        }
        return sum(numbers) / numbers.length;
    }
    
    private static double sum(double[] numbers) {
        double sum = 0;
        for (double num : numbers) {
            sum += num;
        }
        return sum;
    }
}
```

## VIII. So sánh Abstract Class và Interface

### Bảng so sánh

| Đặc điểm | Abstract Class | Interface |
|----------|---------------|-----------|
| **Khai báo** | `abstract class` | `interface` |
| **Fields** | ✅ Có thể có instance và static | ✅ Chỉ có constants (public static final) |
| **Methods** | ✅ Có thể có abstract và concrete | ✅ Chỉ abstract (trừ default/static) |
| **Constructors** | ✅ Có | ❌ Không có |
| **Multiple Inheritance** | ❌ Không (chỉ 1 class) | ✅ Có (nhiều interfaces) |
| **Access Modifiers** | ✅ Tất cả (public, private, protected) | ✅ Chỉ public (mặc định) |
| **Default Methods** | ✅ Có (concrete methods) | ✅ Có (Java 8+) |
| **Static Methods** | ✅ Có | ✅ Có (Java 8+) |
| **Private Methods** | ✅ Có | ✅ Có (Java 9+) |
| **Khi nào dùng** | Khi cần state chung + behavior mặc định | Khi chỉ cần contract (behavior) |

### Ví dụ so sánh

```java
// Abstract Class - Có state và behavior mặc định
public abstract class Animal {
    // Instance variable (state)
    protected String name;
    protected int age;
    
    // Constructor
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Concrete method (behavior mặc định)
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
    
    // Abstract method (behavior phải implement)
    public abstract void makeSound();
}

// Interface - Chỉ contract (behavior)
public interface Flyable {
    // Constant
    int MAX_ALTITUDE = 10000;
    
    // Abstract method (contract - phải implement)
    void fly();
    
    // Default method (Java 8+)
    default void takeOff() {
        System.out.println("Cất cánh...");
    }
    
    // Static method (Java 8+)
    static void checkAltitude(int altitude) {
        if (altitude > MAX_ALTITUDE) {
            System.out.println("Cảnh báo: Độ cao quá mức!");
        }
    }
}
```

## IX. Multiple Inheritance với Interfaces

### Multiple Inheritance

Java **không hỗ trợ** multiple inheritance cho classes, nhưng **hỗ trợ** cho interfaces.

### Ví dụ

```java
// Interface 1
public interface Flyable {
    void fly();
}

// Interface 2
public interface Swimmable {
    void swim();
}

// Interface 3
public interface Runnable {
    void run();
}

// Interface kế thừa nhiều interfaces
public interface Animal extends Flyable, Swimmable, Runnable {
    void eat();
}

// Lớp implement interface
public class Duck implements Animal {
    @Override
    public void fly() {
        System.out.println("Vịt bay...");
    }
    
    @Override
    public void swim() {
        System.out.println("Vịt bơi...");
    }
    
    @Override
    public void run() {
        System.out.println("Vịt chạy...");
    }
    
    @Override
    public void eat() {
        System.out.println("Vịt ăn...");
    }
}

// Sử dụng
public class MultipleInheritance {
    public static void main(String[] args) {
        Duck duck = new Duck();
        
        // Có thể dùng như nhiều interfaces
        Flyable flyable = duck;
        Swimmable swimmable = duck;
        Runnable runnable = duck;
        Animal animal = duck;
        
        flyable.fly();   // Vịt bay...
        swimmable.swim(); // Vịt bơi...
        runnable.run();   // Vịt chạy...
        animal.eat();     // Vịt ăn...
    }
}
```

## X. Kết hợp Abstract Class và Interface

### Ví dụ: Drawing System

```java
// Interface - Contract
public interface Drawable {
    void draw();
    String getColor();
    void setColor(String color);
}

// Abstract Class - State và behavior mặc định
public abstract class AbstractDrawingTool implements Drawable {
    // State (instance variables)
    protected String color;
    protected int size;
    
    // Constructor
    protected AbstractDrawingTool(String color, int size) {
        this.color = color;
        this.size = size;
    }
    
    // Concrete methods - Behavior mặc định
    @Override
    public String getColor() {
        return color;
    }
    
    @Override
    public void setColor(String color) {
        this.color = color;
    }
    
    // Abstract method - Phải implement
    public abstract void draw();
    
    // Concrete method - Behavior chung
    public void displayInfo() {
        System.out.println("Màu: " + color + ", Kích thước: " + size);
    }
}

// Concrete Class 1
public class Pencil extends AbstractDrawingTool {
    public Pencil(String color, int size) {
        super(color, size);
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ bằng bút chì màu " + color + " kích thước " + size);
    }
}

// Concrete Class 2
public class Brush extends AbstractDrawingTool {
    public Brush(String color, int size) {
        super(color, size);
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ bằng cọ màu " + color + " kích thước " + size);
    }
}

// Sử dụng
public class DrawingSystem {
    public static void drawWithTool(Drawable tool) {
        tool.draw();
    }
    
    public static void main(String[] args) {
        Drawable pencil = new Pencil("Đỏ", 2);
        Drawable brush = new Brush("Xanh", 5);
        
        drawWithTool(pencil);  // Polymorphism
        drawWithTool(brush);   // Polymorphism
        
        // Có thể downcast để sử dụng phương thức của AbstractDrawingTool
        if (pencil instanceof AbstractDrawingTool) {
            AbstractDrawingTool tool = (AbstractDrawingTool) pencil;
            tool.displayInfo();  // Sử dụng phương thức của abstract class
        }
    }
}
```

## XI. Khi nào dùng Abstract Class, khi nào dùng Interface?

### Dùng Abstract Class khi:

- ✅ Cần **state chung** (instance variables)
- ✅ Cần **behavior mặc định** (concrete methods)
- ✅ Cần **constructors**
- ✅ Các lớp con có **quan hệ IS-A** mạnh mẽ

**Ví dụ**: `Animal` → `Dog`, `Cat`, `Bird` (cùng có name, age, eat(), sleep())

### Dùng Interface khi:

- ✅ Chỉ cần **contract** (behavior mà các lớp phải cung cấp)
- ✅ Cần **multiple inheritance**
- ✅ Các lớp không có quan hệ gần (nhưng cần cùng hành vi)
- ✅ Muốn định nghĩa **"cái gì"** (what) thay vì "làm thế nào" (how)

**Ví dụ**: `Flyable`, `Swimmable`, `Runnable` (hành vi có thể áp dụng cho nhiều loại đối tượng khác nhau)

### Có thể kết hợp cả hai

**Ví dụ**: Interface định nghĩa contract, Abstract Class cung cấp implementation mặc định:

```java
// Interface - Contract
public interface PaymentMethod {
    void processPayment(double amount);
}

// Abstract Class - Implementation mặc định
public abstract class AbstractPayment implements PaymentMethod {
    protected String accountNumber;
    protected double balance;
    
    public AbstractPayment(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }
    
    @Override
    public void processPayment(double amount) {
        if (validate(amount)) {
            executePayment(amount);
            logTransaction(amount);
        }
    }
    
    protected boolean validate(double amount) {
        return amount > 0 && amount <= balance;
    }
    
    protected abstract void executePayment(double amount);
    
    protected void logTransaction(double amount) {
        System.out.println("Đã thanh toán: " + amount + " từ TK: " + accountNumber);
    }
}
```

## XII. Ví dụ thực tế

### Ví dụ 1: Hệ thống hình học

```java
// Interface
public interface Shape {
    double calculateArea();
    double calculatePerimeter();
    void displayInfo();
}

// Abstract Class
public abstract class AbstractShape implements Shape {
    protected String name;
    protected String color;
    
    public AbstractShape(String name, String color) {
        this.name = name;
        this.color = color;
    }
    
    // Concrete method - Behavior mặc định
    @Override
    public void displayInfo() {
        System.out.println("=== THÔNG TIN HÌNH ===");
        System.out.println("Tên: " + name);
        System.out.println("Màu: " + color);
        System.out.println("Diện tích: " + calculateArea());
        System.out.println("Chu vi: " + calculatePerimeter());
    }
    
    // Abstract methods - Phải implement
    // calculateArea() và calculatePerimeter() sẽ được override
}

// Concrete Class 1
public class Circle extends AbstractShape {
    private double radius;
    
    public Circle(String name, String color, double radius) {
        super(name, color);
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

// Concrete Class 2
public class Rectangle extends AbstractShape {
    private double width;
    private double height;
    
    public Rectangle(String name, String color, double width, double height) {
        super(name, color);
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * (width + height);
    }
}

// Sử dụng
public class ShapeSystem {
    public static void processShape(Shape shape) {
        shape.displayInfo();  // Polymorphism
        System.out.println();
    }
    
    public static void main(String[] args) {
        Shape circle = new Circle("Hình tròn", "Đỏ", 5.0);
        Shape rectangle = new Rectangle("Hình chữ nhật", "Xanh", 10.0, 5.0);
        
        processShape(circle);    // Display thông tin hình tròn
        processShape(rectangle); // Display thông tin hình chữ nhật
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu tính trừu tượng là gì và tại sao nó quan trọng
- ✅ Phân biệt được Abstract Classes và Interfaces
- ✅ Nắm được Abstract Methods và cách sử dụng
- ✅ Hiểu về Default Methods và Static Methods trong Interfaces (Java 8+)
- ✅ Biết Private Methods trong Interfaces (Java 9+)
- ✅ Nắm được khi nào dùng Abstract Class, khi nào dùng Interface
- ✅ Áp dụng abstraction vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo hệ thống phương tiện với Abstract Class**:
   - Abstract Class: `Vehicle` với methods: `start()`, `stop()`, `accelerate()`
   - Concrete Classes: `Car`, `Motorcycle`, `Bicycle`
   - Mỗi lớp override các phương thức

2. **Tạo hệ thống với Interfaces**:
   - Interfaces: `Flyable`, `Swimmable`, `Runnable`
   - Classes: `Bird` (Flyable, Runnable), `Fish` (Swimmable), `Duck` (tất cả)

3. **Kết hợp Abstract Class và Interface**:
   - Interface: `Drawable` với `draw()`
   - Abstract Class: `AbstractTool` implements `Drawable`
   - Concrete Classes: `Pencil`, `Brush`, `Marker`

## Tài liệu tham khảo

- [Oracle Java Tutorial - Abstract Classes](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)
- [Oracle Java Tutorial - Interfaces](https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html)
- [Java Default Methods](https://www.baeldung.com/java-static-default-methods)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
