# Bài 16: Constructor (Hàm khởi tạo) trong Java

> **Mục tiêu**: Hiểu được constructor là gì, các loại constructor, cách sử dụng `this` trong constructor, và constructor overloading.

## I. Giới thiệu về Constructor

### Constructor là gì?

**Constructor (Hàm khởi tạo)** là một phương thức đặc biệt được sử dụng để **khởi tạo** (tạo và thiết lập giá trị ban đầu) cho một đối tượng khi nó được tạo ra.

### Đặc điểm của Constructor

1. **Tên trùng với tên lớp**: Constructor phải có tên giống hệt tên lớp chứa nó
2. **Không có kiểu trả về**: Constructor không có `return type` (không phải `void`, `int`, v.v.)
3. **Tự động gọi**: Constructor được tự động gọi khi tạo đối tượng bằng từ khóa `new`
4. **Không thể gọi trực tiếp**: Không thể gọi constructor như một phương thức thông thường

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn đang xây một **ngôi nhà**:

- **Blueprint** (Bản thiết kế) = **Class**
- **Ngôi nhà thực tế** = **Object** (đối tượng)
- **Quá trình xây dựng** = **Constructor** (khởi tạo các giá trị ban đầu)

Khi xây nhà, bạn cần:
- Thiết lập diện tích, số phòng, màu sơn, v.v. = Constructor thiết lập các giá trị ban đầu cho đối tượng

## II. Cú pháp và các loại Constructor

### Cú pháp cơ bản

```java
[Access Modifier] ClassName([Parameter List]) {
    // Code khởi tạo
}
```

### 1. Default Constructor (Constructor mặc định)

**Default Constructor** (hay **no-argument constructor**) là constructor **không có tham số**.

```java
public class Student {
    private String name;
    private int age;
    
    // Default constructor
    public Student() {
        // Khởi tạo giá trị mặc định
        this.name = "Chưa có tên";
        this.age = 0;
    }
}
```

**Lưu ý quan trọng**:
- Nếu bạn **không tạo constructor nào**, Java sẽ **tự động tạo** một default constructor ẩn
- Constructor mặc định này sẽ khởi tạo các fields với giá trị mặc định (0, null, false, v.v.)
- Khi bạn tạo **bất kỳ constructor nào** (có tham số), constructor mặc định sẽ **không còn tồn tại** nữa

```java
public class Example {
    private int value;
    
    // Nếu không có constructor nào, Java tự tạo:
    // public Example() { }
    
    // Nếu bạn tạo constructor có tham số:
    public Example(int value) {
        this.value = value;
    }
    
    // Thì phải tự tạo default constructor nếu cần:
    public Example() {
        this.value = 0;
    }
}
```

### 2. Parameterized Constructor (Constructor có tham số)

**Parameterized Constructor** là constructor **có tham số** để khởi tạo đối tượng với giá trị cụ thể.

```java
public class Student {
    private String name;
    private int age;
    private double gpa;
    
    // Parameterized constructor
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Getters
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public double getGpa() {
        return gpa;
    }
    
    public static void main(String[] args) {
        // Sử dụng constructor có tham số
        Student student = new Student("Nguyễn Văn A", 20, 8.5);
        
        System.out.println("Tên: " + student.getName());
        System.out.println("Tuổi: " + student.getAge());
        System.out.println("Điểm TB: " + student.getGpa());
    }
}
```

**Kết quả**:
```
Tên: Nguyễn Văn A
Tuổi: 20
Điểm TB: 8.5
```

## III. Từ khóa `this`

### `this` là gì?

**`this`** là một từ khóa đặc biệt trong Java, đại diện cho **đối tượng hiện tại** (object đang được tạo hoặc đang gọi phương thức).

### Sử dụng `this` trong Constructor

**`this`** thường được sử dụng trong constructor để phân biệt giữa **parameter** và **instance variable** khi chúng có cùng tên.

```java
public class Student {
    private String name;  // Instance variable
    private int age;
    
    public Student(String name, int age) {  // Parameters
        // Sử dụng 'this' để phân biệt
        this.name = name;  // this.name = instance variable, name = parameter
        this.age = age;
    }
}
```

### Ví dụ minh họa sự khác biệt

**Không dùng `this`** (có thể gây nhầm lẫn):
```java
public class Student {
    private String name;
    private int age;
    
    public Student(String n, int a) {  // Đặt tên khác để tránh nhầm lẫn
        name = n;
        age = a;
    }
}
```

**Dùng `this`** (rõ ràng hơn):
```java
public class Student {
    private String name;
    private int age;
    
    public Student(String name, int age) {  // Có thể dùng tên giống
        this.name = name;  // Rõ ràng: this.name là instance variable
        this.age = age;    //          name là parameter
    }
}
```

### Các cách sử dụng `this`

**1. Tham chiếu đến instance variables**:
```java
public class Example {
    private int value;
    
    public Example(int value) {
        this.value = value;  // this.value = instance variable
    }
}
```

**2. Gọi constructor khác trong cùng lớp** (Constructor chaining):
```java
public class Student {
    private String name;
    private int age;
    private double gpa;
    
    // Constructor đầy đủ
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Constructor chỉ có tên và tuổi
    public Student(String name, int age) {
        this(name, age, 0.0);  // Gọi constructor trên, gpa = 0.0
    }
    
    // Constructor chỉ có tên
    public Student(String name) {
        this(name, 0, 0.0);  // Gọi constructor trên, age = 0, gpa = 0.0
    }
}
```

> **Lưu ý**: Khi gọi constructor khác bằng `this()`, lệnh này **phải là lệnh đầu tiên** trong constructor.

## IV. Constructor Overloading (Nạp chồng Constructor)

### Constructor Overloading là gì?

**Constructor Overloading** (Nạp chồng constructor) là tạo **nhiều constructor** trong cùng một lớp với **số lượng hoặc kiểu tham số khác nhau**.

### Ví dụ

```java
public class Student {
    private String name;
    private int age;
    private double gpa;
    
    // Constructor 1: Không có tham số
    public Student() {
        this.name = "Chưa có tên";
        this.age = 0;
        this.gpa = 0.0;
    }
    
    // Constructor 2: Chỉ có tên
    public Student(String name) {
        this.name = name;
        this.age = 0;
        this.gpa = 0.0;
    }
    
    // Constructor 3: Có tên và tuổi
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.gpa = 0.0;
    }
    
    // Constructor 4: Đầy đủ thông tin
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Hiển thị thông tin
    public void displayInfo() {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Điểm TB: " + gpa);
    }
    
    public static void main(String[] args) {
        // Tạo đối tượng với các constructor khác nhau
        Student s1 = new Student();                      // Constructor 1
        Student s2 = new Student("Nguyễn Văn A");       // Constructor 2
        Student s3 = new Student("Trần Thị B", 20);     // Constructor 3
        Student s4 = new Student("Lê Văn C", 21, 8.5);  // Constructor 4
        
        s1.displayInfo();
        System.out.println();
        s2.displayInfo();
        System.out.println();
        s3.displayInfo();
        System.out.println();
        s4.displayInfo();
    }
}
```

**Kết quả**:
```
=== THÔNG TIN SINH VIÊN ===
Tên: Chưa có tên
Tuổi: 0
Điểm TB: 0.0

=== THÔNG TIN SINH VIÊN ===
Tên: Nguyễn Văn A
Tuổi: 0
Điểm TB: 0.0

=== THÔNG TIN SINH VIÊN ===
Tên: Trần Thị B
Tuổi: 20
Điểm TB: 0.0

=== THÔNG TIN SINH VIÊN ===
Tên: Lê Văn C
Tuổi: 21
Điểm TB: 8.5
```

### Sử dụng Constructor chaining (khuyến nghị)

Thay vì viết lại code, bạn có thể gọi constructor khác bằng `this()`:

```java
public class Student {
    private String name;
    private int age;
    private double gpa;
    
    // Constructor đầy đủ - constructor chính
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Constructor chỉ có tên và tuổi - gọi constructor chính
    public Student(String name, int age) {
        this(name, age, 0.0);  // Gọi constructor chính với gpa = 0.0
    }
    
    // Constructor chỉ có tên - gọi constructor chính
    public Student(String name) {
        this(name, 0, 0.0);  // Gọi constructor chính với age = 0, gpa = 0.0
    }
    
    // Default constructor - gọi constructor chính
    public Student() {
        this("Chưa có tên", 0, 0.0);  // Gọi constructor chính
    }
}
```

**Lợi ích**:
- ✅ Giảm code trùng lặp
- ✅ Dễ bảo trì: Sửa logic ở một nơi
- ✅ Nhất quán: Tất cả constructor đều gọi constructor chính

## V. Ví dụ thực tế

### Ví dụ 1: Lớp Car (Ô tô)

```java
public class Car {
    private String brand;
    private String model;
    private int year;
    private double price;
    private String color;
    
    // Constructor đầy đủ
    public Car(String brand, String model, int year, double price, String color) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.price = price;
        this.color = color;
    }
    
    // Constructor không có màu (mặc định màu đen)
    public Car(String brand, String model, int year, double price) {
        this(brand, model, year, price, "Đen");
    }
    
    // Constructor không có giá (dùng để đăng ký)
    public Car(String brand, String model, int year) {
        this(brand, model, year, 0.0, "Đen");
    }
    
    // Constructor mặc định
    public Car() {
        this("Chưa xác định", "Chưa xác định", 0, 0.0, "Đen");
    }
    
    // Phương thức hiển thị
    public void displayInfo() {
        System.out.println("=== THÔNG TIN XE ===");
        System.out.println("Hãng: " + brand);
        System.out.println("Model: " + model);
        System.out.println("Năm: " + year);
        System.out.println("Giá: " + price);
        System.out.println("Màu: " + color);
    }
    
    public static void main(String[] args) {
        Car car1 = new Car("Toyota", "Camry", 2023, 1500000000, "Trắng");
        Car car2 = new Car("Honda", "Civic", 2023, 1200000000);
        Car car3 = new Car("Mazda", "CX-5", 2023);
        Car car4 = new Car();
        
        car1.displayInfo();
        System.out.println();
        car2.displayInfo();
        System.out.println();
        car3.displayInfo();
        System.out.println();
        car4.displayInfo();
    }
}
```

### Ví dụ 2: Lớp BankAccount với validation

```java
public class BankAccount {
    private String accountNumber;
    private String ownerName;
    private double balance;
    
    // Constructor đầy đủ với kiểm tra
    public BankAccount(String accountNumber, String ownerName, double balance) {
        setAccountNumber(accountNumber);
        setOwnerName(ownerName);
        deposit(balance);  // Sử dụng deposit để kiểm tra
    }
    
    // Constructor chỉ có số tài khoản và tên chủ
    public BankAccount(String accountNumber, String ownerName) {
        this(accountNumber, ownerName, 0.0);
    }
    
    // Setters với validation
    public void setAccountNumber(String accountNumber) {
        if (accountNumber != null && accountNumber.length() > 0) {
            this.accountNumber = accountNumber;
        } else {
            throw new IllegalArgumentException("Số tài khoản không hợp lệ!");
        }
    }
    
    public void setOwnerName(String ownerName) {
        if (ownerName != null && ownerName.trim().length() > 0) {
            this.ownerName = ownerName;
        } else {
            throw new IllegalArgumentException("Tên chủ tài khoản không hợp lệ!");
        }
    }
    
    // Phương thức nạp tiền
    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
        } else {
            System.out.println("Số tiền nạp phải lớn hơn 0!");
        }
    }
    
    // Phương thức rút tiền
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            this.balance -= amount;
        } else {
            System.out.println("Số dư không đủ hoặc số tiền không hợp lệ!");
        }
    }
    
    // Getters
    public String getAccountNumber() {
        return accountNumber;
    }
    
    public String getOwnerName() {
        return ownerName;
    }
    
    public double getBalance() {
        return balance;
    }
    
    // Hiển thị thông tin
    public void displayInfo() {
        System.out.println("=== THÔNG TIN TÀI KHOẢN ===");
        System.out.println("Số TK: " + accountNumber);
        System.out.println("Chủ TK: " + ownerName);
        System.out.println("Số dư: " + balance);
    }
    
    public static void main(String[] args) {
        BankAccount acc1 = new BankAccount("ACC001", "Nguyễn Văn A", 1000000);
        BankAccount acc2 = new BankAccount("ACC002", "Trần Thị B");
        
        acc1.displayInfo();
        System.out.println();
        acc2.displayInfo();
    }
}
```

## VI. So sánh Constructor và Method

| Đặc điểm | Constructor | Method |
|----------|-------------|--------|
| **Tên** | Phải trùng với tên lớp | Bất kỳ tên nào (theo quy tắc đặt tên) |
| **Kiểu trả về** | Không có (không phải `void`) | Có (hoặc `void`) |
| **Tự động gọi** | Tự động khi tạo đối tượng | Phải gọi thủ công |
| **Mục đích** | Khởi tạo đối tượng | Thực hiện một hành động |
| **Kế thừa** | Không được kế thừa | Được kế thừa |

```java
public class Example {
    // Constructor
    public Example() {
        // Khởi tạo đối tượng
    }
    
    // Method
    public void doSomething() {
        // Thực hiện hành động
    }
}
```

## VII. Lưu ý quan trọng

### 1. Constructor không thể trả về giá trị

```java
// ❌ SAI
public class Example {
    public Example() {
        return;  // Chỉ có thể return; (không có giá trị), không thể return value;
    }
}
```

### 2. Constructor không được khai báo là `static` hoặc `final`

```java
// ❌ SAI
public class Example {
    static public Example() { }  // Lỗi!
    final public Example() { }   // Lỗi!
}
```

### 3. Constructor có thể `private`

```java
public class Singleton {
    private static Singleton instance;
    
    // Private constructor để ngăn tạo đối tượng từ bên ngoài
    private Singleton() {
    }
    
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

> **Lưu ý**: Private constructor thường dùng trong **Singleton Pattern** (sẽ học ở các bài nâng cao).

### 4. Constructor và Default Values

```java
public class Example {
    private int value;
    private String name;
    private boolean active;
    
    // Nếu không khởi tạo trong constructor:
    public Example() {
        // value = 0 (mặc định)
        // name = null (mặc định)
        // active = false (mặc định)
    }
    
    // Hoặc khởi tạo giá trị mặc định:
    public Example() {
        this.value = 0;
        this.name = "Default";
        this.active = true;
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu constructor là gì và tại sao nó quan trọng
- ✅ Nắm được các loại constructor: Default và Parameterized
- ✅ Biết cách sử dụng từ khóa `this` trong constructor
- ✅ Hiểu về constructor overloading và constructor chaining
- ✅ Áp dụng constructor vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo lớp `Rectangle` với các constructor**:
   - Constructor mặc định (width = 0, height = 0)
   - Constructor có width và height
   - Constructor chính nhận width và height, các constructor khác gọi constructor chính

2. **Tạo lớp `Book` với các constructor**:
   - Constructor đầy đủ: title, author, price, pages
   - Constructor không có price (price = 0)
   - Constructor chỉ có title và author
   - Tất cả constructor đều validate dữ liệu

3. **Tạo lớp `Employee` với constructor overloading**:
   - Constructor đầy đủ: id, name, salary, department
   - Constructor không có department (department = "Chưa phân công")
   - Constructor chính, các constructor khác gọi constructor chính

## Tài liệu tham khảo

- [Oracle Java Tutorial - Constructors](https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html)
- [Java Constructor Overloading](https://www.javatpoint.com/constructor-overloading-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
