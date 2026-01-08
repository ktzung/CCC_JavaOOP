# Bài 6: Lập trình hướng đối tượng trong Java (OOP)

> **Mục tiêu**: Hiểu được OOP là gì, sự khác biệt giữa lập trình hướng cấu trúc và OOP, các đặc trưng cơ bản của OOP, và lợi ích của việc sử dụng OOP.

## I. Giới thiệu về OOP

### OOP là gì?

**Lập trình hướng đối tượng (Object-Oriented Programming - OOP)** là một kỹ thuật lập trình cho phép lập trình viên tạo ra các đối tượng trong code để trừu tượng hóa các đối tượng trong cuộc sống thực, giúp tương tác, tính toán và xử lý một cách hiệu quả.

### Tại sao OOP quan trọng?

OOP là một trong những kỹ thuật lập trình quan trọng nhất và được sử dụng rộng rãi hiện nay. Hầu hết các ngôn ngữ lập trình hiện đại như Java, Python, C++, C#, JavaScript... đều hỗ trợ OOP.

## II. OOP trong lập trình - Ví dụ đời thường

### Ví dụ: Tạo một chiếc ô tô

Hãy tưởng tượng bạn muốn tạo ra một **chiếc ô tô**:

**Bước 1: Thiết kế (Design)**
- Bạn cần tạo một **bản thiết kế** (blueprint) của chiếc ô tô
- Bản thiết kế mô tả:
  - **Thông tin, đặc điểm** (Properties/Attributes): tên, màu sắc, kích thước, trọng lượng, số ghế, động cơ...
  - **Hành động, chức năng** (Methods/Behaviors): khởi động, dừng, tăng tốc, phanh, rẽ trái, rẽ phải...

**Bước 2: Tạo sản phẩm (Create Object)**
- Từ bản thiết kế, bạn có thể tạo ra **chiếc ô tô thực tế**
- Chiếc ô tô này sẽ có các đặc điểm và hành động giống như bản thiết kế

**Bước 3: Tạo nhiều sản phẩm (Multiple Objects)**
- Bạn có thể tạo ra **nhiều chiếc ô tô** dựa trên cùng một bản thiết kế
- Tất cả các chiếc ô tô đều có các đặc điểm và hành động giống nhau
- Nhưng **giá trị** của các đặc điểm có thể khác nhau:
  - Chiếc xe 1: màu đỏ, 4 ghế
  - Chiếc xe 2: màu xanh, 5 ghế
  - Chiếc xe 3: màu trắng, 7 ghế

**Mỗi chiếc ô tô được tạo ra được gọi là một "thực thể" (instance) của bản thiết kế.**

## III. Class và Object trong Java

### 1. Class (Lớp)

**Class** (Lớp) trong Java tương đương với **bản thiết kế** trong ví dụ trên.

**Định nghĩa**: `Class` là một kiểu dữ liệu (data type) bao gồm:
- **Thuộc tính (Properties/Attributes)**: Thể hiện qua biến (variables/fields)
- **Phương thức (Methods)**: Thể hiện qua hàm (functions)

**Đặc điểm**:
- Class là một đơn vị trừu tượng (không thể sử dụng trực tiếp)
- Class định nghĩa cấu trúc và hành vi của các đối tượng
- Khác với kiểu dữ liệu nguyên thủy (primitive types), class là sự kết hợp của nhiều thành phần

**Ví dụ**:
```java
// Class Car - Bản thiết kế của ô tô
public class Car {
    // Thuộc tính (Attributes/Properties)
    String brand;      // Hãng xe
    String color;      // Màu sắc
    int seats;         // Số ghế
    double price;      // Giá tiền
    
    // Phương thức (Methods/Behaviors)
    public void start() {
        System.out.println("Xe đang khởi động...");
    }
    
    public void stop() {
        System.out.println("Xe đã dừng lại.");
    }
    
    public void accelerate() {
        System.out.println("Xe đang tăng tốc...");
    }
}
```

### 2. Object (Đối tượng)

**Object** (Đối tượng) trong Java tương đương với **chiếc ô tô thực tế** trong ví dụ trên.

**Định nghĩa**: `Object` là một **thực thể (instance)** được tạo ra từ một class.

**Đặc điểm**:
- Object là một instance cụ thể của class
- Mỗi object có giá trị riêng cho các thuộc tính
- Các object khác nhau (ngay cả khi có cùng giá trị) là khác nhau trong bộ nhớ

**Ví dụ**:
```java
public class CarDemo {
    public static void main(String[] args) {
        // Tạo các object (đối tượng) từ class Car
        
        // Object 1: Chiếc xe Toyota màu đỏ
        Car car1 = new Car();
        car1.brand = "Toyota";
        car1.color = "Đỏ";
        car1.seats = 5;
        car1.price = 500000000;
        
        // Object 2: Chiếc xe Honda màu xanh
        Car car2 = new Car();
        car2.brand = "Honda";
        car2.color = "Xanh";
        car2.seats = 7;
        car2.price = 700000000;
        
        // Sử dụng các phương thức
        car1.start();    // Xe Toyota khởi động
        car2.start();    // Xe Honda khởi động
    }
}
```

**Kết quả**:
```
Xe đang khởi động...
Xe đang khởi động...
```

## IV. So sánh Lập trình hướng cấu trúc và OOP

### Lập trình hướng cấu trúc (Procedural Programming)

**Đặc điểm**:
- Dữ liệu (data) và hàm (functions) **tách biệt** nhau
- Hàm xử lý dữ liệu: `operation(data, parameters)`
- Thường dùng trong các ngôn ngữ như C, Pascal

**Ví dụ (C style)**:
```c
// Dữ liệu và hàm tách biệt
int numbers[100];
int count;

void init(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] = 0;
    }
}

void sort(int arr[], int size) {
    // Code sắp xếp
}

void display(int arr[], int size) {
    // Code hiển thị
}

int main() {
    init(numbers, 100);
    sort(numbers, 100);
    display(numbers, 100);
}
```

**Vấn đề**:
- ❌ Khó tái sử dụng code
- ❌ Khó bảo vệ dữ liệu (data có thể bị thay đổi từ bất kỳ đâu)
- ❌ Khó mở rộng và bảo trì với hệ thống lớn

### Lập trình hướng đối tượng (OOP)

**Đặc điểm**:
- Dữ liệu (data) và hàm (methods) **gắn liền** với nhau trong class
- Đối tượng cung cấp dịch vụ: `object.operation(parameters)`
- Dữ liệu được bảo vệ (encapsulation)

**Ví dụ (Java style)**:
```java
// Dữ liệu và phương thức gắn liền trong class
public class NumberList {
    private int[] numbers;
    private int count;
    
    public void init() {
        // Code khởi tạo
        numbers = new int[100];
        for (int i = 0; i < 100; i++) {
            numbers[i] = 0;
        }
    }
    
    public void sort() {
        // Code sắp xếp
    }
    
    public void display() {
        // Code hiển thị
    }
}

public class Main {
    public static void main(String[] args) {
        NumberList list = new NumberList();
        list.init();
        list.sort();
        list.display();
    }
}
```

**Lợi ích**:
- ✅ Dễ tái sử dụng code
- ✅ Bảo vệ dữ liệu tốt hơn (encapsulation)
- ✅ Dễ mở rộng và bảo trì
- ✅ Mô phỏng thế giới thực tốt hơn

## V. Bốn tính chất đặc trưng của OOP

Lập trình hướng đối tượng có **4 tính chất đặc trưng** (Four Pillars of OOP):

### 1. Tính đóng gói (Encapsulation)

**Định nghĩa**: Che giấu dữ liệu bên trong đối tượng và chỉ cho phép truy cập thông qua các phương thức công khai.

**Mục đích**: Bảo vệ đối tượng khỏi việc truy cập và sửa đổi không hợp lệ từ bên ngoài.

**Ví dụ**:
```java
public class BankAccount {
    private double balance;  // Private - không thể truy cập trực tiếp
    
    public void deposit(double amount) {  // Public method
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public double getBalance() {  // Public method
        return balance;
    }
}
```

> **Sẽ học chi tiết ở bài 14: Encapsulation**

### 2. Tính kế thừa (Inheritance)

**Định nghĩa**: Cho phép một lớp kế thừa các thuộc tính và phương thức từ lớp khác.

**Mục đích**: Tái sử dụng code và mở rộng chức năng mà không cần viết lại.

**Ví dụ**:
```java
// Lớp cha
public class Animal {
    String name;
    int age;
    
    public void eat() {
        System.out.println("Động vật đang ăn...");
    }
}

// Lớp con kế thừa từ Animal
public class Dog extends Animal {
    public void bark() {
        System.out.println("Gâu gâu!");
    }
}
```

> **Sẽ học chi tiết ở bài 17: Inheritance**

### 3. Tính đa hình (Polymorphism)

**Định nghĩa**: Khả năng các đối tượng thuộc các lớp khác nhau có thể phản ứng khác nhau với cùng một thông điệp.

**Mục đích**: Linh hoạt trong việc sử dụng các đối tượng từ các lớp khác nhau.

**Ví dụ**:
```java
// Cùng một phương thức "makeSound()" nhưng mỗi động vật kêu khác nhau
Animal dog = new Dog();
dog.makeSound();  // "Gâu gâu!"

Animal cat = new Cat();
cat.makeSound();  // "Meo meo!"
```

> **Sẽ học chi tiết ở bài 20: Polymorphism**

### 4. Tính trừu tượng (Abstraction)

**Định nghĩa**: Ẩn giấu chi tiết triển khai và chỉ hiển thị những gì cần thiết.

**Mục đích**: Tập trung vào "cái gì" (what) thay vì "làm thế nào" (how).

**Ví dụ**:
```java
// Abstract class - chỉ định nghĩa, không triển khai chi tiết
public abstract class Shape {
    public abstract void draw();  // Chỉ khai báo, không có code
}

public class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Vẽ hình tròn");
    }
}
```

> **Sẽ học chi tiết ở bài 21: Abstraction**

## VI. Lợi ích của OOP

### 1. Tái sử dụng code (Code Reusability)

- Viết code một lần, sử dụng nhiều lần
- Tạo class một lần, tạo nhiều object từ class đó

### 2. Dễ bảo trì (Maintainability)

- Sửa lỗi ở một nơi → áp dụng cho tất cả
- Thay đổi logic tập trung → dễ quản lý

### 3. Mô phỏng thế giới thực (Real-world Modeling)

- Class và Object giúp mô phỏng các đối tượng trong cuộc sống
- Dễ hiểu, dễ suy nghĩ như cách chúng ta nhìn thế giới

### 4. Tổ chức code tốt hơn (Better Organization)

- Chia nhỏ chương trình thành các phần dễ quản lý
- Mỗi class có trách nhiệm riêng

### 5. Mở rộng dễ dàng (Extensibility)

- Dễ thêm tính năng mới thông qua inheritance
- Không cần sửa code cũ

## VII. Ví dụ thực tế: Hệ thống quản lý thư viện

```java
// Class Book - Bản thiết kế của sách
public class Book {
    // Thuộc tính
    private String title;
    private String author;
    private String isbn;
    private boolean isAvailable;
    
    // Constructor
    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.isAvailable = true;  // Mặc định sách có sẵn
    }
    
    // Phương thức
    public void borrow() {
        if (isAvailable) {
            isAvailable = false;
            System.out.println("Đã mượn sách: " + title);
        } else {
            System.out.println("Sách đã được mượn: " + title);
        }
    }
    
    public void returnBook() {
        isAvailable = true;
        System.out.println("Đã trả sách: " + title);
    }
    
    public void displayInfo() {
        System.out.println("=== THÔNG TIN SÁCH ===");
        System.out.println("Tiêu đề: " + title);
        System.out.println("Tác giả: " + author);
        System.out.println("ISBN: " + isbn);
        System.out.println("Trạng thái: " + (isAvailable ? "Có sẵn" : "Đã mượn"));
    }
    
    // Getters
    public String getTitle() {
        return title;
    }
    
    public boolean isAvailable() {
        return isAvailable;
    }
}

// Sử dụng
public class LibrarySystem {
    public static void main(String[] args) {
        // Tạo các object (sách) từ class Book
        Book book1 = new Book("Java Programming", "John Doe", "978-1234567890");
        Book book2 = new Book("Python Basics", "Jane Smith", "978-0987654321");
        Book book3 = new Book("Database Design", "Bob Johnson", "978-1122334455");
        
        // Hiển thị thông tin
        book1.displayInfo();
        System.out.println();
        
        // Mượn sách
        book1.borrow();
        System.out.println();
        
        // Cố gắng mượn lại
        book1.borrow();  // Sẽ báo là đã được mượn
        System.out.println();
        
        // Trả sách
        book1.returnBook();
        System.out.println();
        
        // Hiển thị lại thông tin
        book1.displayInfo();
    }
}
```

**Kết quả**:
```
=== THÔNG TIN SÁCH ===
Tiêu đề: Java Programming
Tác giả: John Doe
ISBN: 978-1234567890
Trạng thái: Có sẵn

Đã mượn sách: Java Programming

Sách đã được mượn: Java Programming

Đã trả sách: Java Programming

=== THÔNG TIN SÁCH ===
Tiêu đề: Java Programming
Tác giả: John Doe
ISBN: 978-1234567890
Trạng thái: Có sẵn
```

## VIII. So sánh Class và Object

| Đặc điểm | Class (Lớp) | Object (Đối tượng) |
|----------|-------------|-------------------|
| **Định nghĩa** | Bản thiết kế, khuôn mẫu | Thực thể cụ thể được tạo từ class |
| **Tương tự** | Blueprint của ngôi nhà | Ngôi nhà thực tế |
| **Tồn tại** | Tồn tại trong code (template) | Tồn tại trong bộ nhớ khi chương trình chạy |
| **Số lượng** | 1 class | Nhiều object từ 1 class |
| **Sử dụng** | Để tạo object | Để sử dụng các chức năng |

**Ví dụ**:
```java
// Class Car - chỉ có 1 định nghĩa
public class Car {
    String brand;
    String color;
}

// Có thể tạo nhiều object từ 1 class
Car car1 = new Car();  // Object 1
Car car2 = new Car();  // Object 2
Car car3 = new Car();  // Object 3
```

## IX. Tổng kết OOP

### OOP giúp giải quyết vấn đề gì?

**Vấn đề với lập trình cấu trúc (C)**:
- Code lặp lại nhiều
- Khó bảo trì với hệ thống lớn
- Dữ liệu không được bảo vệ
- Khó mở rộng

**Giải pháp với OOP (Java)**:
- ✅ Tái sử dụng code (Inheritance)
- ✅ Bảo vệ dữ liệu (Encapsulation)
- ✅ Linh hoạt (Polymorphism)
- ✅ Tổ chức tốt (Abstraction)

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu OOP là gì và tại sao nó quan trọng
- ✅ Phân biệt được Class và Object
- ✅ So sánh được lập trình hướng cấu trúc và OOP
- ✅ Nắm được 4 tính chất đặc trưng của OOP
- ✅ Hiểu lợi ích của việc sử dụng OOP
- ✅ Áp dụng OOP vào ví dụ thực tế

## Bài tập thực hành

1. **Tạo class `Student` với các thành phần**:
   - Thuộc tính: name, age, studentId, gpa
   - Phương thức: displayInfo(), study(), takeExam()
   - Tạo 3 object Student khác nhau

2. **Tạo class `Product` (Sản phẩm)**:
   - Thuộc tính: name, price, quantity, category
   - Phương thức: displayInfo(), calculateTotal(), checkStock()
   - Tạo 5 object Product khác nhau

3. **Tạo class `BankAccount`**:
   - Thuộc tính: accountNumber, ownerName, balance
   - Phương thức: deposit(), withdraw(), displayBalance()
   - Tạo 2 object BankAccount và thực hiện các giao dịch

## Tài liệu tham khảo

- [Oracle Java Tutorial - Classes and Objects](https://docs.oracle.com/javase/tutorial/java/concepts/index.html)
- [OOP Concepts in Java](https://www.javatpoint.com/java-oops-concepts)
- [Introduction to OOP](https://www.programiz.com/java-programming/object-oriented-programming)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
