# Bài 19: Project - Phase 3: Thêm Methods và Áp dụng Polymorphism

> **Mục tiêu**: Thêm methods `input()` và `display()` vào các class, áp dụng Method Overriding (Polymorphism), và tạo chương trình tương tác với người dùng.

## I. Giới thiệu về Phase 3

### Mục tiêu

Trong Phase 3, chúng ta sẽ:
1. Thêm methods `input()` và `display()` vào class `Person`
2. Override các methods này trong `Student` và `Staff`
3. Áp dụng **Polymorphism** (Method Overriding)
4. Tạo chương trình tương tác với người dùng

### Tại sao cần Methods?

Methods trong class cho phép:
- ✅ **Tương tác với đối tượng**: Nhập dữ liệu, hiển thị thông tin
- ✅ **Encapsulation**: Logic xử lý nằm trong class
- ✅ **Reusability**: Có thể gọi nhiều lần
- ✅ **Polymorphism**: Mỗi lớp có thể override theo cách riêng

## II. Thêm Methods vào Person

### Method display() - Hiển thị thông tin

Thêm method `display()` vào class `Person`:

```java
package entity;

public class Person {
    // ... fields và getters/setters ...
    
    // Method hiển thị thông tin
    public void display() {
        System.out.println("=== THÔNG TIN ===");
        System.out.println("Mã số: " + rollNumber);
        System.out.println("Tên: " + name);
        System.out.println("Giới tính: " + (gender ? "Nam" : "Nữ"));
        System.out.println("Ngày sinh: " + dob);
        System.out.println("Email: " + email);
        System.out.println("SĐT: " + mobile);
        System.out.println("Địa chỉ: " + address);
    }
}
```

**Hoặc hiển thị dạng bảng** (đẹp hơn):

```java
public void display() {
    System.out.printf("| %-10s | %-20s | %-5s | %-12s | %-30s | %-12s | %-20s |%n",
                     rollNumber, name, 
                     gender ? "Nam" : "Nữ", 
                     dob, email, mobile, address);
}
```

### Method input() - Nhập dữ liệu

Thêm method `input()` vào class `Person`:

```java
package entity;

import java.util.Scanner;

public class Person {
    // ... fields và getters/setters ...
    
    // Method nhập dữ liệu từ bàn phím
    public void input() {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập mã số: ");
        setRollNumber(scanner.nextLine());
        
        System.out.print("Nhập tên: ");
        setName(scanner.nextLine());
        
        System.out.print("Nhập giới tính (true=Nam, false=Nữ): ");
        setGender(Boolean.parseBoolean(scanner.nextLine()));
        
        System.out.print("Nhập ngày sinh (DD/MM/YYYY): ");
        setDob(scanner.nextLine());
        
        System.out.print("Nhập email: ");
        setEmail(scanner.nextLine());
        
        System.out.print("Nhập số điện thoại: ");
        setMobile(scanner.nextLine());
        
        System.out.print("Nhập địa chỉ: ");
        setAddress(scanner.nextLine());
    }
}
```

### Code hoàn chỉnh Person.java

```java
package entity;

import java.util.Scanner;

public class Person {
    // Private fields
    private String rollNumber;
    private String name;
    private boolean gender;
    private String dob;
    private String email;
    private String mobile;
    private String address;
    
    // ... getters và setters ...
    
    // Method nhập dữ liệu
    public void input() {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("\n=== NHẬP THÔNG TIN ===");
        System.out.print("Mã số: ");
        setRollNumber(scanner.nextLine());
        
        System.out.print("Tên: ");
        setName(scanner.nextLine());
        
        System.out.print("Giới tính (true=Nam, false=Nữ): ");
        setGender(Boolean.parseBoolean(scanner.nextLine()));
        
        System.out.print("Ngày sinh (DD/MM/YYYY): ");
        setDob(scanner.nextLine());
        
        System.out.print("Email: ");
        setEmail(scanner.nextLine());
        
        System.out.print("Số điện thoại: ");
        setMobile(scanner.nextLine());
        
        System.out.print("Địa chỉ: ");
        setAddress(scanner.nextLine());
    }
    
    // Method hiển thị thông tin
    public void display() {
        System.out.println("\n=== THÔNG TIN ===");
        System.out.println("Mã số: " + rollNumber);
        System.out.println("Tên: " + name);
        System.out.println("Giới tính: " + (gender ? "Nam" : "Nữ"));
        System.out.println("Ngày sinh: " + dob);
        System.out.println("Email: " + email);
        System.out.println("SĐT: " + mobile);
        System.out.println("Địa chỉ: " + address);
    }
}
```

## III. Override Methods trong Student

### Override display() trong Student

Sửa class `Student` để override method `display()`:

```java
package entity;

import java.util.Scanner;

public class Student extends Person {
    private double mark;
    
    // ... getters và setters ...
    
    // Override method display() từ Person
    @Override
    public void display() {
        super.display();  // Gọi display() của Person trước
        System.out.println("Điểm TB: " + mark);
        System.out.println("Xếp loại: " + getGrade());  // Method riêng của Student
    }
    
    // Override method input() từ Person
    @Override
    public void input() {
        super.input();  // Gọi input() của Person trước
        
        Scanner scanner = new Scanner(System.in);
        System.out.print("Nhập điểm TB: ");
        setMark(Double.parseDouble(scanner.nextLine()));
    }
    
    // Method riêng của Student - Tính xếp loại
    public String getGrade() {
        if (mark >= 9.0) return "Xuất sắc";
        if (mark >= 8.0) return "Giỏi";
        if (mark >= 7.0) return "Khá";
        if (mark >= 5.0) return "Trung bình";
        return "Yếu";
    }
}
```

## IV. Override Methods trong Staff

### Override display() trong Staff

Sửa class `Staff` để override method `display()`:

```java
package entity;

import java.util.Scanner;

public class Staff extends Person {
    private String workMobile;
    private long salary;
    
    // ... getters và setters ...
    
    // Override method display() từ Person
    @Override
    public void display() {
        super.display();  // Gọi display() của Person trước
        System.out.println("SĐT công việc: " + workMobile);
        System.out.println("Lương: " + formatSalary(salary) + " VNĐ");
    }
    
    // Override method input() từ Person
    @Override
    public void input() {
        super.input();  // Gọi input() của Person trước
        
        Scanner scanner = new Scanner(System.in);
        System.out.print("Nhập SĐT công việc: ");
        setWorkMobile(scanner.nextLine());
        
        System.out.print("Nhập lương: ");
        setSalary(Long.parseLong(scanner.nextLine()));
    }
    
    // Method riêng của Staff - Format lương
    private String formatSalary(long salary) {
        return String.format("%,d", salary);  // Format: 15,000,000
    }
}
```

## V. Áp dụng Polymorphism

### Polymorphism với Person Reference

Có thể sử dụng **Polymorphism** - cùng một method, kết quả khác nhau:

```java
package main;

import entity.Person;
import entity.Student;
import entity.Staff;

public class Main {
    // Method nhận Person (có thể là Student hoặc Staff)
    public static void processPerson(Person person) {
        // Polymorphism - Mỗi loại tự biết cách display()
        person.display();  // Runtime: Gọi display() của class thực tế
    }
    
    public static void main(String[] args) {
        // Tạo Student
        Student student = new Student();
        student.setRollNumber("SV001");
        student.setName("Nguyễn Văn A");
        student.setGender(true);
        student.setDob("11/11/2000");
        student.setEmail("nguyenvana@example.com");
        student.setMobile("0912345678");
        student.setAddress("Hà Nội");
        student.setMark(8.5);
        
        // Tạo Staff
        Staff staff = new Staff();
        staff.setRollNumber("NV001");
        staff.setName("Trần Thị B");
        staff.setGender(false);
        staff.setDob("20/05/1995");
        staff.setEmail("tranthib@example.com");
        staff.setMobile("0987654321");
        staff.setAddress("TP. Hồ Chí Minh");
        staff.setWorkMobile("0241234567");
        staff.setSalary(15000000);
        
        // Polymorphism - Cùng một method, kết quả khác nhau
        System.out.println("=== SINH VIÊN ===");
        processPerson(student);  // Gọi display() của Student
        
        System.out.println("\n=== NHÂN VIÊN ===");
        processPerson(staff);    // Gọi display() của Staff
    }
}
```

**Kết quả**:
```
=== SINH VIÊN ===

=== THÔNG TIN ===
Mã số: SV001
Tên: Nguyễn Văn A
Giới tính: Nam
Ngày sinh: 11/11/2000
Email: nguyenvana@example.com
SĐT: 0912345678
Địa chỉ: Hà Nội
Điểm TB: 8.5
Xếp loại: Giỏi

=== NHÂN VIÊN ===

=== THÔNG TIN ===
Mã số: NV001
Tên: Trần Thị B
Giới tính: Nữ
Ngày sinh: 20/05/1995
Email: tranthib@example.com
SĐT: 0987654321
Địa chỉ: TP. Hồ Chí Minh
SĐT công việc: 0241234567
Lương: 15,000,000 VNĐ
```

## VI. Chương trình tương tác với người dùng

### Tạo Menu đơn giản

```java
package main;

import entity.Student;
import entity.Staff;
import java.util.Scanner;

public class Main {
    private static Scanner scanner = new Scanner(System.in);
    
    public static void main(String[] args) {
        boolean running = true;
        
        while (running) {
            showMenu();
            int choice = getChoice();
            
            switch (choice) {
                case 1:
                    createStudent();
                    break;
                case 2:
                    createStaff();
                    break;
                case 3:
                    System.out.println("Tạm biệt!");
                    running = false;
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ!");
            }
        }
        
        scanner.close();
    }
    
    private static void showMenu() {
        System.out.println("\n=== MENU ===");
        System.out.println("1. Tạo sinh viên mới");
        System.out.println("2. Tạo nhân viên mới");
        System.out.println("3. Thoát");
        System.out.print("Chọn: ");
    }
    
    private static int getChoice() {
        try {
            return Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            return -1;
        }
    }
    
    private static void createStudent() {
        System.out.println("\n=== TẠO SINH VIÊN MỚI ===");
        Student student = new Student();
        student.input();  // Polymorphism - Gọi input() của Student
        student.display();  // Polymorphism - Gọi display() của Student
    }
    
    private static void createStaff() {
        System.out.println("\n=== TẠO NHÂN VIÊN MỚI ===");
        Staff staff = new Staff();
        staff.input();  // Polymorphism - Gọi input() của Staff
        staff.display();  // Polymorphism - Gọi display() của Staff
    }
}
```

## VII. Ví dụ nâng cao: Quản lý danh sách

### Quản lý danh sách với ArrayList

```java
package main;

import entity.Person;
import entity.Student;
import entity.Staff;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class ManagementSystem {
    private static List<Person> people = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);
    
    public static void main(String[] args) {
        boolean running = true;
        
        while (running) {
            showMenu();
            int choice = getChoice();
            
            switch (choice) {
                case 1:
                    addStudent();
                    break;
                case 2:
                    addStaff();
                    break;
                case 3:
                    displayAll();
                    break;
                case 4:
                    searchByName();
                    break;
                case 5:
                    running = false;
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ!");
            }
        }
        
        scanner.close();
    }
    
    private static void showMenu() {
        System.out.println("\n=== HỆ THỐNG QUẢN LÝ ===");
        System.out.println("1. Thêm sinh viên");
        System.out.println("2. Thêm nhân viên");
        System.out.println("3. Hiển thị tất cả");
        System.out.println("4. Tìm kiếm theo tên");
        System.out.println("5. Thoát");
        System.out.print("Chọn: ");
    }
    
    private static int getChoice() {
        try {
            return Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            return -1;
        }
    }
    
    private static void addStudent() {
        System.out.println("\n=== THÊM SINH VIÊN ===");
        Student student = new Student();
        student.input();
        people.add(student);
        System.out.println("✅ Đã thêm sinh viên!");
    }
    
    private static void addStaff() {
        System.out.println("\n=== THÊM NHÂN VIÊN ===");
        Staff staff = new Staff();
        staff.input();
        people.add(staff);
        System.out.println("✅ Đã thêm nhân viên!");
    }
    
    private static void displayAll() {
        if (people.isEmpty()) {
            System.out.println("Danh sách rỗng!");
            return;
        }
        
        System.out.println("\n=== DANH SÁCH TẤT CẢ ===");
        for (int i = 0; i < people.size(); i++) {
            System.out.println("\n--- Người thứ " + (i + 1) + " ---");
            // Polymorphism - Mỗi loại tự biết cách display()
            people.get(i).display();
        }
    }
    
    private static void searchByName() {
        System.out.print("\nNhập tên cần tìm: ");
        String searchName = scanner.nextLine().toLowerCase();
        
        boolean found = false;
        for (Person person : people) {
            if (person.getName().toLowerCase().contains(searchName)) {
                person.display();
                found = true;
            }
        }
        
        if (!found) {
            System.out.println("❌ Không tìm thấy!");
        }
    }
}
```

## VIII. Lợi ích của Polymorphism

### 1. Code linh hoạt

```java
// Có thể xử lý nhiều loại đối tượng cùng lúc
List<Person> people = new ArrayList<>();
people.add(new Student());
people.add(new Staff());
people.add(new Student());

// Cùng một method, mỗi loại tự xử lý
for (Person person : people) {
    person.display();  // Polymorphism - Mỗi loại display khác nhau
}
```

### 2. Dễ mở rộng

Thêm class mới (ví dụ: `Teacher`) không cần sửa code cũ:

```java
public class Teacher extends Person {
    private String subject;
    
    @Override
    public void display() {
        super.display();
        System.out.println("Môn dạy: " + subject);
    }
}

// Code cũ vẫn hoạt động!
people.add(new Teacher());  // ✅ OK
```

### 3. Giảm coupling

Code phụ thuộc vào abstraction (Person), không phụ thuộc implementation cụ thể:

```java
// ✅ TỐT: Phụ thuộc vào Person (abstraction)
public void processPerson(Person person) {
    person.display();  // Không cần biết là Student hay Staff
}

// ❌ KHÔNG TỐT: Phụ thuộc vào implementation cụ thể
public void processStudent(Student student) {
    student.display();  // Chỉ xử lý được Student
}
```

## IX. Best Practices

### 1. Luôn dùng @Override annotation

```java
@Override  // ✅ Khuyến nghị - Giúp compiler kiểm tra
public void display() {
    super.display();
    // ...
}
```

### 2. Gọi super.method() khi cần

```java
@Override
public void display() {
    super.display();  // ✅ Gọi method của lớp cha trước
    // Thêm code riêng của lớp con
    System.out.println("Điểm TB: " + mark);
}
```

### 3. Tổ chức code rõ ràng

```java
// ✅ TỐT: Methods được tổ chức rõ ràng
public class Student extends Person {
    // Fields
    private double mark;
    
    // Constructors
    // ...
    
    // Getters/Setters
    // ...
    
    // Override methods
    @Override
    public void display() { }
    
    @Override
    public void input() { }
    
    // Methods riêng
    public String getGrade() { }
}
```

## X. Bài tập thực hành

### Bài tập 1: Hoàn thiện Methods

1. Cải thiện method `display()` với format đẹp hơn (bảng)
2. Thêm validation trong method `input()`
3. Thêm method `update()` để cập nhật thông tin

### Bài tập 2: Tạo Class Teacher

Tạo class `Teacher` kế thừa từ `Person` với:
- Methods: `input()`, `display()` (override)
- Method riêng: `calculateSalary()` (dựa trên số giờ dạy)

### Bài tập 3: Tạo Menu đầy đủ

Tạo menu với các chức năng:
- Thêm sinh viên/nhân viên
- Hiển thị danh sách
- Tìm kiếm
- Sắp xếp
- Xóa

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Thêm methods `input()` và `display()` vào Person
- ✅ Override methods trong Student và Staff
- ✅ Áp dụng Polymorphism (Method Overriding)
- ✅ Sử dụng `super` để gọi method của lớp cha
- ✅ Tạo chương trình tương tác với người dùng
- ✅ Quản lý danh sách với ArrayList và Polymorphism

## Cấu trúc Project hiện tại

```
StudentManagementSystem/
└── src/
    ├── entity/
    │   ├── Person.java    ✅ Có input(), display()
    │   ├── Student.java   ✅ Override input(), display()
    │   └── Staff.java     ✅ Override input(), display()
    └── main/
        └── Main.java      ✅ Menu tương tác
```

## Bước tiếp theo

Ở **Phase 4**, chúng ta sẽ:
- Chuyển Person thành **Abstract Class**
- Tạo **Interfaces** cho các chức năng
- Áp dụng **Abstraction** vào project

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
