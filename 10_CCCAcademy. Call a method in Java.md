# Bài 10: Gọi phương thức (Call a Method) trong Java

> **Mục tiêu**: Hiểu cách gọi phương thức trong Java, phân biệt static methods và instance methods, và cách sử dụng chúng đúng cách.

## I. Giới thiệu về gọi phương thức

### Gọi phương thức là gì?

**Gọi phương thức (Calling a method)** là cách để **thực thi** code trong phương thức đó. Khi gọi phương thức, code trong phương thức sẽ được thực thi từ đầu đến cuối.

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **máy tính**:
- **Phương thức** = Một chức năng của máy tính (cộng, trừ, nhân, chia)
- **Gọi phương thức** = Bấm nút để thực hiện chức năng đó
- **Kết quả** = Màn hình hiển thị kết quả (nếu phương thức trả về giá trị)

**Ví dụ**:
- `calculator.add(10, 20)` = Bấm nút cộng với 10 + 20
- Kết quả: 30 (hiển thị trên màn hình)

## II. Phân loại phương thức theo cách gọi

Trong Java, có **2 loại phương thức** chính dựa trên cách gọi:

1. **Static Methods** (Phương thức tĩnh) - Gọi qua tên lớp
2. **Instance Methods** (Phương thức instance) - Gọi qua đối tượng

## III. Static Methods (Phương thức tĩnh)

### Static Methods là gì?

**Static methods** là phương thức được khai báo với từ khóa `static`, thuộc về **lớp** chứ không thuộc về đối tượng.

### Đặc điểm

- ✅ Thuộc về **lớp**, không thuộc về đối tượng
- ✅ **Không cần** tạo đối tượng để gọi
- ✅ Gọi qua **tên lớp**: `ClassName.methodName()`
- ✅ **Chỉ có thể** truy cập static members (static variables/methods)

### Cách gọi Static Methods

**1. Trong cùng lớp** - Gọi trực tiếp:
```java
public class StaticMethods {
    // Static method
    public static void displayMessage() {
        System.out.println("Hello from static method!");
    }
    
    // Static method có tham số
    public static int sum(int a, int b) {
        return a + b;
    }
    
    public static void main(String[] args) {
        // Gọi trực tiếp (trong cùng lớp)
        displayMessage();  // ✅ OK - Trong cùng lớp
        
        int result = sum(10, 20);  // ✅ OK
        System.out.println("Sum: " + result);  // 30
    }
}
```

**2. Từ lớp khác - Gọi qua tên lớp**:
```java
// Lớp Utility
public class MathUtils {
    public static int add(int a, int b) {
        return a + b;
    }
    
    public static double calculateArea(double radius) {
        return Math.PI * radius * radius;
    }
}

// Lớp khác sử dụng
public class Test {
    public static void main(String[] args) {
        // Gọi qua tên lớp - ✅ Khuyến nghị
        int sum = MathUtils.add(10, 20);
        double area = MathUtils.calculateArea(5.0);
        
        System.out.println("Sum: " + sum);      // 30
        System.out.println("Area: " + area);    // 78.539...
    }
}
```

**3. Sử dụng static import** (Java 5+):
```java
import static java.lang.Math.*;
import static java.lang.System.out;

public class StaticImport {
    public static void main(String[] args) {
        // Không cần Math. nữa
        double max = max(10.5, 20.3);
        double pow = pow(2, 3);
        double pi = PI;
        
        // Không cần System. nữa
        out.println("Max: " + max);
        out.println("Pow: " + pow);
        out.println("Pi: " + pi);
    }
}
```

### Ví dụ: Lớp Math trong Java

```java
public class MathExamples {
    public static void main(String[] args) {
        // Tất cả đều là static methods - Gọi qua tên lớp
        double max = Math.max(10, 20);        // 20.0
        double min = Math.min(10, 20);        // 10.0
        double pow = Math.pow(2, 3);          // 8.0
        double sqrt = Math.sqrt(16);          // 4.0
        double abs = Math.abs(-10);           // 10.0
        double round = Math.round(3.7);       // 4.0
        
        // Static constants
        double pi = Math.PI;                  // 3.14159...
        double e = Math.E;                    // 2.71828...
        
        System.out.println("Max: " + max);
        System.out.println("Min: " + min);
        System.out.println("Pi: " + pi);
    }
}
```

### Hạn chế của Static Methods

**Static methods KHÔNG THỂ**:
1. ❌ Truy cập instance variables trực tiếp
2. ❌ Gọi instance methods trực tiếp
3. ❌ Sử dụng `this` và `super`
4. ❌ Override (sẽ học ở bài Polymorphism)

**Ví dụ lỗi**:
```java
public class StaticLimitations {
    // Instance variable
    private String name = "Test";
    
    // Instance method
    public void instanceMethod() {
        System.out.println("Instance method");
    }
    
    // Static method
    public static void staticMethod() {
        // ❌ LỖI: Không thể truy cập instance variable
        // System.out.println(name);  // Lỗi!
        
        // ❌ LỖI: Không thể gọi instance method
        // instanceMethod();  // Lỗi!
        
        // ✅ OK: Phải tạo đối tượng trước
        StaticLimitations obj = new StaticLimitations();
        System.out.println(obj.name);  // OK
        obj.instanceMethod();          // OK
    }
}
```

## IV. Instance Methods (Phương thức instance)

### Instance Methods là gì?

**Instance methods** là phương thức **không có** từ khóa `static`, thuộc về **đối tượng** chứ không thuộc về lớp.

### Đặc điểm

- ✅ Thuộc về **đối tượng**, không thuộc về lớp
- ✅ **Phải tạo** đối tượng để gọi
- ✅ Gọi qua **đối tượng**: `object.methodName()`
- ✅ **Có thể** truy cập cả instance và static members

### Cách gọi Instance Methods

**1. Tạo đối tượng rồi gọi**:
```java
public class InstanceMethods {
    // Instance variable
    private String name;
    
    // Constructor
    public InstanceMethods(String name) {
        this.name = name;
    }
    
    // Instance method
    public void displayName() {
        System.out.println("Name: " + name);
    }
    
    // Instance method có tham số
    public void setName(String newName) {
        this.name = newName;
    }
    
    // Instance method có trả về
    public String getName() {
        return name;
    }
    
    public static void main(String[] args) {
        // ✅ PHẢI tạo đối tượng trước
        InstanceMethods obj = new InstanceMethods("Nguyễn Văn A");
        
        // Gọi instance methods qua đối tượng
        obj.displayName();         // Name: Nguyễn Văn A
        obj.setName("Trần Thị B");
        obj.displayName();         // Name: Trần Thị B
        
        String name = obj.getName();
        System.out.println("Lấy tên: " + name);  // Lấy tên: Trần Thị B
    }
}
```

**2. Gọi từ phương thức khác trong cùng lớp**:
```java
public class MethodCalling {
    private int value = 10;
    
    // Instance method 1
    public void method1() {
        System.out.println("Method 1: " + value);
        method2();  // ✅ Gọi instance method khác trong cùng lớp
    }
    
    // Instance method 2
    public void method2() {
        System.out.println("Method 2: " + value);
    }
    
    // Static method
    public static void staticMethod() {
        // ❌ KHÔNG THỂ: method1();  // Lỗi!
        
        // ✅ PHẢI: Tạo đối tượng trước
        MethodCalling obj = new MethodCalling();
        obj.method1();  // OK
    }
    
    public static void main(String[] args) {
        MethodCalling obj = new MethodCalling();
        obj.method1();
        System.out.println();
        staticMethod();
    }
}
```

### Ví dụ thực tế

```java
public class Calculator {
    // Instance variable - Lưu giá trị hiện tại
    private double currentValue = 0;
    
    // Constructor
    public Calculator() {
        this.currentValue = 0;
    }
    
    // Instance method - Cộng
    public void add(double value) {
        this.currentValue += value;
        System.out.println("Đã cộng " + value + ". Giá trị hiện tại: " + currentValue);
    }
    
    // Instance method - Trừ
    public void subtract(double value) {
        this.currentValue -= value;
        System.out.println("Đã trừ " + value + ". Giá trị hiện tại: " + currentValue);
    }
    
    // Instance method - Nhân
    public void multiply(double value) {
        this.currentValue *= value;
        System.out.println("Đã nhân " + value + ". Giá trị hiện tại: " + currentValue);
    }
    
    // Instance method - Chia
    public void divide(double value) {
        if (value != 0) {
            this.currentValue /= value;
            System.out.println("Đã chia " + value + ". Giá trị hiện tại: " + currentValue);
        } else {
            System.out.println("Lỗi: Không thể chia cho 0!");
        }
    }
    
    // Instance method - Lấy giá trị hiện tại
    public double getCurrentValue() {
        return currentValue;
    }
    
    // Instance method - Đặt giá trị
    public void setCurrentValue(double value) {
        this.currentValue = value;
    }
    
    // Instance method - Reset
    public void reset() {
        this.currentValue = 0;
        System.out.println("Đã reset. Giá trị hiện tại: " + currentValue);
    }
    
    public static void main(String[] args) {
        // ✅ PHẢI tạo đối tượng trước
        Calculator calc = new Calculator();
        
        // Gọi instance methods qua đối tượng
        calc.add(10);
        calc.multiply(3);
        calc.subtract(5);
        calc.divide(2);
        
        System.out.println("\nGiá trị cuối cùng: " + calc.getCurrentValue());
        
        calc.reset();
        System.out.println("Sau khi reset: " + calc.getCurrentValue());
    }
}
```

**Kết quả**:
```
Đã cộng 10.0. Giá trị hiện tại: 10.0
Đã nhân 3.0. Giá trị hiện tại: 30.0
Đã trừ 5.0. Giá trị hiện tại: 25.0
Đã chia 2.0. Giá trị hiện tại: 12.5

Giá trị cuối cùng: 12.5
Đã reset. Giá trị hiện tại: 0.0
Sau khi reset: 0.0
```

## V. So sánh Static và Instance Methods

### Bảng so sánh

| Đặc điểm | Static Methods | Instance Methods |
|----------|---------------|------------------|
| **Thuộc về** | Class | Object |
| **Cách gọi** | `ClassName.methodName()` | `object.methodName()` |
| **Cần tạo đối tượng?** | ❌ Không | ✅ Có |
| **Truy cập static members** | ✅ Có | ✅ Có |
| **Truy cập instance members** | ❌ Không (trừ qua đối tượng) | ✅ Có |
| **Sử dụng `this`** | ❌ Không | ✅ Có |
| **Sử dụng `super`** | ❌ Không | ✅ Có |
| **Có thể override?** | ❌ Không | ✅ Có |

### Ví dụ so sánh

```java
public class CompareMethods {
    // Instance variable
    private String name = "Instance Name";
    
    // Static variable
    private static String staticName = "Static Name";
    
    // Static method
    public static void staticMethod() {
        // ✅ Có thể truy cập static variable
        System.out.println("Static: " + staticName);
        
        // ❌ KHÔNG THỂ truy cập instance variable
        // System.out.println(name);  // Lỗi!
        
        // ✅ PHẢI tạo đối tượng để truy cập instance variable
        CompareMethods obj = new CompareMethods();
        System.out.println("Instance (qua obj): " + obj.name);
    }
    
    // Instance method
    public void instanceMethod() {
        // ✅ Có thể truy cập cả instance và static
        System.out.println("Instance: " + name);      // OK
        System.out.println("Static: " + staticName);  // OK
        
        // ✅ Có thể gọi static method
        staticMethod();  // OK
        
        // ✅ Có thể gọi instance method khác
        anotherInstanceMethod();  // OK
        
        // ✅ Có thể dùng this
        System.out.println("This.name: " + this.name);  // OK
    }
    
    // Instance method khác
    public void anotherInstanceMethod() {
        System.out.println("Another instance method");
    }
    
    public static void main(String[] args) {
        // Gọi static method - Không cần đối tượng
        CompareMethods.staticMethod();
        System.out.println();
        
        // Gọi instance method - Cần đối tượng
        CompareMethods obj = new CompareMethods();
        obj.instanceMethod();
    }
}
```

## VI. Chuỗi gọi phương thức (Method Chaining)

### Method Chaining là gì?

**Method Chaining** là cách gọi **nhiều phương thức** liên tiếp trên cùng một đối tượng.

### Ví dụ

```java
public class StringBuilder {
    private String value = "";
    
    // Return this để cho phép chaining
    public StringBuilder append(String str) {
        this.value += str;
        return this;  // ✅ Trả về chính đối tượng này
    }
    
    public StringBuilder append(int num) {
        this.value += num;
        return this;  // ✅ Trả về chính đối tượng này
    }
    
    public String toString() {
        return value;
    }
    
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        
        // Method chaining - Gọi nhiều phương thức liên tiếp
        sb.append("Hello")
          .append(" ")
          .append("World")
          .append("!")
          .append(123);
        
        System.out.println(sb.toString());  // Hello World!123
    }
}
```

**Điều kiện để method chaining**:
- Phương thức phải **trả về** đối tượng (thường là `this`)
- Cho phép gọi phương thức tiếp theo trên kết quả trả về

## VII. Ví dụ thực tế

### Ví dụ 1: Hệ thống quản lý tài khoản

```java
public class BankAccount {
    // Instance variables
    private String accountNumber;
    private String ownerName;
    private double balance;
    
    // Static variable
    private static int totalAccounts = 0;
    
    // Constructor
    public BankAccount(String accountNumber, String ownerName, double initialBalance) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = initialBalance;
        totalAccounts++;
    }
    
    // Instance methods
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Đã nạp " + amount + ". Số dư: " + balance);
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Đã rút " + amount + ". Số dư: " + balance);
        } else {
            System.out.println("Số dư không đủ hoặc số tiền không hợp lệ!");
        }
    }
    
    public double getBalance() {
        return balance;
    }
    
    public void displayInfo() {
        System.out.println("=== THÔNG TIN TÀI KHOẢN ===");
        System.out.println("Số TK: " + accountNumber);
        System.out.println("Chủ TK: " + ownerName);
        System.out.println("Số dư: " + balance);
    }
    
    // Static method
    public static int getTotalAccounts() {
        return totalAccounts;
    }
    
    public static void main(String[] args) {
        // Tạo đối tượng
        BankAccount acc1 = new BankAccount("ACC001", "Nguyễn Văn A", 1000000);
        BankAccount acc2 = new BankAccount("ACC002", "Trần Thị B", 2000000);
        
        // Gọi instance methods qua đối tượng
        acc1.deposit(500000);
        acc1.withdraw(200000);
        acc1.displayInfo();
        
        System.out.println();
        
        // Gọi static method qua tên lớp
        System.out.println("Tổng số tài khoản: " + BankAccount.getTotalAccounts());  // 2
    }
}
```

### Ví dụ 2: Utility Class với static methods

```java
public class StringUtils {
    // Private constructor để ngăn tạo đối tượng
    private StringUtils() {
        throw new AssertionError("Cannot instantiate utility class");
    }
    
    // Static methods - Tiện ích
    public static boolean isEmpty(String str) {
        return str == null || str.trim().isEmpty();
    }
    
    public static String capitalize(String str) {
        if (isEmpty(str)) {
            return str;
        }
        return str.substring(0, 1).toUpperCase() + str.substring(1).toLowerCase();
    }
    
    public static String reverse(String str) {
        if (str == null) {
            return null;
        }
        return new StringBuilder(str).reverse().toString();
    }
    
    public static int countWords(String str) {
        if (isEmpty(str)) {
            return 0;
        }
        return str.trim().split("\\s+").length;
    }
    
    public static void main(String[] args) {
        // Gọi static methods qua tên lớp
        System.out.println(StringUtils.isEmpty(""));              // true
        System.out.println(StringUtils.isEmpty("  "));            // true
        System.out.println(StringUtils.capitalize("hello"));      // Hello
        System.out.println(StringUtils.reverse("Java"));          // avaJ
        System.out.println(StringUtils.countWords("Hello World")); // 2
    }
}
```

## VIII. Lưu ý quan trọng

### 1. Không thể gọi instance method từ static method mà không có đối tượng

```java
public class ErrorExample {
    private String name = "Test";
    
    public void instanceMethod() {
        System.out.println("Instance method: " + name);
    }
    
    public static void staticMethod() {
        // ❌ LỖI: instanceMethod();  // Lỗi!
        
        // ✅ OK: Tạo đối tượng trước
        ErrorExample obj = new ErrorExample();
        obj.instanceMethod();  // OK
    }
}
```

### 2. Có thể gọi static method từ instance method

```java
public class CorrectExample {
    private static String staticName = "Static";
    private String instanceName = "Instance";
    
    public static void staticMethod() {
        System.out.println("Static method");
    }
    
    public void instanceMethod() {
        // ✅ OK: Gọi static method từ instance method
        staticMethod();  // OK
        System.out.println("Instance method");
    }
}
```

### 3. Method chaining chỉ hoạt động khi phương thức trả về đối tượng

```java
public class MethodChaining {
    private int value = 0;
    
    // ✅ Cho phép chaining - Trả về this
    public MethodChaining add(int n) {
        value += n;
        return this;
    }
    
    // ❌ Không cho phép chaining - Trả về void
    public void subtract(int n) {
        value -= n;
        // return this;  // Nếu muốn chaining, phải trả về this
    }
    
    public int getValue() {
        return value;
    }
    
    public static void main(String[] args) {
        MethodChaining obj = new MethodChaining();
        
        // ✅ Method chaining
        obj.add(10).add(20).add(30);
        System.out.println("Value: " + obj.getValue());  // 60
        
        // ❌ Không thể chain với subtract
        // obj.subtract(5).add(10);  // Lỗi!
    }
}
```

## IX. Best Practices

### 1. Khi nào dùng Static Methods?

**Dùng static methods khi**:
- ✅ Phương thức không cần dữ liệu từ đối tượng (utility methods)
- ✅ Phương thức chỉ xử lý tham số
- ✅ Không cần trạng thái của đối tượng

**Ví dụ**: `Math.max()`, `Math.min()`, `StringUtils.isEmpty()`

### 2. Khi nào dùng Instance Methods?

**Dùng instance methods khi**:
- ✅ Phương thức cần dữ liệu từ đối tượng
- ✅ Phương thức thay đổi trạng thái đối tượng
- ✅ Mỗi đối tượng cần hành vi riêng

**Ví dụ**: `account.deposit()`, `student.displayInfo()`, `car.start()`

### 3. Naming Convention

- **Static methods**: Thường là utility methods, không có động từ (ví dụ: `Math.max()`)
- **Instance methods**: Thường là động từ (ví dụ: `display()`, `calculate()`, `getValue()`)

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu cách gọi phương thức trong Java
- ✅ Phân biệt được static methods và instance methods
- ✅ Nắm được cách gọi static methods (qua tên lớp)
- ✅ Nắm được cách gọi instance methods (qua đối tượng)
- ✅ Hiểu các hạn chế và quy tắc
- ✅ Biết cách sử dụng method chaining
- ✅ Áp dụng vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo lớp Calculator với static và instance methods**:
   - Static methods: `add()`, `subtract()` (tiện ích)
   - Instance methods: `getHistory()`, `clear()` (cần trạng thái)

2. **Tạo lớp Student với các methods**:
   - Instance methods: `updateGpa()`, `displayInfo()`
   - Static method: `getTotalStudents()`

3. **Thực hành method chaining**:
   - Tạo lớp với các phương thức trả về `this`
   - Gọi nhiều phương thức liên tiếp

## Tài liệu tham khảo

- [Oracle Java Tutorial - Methods](https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html)
- [Java Static vs Instance Methods](https://www.javatpoint.com/static-keyword-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
