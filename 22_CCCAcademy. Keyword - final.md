# Bài 22: Từ khóa `final` trong Java

> **Mục tiêu**: Hiểu được từ khóa `final` trong Java, cách sử dụng `final` với variables, methods, classes, và khi nào nên sử dụng `final`.

## I. Giới thiệu về từ khóa `final`

### `final` là gì?

Từ khóa **`final`** trong Java được sử dụng để **hạn chế** (restrict) người dùng. Nó có thể được áp dụng cho:

1. **Variables** (Biến) - Không thể thay đổi giá trị
2. **Methods** (Phương thức) - Không thể override
3. **Classes** (Lớp) - Không thể kế thừa
4. **Parameters** (Tham số) - Không thể thay đổi trong method

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **hộp khóa**:

- **`final` variable** = Hộp khóa có khóa vĩnh viễn (không thể mở để thay đổi)
- **`final` method** = Cách làm không thể thay đổi (như công thức nấu ăn gia truyền)
- **`final` class** = Hộp khóa không thể sao chép (như bản gốc không thể copy)

## II. Final Variables (Biến final)

### Final Variable là gì?

**Final variable** là biến không thể **thay đổi giá trị** sau khi được khởi tạo (giống như hằng số).

### Đặc điểm

- ✅ **Không thể thay đổi** giá trị sau khi khởi tạo
- ✅ **Phải khởi tạo** trước khi sử dụng (trừ blank final variable)
- ✅ Có thể khởi tạo tại **thời điểm khai báo** hoặc trong **constructor/block**

### Các loại Final Variables

**1. Final Instance Variable**:
```java
public class FinalVariable {
    // ✅ OK: Khởi tạo khi khai báo
    private final int MAX_SIZE = 100;
    
    // ✅ OK: Blank final variable (khởi tạo trong constructor)
    private final int MIN_SIZE;
    
    // Constructor
    public FinalVariable(int minSize) {
        this.MIN_SIZE = minSize;  // ✅ Phải khởi tạo trong constructor
    }
    
    // ❌ LỖI: Không thể thay đổi sau khi khởi tạo
    public void changeValue() {
        // MAX_SIZE = 200;  // Lỗi!
        // MIN_SIZE = 50;   // Lỗi!
    }
}
```

**2. Final Static Variable (Constants)**:
```java
public class Constants {
    // Final static variable - Constant (Hằng số)
    public static final double PI = 3.14159;
    public static final int MAX_STUDENTS = 100;
    public static final String DEFAULT_NAME = "Unknown";
    
    // ✅ OK: Khởi tạo trong static block
    public static final double E;
    
    static {
        E = 2.71828;  // ✅ Khởi tạo trong static block
    }
    
    public static void main(String[] args) {
        System.out.println("PI: " + PI);
        System.out.println("E: " + E);
        
        // ❌ LỖI: Không thể thay đổi
        // PI = 3.14;  // Lỗi!
    }
}
```

**3. Final Local Variable**:
```java
public class FinalLocalVariable {
    public void method() {
        // Final local variable
        final int value = 10;
        
        // ❌ LỖI: Không thể thay đổi
        // value = 20;  // Lỗi!
        
        System.out.println("Value: " + value);
    }
}
```

**4. Final Parameter**:
```java
public class FinalParameter {
    // Final parameter - Không thể thay đổi trong method
    public void method(final int param, final String name) {
        // ❌ LỖI: Không thể thay đổi parameter
        // param = 100;    // Lỗi!
        // name = "New";   // Lỗi!
        
        System.out.println("Param: " + param);
        System.out.println("Name: " + name);
    }
    
    public static void main(String[] args) {
        FinalParameter obj = new FinalParameter();
        obj.method(10, "Hello");
    }
}
```

### Ví dụ: Blank Final Variable

**Blank final variable** là final variable được khai báo nhưng **chưa khởi tạo**, phải khởi tạo trong constructor hoặc block:

```java
public class BlankFinalVariable {
    // Blank final variable - Chưa khởi tạo
    private final int value;
    private final String name;
    
    // Constructor 1
    public BlankFinalVariable(int value) {
        this.value = value;  // ✅ Phải khởi tạo
        this.name = "Default";  // ✅ Phải khởi tạo
    }
    
    // Constructor 2
    public BlankFinalVariable(int value, String name) {
        this.value = value;    // ✅ Phải khởi tạo
        this.name = name;      // ✅ Phải khởi tạo
    }
    
    // ❌ LỖI: Nếu có constructor không khởi tạo final variable
    // public BlankFinalVariable() {
    //     // Lỗi! value và name chưa được khởi tạo
    // }
    
    public void display() {
        System.out.println("Value: " + value);
        System.out.println("Name: " + name);
    }
    
    public static void main(String[] args) {
        BlankFinalVariable obj1 = new BlankFinalVariable(10);
        BlankFinalVariable obj2 = new BlankFinalVariable(20, "Custom");
        
        obj1.display();
        obj2.display();
    }
}
```

### Lưu ý về Final Variables với Objects

Khi một **reference variable** là final, **reference** không thể thay đổi, nhưng **object** mà nó trỏ đến **vẫn có thể thay đổi**:

```java
public class FinalReference {
    public static void main(String[] args) {
        // Final reference
        final StringBuilder sb = new StringBuilder("Hello");
        
        // ❌ LỖI: Không thể gán reference mới
        // sb = new StringBuilder("World");  // Lỗi!
        
        // ✅ OK: Có thể thay đổi object mà reference trỏ đến
        sb.append(" World");  // OK
        sb.append("!");
        System.out.println(sb.toString());  // "Hello World!"
        
        // Final reference với immutable object (String)
        final String str = "Hello";
        // ✅ OK: Gán lại (tạo object mới)
        String newStr = str + " World";  // Tạo String mới
        // str vẫn là "Hello" (immutable)
    }
}
```

## III. Final Methods (Phương thức final)

### Final Method là gì?

**Final method** là phương thức **không thể bị override** bởi lớp con.

### Đặc điểm

- ✅ **Không thể override** bởi lớp con
- ✅ Có thể sử dụng trong **abstract class** và **concrete class**
- ✅ Thường dùng để **bảo vệ** implementation quan trọng

### Ví dụ

```java
// Lớp cha
public class Parent {
    // Final method - Không thể override
    public final void finalMethod() {
        System.out.println("Final method - Không thể override");
    }
    
    // Non-final method - Có thể override
    public void overridableMethod() {
        System.out.println("Có thể override");
    }
}

// Lớp con
public class Child extends Parent {
    // ❌ LỖI: Không thể override final method
    // @Override
    // public void finalMethod() { }  // Compiler error!
    
    // ✅ OK: Có thể override non-final method
    @Override
    public void overridableMethod() {
        System.out.println("Đã override");
    }
    
    public static void main(String[] args) {
        Child child = new Child();
        child.finalMethod();        // "Final method - Không thể override" (từ Parent)
        child.overridableMethod();  // "Đã override" (từ Child)
    }
}
```

### Khi nào dùng Final Methods?

**Dùng final methods khi**:
- ✅ Phương thức quan trọng, không muốn lớp con thay đổi
- ✅ Phương thức liên quan đến bảo mật hoặc tính toàn vẹn dữ liệu
- ✅ Muốn đảm bảo behavior nhất quán

**Ví dụ**:
```java
public class BankAccount {
    private double balance;
    
    // Final method - Không thể override (quan trọng cho tính toàn vẹn)
    public final void validateBalance() {
        if (balance < 0) {
            throw new IllegalArgumentException("Số dư không thể âm!");
        }
    }
    
    public void deposit(double amount) {
        balance += amount;
        validateBalance();  // Luôn gọi phương thức validate này
    }
    
    public void withdraw(double amount) {
        balance -= amount;
        validateBalance();  // Luôn gọi phương thức validate này
    }
}
```

## IV. Final Classes (Lớp final)

### Final Class là gì?

**Final class** là lớp **không thể được kế thừa** (không thể có subclass).

### Đặc điểm

- ✅ **Không thể kế thừa** bởi lớp khác
- ✅ Tất cả methods trong final class **mặc định là final** (không thể override, nhưng không phải khai báo final)
- ✅ Thường dùng cho các lớp **utility** hoặc **immutable**

### Ví dụ

```java
// Final class - Không thể kế thừa
public final class MathUtils {
    // Private constructor - Ngăn tạo đối tượng
    private MathUtils() {
        throw new AssertionError("Cannot instantiate utility class");
    }
    
    // Static methods - Utility methods
    public static int max(int a, int b) {
        return a > b ? a : b;
    }
    
    public static double calculateCircleArea(double radius) {
        return Math.PI * radius * radius;
    }
}

// ❌ LỖI: Không thể kế thừa final class
// public class ExtendedMathUtils extends MathUtils { }  // Compiler error!

// Sử dụng
public class FinalClassExample {
    public static void main(String[] args) {
        // Chỉ có thể sử dụng, không thể kế thừa
        int max = MathUtils.max(10, 20);
        double area = MathUtils.calculateCircleArea(5.0);
        
        System.out.println("Max: " + max);    // 20
        System.out.println("Area: " + area);  // 78.539...
    }
}
```

### Ví dụ: Lớp String trong Java

Lớp `String` trong Java là **final**:

```java
// String là final class trong Java
public final class String implements Serializable, Comparable<String>, CharSequence {
    // ...
}

// ❌ KHÔNG THỂ kế thừa String
// public class MyString extends String { }  // Compiler error!
```

**Lý do**: String là **immutable** và là lớp cơ bản của Java. Cho phép kế thừa có thể gây ra vấn đề về bảo mật và tính toàn vẹn.

## V. Final Parameters (Tham số final)

### Final Parameter là gì?

**Final parameter** là tham số của phương thức được khai báo với từ khóa `final`, **không thể thay đổi** trong phương thức.

### Ví dụ

```java
public class FinalParameter {
    // Final parameter - Không thể thay đổi trong method
    public void process(final int value, final String name) {
        // ❌ LỖI: Không thể thay đổi final parameter
        // value = 100;    // Lỗi!
        // name = "New";   // Lỗi!
        
        System.out.println("Value: " + value);
        System.out.println("Name: " + name);
        
        // ✅ OK: Có thể sử dụng giá trị
        int result = value * 2;
        System.out.println("Result: " + result);
    }
    
    // Final parameter với object
    public void modifyObject(final StringBuilder sb) {
        // ❌ LỖI: Không thể gán reference mới
        // sb = new StringBuilder("New");  // Lỗi!
        
        // ✅ OK: Có thể thay đổi object mà reference trỏ đến
        sb.append(" World");
    }
    
    public static void main(String[] args) {
        FinalParameter obj = new FinalParameter();
        obj.process(10, "Hello");
        
        StringBuilder sb = new StringBuilder("Hello");
        obj.modifyObject(sb);
        System.out.println("After modify: " + sb.toString());  // "Hello World"
    }
}
```

### Lợi ích của Final Parameters

- ✅ **An toàn**: Tránh vô tình thay đổi parameter
- ✅ **Rõ ràng**: Code rõ ràng hơn - parameter không thể thay đổi
- ✅ **Debug dễ hơn**: Biết chắc parameter không bị thay đổi

## VI. Ví dụ thực tế

### Ví dụ 1: Constants Class (Lớp hằng số)

```java
// Final class với final static variables (Constants)
public final class AppConstants {
    // Private constructor - Ngăn tạo đối tượng
    private AppConstants() {
        throw new AssertionError("Cannot instantiate constants class");
    }
    
    // Constants - Final static variables
    public static final String APP_NAME = "My Application";
    public static final String VERSION = "1.0.0";
    public static final int MAX_USERS = 1000;
    public static final double TAX_RATE = 0.1;
    public static final String DEFAULT_LANGUAGE = "vi";
    
    // Database constants
    public static final String DB_URL = "jdbc:mysql://localhost:3306/mydb";
    public static final int DB_TIMEOUT = 30;
}

// Sử dụng
public class UseConstants {
    public static void main(String[] args) {
        System.out.println("App: " + AppConstants.APP_NAME);
        System.out.println("Version: " + AppConstants.VERSION);
        System.out.println("Max Users: " + AppConstants.MAX_USERS);
        
        // ❌ LỖI: Không thể thay đổi constants
        // AppConstants.MAX_USERS = 2000;  // Lỗi!
    }
}
```

### Ví dụ 2: Immutable Class với Final

```java
// Immutable class - Tất cả fields là final
public final class Person {
    // Final fields - Không thể thay đổi
    private final String name;
    private final int age;
    private final String email;
    
    // Constructor - Khởi tạo tất cả final fields
    public Person(String name, int age, String email) {
        this.name = name;
        this.age = age;
        this.email = email;
    }
    
    // Chỉ có getters, không có setters (immutable)
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public String getEmail() {
        return email;
    }
    
    // Method với final parameters
    public boolean equals(final Person other) {
        if (other == null) {
            return false;
        }
        return this.name.equals(other.name) &&
               this.age == other.age &&
               this.email.equals(other.email);
    }
    
    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + ", email='" + email + "'}";
    }
}

// Sử dụng
public class ImmutableExample {
    public static void main(String[] args) {
        Person person = new Person("Nguyễn Văn A", 20, "a@example.com");
        
        System.out.println(person);
        
        // ❌ LỖI: Không có setters - Không thể thay đổi
        // person.setName("New Name");  // Lỗi!
        
        // ✅ Tạo object mới nếu muốn thay đổi
        Person newPerson = new Person("Trần Thị B", 21, "b@example.com");
        System.out.println(newPerson);
    }
}
```

### Ví dụ 3: Utility Class với Final

```java
// Final class - Utility class
public final class StringUtils {
    // Private constructor - Ngăn tạo đối tượng
    private StringUtils() {
        throw new AssertionError("Cannot instantiate utility class");
    }
    
    // Static methods - Utility methods
    public static boolean isEmpty(final String str) {
        return str == null || str.trim().isEmpty();
    }
    
    public static String capitalize(final String str) {
        if (isEmpty(str)) {
            return str;
        }
        return str.substring(0, 1).toUpperCase() + str.substring(1).toLowerCase();
    }
    
    public static String reverse(final String str) {
        if (str == null) {
            return null;
        }
        return new StringBuilder(str).reverse().toString();
    }
    
    // Final method trong static context (không thể override vì static)
    public static final String DEFAULT_VALUE = "Default";
    
    public static void main(String[] args) {
        System.out.println(isEmpty(""));              // true
        System.out.println(capitalize("hello"));      // Hello
        System.out.println(reverse("Java"));          // avaJ
    }
}
```

## VII. Best Practices

### 1. Khi nào dùng `final`?

**Dùng `final` khi**:
- ✅ **Variables**: Giá trị không bao giờ thay đổi (constants, immutable objects)
- ✅ **Methods**: Không muốn lớp con override (bảo vệ implementation)
- ✅ **Classes**: Không muốn lớp con kế thừa (utility classes, immutable classes)
- ✅ **Parameters**: Không muốn vô tình thay đổi parameter trong method

### 2. Naming Convention cho Constants

```java
public class Constants {
    // ✅ TỐT: UPPER_SNAKE_CASE cho constants
    public static final int MAX_SIZE = 100;
    public static final String DEFAULT_NAME = "Unknown";
    public static final double PI = 3.14159;
    
    // ❌ KHÔNG TỐT: camelCase cho constants
    // public static final int maxSize = 100;  // Không khuyến nghị
}
```

### 3. Immutable Objects với Final

```java
// Immutable class - Tất cả fields là final + private + không có setters
public final class Point {
    private final double x;  // Final - Không thể thay đổi
    private final double y;  // Final - Không thể thay đổi
    
    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    // Chỉ có getters
    public double getX() {
        return x;
    }
    
    public double getY() {
        return y;
    }
    
    // Không có setters - Immutable
}
```

## VIII. Lưu ý quan trọng

### 1. Final không có nghĩa là Immutable

```java
public class FinalNotImmutable {
    // Final reference, nhưng object vẫn có thể thay đổi
    private final List<String> list = new ArrayList<>();
    
    public void addItem(String item) {
        // ✅ OK: Thay đổi object (list.add)
        list.add(item);
        
        // ❌ LỖI: Không thể gán reference mới
        // list = new ArrayList<>();  // Lỗi!
    }
    
    // Để immutable, phải return copy
    public List<String> getList() {
        return new ArrayList<>(list);  // Return copy
    }
}
```

### 2. Final Methods trong Abstract Class

```java
public abstract class AbstractClass {
    // ✅ OK: Final method trong abstract class
    public final void finalMethod() {
        System.out.println("Final method");
    }
    
    // Abstract method - Phải override
    public abstract void abstractMethod();
}

public class ConcreteClass extends AbstractClass {
    @Override
    public void abstractMethod() {
        System.out.println("Implemented");
    }
    
    // ❌ LỖI: Không thể override final method
    // @Override
    // public void finalMethod() { }  // Lỗi!
}
```

### 3. Static Methods không thể final (không cần thiết)

```java
public class StaticMethodFinal {
    // ⚠️ KHÔNG CẦN: Static methods không thể override (chỉ hide)
    // public static final void staticMethod() { }  // final không cần thiết
    
    // ✅ OK: Chỉ cần static
    public static void staticMethod() {
        System.out.println("Static method");
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu từ khóa `final` là gì và tại sao nó quan trọng
- ✅ Nắm được final variables (instance, static, local, parameters)
- ✅ Hiểu final methods và khi nào dùng chúng
- ✅ Nắm được final classes và khi nào dùng chúng
- ✅ Hiểu về blank final variables
- ✅ Nắm được best practices khi sử dụng `final`

## Bài tập thực hành

1. **Tạo lớp Constants**:
   - Final class với các final static variables
   - Constants cho ứng dụng của bạn

2. **Tạo Immutable Class**:
   - Tất cả fields là final
   - Chỉ có getters, không có setters
   - Constructor để khởi tạo tất cả fields

3. **Sử dụng final parameters**:
   - Tạo methods với final parameters
   - Tránh vô tình thay đổi parameters

## Tài liệu tham khảo

- [Oracle Java Tutorial - Final](https://docs.oracle.com/javase/tutorial/java/IandI/final.html)
- [Java Final Keyword](https://www.javatpoint.com/final-keyword)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
