# Bài 5: Phương thức (Method) trong Java

> **Mục tiêu**: Hiểu được phương thức là gì, cách khai báo và sử dụng phương thức, phân biệt các loại phương thức, và áp dụng phương thức để tổ chức code tốt hơn.

## I. Giới thiệu về phương thức (Method)

### Phương thức là gì?

**Phương thức (Method)** là một khối code được đặt tên để thực hiện một nhiệm vụ cụ thể. Phương thức cho phép:
- **Tái sử dụng code**: Viết một lần, dùng nhiều lần
- **Tổ chức code**: Chia nhỏ chương trình thành các phần dễ quản lý
- **Dễ bảo trì**: Sửa lỗi hoặc thay đổi ở một nơi

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **máy tính**:
- **Phương thức cộng**: `cong(a, b)` → Trả về a + b
- **Phương thức nhân**: `nhan(a, b)` → Trả về a * b
- **Phương thức hiển thị**: `hienThiKetQua(kq)` → In ra màn hình

Thay vì viết lại code tính toán mỗi lần, bạn chỉ cần gọi phương thức!

## II. Cấu trúc của phương thức (Method Structure)

### Cú pháp khai báo phương thức

```java
[Access Modifier] [static] [Return Type] [Method Name] ([Parameter List]) {
    // Method Body - Code thực hiện
    [return statement;]
}
```

### Các thành phần của phương thức

| Thành phần | Mô tả | Ví dụ |
|------------|-------|-------|
| **Access Modifier** | Xác định phạm vi truy cập | `public`, `private`, `protected` |
| **static** | Phương thức thuộc về lớp | `static` (sẽ học ở bài sau) |
| **Return Type** | Kiểu dữ liệu trả về | `int`, `String`, `void` (không trả về) |
| **Method Name** | Tên phương thức | `sum`, `calculateArea`, `display` |
| **Parameter List** | Danh sách tham số | `(int a, int b)`, `()` (không có tham số) |
| **Method Body** | Khối code thực hiện | `{ ... }` |
| **return statement** | Trả về giá trị | `return result;` |

### Ví dụ minh họa

```java
public class MethodExample {
    
    // Phương thức không có tham số, không trả về giá trị
    public void displayHello() {
        System.out.println("Xin chào Java!");
    }
    
    // Phương thức có tham số, không trả về giá trị
    public void displayMessage(String message) {
        System.out.println(message);
    }
    
    // Phương thức có tham số, trả về giá trị
    public int sum(int a, int b) {
        int result = a + b;
        return result;  // Trả về kết quả
    }
    
    // Phương thức tính diện tích hình chữ nhật
    public double calculateArea(double width, double height) {
        return width * height;  // Trả về trực tiếp
    }
    
    // Phương thức main để chạy chương trình
    public static void main(String[] args) {
        MethodExample obj = new MethodExample();
        
        // Gọi các phương thức
        obj.displayHello();
        obj.displayMessage("Tôi đang học Java!");
        
        int total = obj.sum(10, 20);
        System.out.println("Tổng: " + total);  // Tổng: 30
        
        double area = obj.calculateArea(5.5, 3.2);
        System.out.println("Diện tích: " + area);  // Diện tích: 17.6
    }
}
```

## III. Phân loại phương thức

### 1. Phương thức có trả về giá trị (Return Method)

Phương thức **trả về** một giá trị sau khi thực hiện xong.

**Cú pháp**:
```java
public [Return Type] methodName([parameters]) {
    // Code thực hiện
    return value;  // Phải có return statement
}
```

**Ví dụ**:
```java
public class ReturnMethods {
    
    // Trả về số nguyên
    public int getSum(int a, int b) {
        return a + b;
    }
    
    // Trả về số thực
    public double getAverage(int a, int b, int c) {
        return (a + b + c) / 3.0;  // 3.0 để có kết quả số thực
    }
    
    // Trả về chuỗi
    public String getFullName(String firstName, String lastName) {
        return firstName + " " + lastName;
    }
    
    // Trả về boolean
    public boolean isEven(int number) {
        return number % 2 == 0;
    }
    
    public static void main(String[] args) {
        ReturnMethods obj = new ReturnMethods();
        
        int sum = obj.getSum(5, 10);
        System.out.println("Tổng: " + sum);  // 15
        
        double avg = obj.getAverage(10, 20, 30);
        System.out.println("Trung bình: " + avg);  // 20.0
        
        String fullName = obj.getFullName("Nguyễn", "Văn A");
        System.out.println("Họ tên: " + fullName);  // Nguyễn Văn A
        
        boolean even = obj.isEven(10);
        System.out.println("Số chẵn? " + even);  // true
    }
}
```

**Lưu ý quan trọng**:
- Phải có `return` statement trong phương thức có kiểu trả về (trừ `void`)
- Kiểu dữ liệu của giá trị `return` phải khớp với `Return Type`

### 2. Phương thức không trả về giá trị (Void Method)

Phương thức **không trả về** giá trị (kiểu trả về là `void`).

**Cú pháp**:
```java
public void methodName([parameters]) {
    // Code thực hiện
    // Không có return statement
}
```

**Ví dụ**:
```java
public class VoidMethods {
    
    // Hiển thị thông báo
    public void displayMessage(String message) {
        System.out.println(message);
    }
    
    // Hiển thị thông tin sinh viên
    public void displayStudentInfo(String name, int age, double gpa) {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Điểm TB: " + gpa);
    }
    
    // In hình tam giác
    public void printTriangle(int rows) {
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
    
    public static void main(String[] args) {
        VoidMethods obj = new VoidMethods();
        
        obj.displayMessage("Xin chào!");
        obj.displayStudentInfo("Nguyễn Văn A", 20, 8.5);
        obj.printTriangle(5);
    }
}
```

**Lưu ý**:
- Phương thức `void` **không cần** `return` statement
- Nếu muốn thoát sớm, có thể dùng `return;` (không có giá trị)

```java
public void checkAge(int age) {
    if (age < 0) {
        System.out.println("Tuổi không hợp lệ!");
        return;  // Thoát sớm
    }
    System.out.println("Tuổi: " + age);
}
```

## IV. Phân loại theo nguồn gốc

### 1. Predefined Methods (Phương thức có sẵn)

Các phương thức được Java cung cấp sẵn, bạn chỉ cần gọi.

**Ví dụ**:
```java
public class PredefinedMethods {
    public static void main(String[] args) {
        // Math.max() - Tìm số lớn hơn
        int max = Math.max(10, 20);
        System.out.println("Max: " + max);  // 20
        
        // Math.min() - Tìm số nhỏ hơn
        int min = Math.min(10, 20);
        System.out.println("Min: " + min);  // 10
        
        // Math.pow() - Lũy thừa
        double power = Math.pow(2, 3);
        System.out.println("2^3 = " + power);  // 8.0
        
        // Math.sqrt() - Căn bậc hai
        double sqrt = Math.sqrt(16);
        System.out.println("√16 = " + sqrt);  // 4.0
        
        // Math.abs() - Giá trị tuyệt đối
        int abs = Math.abs(-10);
        System.out.println("|-10| = " + abs);  // 10
        
        // String.length() - Độ dài chuỗi
        String str = "Hello";
        int length = str.length();
        System.out.println("Độ dài: " + length);  // 5
    }
}
```

### 2. User-defined Methods (Phương thức tự định nghĩa)

Các phương thức do bạn tự viết.

**Ví dụ**:
```java
public class UserDefinedMethods {
    
    // Phương thức tính giai thừa
    public int factorial(int n) {
        if (n <= 1) {
            return 1;
        }
        return n * factorial(n - 1);  // Đệ quy
    }
    
    // Phương thức kiểm tra số nguyên tố
    public boolean isPrime(int n) {
        if (n < 2) return false;
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
    
    // Phương thức tính lương
    public double calculateSalary(double baseSalary, double bonus, double tax) {
        return baseSalary + bonus - tax;
    }
    
    public static void main(String[] args) {
        UserDefinedMethods obj = new UserDefinedMethods();
        
        int fact = obj.factorial(5);
        System.out.println("5! = " + fact);  // 120
        
        boolean prime = obj.isPrime(17);
        System.out.println("17 là số nguyên tố? " + prime);  // true
        
        double salary = obj.calculateSalary(10000000, 2000000, 1000000);
        System.out.println("Lương: " + salary);  // 11000000.0
    }
}
```

## V. Quy tắc đặt tên phương thức

### Nguyên tắc đặt tên

1. **Bắt đầu bằng chữ cái thường**
2. **Sử dụng động từ** (verb) để mô tả hành động
3. **CamelCase**: Viết hoa chữ đầu mỗi từ (trừ từ đầu tiên)
4. **Có ý nghĩa**: Tên phải mô tả rõ chức năng

### Ví dụ đúng và sai

| ✅ Đúng | ❌ Sai | Lý do |
|---------|--------|-------|
| `calculateSum()` | `sum()`, `s()` | Quá ngắn, không rõ ràng |
| `displayInfo()` | `displayinfo()`, `DisplayInfo()` | Sai format CamelCase |
| `getStudentName()` | `getStudent()` | Rõ ràng hơn về chức năng |
| `isValid()` | `check()`, `valid()` | Dùng động từ, rõ ràng |
| `findMax()` | `max()`, `maximum()` | Dùng động từ |

### Quy ước đặt tên theo kiểu trả về

- **Getter**: Bắt đầu bằng `get` → `getName()`, `getAge()`
- **Setter**: Bắt đầu bằng `set` → `setName()`, `setAge()`
- **Boolean**: Bắt đầu bằng `is`/`has` → `isValid()`, `hasPermission()`
- **Tính toán**: Động từ → `calculate()`, `find()`, `search()`
- **Hiển thị**: Động từ → `display()`, `print()`, `show()`

## VI. Tham số (Parameters)

### Tham số là gì?

**Tham số (Parameters)** là các biến được truyền vào phương thức để phương thức sử dụng.

### Phân biệt Parameter và Argument

- **Parameter**: Biến trong khai báo phương thức
- **Argument**: Giá trị thực tế được truyền khi gọi phương thức

```java
public class Parameters {
    
    // a, b là parameters (tham số)
    public int sum(int a, int b) {
        return a + b;
    }
    
    public static void main(String[] args) {
        Parameters obj = new Parameters();
        
        // 10, 20 là arguments (đối số)
        int result = obj.sum(10, 20);
        System.out.println("Kết quả: " + result);
    }
}
```

### Các loại tham số

**1. Không có tham số**:
```java
public void displayHello() {
    System.out.println("Hello!");
}
```

**2. Một tham số**:
```java
public void greet(String name) {
    System.out.println("Xin chào, " + name + "!");
}
```

**3. Nhiều tham số**:
```java
public void displayInfo(String name, int age, double gpa) {
    System.out.println("Tên: " + name);
    System.out.println("Tuổi: " + age);
    System.out.println("Điểm TB: " + gpa);
}
```

**4. Tham số là mảng**:
```java
public void printArray(int[] numbers) {
    for (int num : numbers) {
        System.out.print(num + " ");
    }
}
```

**5. Varargs (Variable Arguments) - Java 5+**:
```java
public int sum(int... numbers) {  // Có thể truyền nhiều số
    int total = 0;
    for (int num : numbers) {
        total += num;
    }
    return total;
}

// Sử dụng
int result1 = obj.sum(1, 2, 3);           // 6
int result2 = obj.sum(1, 2, 3, 4, 5);     // 15
```

## VII. Ví dụ thực tế

### Ví dụ 1: Lớp Calculator (Máy tính)

```java
public class Calculator {
    
    // Cộng
    public int add(int a, int b) {
        return a + b;
    }
    
    // Trừ
    public int subtract(int a, int b) {
        return a - b;
    }
    
    // Nhân
    public int multiply(int a, int b) {
        return a * b;
    }
    
    // Chia (trả về số thực)
    public double divide(int a, int b) {
        if (b == 0) {
            System.out.println("Lỗi: Không thể chia cho 0!");
            return 0;
        }
        return (double) a / b;
    }
    
    // Tính lũy thừa
    public double power(double base, double exponent) {
        return Math.pow(base, exponent);
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        System.out.println("10 + 5 = " + calc.add(10, 5));
        System.out.println("10 - 5 = " + calc.subtract(10, 5));
        System.out.println("10 * 5 = " + calc.multiply(10, 5));
        System.out.println("10 / 5 = " + calc.divide(10, 5));
        System.out.println("2^8 = " + calc.power(2, 8));
    }
}
```

### Ví dụ 2: Lớp Student với các phương thức

```java
public class Student {
    private String name;
    private int age;
    private double gpa;
    
    // Constructor (sẽ học ở bài sau)
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Getter methods
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public double getGpa() {
        return gpa;
    }
    
    // Setter methods
    public void setName(String name) {
        this.name = name;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public void setGpa(double gpa) {
        this.gpa = gpa;
    }
    
    // Phương thức tính xếp loại
    public String getGrade() {
        if (gpa >= 9.0) return "Xuất sắc";
        if (gpa >= 8.0) return "Giỏi";
        if (gpa >= 7.0) return "Khá";
        if (gpa >= 5.0) return "Trung bình";
        return "Yếu";
    }
    
    // Phương thức hiển thị thông tin
    public void displayInfo() {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Điểm TB: " + gpa);
        System.out.println("Xếp loại: " + getGrade());
    }
    
    public static void main(String[] args) {
        Student student = new Student("Nguyễn Văn A", 20, 8.5);
        student.displayInfo();
    }
}
```

## VIII. Lợi ích của việc sử dụng phương thức

### 1. Tái sử dụng code (Code Reusability)

```java
// Thay vì viết lại code mỗi lần
int sum1 = a1 + b1;
int sum2 = a2 + b2;
int sum3 = a3 + b3;

// Chỉ cần viết phương thức một lần
public int sum(int a, int b) {
    return a + b;
}

// Gọi nhiều lần
int sum1 = sum(a1, b1);
int sum2 = sum(a2, b2);
int sum3 = sum(a3, b3);
```

### 2. Dễ bảo trì (Maintainability)

- Sửa lỗi ở một nơi → áp dụng cho tất cả nơi sử dụng
- Thay đổi logic → chỉ cần sửa trong phương thức

### 3. Tổ chức code tốt hơn (Better Organization)

- Chia nhỏ chương trình thành các phần nhỏ
- Mỗi phương thức thực hiện một nhiệm vụ cụ thể
- Code dễ đọc, dễ hiểu hơn

### 4. Testing dễ dàng hơn (Easier Testing)

- Có thể test từng phương thức riêng lẻ
- Dễ tìm và sửa lỗi

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu phương thức là gì và tại sao nó quan trọng
- ✅ Nắm được cấu trúc của phương thức
- ✅ Phân biệt được phương thức có trả về và void
- ✅ Biết cách đặt tên phương thức đúng quy tắc
- ✅ Hiểu về tham số và cách sử dụng
- ✅ Áp dụng phương thức vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo lớp `Rectangle` với các phương thức**:
   - `calculateArea()` - Tính diện tích
   - `calculatePerimeter()` - Tính chu vi
   - `displayInfo()` - Hiển thị thông tin

2. **Tạo lớp `BankAccount` với các phương thức**:
   - `deposit(amount)` - Gửi tiền
   - `withdraw(amount)` - Rút tiền
   - `getBalance()` - Lấy số dư
   - `displayInfo()` - Hiển thị thông tin

3. **Tạo phương thức tính giai thừa**:
   - Sử dụng vòng lặp
   - Kiểm tra số hợp lệ (>= 0)

## Tài liệu tham khảo

- [Oracle Java Tutorial - Methods](https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html)
- [Java Method Overloading](https://www.javatpoint.com/method-overloading-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
