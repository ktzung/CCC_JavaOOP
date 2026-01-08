# Hệ thống Bài tập Thực hành - Khóa học Java OOP

## 📚 Mục đích

Tài liệu này cung cấp hệ thống bài tập thực hành độc lập, bổ sung cho các bài tập trong từng bài học. Các bài tập được sắp xếp theo mức độ từ dễ đến khó, giúp học viên củng cố và nâng cao kiến thức.

---

## 🎯 Cấu trúc Hệ thống Bài tập

### Phân loại theo Mức độ

- 🟢 **Cơ bản (Basic)**: Áp dụng trực tiếp kiến thức đã học
- 🟡 **Trung bình (Intermediate)**: Kết hợp nhiều khái niệm
- 🔴 **Nâng cao (Advanced)**: Yêu cầu tư duy và thiết kế

### Phân loại theo Chủ đề

- 📦 **Mini Projects**: Dự án nhỏ hoàn chỉnh
- 🔧 **Practice Exercises**: Bài tập thực hành
- 🧩 **Challenge Problems**: Thử thách nâng cao

---

## 📖 PHẦN 1: NHẬP MÔN JAVA

### Module 1: Java Cơ bản (Sau Bài 01-04)

#### Bài tập 1.0: Bài tập theo từng Bài học

##### Bài tập cho Bài 01: Giới thiệu và Cài đặt môi trường 🟢

**Mục tiêu**: Làm quen với môi trường Java, compile và run.

**Yêu cầu**:
1. Tạo chương trình "Hello World" đầu tiên
2. In ra thông tin về Java version
3. In ra thông tin về hệ điều hành
4. Tạo 3 class khác nhau, mỗi class in một thông điệp khác nhau

**Gợi ý**:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        System.out.println("Java Version: " + System.getProperty("java.version"));
        System.out.println("OS: " + System.getProperty("os.name"));
    }
}
```

---

##### Bài tập cho Bài 02: Cấu trúc của một lớp Java 🟢

**Mục tiêu**: Hiểu cấu trúc class, main method, naming conventions.

**Yêu cầu**:
1. Tạo class `Student` với:
   - Fields: `name`, `age`, `grade`
   - Method `displayInfo()` để hiển thị thông tin
   - Method `main()` để test

2. Tạo class `Car` với:
   - Fields: `brand`, `model`, `year`
   - Method `startEngine()` in ra "Engine started"
   - Method `displayInfo()` hiển thị thông tin xe

**Gợi ý**:
```java
public class Student {
    String name;
    int age;
    String grade;
    
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Grade: " + grade);
    }
    
    public static void main(String[] args) {
        Student student = new Student();
        student.name = "Nguyễn Văn A";
        student.age = 20;
        student.grade = "A";
        student.displayInfo();
    }
}
```

**Mở rộng** (🟡):
- Tạo thêm class `Teacher` với các fields và methods tương tự
- Áp dụng naming conventions đúng

---

##### Bài tập cho Bài 03: Data types 🟢

**Mục tiêu**: Thực hành với primitive types và reference types.

**Yêu cầu**:
1. Tạo chương trình khai báo và khởi tạo các kiểu dữ liệu:
   - Primitive: `int`, `double`, `boolean`, `char`
   - Reference: `String`, `int[]` (array)

2. Hiển thị giá trị và kích thước của từng kiểu
3. Thực hiện các phép toán: cộng, trừ, nhân, chia
4. So sánh giá trị primitive và reference

**Gợi ý**:
```java
public class DataTypesDemo {
    public static void main(String[] args) {
        // Primitive types
        int age = 25;
        double salary = 5000.50;
        boolean isActive = true;
        char grade = 'A';
        
        // Reference types
        String name = "John";
        int[] numbers = {1, 2, 3, 4, 5};
        
        // Display
        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
        System.out.println("Is Active: " + isActive);
        System.out.println("Grade: " + grade);
        System.out.println("Name: " + name);
        System.out.println("Numbers: " + Arrays.toString(numbers));
        
        // Operations
        int sum = age + 10;
        double product = salary * 1.1;
        System.out.println("Sum: " + sum);
        System.out.println("Product: " + product);
    }
}
```

**Mở rộng** (🟡):
- Tạo class `TypeConverter` với methods chuyển đổi giữa các types
- Kiểm tra default values của các types

---

##### Bài tập cho Bài 04: Java Output 🟢

**Mục tiêu**: Thực hành với System.out.print(), println(), printf().

**Yêu cầu**:
1. Sử dụng `print()`, `println()`, `printf()` để hiển thị:
   - Thông tin sinh viên (tên, tuổi, điểm)
   - Bảng điểm với format đẹp
   - Số tiền với format VNĐ

2. Sử dụng Text Blocks (Java 15+) để hiển thị:
   - Menu chương trình
   - Bảng thông tin

**Gợi ý**:
```java
public class OutputDemo {
    public static void main(String[] args) {
        String name = "Nguyễn Văn A";
        int age = 20;
        double gpa = 8.5;
        
        // Using println
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("GPA: " + gpa);
        
        // Using printf
        System.out.printf("Name: %s, Age: %d, GPA: %.2f%n", name, age, gpa);
        
        // Using Text Blocks (Java 15+)
        String menu = """
            ╔════════════════════════════╗
            ║        MENU                ║
            ╠════════════════════════════╣
            ║ 1. Option 1                ║
            ║ 2. Option 2                ║
            ║ 3. Option 3                ║
            ╚════════════════════════════╝
            """;
        System.out.println(menu);
    }
}
```

**Mở rộng** (🟡):
- Tạo bảng điểm với format đẹp
- Format số tiền: 1,000,000 VNĐ

#### Bài tập 1.1: Calculator Cơ bản 🟢

**Mục tiêu**: Làm quen với cú pháp Java, class, method, input/output.

**Yêu cầu**:
Tạo một chương trình máy tính đơn giản với các chức năng:
- Cộng, trừ, nhân, chia 2 số
- Nhập số từ bàn phím
- Hiển thị kết quả

**Gợi ý**:
```java
public class Calculator {
    // Tạo các method: add, subtract, multiply, divide
    // Sử dụng Scanner để nhập
    // Sử dụng System.out để xuất
}
```

**Mở rộng** (🟡):
- Thêm tính năng: lũy thừa, căn bậc 2
- Xử lý chia cho 0
- Làm tròn kết quả đến 2 chữ số thập phân

---

#### Bài tập 1.2: Quản lý Thông tin Cá nhân 🟢

**Mục tiêu**: Thực hành với String, input/output, format.

**Yêu cầu**:
Tạo chương trình quản lý thông tin cá nhân:
- Nhập: Họ tên, tuổi, email, số điện thoại, địa chỉ
- Hiển thị thông tin đã nhập với format đẹp
- Kiểm tra email có chứa "@" không

**Gợi ý**:
```java
public class PersonalInfo {
    public static void main(String[] args) {
        // Nhập thông tin
        // Kiểm tra email
        // Hiển thị với format
    }
}
```

**Mở rộng** (🟡):
- Validate số điện thoại (10 số, bắt đầu bằng 0)
- Validate email (có @ và .)
- Format số điện thoại: 0912-345-678

---

#### Bài tập 1.3: Chương trình Chào hỏi 🟢

**Mục tiêu**: Thực hành với String, method, conditional.

**Yêu cầu**:
Tạo chương trình chào hỏi thông minh:
- Nhập tên và giờ hiện tại (0-23)
- Chào theo giờ:
  - 5-11: "Chào buổi sáng"
  - 12-17: "Chào buổi chiều"
  - 18-22: "Chào buổi tối"
  - 23-4: "Chào buổi đêm"

**Gợi ý**:
```java
public class Greeting {
    public static String getGreeting(int hour) {
        // Logic chào theo giờ
    }
}
```

---

##### Bài tập cho Bài 05: Method 🟡

**Mục tiêu**: Thực hành tạo và sử dụng methods.

**Yêu cầu**:
1. Tạo class `Calculator` với các methods:
   - `add(int a, int b)`: int
   - `subtract(int a, int b)`: int
   - `multiply(int a, int b)`: int
   - `divide(int a, int b)`: double
   - `power(int base, int exponent)`: int
   - `modulo(int a, int b)`: int

2. Tạo class `StringHelper` với các methods:
   - `reverse(String str)`: String
   - `countWords(String str)`: int
   - `toUpperCase(String str)`: String
   - `toLowerCase(String str)`: String
   - `isPalindrome(String str)`: boolean

3. Thực hành method overloading:
   - `add(int a, int b)`: int
   - `add(double a, double b)`: double
   - `add(String a, String b)`: String

**Gợi ý**:
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
    
    public String add(String a, String b) {
        return a + b;
    }
    
    // ... các methods khác
}
```

**Mở rộng** (🟡):
- Tạo method với varargs: `sum(int... numbers)`
- Tạo method recursive: `factorial(int n)`

---

##### Bài tập cho Bài 06: OOP in Java 🟡

**Mục tiêu**: Áp dụng OOP cơ bản, Class vs Object.

**Yêu cầu**:
1. Tạo class `Car` với:
   - Fields: `brand`, `model`, `year`, `color`, `price`
   - Methods: `start()`, `stop()`, `accelerate()`, `brake()`, `displayInfo()`

2. Tạo class `BankAccount` với:
   - Fields: `accountNumber`, `ownerName`, `balance`
   - Methods: `deposit(double amount)`, `withdraw(double amount)`, `displayBalance()`

3. Tạo nhiều objects và so sánh:
   - Tạo 3 đối tượng Car khác nhau
   - Tạo 2 đối tượng BankAccount khác nhau
   - Hiển thị thông tin tất cả objects

**Gợi ý**:
```java
public class Car {
    String brand;
    String model;
    int year;
    String color;
    double price;
    
    public void start() {
        System.out.println(brand + " " + model + " is starting...");
    }
    
    public void displayInfo() {
        System.out.println("Brand: " + brand);
        System.out.println("Model: " + model);
        System.out.println("Year: " + year);
        System.out.println("Color: " + color);
        System.out.println("Price: " + price);
    }
}
```

**Mở rộng** (🟡):
- Tạo class `Garage` chứa ArrayList<Car>
- Tạo class `Bank` chứa ArrayList<BankAccount>

---

### Module 2: Methods và OOP Cơ bản (Sau Bài 05-06)

#### Bài tập 2.1: Thư viện Methods 🟡

**Mục tiêu**: Thực hành tạo và sử dụng methods.

**Yêu cầu**:
Tạo class `MathUtils` với các static methods:
- `isEven(int n)`: Kiểm tra số chẵn
- `isPrime(int n)`: Kiểm tra số nguyên tố
- `factorial(int n)`: Tính giai thừa
- `fibonacci(int n)`: Tính số Fibonacci thứ n
- `gcd(int a, int b)`: Tìm ước chung lớn nhất
- `lcm(int a, int b)`: Tìm bội chung nhỏ nhất

**Gợi ý**:
```java
public class MathUtils {
    public static boolean isEven(int n) {
        return n % 2 == 0;
    }
    
    public static boolean isPrime(int n) {
        // Logic kiểm tra số nguyên tố
    }
    
    // ... các methods khác
}
```

**Mở rộng** (🔴):
- Tạo class `StringUtils` với methods: reverse, palindrome, countWords
- Tạo class `ArrayUtils` với methods: findMax, findMin, average

---

#### Bài tập 2.2: Hệ thống Quản lý Sách Mini 🟡

**Mục tiêu**: Áp dụng OOP cơ bản, class, object.

**Yêu cầu**:
Tạo class `Book` với:
- Fields: `title`, `author`, `price`, `quantity`
- Methods: `displayInfo()`, `calculateTotalValue()`
- Tạo 3-5 đối tượng Book và hiển thị thông tin

**Gợi ý**:
```java
public class Book {
    String title;
    String author;
    double price;
    int quantity;
    
    public void displayInfo() {
        // Hiển thị thông tin
    }
    
    public double calculateTotalValue() {
        return price * quantity;
    }
}
```

**Mở rộng** (🟡):
- Thêm method `applyDiscount(double percent)`
- Thêm method `isAvailable()` (quantity > 0)
- Tính tổng giá trị tất cả sách

---

### Module 3: Wrapper Classes, Static, Scope, Methods (Sau Bài 07-10)

##### Bài tập cho Bài 07: Wrapper Classes 🟡

**Mục tiêu**: Thực hành với Wrapper Classes, boxing/unboxing.

**Yêu cầu**:
1. Tạo chương trình chuyển đổi giữa primitive và Wrapper:
   - `int` ↔ `Integer`
   - `double` ↔ `Double`
   - `boolean` ↔ `Boolean`
   - `char` ↔ `Character`

2. Sử dụng các methods của Wrapper Classes:
   - `Integer.parseInt()`, `Integer.valueOf()`
   - `Double.parseDouble()`, `Double.valueOf()`
   - `Character.isDigit()`, `Character.isLetter()`
   - `Boolean.parseBoolean()`

3. Thực hành auto-boxing và unboxing

**Gợi ý**:
```java
public class WrapperDemo {
    public static void main(String[] args) {
        // Manual boxing
        Integer num1 = Integer.valueOf(10);
        Integer num2 = new Integer(20);
        
        // Auto-boxing
        Integer num3 = 30;
        
        // Manual unboxing
        int value1 = num1.intValue();
        
        // Auto-unboxing
        int value2 = num3;
        
        // Useful methods
        String str = "123";
        int num = Integer.parseInt(str);
        
        char ch = '5';
        boolean isDigit = Character.isDigit(ch);
        boolean isLetter = Character.isLetter(ch);
    }
}
```

**Mở rộng** (🟡):
- Tạo class `NumberConverter` với methods chuyển đổi String → Number
- Sử dụng Wrapper Classes trong ArrayList

---

##### Bài tập cho Bài 08: Keyword static 🟡

**Mục tiêu**: Thực hành với static variables, methods, blocks.

**Yêu cầu**:
1. Tạo class `Counter` với:
   - Static variable `count` (đếm số đối tượng được tạo)
   - Instance variable `id`
   - Static method `getCount()`: int
   - Constructor tăng count mỗi khi tạo object

2. Tạo class `MathUtils` với static methods:
   - `max(int a, int b)`: int
   - `min(int a, int b)`: int
   - `abs(int n)`: int
   - `pow(int base, int exp)`: int

3. Tạo class `Constants` với static final variables:
   - `PI = 3.14159`
   - `MAX_SIZE = 100`
   - `APP_NAME = "MyApp"`

**Gợi ý**:
```java
public class Counter {
    private static int count = 0;
    private int id;
    
    public Counter() {
        count++;
        this.id = count;
    }
    
    public static int getCount() {
        return count;
    }
    
    public int getId() {
        return id;
    }
}

public class MathUtils {
    public static int max(int a, int b) {
        return a > b ? a : b;
    }
    
    public static int min(int a, int b) {
        return a < b ? a : b;
    }
}
```

**Mở rộng** (🟡):
- Tạo static block để khởi tạo static variables
- Sử dụng static import

---

##### Bài tập cho Bài 09: Scope of variables 🟢

**Mục tiêu**: Hiểu về phạm vi biến, variable shadowing.

**Yêu cầu**:
1. Tạo class `ScopeDemo` với:
   - Class-level variable: `name`
   - Method-level variable: `name` (shadowing)
   - Block-level variable: `count`
   - Hiển thị giá trị của từng biến

2. Tạo class `VariableShadowing` để minh họa:
   - Class variable và method parameter cùng tên
   - Sử dụng `this` để truy cập class variable

**Gợi ý**:
```java
public class ScopeDemo {
    private String name = "Class Level";  // Class-level
    
    public void method1() {
        String name = "Method Level";  // Method-level (shadowing)
        System.out.println("Method variable: " + name);
        System.out.println("Class variable: " + this.name);
        
        {
            int count = 10;  // Block-level
            System.out.println("Block variable: " + count);
        }
        // System.out.println(count);  // Error: count không tồn tại ở đây
    }
}
```

**Mở rộng** (🟡):
- Tạo ví dụ về lifetime của biến
- So sánh instance variable vs local variable

---

##### Bài tập cho Bài 10: Call a method in Java 🟢

**Mục tiêu**: Thực hành gọi static và instance methods.

**Yêu cầu**:
1. Tạo class `Calculator` với:
   - Static methods: `add()`, `subtract()`, `multiply()`, `divide()`
   - Instance methods: `setValue()`, `getValue()`, `calculate()`

2. Thực hành gọi methods:
   - Gọi static method: `Calculator.add(5, 3)`
   - Gọi instance method: `calc.setValue(10)`
   - Method chaining

3. Tạo class `StringBuilder` demo với method chaining

**Gợi ý**:
```java
public class Calculator {
    private double value;
    
    // Static methods
    public static double add(double a, double b) {
        return a + b;
    }
    
    // Instance methods
    public Calculator setValue(double value) {
        this.value = value;
        return this;  // Method chaining
    }
    
    public Calculator add(double num) {
        this.value += num;
        return this;
    }
    
    public double getValue() {
        return value;
    }
}

// Usage
Calculator calc = new Calculator();
double result = calc.setValue(10).add(5).add(3).getValue();  // Method chaining
```

**Mở rộng** (🟡):
- Tạo utility class với static methods
- Thực hành method chaining với nhiều methods

---

### Module 3: String và Regex (Sau Bài 11-13)

##### Bài tập cho Bài 11: Java Input 🟡

**Mục tiêu**: Thực hành với Scanner, input validation.

**Yêu cầu**:
1. Tạo chương trình nhập thông tin sinh viên:
   - Nhập tên, tuổi, điểm
   - Sử dụng `nextLine()`, `nextInt()`, `nextDouble()`
   - Xử lý lỗi khi nhập sai kiểu

2. Tạo class `InputValidator` với methods:
   - `readInt(String prompt)`: int (với validation)
   - `readDouble(String prompt)`: double (với validation)
   - `readString(String prompt)`: String
   - `readBoolean(String prompt)`: boolean

3. Thực hành `hasNext...()` methods để kiểm tra trước khi đọc

**Gợi ý**:
```java
import java.util.Scanner;

public class InputDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập tên: ");
        String name = scanner.nextLine();
        
        System.out.print("Nhập tuổi: ");
        int age = scanner.nextInt();
        scanner.nextLine();  // Consume newline
        
        System.out.print("Nhập điểm: ");
        double score = scanner.nextDouble();
        
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Điểm: " + score);
        
        scanner.close();
    }
}
```

**Mở rộng** (🟡):
- Sử dụng `try-with-resources`
- Tạo menu với input validation
- Xử lý lỗi khi nhập sai format

---

##### Bài tập cho Bài 12: String 🟡

**Mục tiêu**: Thực hành với String methods.

#### Bài tập 3.1: Xử lý Văn bản 🟡

**Mục tiêu**: Thực hành với String methods.

**Yêu cầu**:
Tạo chương trình xử lý văn bản:
- Đếm số từ trong câu
- Đếm số câu (kết thúc bằng . ! ?)
- Tìm từ dài nhất
- Đảo ngược câu
- Chuyển đổi chữ hoa/thường

**Gợi ý**:
```java
public class TextProcessor {
    public static int countWords(String text) {
        // Sử dụng split(" ")
    }
    
    public static String reverse(String text) {
        // Sử dụng StringBuilder
    }
}
```

---

**Mở rộng** (🟡):
- So sánh hiệu năng `+` vs `StringBuilder`
- Thực hành với String Pool
- So sánh `==` vs `equals()`

---

##### Bài tập cho Bài 13: Regex 🟡

**Mục tiêu**: Thực hành với Regular Expressions.

#### Bài tập 3.2: Validator System 🟡

**Mục tiêu**: Thực hành với Regex.

**Yêu cầu**:
Tạo class `Validator` với các methods validate:
- `validateEmail(String email)`: Email hợp lệ
- `validatePhone(String phone)`: SĐT Việt Nam (10 số, bắt đầu 0)
- `validatePassword(String password)`: 
  - Ít nhất 8 ký tự
  - Có chữ hoa, chữ thường, số
  - Có ký tự đặc biệt
- `validateDate(String date)`: DD/MM/YYYY

**Gợi ý**:
```java
public class Validator {
    public static boolean validateEmail(String email) {
        String pattern = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$";
        return email.matches(pattern);
    }
    
    // ... các methods khác
}
```

**Mở rộng** (🔴):
- Validate số CMND/CCCD (12 số)
- Validate mã số thuế
- Validate URL

---

## 🎓 PHẦN 2: LẬP TRÌNH HƯỚNG ĐỐI TƯỢNG

**Mở rộng** (🟡):
- Sử dụng `Pattern` và `Matcher` classes
- Tìm và thay thế với regex
- Validate số CMND/CCCD

---

### Module 4: Encapsulation (Sau Bài 14-15)

##### Bài tập cho Bài 14: Encapsulation 🟡

#### Bài tập 4.1: Hệ thống Quản lý Sản phẩm 🟡

**Mục tiêu**: Áp dụng Encapsulation.

**Yêu cầu**:
Tạo class `Product` với:
- Private fields: `id`, `name`, `price`, `quantity`, `category`
- Public getters/setters với validation:
  - `price > 0`
  - `quantity >= 0`
  - `name` không rỗng
- Method `displayInfo()`
- Method `calculateTotalValue()`

**Gợi ý**:
```java
public class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;
    private String category;
    
    // Getters
    public String getId() { return id; }
    
    // Setters với validation
    public void setPrice(double price) {
        if (price > 0) {
            this.price = price;
        } else {
            System.out.println("⚠️ Giá phải > 0");
        }
    }
    
    // Methods
    public void displayInfo() { }
    public double calculateTotalValue() { }
}
```

**Mở rộng** (🟡):
- Thêm method `applyDiscount(double percent)`
- Thêm method `updateQuantity(int amount)` (có thể âm)
- Thêm method `isLowStock()` (quantity < 10)

---

#### Bài tập 4.2: Hệ thống Quản lý Tài khoản Ngân hàng 🟡

**Mục tiêu**: Áp dụng Encapsulation với validation phức tạp.

**Yêu cầu**:
Tạo class `BankAccount` với:
- Private fields: `accountNumber`, `ownerName`, `balance`, `accountType`
- Validation:
  - `accountNumber`: 10-12 số
  - `balance >= 0`
  - `accountType`: "Savings" hoặc "Checking"
- Methods:
  - `deposit(double amount)`: Gửi tiền
  - `withdraw(double amount)`: Rút tiền (kiểm tra số dư)
  - `displayInfo()`

**Gợi ý**:
```java
public class BankAccount {
    private String accountNumber;
    private String ownerName;
    private double balance;
    private String accountType;
    
    public boolean deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            return true;
        }
        return false;
    }
    
    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }
}
```

**Mở rộng** (🔴):
- Thêm transaction history (ArrayList)
- Thêm method `transfer(BankAccount other, double amount)`
- Thêm interest calculation cho Savings account

---

**Mở rộng** (🟡):
- So sánh private vs public fields
- Tạo immutable class với final fields
- Validation phức tạp hơn

---

##### Bài tập cho Bài 15: Project Phase 1 🟡

**Mục tiêu**: Áp dụng Encapsulation vào project thực tế.

**Yêu cầu**: Làm theo hướng dẫn trong Bài 15: Project Phase 1

---

### Module 5: Constructor và Inheritance (Sau Bài 16-17)

##### Bài tập cho Bài 16: Constructor 🟡

**Mục tiêu**: Thực hành với Constructor, constructor overloading, `this`.

**Yêu cầu**:
1. Tạo class `Student` với:
   - Default constructor
   - Parameterized constructor với tất cả fields
   - Constructor với một số fields
   - Constructor chaining với `this()`

2. Tạo class `BankAccount` với:
   - Constructor mặc định (balance = 0)
   - Constructor với accountNumber và ownerName
   - Constructor với tất cả fields
   - Sử dụng `this` để disambiguate

**Gợi ý**:
```java
public class Student {
    private String id;
    private String name;
    private int age;
    
    // Default constructor
    public Student() {
        this.id = "Unknown";
        this.name = "Unknown";
        this.age = 0;
    }
    
    // Constructor chaining
    public Student(String id, String name) {
        this(id, name, 0);  // Gọi constructor khác
    }
    
    // Full constructor
    public Student(String id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }
}
```

**Mở rộng** (🟡):
- Tạo constructor copy
- Constructor với validation

---

##### Bài tập cho Bài 17: Inheritance 🟡

**Mục tiêu**: Thực hành với Inheritance, `extends`, `super`.

**Yêu cầu**:
1. Tạo class `Animal` (lớp cha):
   - Fields: `name`, `age`, `species`
   - Methods: `eat()`, `sleep()`, `displayInfo()`

2. Tạo class `Dog` extends `Animal`:
   - Thêm field: `breed`
   - Override `displayInfo()`
   - Thêm method: `bark()`

3. Tạo class `Cat` extends `Animal`:
   - Thêm field: `isIndoor`
   - Override `displayInfo()`
   - Thêm method: `meow()`

4. Sử dụng `super` để gọi constructor và methods của lớp cha

**Gợi ý**:
```java
public class Animal {
    protected String name;
    protected int age;
    protected String species;
    
    public Animal(String name, int age, String species) {
        this.name = name;
        this.age = age;
        this.species = species;
    }
    
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Species: " + species);
    }
}

public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age, "Dog");  // Gọi constructor của lớp cha
        this.breed = breed;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();  // Gọi method của lớp cha
        System.out.println("Breed: " + breed);
    }
    
    public void bark() {
        System.out.println(name + " is barking!");
    }
}
```

**Mở rộng** (🟡):
- Tạo multi-level inheritance: Animal → Dog → Puppy
- Sử dụng protected access modifier

#### Bài tập 5.1: Hệ thống Quản lý Phương tiện 🟡

**Mục tiêu**: Áp dụng Constructor và Inheritance.

**Yêu cầu**:
1. Tạo class `Vehicle` (lớp cha):
   - Fields: `brand`, `model`, `year`, `price`
   - Constructors: default, parameterized
   - Method `displayInfo()`

2. Tạo class `Car` extends `Vehicle`:
   - Thêm field: `numberOfSeats`
   - Constructor với `super()`
   - Override `displayInfo()`

3. Tạo class `Motorcycle` extends `Vehicle`:
   - Thêm field: `engineCapacity`
   - Constructor với `super()`
   - Override `displayInfo()`

**Gợi ý**:
```java
public class Vehicle {
    protected String brand;
    protected String model;
    protected int year;
    protected double price;
    
    public Vehicle() { }
    
    public Vehicle(String brand, String model, int year, double price) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.price = price;
    }
    
    public void displayInfo() {
        System.out.println("Brand: " + brand);
        // ...
    }
}

public class Car extends Vehicle {
    private int numberOfSeats;
    
    public Car(String brand, String model, int year, double price, int numberOfSeats) {
        super(brand, model, year, price);
        this.numberOfSeats = numberOfSeats;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Seats: " + numberOfSeats);
    }
}
```

**Mở rộng** (🔴):
- Thêm class `Truck` extends `Vehicle` với field `loadCapacity`
- Tạo method `calculateDepreciation(int currentYear)` trong Vehicle
- Tạo method `isVintage(int currentYear)` (nếu > 25 năm)

---

#### Bài tập 5.2: Hệ thống Quản lý Nhân sự 🟡

**Mục tiêu**: Áp dụng Inheritance với nhiều lớp.

**Yêu cầu**:
1. Tạo class `Person`:
   - Fields: `id`, `name`, `age`, `email`, `phone`
   - Constructors và methods

2. Tạo class `Employee` extends `Person`:
   - Thêm: `employeeId`, `department`, `salary`
   - Method `calculateAnnualSalary()`

3. Tạo class `Manager` extends `Employee`:
   - Thêm: `teamSize`, `bonus`
   - Override `calculateAnnualSalary()` (salary + bonus)

**Gợi ý**:
```java
public class Person {
    protected String id;
    protected String name;
    protected int age;
    // ...
}

public class Employee extends Person {
    private String employeeId;
    private String department;
    private double salary;
    
    public double calculateAnnualSalary() {
        return salary * 12;
    }
}

public class Manager extends Employee {
    private int teamSize;
    private double bonus;
    
    @Override
    public double calculateAnnualSalary() {
        return super.calculateAnnualSalary() + bonus;
    }
}
```

**Mở rộng** (🔴):
- Thêm class `Intern` extends `Employee` với `stipend`
- Tạo method `promote()` để chuyển Employee → Manager
- Tính tổng lương tất cả nhân viên

---

##### Bài tập cho Bài 18-19: Project Phase 2-3 🟡

**Mục tiêu**: Áp dụng Inheritance và Polymorphism vào project.

**Yêu cầu**: Làm theo hướng dẫn trong Bài 18-19: Project Phase 2-3

---

### Module 6: Polymorphism và Abstraction (Sau Bài 20-21)

##### Bài tập cho Bài 20: Polymorphism 🟡

**Mục tiêu**: Thực hành với Method Overloading và Overriding.

**Yêu cầu**:
1. Tạo class `Calculator` với method overloading:
   - `add(int a, int b)`: int
   - `add(double a, double b)`: double
   - `add(int a, int b, int c)`: int
   - `add(String a, String b)`: String

2. Tạo class hierarchy với method overriding:
   - `Animal` với method `makeSound()`
   - `Dog` extends `Animal`, override `makeSound()` → "Woof!"
   - `Cat` extends `Animal`, override `makeSound()` → "Meow!"

3. Thực hành upcasting và downcasting:
   - Tạo ArrayList<Animal> chứa Dog và Cat
   - Gọi `makeSound()` trên mỗi object (polymorphism)

**Gợi ý**:
```java
public class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

// Polymorphism
Animal animal1 = new Dog();
Animal animal2 = new Cat();
animal1.makeSound();  // "Woof!" - Runtime polymorphism
animal2.makeSound();  // "Meow!" - Runtime polymorphism
```

**Mở rộng** (🟡):
- Sử dụng `instanceof` để kiểm tra type
- Downcasting an toàn

---

##### Bài tập cho Bài 21: Abstraction 🟡

**Mục tiêu**: Thực hành với Abstract Classes và Interfaces.

**Yêu cầu**:
1. Tạo abstract class `Shape`:
   - Abstract method `calculateArea()`
   - Abstract method `calculatePerimeter()`
   - Concrete method `displayInfo()`

2. Tạo các class extends `Shape`:
   - `Circle`, `Rectangle`, `Triangle`

3. Tạo interface `Drawable`:
   - Method `draw()`
   - Default method `getColor()` (Java 8+)

4. Tạo class implements `Drawable`:
   - `Circle` implements `Drawable`

**Gợi ý**:
```java
public abstract class Shape {
    public abstract double calculateArea();
    public abstract double calculatePerimeter();
    
    public void displayInfo() {
        System.out.println("Area: " + calculateArea());
        System.out.println("Perimeter: " + calculatePerimeter());
    }
}

public interface Drawable {
    void draw();
    
    default String getColor() {
        return "Black";
    }
}

public class Circle extends Shape implements Drawable {
    private double radius;
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

**Mở rộng** (🟡):
- Sử dụng static methods trong interface (Java 8+)
- Sử dụng private methods trong interface (Java 9+)

---

##### Bài tập cho Bài 22: Keyword final 🟡

**Mục tiêu**: Thực hành với `final` keyword.

**Yêu cầu**:
1. Tạo class `Constants` với final variables:
   - `PI = 3.14159`
   - `MAX_SIZE = 100`
   - `APP_NAME = "MyApp"`

2. Tạo class `Parent` với:
   - Final method `displayInfo()`
   - Non-final method `calculate()`

3. Tạo class `Child` extends `Parent`:
   - Không thể override `displayInfo()` (final)
   - Có thể override `calculate()`

4. Tạo final class `Utility`:
   - Không thể extend

**Gợi ý**:
```java
public class Constants {
    public static final double PI = 3.14159;
    public static final int MAX_SIZE = 100;
    public static final String APP_NAME = "MyApp";
}

public class Parent {
    public final void displayInfo() {
        System.out.println("Parent info");
    }
    
    public void calculate() {
        System.out.println("Parent calculate");
    }
}

public class Child extends Parent {
    // Cannot override displayInfo() - it's final
    
    @Override
    public void calculate() {
        System.out.println("Child calculate");
    }
}

public final class Utility {
    // Cannot be extended
}
```

**Mở rộng** (🟡):
- Tạo immutable class với final fields
- Blank final variables

---

##### Bài tập cho Bài 23: Project Phase 4 🟡

**Mục tiêu**: Áp dụng Abstraction vào project.

**Yêu cầu**: Làm theo hướng dẫn trong Bài 23: Project Phase 4

---

### Module 7: Collections và Lambda (Sau Bài 24-27)

##### Bài tập cho Bài 24: ArrayList 🟡

**Mục tiêu**: Thực hành với ArrayList, Collections Framework.

**Yêu cầu**:
1. Tạo class `StudentManager` với ArrayList<Student>:
   - `addStudent(Student s)`
   - `removeStudent(String id)`
   - `findStudent(String id)`: Student
   - `displayAll()`
   - `getSize()`: int

2. Thực hành các cách iterate:
   - For loop
   - For-each loop
   - Iterator
   - Lambda (Java 8+)

3. Sử dụng Wrapper Classes trong ArrayList:
   - ArrayList<Integer>
   - ArrayList<Double>
   - Auto-boxing/unboxing

**Gợi ý**:
```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class StudentManager {
    private List<Student> students = new ArrayList<>();
    
    public void addStudent(Student student) {
        students.add(student);
    }
    
    public void displayAll() {
        // For-each loop
        for (Student student : students) {
            student.displayInfo();
        }
        
        // Lambda (Java 8+)
        students.forEach(Student::displayInfo);
    }
}
```

**Mở rộng** (🟡):
- So sánh ArrayList vs Array
- Xử lý `ConcurrentModificationException`
- Sử dụng `Collections` utility class

---

##### Bài tập cho Bài 25: Sort Object 🟡

**Mục tiêu**: Thực hành với Comparable và Comparator.

**Yêu cầu**:
1. Tạo class `Student` implements `Comparable<Student>`:
   - Sort by GPA (descending)

2. Tạo class `Product` với Comparator:
   - Sort by price
   - Sort by name
   - Sort by category then price

3. Sử dụng `Collections.sort()` và `list.sort()`

**Gợi ý**:
```java
public class Student implements Comparable<Student> {
    private String id;
    private String name;
    private double gpa;
    
    @Override
    public int compareTo(Student other) {
        return Double.compare(other.gpa, this.gpa);  // Descending
    }
}

// Using Comparator
students.sort(Comparator.comparing(Student::getName));
students.sort(Comparator.comparing(Student::getGpa).reversed());
students.sort(Comparator.comparing(Student::getGpa)
                        .thenComparing(Student::getName));
```

**Mở rộng** (🟡):
- Multi-criteria sorting
- Custom Comparator với anonymous class

---

##### Bài tập cho Bài 26-27: Lambda Expressions 🟡

**Mục tiêu**: Thực hành với Lambda Expressions và Functional Interfaces.

**Yêu cầu**:
1. Sử dụng Lambda với Collections:
   - `forEach()`
   - `removeIf()`
   - `replaceAll()`

2. Sử dụng Lambda với Comparator:
   - `Comparator.comparing()`
   - `Comparator.comparingInt()`
   - `.reversed()`
   - `.thenComparing()`

3. Sử dụng Functional Interfaces:
   - `Function<T, R>`
   - `Predicate<T>`
   - `Consumer<T>`
   - `Supplier<T>`

**Gợi ý**:
```java
import java.util.function.*;

// Lambda với Collections
students.forEach(s -> System.out.println(s.getName()));
students.removeIf(s -> s.getGpa() < 5.0);

// Lambda với Comparator
students.sort(Comparator.comparing(Student::getName));
students.sort(Comparator.comparingDouble(Student::getGpa).reversed());

// Functional Interfaces
Function<String, Integer> length = s -> s.length();
Predicate<Student> isExcellent = s -> s.getGpa() >= 8.0;
Consumer<Student> print = s -> System.out.println(s);
Supplier<Student> createStudent = () -> new Student();
```

**Mở rộng** (🟡):
- Method References
- Stream API cơ bản

---

##### Bài tập cho Bài 28: Project Phase 5 🟡

**Mục tiêu**: Áp dụng Collections và Lambda vào project.

**Yêu cầu**: Làm theo hướng dẫn trong Bài 28: Project Phase 5

---

### Module 8: Java IO (Sau Bài 29)

##### Bài tập cho Bài 29: Java IO 🟡

**Mục tiêu**: Thực hành với File I/O.

**Yêu cầu**:
1. Tạo class `FileManager` với:
   - `writeToFile(String content, String filePath)`: boolean
   - `readFromFile(String filePath)`: String
   - `appendToFile(String content, String filePath)`: boolean
   - `deleteFile(String filePath)`: boolean

2. Sử dụng `try-with-resources`:
   - `FileWriter`, `FileReader`
   - `BufferedWriter`, `BufferedReader`
   - `FileInputStream`, `FileOutputStream`

3. Xử lý exceptions:
   - `FileNotFoundException`
   - `IOException`

**Gợi ý**:
```java
import java.io.*;

public class FileManager {
    public boolean writeToFile(String content, String filePath) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            writer.write(content);
            return true;
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
            return false;
        }
    }
    
    public String readFromFile(String filePath) {
        StringBuilder content = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                content.append(line).append("\n");
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        return content.toString();
    }
}
```

**Mở rộng** (🟡):
- Lưu/đọc object (cần serialization)
- Tạo backup file
- Validate file format

---

##### Bài tập cho Bài 30: Project Phase 6 🟡

**Mục tiêu**: Áp dụng Java IO vào project.

**Yêu cầu**: Làm theo hướng dẫn trong Bài 30: Project Phase 6

---

#### Bài tập 6.1: Hệ thống Hình học 🟡

**Mục tiêu**: Áp dụng Polymorphism và Abstraction.

**Yêu cầu**:
1. Tạo abstract class `Shape`:
   - Abstract method `calculateArea()`
   - Abstract method `calculatePerimeter()`
   - Concrete method `displayInfo()`

2. Tạo class `Circle` extends `Shape`:
   - Field: `radius`
   - Implement abstract methods

3. Tạo class `Rectangle` extends `Shape`:
   - Fields: `width`, `height`
   - Implement abstract methods

4. Tạo class `Triangle` extends `Shape`:
   - Fields: `a`, `b`, `c`
   - Implement abstract methods

**Gợi ý**:
```java
public abstract class Shape {
    public abstract double calculateArea();
    public abstract double calculatePerimeter();
    
    public void displayInfo() {
        System.out.println("Area: " + calculateArea());
        System.out.println("Perimeter: " + calculatePerimeter());
    }
}

public class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
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
```

**Mở rộng** (🔴):
- Tạo ArrayList<Shape> chứa nhiều hình
- Tính tổng diện tích tất cả hình
- Sắp xếp theo diện tích

---

#### Bài tập 6.2: Hệ thống Thanh toán 🟡

**Mục tiêu**: Áp dụng Interface và Polymorphism.

**Yêu cầu**:
1. Tạo interface `PaymentMethod`:
   - Method `pay(double amount)`: boolean
   - Method `getPaymentInfo()`: String

2. Tạo class `CreditCard` implements `PaymentMethod`:
   - Fields: `cardNumber`, `cardHolder`, `expiryDate`
   - Implement methods

3. Tạo class `PayPal` implements `PaymentMethod`:
   - Fields: `email`, `password`
   - Implement methods

4. Tạo class `Cash` implements `PaymentMethod`:
   - Implement methods

5. Tạo class `PaymentProcessor`:
   - Method `processPayment(PaymentMethod method, double amount)`

**Gợi ý**:
```java
public interface PaymentMethod {
    boolean pay(double amount);
    String getPaymentInfo();
}

public class CreditCard implements PaymentMethod {
    private String cardNumber;
    private String cardHolder;
    private String expiryDate;
    
    @Override
    public boolean pay(double amount) {
        // Logic thanh toán
        return true;
    }
    
    @Override
    public String getPaymentInfo() {
        return "Credit Card: " + cardNumber;
    }
}

public class PaymentProcessor {
    public void processPayment(PaymentMethod method, double amount) {
        if (method.pay(amount)) {
            System.out.println("Payment successful: " + method.getPaymentInfo());
        }
    }
}
```

**Mở rộng** (🔴):
- Thêm class `BankTransfer` implements `PaymentMethod`
- Thêm transaction history
- Tính phí giao dịch cho mỗi phương thức

---

### Module 7: Collections và Lambda (Sau Bài 24-27)

#### Bài tập 7.1: Hệ thống Quản lý Danh sách Sinh viên 🟡

**Mục tiêu**: Áp dụng ArrayList và Sorting.

**Yêu cầu**:
1. Tạo class `Student`:
   - Fields: `id`, `name`, `age`, `gpa`
   - Implement `Comparable<Student>` (sort by GPA)

2. Tạo class `StudentManager`:
   - ArrayList<Student>
   - Methods:
     - `addStudent(Student s)`
     - `removeStudent(String id)`
     - `findStudent(String id)`: Student
     - `sortByGPA()`: Sử dụng Comparable
     - `sortByName()`: Sử dụng Comparator
     - `displayAll()`
     - `getTopStudents(int n)`: Top n sinh viên

**Gợi ý**:
```java
public class Student implements Comparable<Student> {
    private String id;
    private String name;
    private int age;
    private double gpa;
    
    @Override
    public int compareTo(Student other) {
        return Double.compare(other.gpa, this.gpa); // Descending
    }
}

public class StudentManager {
    private List<Student> students = new ArrayList<>();
    
    public void sortByGPA() {
        Collections.sort(students);
    }
    
    public void sortByName() {
        students.sort(Comparator.comparing(Student::getName));
    }
}
```

**Mở rộng** (🔴):
- Sắp xếp theo nhiều tiêu chí (GPA → Name)
- Tìm kiếm theo tên (contains)
- Tính điểm trung bình của tất cả sinh viên
- Lọc sinh viên có GPA >= 8.0

---

#### Bài tập 7.2: Hệ thống Quản lý Sản phẩm với Lambda 🟡

**Mục tiêu**: Áp dụng Lambda Expressions.

**Yêu cầu**:
1. Tạo class `Product` (như Bài tập 4.1)

2. Tạo class `ProductManager`:
   - ArrayList<Product>
   - Methods với Lambda:
     - `filterByCategory(String category)`: List<Product>
     - `filterByPriceRange(double min, double max)`: List<Product>
     - `sortByPrice()`: Sử dụng Lambda
     - `sortByPriceDesc()`: Sử dụng Lambda
     - `sortByCategoryThenPrice()`: Sử dụng Lambda
     - `getTotalValue()`: double
     - `getAveragePrice()`: double

**Gợi ý**:
```java
public class ProductManager {
    private List<Product> products = new ArrayList<>();
    
    public List<Product> filterByCategory(String category) {
        return products.stream()
                      .filter(p -> p.getCategory().equals(category))
                      .collect(Collectors.toList());
    }
    
    public void sortByPrice() {
        products.sort(Comparator.comparing(Product::getPrice));
    }
    
    public void sortByCategoryThenPrice() {
        products.sort(Comparator.comparing(Product::getCategory)
                               .thenComparing(Product::getPrice));
    }
}
```

**Mở rộng** (🔴):
- Tìm sản phẩm đắt nhất/rẻ nhất
- Đếm số sản phẩm theo category
- Tính tổng giá trị theo category

---

### Module 8: Java IO (Sau Bài 29)

#### Bài tập 8.1: Hệ thống Lưu trữ Dữ liệu 🟡

**Mục tiêu**: Áp dụng Java IO.

**Yêu cầu**:
1. Tạo class `DataManager`:
   - Method `saveToFile(List<String> data, String filePath)`: boolean
   - Method `loadFromFile(String filePath)`: List<String>
   - Method `appendToFile(String data, String filePath)`: boolean

2. Tạo chương trình:
   - Lưu danh sách tên vào file
   - Đọc danh sách từ file
   - Thêm tên mới vào file

**Gợi ý**:
```java
public class DataManager {
    public boolean saveToFile(List<String> data, String filePath) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            for (String line : data) {
                writer.write(line);
                writer.newLine();
            }
            return true;
        } catch (IOException e) {
            return false;
        }
    }
    
    public List<String> loadFromFile(String filePath) {
        List<String> data = new ArrayList<>();
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                data.add(line);
            }
        } catch (IOException e) {
            // Handle error
        }
        return data;
    }
}
```

**Mở rộng** (🔴):
- Lưu/đọc object (Student, Product) - cần serialization
- Tạo backup file
- Validate file format

---

## 🏆 MINI PROJECTS - Dự án Tổng hợp

### Mini Project 1: Hệ thống Quản lý Thư viện 📚

**Mức độ**: 🟡 Trung bình

**Mục tiêu**: Áp dụng tất cả kiến thức OOP cơ bản.

**Yêu cầu**:

1. **Class `Book`**:
   - Fields: `isbn`, `title`, `author`, `year`, `available` (boolean)
   - Encapsulation với getters/setters
   - Constructor
   - Methods: `displayInfo()`, `borrow()`, `return()`

2. **Class `Member`**:
   - Fields: `memberId`, `name`, `email`, `phone`
   - Encapsulation
   - Constructor
   - Methods: `displayInfo()`

3. **Class `Library`**:
   - ArrayList<Book> books
   - ArrayList<Member> members
   - Methods:
     - `addBook(Book book)`
     - `removeBook(String isbn)`
     - `findBook(String isbn)`: Book
     - `registerMember(Member member)`
     - `borrowBook(String isbn, String memberId)`: boolean
     - `returnBook(String isbn)`: boolean
     - `displayAllBooks()`
     - `displayAvailableBooks()`
     - `displayBorrowedBooks()`

4. **Class `LibraryApp`** (Main):
   - Menu với các chức năng
   - Tương tác với người dùng

**Gợi ý cấu trúc**:
```
LibrarySystem/
└── src/
    ├── entity/
    │   ├── Book.java
    │   └── Member.java
    ├── service/
    │   └── Library.java
    └── main/
        └── LibraryApp.java
```

**Mở rộng** (🔴):
- Lưu/đọc dữ liệu từ file
- Tính phí mượn trả
- Thống kê: Sách mượn nhiều nhất, Thành viên mượn nhiều nhất

---

### Mini Project 2: Hệ thống Quản lý Nhà hàng 🍽️

**Mức độ**: 🟡 Trung bình

**Mục tiêu**: Áp dụng Inheritance, Polymorphism, Collections.

**Yêu cầu**:

1. **Abstract class `MenuItem`**:
   - Fields: `id`, `name`, `price`
   - Abstract method `calculatePrice()`
   - Method `displayInfo()`

2. **Class `Food` extends `MenuItem`**:
   - Field: `category` (Appetizer, Main, Dessert)
   - Implement `calculatePrice()`

3. **Class `Drink` extends `MenuItem`**:
   - Field: `size` (Small, Medium, Large)
   - Implement `calculatePrice()` (size ảnh hưởng giá)

4. **Class `Order`**:
   - ArrayList<MenuItem> items
   - Field: `orderId`, `customerName`, `orderDate`
   - Methods:
     - `addItem(MenuItem item)`
     - `removeItem(String id)`
     - `calculateTotal()`
     - `displayOrder()`

5. **Class `Restaurant`**:
   - ArrayList<MenuItem> menu
   - ArrayList<Order> orders
   - Methods: Quản lý menu, tạo order, xem orders

**Gợi ý**:
```java
public abstract class MenuItem {
    protected String id;
    protected String name;
    protected double basePrice;
    
    public abstract double calculatePrice();
    
    public void displayInfo() {
        System.out.println(name + ": " + calculatePrice());
    }
}

public class Food extends MenuItem {
    private String category;
    
    @Override
    public double calculatePrice() {
        // Logic tính giá theo category
        return basePrice;
    }
}
```

**Mở rộng** (🔴):
- Thêm discount cho order lớn
- Lưu/đọc menu từ file
- Thống kê món bán chạy nhất

---

### Mini Project 3: Hệ thống Quản lý Cửa hàng Điện thoại 📱

**Mức độ**: 🔴 Nâng cao

**Mục tiêu**: Áp dụng tất cả kiến thức đã học.

**Yêu cầu**:

1. **Class `Phone`**:
   - Fields: `brand`, `model`, `price`, `storage`, `ram`, `color`
   - Encapsulation
   - Implement `Comparable<Phone>` (sort by price)

2. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `address`
   - Encapsulation

3. **Interface `PaymentMethod`**:
   - Method `pay(double amount)`: boolean

4. **Class `CashPayment` implements `PaymentMethod`**
5. **Class `CardPayment` implements `PaymentMethod`**

6. **Class `Order`**:
   - Fields: `orderId`, `customer`, `phone`, `quantity`, `paymentMethod`, `orderDate`
   - Methods: `calculateTotal()`, `processPayment()`

7. **Class `PhoneStore`**:
   - ArrayList<Phone> inventory
   - ArrayList<Order> orders
   - Methods:
     - Quản lý inventory (CRUD)
     - Tìm kiếm phone (brand, price range)
     - Sắp xếp phone (price, brand)
     - Tạo order
     - Xem orders
     - Lưu/đọc dữ liệu từ file

8. **Class `PhoneStoreApp`** (Main):
   - Menu đầy đủ
   - Tương tác với người dùng

**Gợi ý cấu trúc**:
```
PhoneStoreSystem/
└── src/
    ├── entity/
    │   ├── Phone.java
    │   ├── Customer.java
    │   └── Order.java
    ├── service/
    │   ├── PaymentMethod.java
    │   ├── CashPayment.java
    │   ├── CardPayment.java
    │   └── PhoneStore.java
    └── main/
        └── PhoneStoreApp.java
```

**Mở rộng** (🔴):
- Thêm warranty cho phone
- Tính discount theo số lượng
- Thống kê: Phone bán chạy nhất, Doanh thu theo tháng

---

## 🧩 CHALLENGE PROBLEMS - Thử thách Nâng cao

### Challenge 1: Hệ thống Quản lý Tài chính Cá nhân 💰

**Mức độ**: 🔴 Nâng cao

**Yêu cầu**:
- Quản lý thu chi
- Phân loại: Income, Expense
- Categories: Food, Transport, Entertainment, Salary, Bonus, etc.
- Thống kê: Tổng thu, tổng chi, số dư
- Lọc theo category, tháng
- Sắp xếp theo ngày, số tiền
- Lưu/đọc từ file

**Gợi ý**:
- Sử dụng Abstract class `Transaction`
- Sử dụng Interface cho các loại transaction
- Sử dụng Lambda để filter và sort
- Sử dụng Java IO để lưu trữ

---

### Challenge 2: Hệ thống Quản lý Dự án 🚀

**Mức độ**: 🔴 Nâng cao

**Yêu cầu**:
- Quản lý Projects, Tasks, Team Members
- Inheritance: Project → Task
- Interface: Assignable (có thể gán cho member)
- Collections: Quản lý tasks, members
- Lambda: Filter tasks theo status, priority
- IO: Lưu/đọc dữ liệu

**Gợi ý**:
- Abstract class `WorkItem`
- Interface `Assignable`
- Enum cho Status, Priority
- Lambda để filter và sort

---

## 📊 Tổng kết Bài tập theo Bài học

### Phần 1: Nhập môn Java

| Bài học | Bài tập tương ứng | Mức độ |
|---------|-------------------|--------|
| **01** - Giới thiệu và Setup | Bài tập 1.0 (Bài 01) | 🟢 |
| **02** - Cấu trúc lớp Java | Bài tập 1.0 (Bài 02) | 🟢 |
| **03** - Data types | Bài tập 1.0 (Bài 03) | 🟢 |
| **04** - Java Output | Bài tập 1.0 (Bài 04) | 🟢 |
| **05** - Method | Bài tập 2.0 (Bài 05) | 🟡 |
| **06** - OOP in Java | Bài tập 2.0 (Bài 06) | 🟡 |
| **07** - Wrapper Classes | Bài tập 3.0 (Bài 07) | 🟡 |
| **08** - Keyword static | Bài tập 3.0 (Bài 08) | 🟡 |
| **09** - Scope of variables | Bài tập 3.0 (Bài 09) | 🟢 |
| **10** - Call a method | Bài tập 3.0 (Bài 10) | 🟢 |
| **11** - Java Input | Bài tập 3.0 (Bài 11) | 🟡 |
| **12** - String | Bài tập 3.1 | 🟡 |
| **13** - Regex | Bài tập 3.2 | 🟡 |

### Phần 2: Lập trình hướng đối tượng

| Bài học | Bài tập tương ứng | Mức độ |
|---------|-------------------|--------|
| **14** - Encapsulation | Bài tập 4.0 (Bài 14) | 🟡 |
| **15** - Project Phase 1 | Bài tập 4.0 (Bài 15) | 🟡 |
| **16** - Constructor | Bài tập 5.0 (Bài 16) | 🟡 |
| **17** - Inheritance | Bài tập 5.0 (Bài 17) | 🟡 |
| **18** - Project Phase 2 | Bài tập 5.0 (Bài 18-19) | 🟡 |
| **19** - Project Phase 3 | Bài tập 5.0 (Bài 18-19) | 🟡 |
| **20** - Polymorphism | Bài tập 6.0 (Bài 20) | 🟡 |
| **21** - Abstraction | Bài tập 6.0 (Bài 21) | 🟡 |
| **22** - Keyword final | Bài tập 6.0 (Bài 22) | 🟡 |
| **23** - Project Phase 4 | Bài tập 6.0 (Bài 23) | 🟡 |
| **24** - ArrayList | Bài tập 7.0 (Bài 24) | 🟡 |
| **25** - Sort Object | Bài tập 7.0 (Bài 25) | 🟡 |
| **26** - Lambda Overview | Bài tập 7.0 (Bài 26-27) | 🟡 |
| **27** - Lambda Advanced | Bài tập 7.0 (Bài 26-27) | 🟡 |
| **28** - Project Phase 5 | Bài tập 7.0 (Bài 28) | 🟡 |
| **29** - Java IO | Bài tập 8.0 (Bài 29) | 🟡 |
| **30** - Project Phase 6 | Bài tập 8.0 (Bài 30) | 🟡 |

### Tổng số bài tập

- **Bài tập theo từng bài học**: 30 bài (mỗi bài học có ít nhất 1 bài tập)
- **Bài tập tổng hợp theo Module**: 8 modules với nhiều bài tập
- **Mini Projects**: 3 projects
- **Challenge Problems**: 2 challenges

**Tổng cộng**: Hơn 50 bài tập thực hành

---

## 📋 Hướng dẫn Sử dụng Hệ thống Bài tập

### Cách tiếp cận

1. **Làm theo thứ tự**: Từ dễ đến khó
2. **Hoàn thành từng module**: Đảm bảo nắm vững trước khi chuyển module
3. **Thực hành thường xuyên**: Làm lại các bài tập để củng cố
4. **Mở rộng**: Thử thêm tính năng mới

### Đánh giá

**Sau mỗi module, học viên nên**:
- ✅ Hiểu và áp dụng được các khái niệm
- ✅ Code chạy đúng, không lỗi
- ✅ Code rõ ràng, dễ đọc
- ✅ Có validation và error handling

### Gợi ý Giải

**Khi gặp khó khăn**:
1. Xem lại bài học liên quan
2. Đọc gợi ý trong bài tập
3. Thử giải từng phần nhỏ
4. Tham khảo code mẫu (nếu có)
5. Hỏi giáo viên/mentor

---

## 🎯 Tổng kết

### Thống kê Hệ thống Bài tập

- ✅ **30 bài tập theo từng bài học**: Mỗi bài học có ít nhất 1 bài tập riêng
- ✅ **8 modules bài tập tổng hợp**: Bài tập kết hợp nhiều khái niệm
- ✅ **3 Mini Projects**: Dự án nhỏ hoàn chỉnh
- ✅ **2 Challenge Problems**: Thử thách nâng cao
- ✅ **Tổng cộng**: Hơn 50 bài tập thực hành

### Phân bố theo Mức độ

- 🟢 **Cơ bản**: ~15 bài tập
- 🟡 **Trung bình**: ~30 bài tập
- 🔴 **Nâng cao**: ~10 bài tập

### Phủ sóng Kiến thức

Hệ thống bài tập này bao phủ đầy đủ:
- ✅ Tất cả 30 bài học trong khóa học
- ✅ 4 Pillars của OOP (Encapsulation, Inheritance, Polymorphism, Abstraction)
- ✅ Collections Framework (ArrayList)
- ✅ Functional Programming (Lambda Expressions)
- ✅ Java IO (File operations)
- ✅ Best Practices (Validation, Exception handling, Code organization)

### Mục tiêu

Hệ thống bài tập này được thiết kế để:
- ✅ Củng cố kiến thức đã học
- ✅ Nâng cao kỹ năng lập trình
- ✅ Áp dụng vào thực tế
- ✅ Chuẩn bị cho các dự án lớn hơn

**Chúc các bạn học tập hiệu quả!** 🎓

---

*Tài liệu này được tạo để hỗ trợ học viên thực hành*
*Cập nhật: 2025-01-XX*
