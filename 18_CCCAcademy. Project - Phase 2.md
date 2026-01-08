# Bài 18: Project - Phase 2: Áp dụng Inheritance

> **Mục tiêu**: Tạo class Person (lớp cha) và áp dụng Inheritance để Student và Staff kế thừa từ Person, giảm code trùng lặp và tổ chức code tốt hơn.

## I. Vấn đề: Code trùng lặp

### Yêu cầu mới

Dự án yêu cầu quản lý thêm đối tượng **Nhân viên (Staff)** với các thuộc tính:

| Thuộc tính | Kiểu dữ liệu | Mô tả |
|------------|--------------|-------|
| **rollNumber** | `String` | Mã số nhân viên |
| **name** | `String` | Họ và tên |
| **gender** | `boolean` | Giới tính |
| **dob** | `String` | Ngày sinh |
| **email** | `String` | Email |
| **mobile** | `String` | Số điện thoại |
| **workMobile** | `String` | Số điện thoại công việc |
| **address** | `String` | Địa chỉ |
| **salary** | `long` | Lương |

### Phát hiện vấn đề

So sánh thuộc tính của **Student** và **Staff**:

| Thuộc tính | Student | Staff |
|------------|---------|-------|
| rollNumber | ✅ | ✅ |
| name | ✅ | ✅ |
| gender | ✅ | ✅ |
| dob | ✅ | ✅ |
| email | ✅ | ✅ |
| mobile | ✅ | ✅ |
| address | ✅ | ✅ |
| **mark** | ✅ | ❌ |
| **workMobile** | ❌ | ✅ |
| **salary** | ❌ | ✅ |

**Nhận xét**:
- ⚠️ **7 thuộc tính trùng lặp** giữa Student và Staff
- ⚠️ Nếu tạo class Staff riêng → **Code trùng lặp rất nhiều**
- ⚠️ Khó bảo trì: Sửa một chỗ phải sửa nhiều nơi

### Giải pháp: Inheritance (Kế thừa)

Tạo class **Person** (lớp cha) chứa các thuộc tính **chung**, sau đó:
- `Student` kế thừa từ `Person` + thêm `mark`
- `Staff` kế thừa từ `Person` + thêm `workMobile`, `salary`

## II. Triển khai Inheritance

### Bước 1: Tạo Class Person (Superclass)

Trong package `entity`, tạo class `Person.java`:

```java
package entity;

public class Person {
    // Các thuộc tính CHUNG của Student và Staff
    private String rollNumber;
    private String name;
    private boolean gender;  // true = Nam, false = Nữ
    private String dob;      // Date of Birth (DD/MM/YYYY)
    private String email;
    private String mobile;
    private String address;
    
    // ========== GETTERS ==========
    
    public String getRollNumber() {
        return rollNumber;
    }
    
    public String getName() {
        return name;
    }
    
    public boolean isGender() {
        return gender;
    }
    
    public String getDob() {
        return dob;
    }
    
    public String getEmail() {
        return email;
    }
    
    public String getMobile() {
        return mobile;
    }
    
    public String getAddress() {
        return address;
    }
    
    // ========== SETTERS ==========
    
    public void setRollNumber(String rollNumber) {
        if (rollNumber != null && !rollNumber.trim().isEmpty()) {
            this.rollNumber = rollNumber.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Mã số không hợp lệ!");
        }
    }
    
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Tên không hợp lệ!");
        }
    }
    
    public void setGender(boolean gender) {
        this.gender = gender;
    }
    
    public void setDob(String dob) {
        if (dob != null && !dob.trim().isEmpty()) {
            this.dob = dob.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Ngày sinh không hợp lệ!");
        }
    }
    
    public void setEmail(String email) {
        if (email != null && !email.trim().isEmpty()) {
            this.email = email.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Email không hợp lệ!");
        }
    }
    
    public void setMobile(String mobile) {
        if (mobile != null && !mobile.trim().isEmpty()) {
            this.mobile = mobile.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Số điện thoại không hợp lệ!");
        }
    }
    
    public void setAddress(String address) {
        if (address != null) {
            this.address = address.trim();
        }
    }
}
```

### Bước 2: Sửa Class Student để kế thừa từ Person

Sửa `Student.java` để kế thừa từ `Person`:

```java
package entity;

public class Student extends Person {  // ✅ Kế thừa từ Person
    // Chỉ còn thuộc tính RIÊNG của Student
    private double mark;  // Điểm trung bình
    
    // ========== GETTER ==========
    
    public double getMark() {
        return mark;
    }
    
    // ========== SETTER ==========
    
    public void setMark(double mark) {
        if (mark >= 0 && mark <= 10) {
            this.mark = mark;
        } else {
            System.out.println("⚠️ Cảnh báo: Điểm phải trong khoảng 0-10!");
        }
    }
}
```

**Lợi ích**:
- ✅ **Giảm code**: Từ ~150 dòng xuống ~20 dòng
- ✅ **Kế thừa**: Tự động có tất cả fields và methods từ Person
- ✅ **Dễ bảo trì**: Sửa Person → Tự động áp dụng cho Student

### Bước 3: Tạo Class Staff kế thừa từ Person

Tạo `Staff.java` trong package `entity`:

```java
package entity;

public class Staff extends Person {  // ✅ Kế thừa từ Person
    // Chỉ còn thuộc tính RIÊNG của Staff
    private String workMobile;  // Số điện thoại công việc
    private long salary;        // Lương
    
    // ========== GETTERS ==========
    
    public String getWorkMobile() {
        return workMobile;
    }
    
    public long getSalary() {
        return salary;
    }
    
    // ========== SETTERS ==========
    
    public void setWorkMobile(String workMobile) {
        if (workMobile != null && !workMobile.trim().isEmpty()) {
            this.workMobile = workMobile.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Số điện thoại công việc không hợp lệ!");
        }
    }
    
    public void setSalary(long salary) {
        if (salary >= 0) {
            this.salary = salary;
        } else {
            System.out.println("⚠️ Cảnh báo: Lương phải >= 0!");
        }
    }
}
```

## III. Cấu trúc Project sau Phase 2

```
StudentManagementSystem/
└── src/
    ├── entity/
    │   ├── Person.java    ✅ Lớp cha (superclass)
    │   ├── Student.java   ✅ Kế thừa Person
    │   └── Staff.java     ✅ Kế thừa Person
    └── main/
        └── Main.java
```

### Sơ đồ Inheritance

```
        Person (Superclass)
        ├── rollNumber
        ├── name
        ├── gender
        ├── dob
        ├── email
        ├── mobile
        └── address
            │
            ├── Student (Subclass)
            │   └── mark
            │
            └── Staff (Subclass)
                ├── workMobile
                └── salary
```

## IV. Test Inheritance

### Test trong Main.java

```java
package main;

import entity.Person;
import entity.Student;
import entity.Staff;

public class Main {
    public static void main(String[] args) {
        System.out.println("=== TEST STUDENT (Kế thừa Person) ===\n");
        
        // Tạo Student
        Student student = new Student();
        
        // Sử dụng methods từ Person (kế thừa)
        student.setRollNumber("SV001");
        student.setName("Nguyễn Văn A");
        student.setGender(true);
        student.setDob("11/11/2000");
        student.setEmail("nguyenvana@example.com");
        student.setMobile("0912345678");
        student.setAddress("Hà Nội");
        
        // Sử dụng method riêng của Student
        student.setMark(8.5);
        
        // Hiển thị thông tin
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Mã SV: " + student.getRollNumber());  // Từ Person
        System.out.println("Tên: " + student.getName());          // Từ Person
        System.out.println("Giới tính: " + (student.isGender() ? "Nam" : "Nữ"));  // Từ Person
        System.out.println("Ngày sinh: " + student.getDob());      // Từ Person
        System.out.println("Email: " + student.getEmail());        // Từ Person
        System.out.println("SĐT: " + student.getMobile());        // Từ Person
        System.out.println("Địa chỉ: " + student.getAddress());    // Từ Person
        System.out.println("Điểm TB: " + student.getMark());      // Từ Student
        
        System.out.println("\n=== TEST STAFF (Kế thừa Person) ===\n");
        
        // Tạo Staff
        Staff staff = new Staff();
        
        // Sử dụng methods từ Person (kế thừa)
        staff.setRollNumber("NV001");
        staff.setName("Trần Thị B");
        staff.setGender(false);
        staff.setDob("20/05/1995");
        staff.setEmail("tranthib@example.com");
        staff.setMobile("0987654321");
        staff.setAddress("TP. Hồ Chí Minh");
        
        // Sử dụng methods riêng của Staff
        staff.setWorkMobile("0241234567");
        staff.setSalary(15000000);
        
        // Hiển thị thông tin
        System.out.println("=== THÔNG TIN NHÂN VIÊN ===");
        System.out.println("Mã NV: " + staff.getRollNumber());      // Từ Person
        System.out.println("Tên: " + staff.getName());                // Từ Person
        System.out.println("Giới tính: " + (staff.isGender() ? "Nam" : "Nữ"));  // Từ Person
        System.out.println("Ngày sinh: " + staff.getDob());            // Từ Person
        System.out.println("Email: " + staff.getEmail());              // Từ Person
        System.out.println("SĐT: " + staff.getMobile());               // Từ Person
        System.out.println("SĐT công việc: " + staff.getWorkMobile()); // Từ Staff
        System.out.println("Địa chỉ: " + staff.getAddress());          // Từ Person
        System.out.println("Lương: " + staff.getSalary() + " VNĐ");   // Từ Staff
    }
}
```

**Kết quả**:
```
=== TEST STUDENT (Kế thừa Person) ===

=== THÔNG TIN SINH VIÊN ===
Mã SV: SV001
Tên: Nguyễn Văn A
Giới tính: Nam
Ngày sinh: 11/11/2000
Email: nguyenvana@example.com
SĐT: 0912345678
Địa chỉ: Hà Nội
Điểm TB: 8.5

=== TEST STAFF (Kế thừa Person) ===

=== THÔNG TIN NHÂN VIÊN ===
Mã NV: NV001
Tên: Trần Thị B
Giới tính: Nữ
Ngày sinh: 20/05/1995
Email: tranthib@example.com
SĐT: 0987654321
SĐT công việc: 0241234567
Địa chỉ: TP. Hồ Chí Minh
Lương: 15000000 VNĐ
```

## V. Lợi ích của Inheritance trong Project

### 1. Giảm code trùng lặp

**Trước Inheritance**:
- Student: ~150 dòng
- Staff: ~150 dòng
- **Tổng: ~300 dòng**

**Sau Inheritance**:
- Person: ~120 dòng
- Student: ~20 dòng
- Staff: ~30 dòng
- **Tổng: ~170 dòng** (giảm ~43%)

### 2. Dễ bảo trì

Khi cần thay đổi logic chung (ví dụ: validation email), chỉ cần sửa ở **Person**:

```java
// Sửa validation email trong Person
public void setEmail(String email) {
    if (email != null && email.contains("@") && email.contains(".")) {
        this.email = email.trim();
    } else {
        System.out.println("⚠️ Email không hợp lệ!");
    }
}

// ✅ Tự động áp dụng cho Student và Staff (không cần sửa gì)
```

### 3. Dễ mở rộng

Thêm class mới (ví dụ: `Teacher`) rất dễ:

```java
public class Teacher extends Person {
    private String subject;  // Môn học
    private int yearsOfExperience;  // Số năm kinh nghiệm
    
    // Chỉ cần thêm thuộc tính riêng
    // Tự động có tất cả từ Person
}
```

## VI. Sử dụng từ khóa `super`

### `super` để truy cập members của lớp cha

```java
public class Student extends Person {
    private double mark;
    
    // Method sử dụng super để truy cập method của Person
    public void displayFullInfo() {
        // Gọi method từ Person (nếu có)
        // super.someMethod();
        
        // Hoặc truy cập field (nếu protected)
        // System.out.println("Mã: " + super.rollNumber);  // Nếu protected
    }
}
```

> **Lưu ý**: Vì các fields trong Person là `private`, không thể truy cập trực tiếp bằng `super.rollNumber`. Phải dùng getters/setters.

## VII. Ví dụ: Polymorphism với Person

Có thể sử dụng **Polymorphism** (sẽ học chi tiết ở Phase 3):

```java
public class Main {
    public static void displayPersonInfo(Person person) {
        // Polymorphism - Có thể nhận Student hoặc Staff
        System.out.println("Mã: " + person.getRollNumber());
        System.out.println("Tên: " + person.getName());
        System.out.println("Email: " + person.getEmail());
    }
    
    public static void main(String[] args) {
        Student student = new Student();
        student.setRollNumber("SV001");
        student.setName("Nguyễn Văn A");
        student.setEmail("student@example.com");
        
        Staff staff = new Staff();
        staff.setRollNumber("NV001");
        staff.setName("Trần Thị B");
        staff.setEmail("staff@example.com");
        
        // Cùng một method, nhận cả Student và Staff
        displayPersonInfo(student);  // ✅ OK
        displayPersonInfo(staff);    // ✅ OK
    }
}
```

## VIII. Best Practices

### 1. Đặt tên lớp cha phù hợp

```java
// ✅ TỐT: Tên có ý nghĩa, phù hợp với quan hệ
public class Person { }  // Person → Student, Staff (hợp lý)

// ❌ KHÔNG TỐT: Tên không phù hợp
public class Car { }     // Car → Student (không hợp lý về mặt ngữ nghĩa)
```

### 2. Chỉ đưa thuộc tính chung vào lớp cha

```java
// ✅ TỐT: Chỉ thuộc tính chung
public class Person {
    private String name;  // Cả Student và Staff đều có
    private String email; // Cả Student và Staff đều có
}

// ❌ KHÔNG TỐT: Đưa thuộc tính riêng vào
public class Person {
    private double mark;  // ❌ Chỉ Student có, Staff không có
}
```

### 3. Sử dụng protected khi cần

Nếu lớp con cần truy cập trực tiếp (hiếm khi cần):

```java
public class Person {
    protected String name;  // Lớp con có thể truy cập trực tiếp
    // ...
}

public class Student extends Person {
    public void someMethod() {
        this.name = "New Name";  // ✅ OK nếu name là protected
    }
}
```

> **Lưu ý**: Thường nên dùng `private` + getters/setters thay vì `protected`.

## IX. Bài tập thực hành

### Bài tập 1: Hoàn thiện Class Staff

1. Thêm validation cho workMobile (10 số, bắt đầu bằng 0)
2. Thêm validation cho salary (>= 0)
3. Test trong Main class

### Bài tập 2: Tạo Class Teacher

Tạo class `Teacher` kế thừa từ `Person` với:
- Thuộc tính riêng: subject, yearsOfExperience
- Getters và Setters với validation
- Test trong Main class

### Bài tập 3: Tạo Class Manager

Tạo class `Manager` kế thừa từ `Staff` với:
- Thuộc tính riêng: department, bonus
- Kế thừa từ Staff (có salary, workMobile)
- Kế thừa từ Person (có name, email, v.v.)

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu vấn đề code trùng lặp và cách giải quyết
- ✅ Tạo class Person (superclass) chứa thuộc tính chung
- ✅ Áp dụng Inheritance: Student và Staff kế thừa Person
- ✅ Giảm code trùng lặp đáng kể
- ✅ Tổ chức code tốt hơn với inheritance hierarchy
- ✅ Test inheritance trong Main class

## Cấu trúc Project hiện tại

```
StudentManagementSystem/
└── src/
    ├── entity/
    │   ├── Person.java    ✅ Lớp cha
    │   ├── Student.java   ✅ Kế thừa Person
    │   └── Staff.java     ✅ Kế thừa Person
    └── main/
        └── Main.java
```

## Bước tiếp theo

Ở **Phase 3**, chúng ta sẽ:
- Thêm methods `input()` và `display()` vào Person
- Override methods trong Student và Staff
- Áp dụng **Polymorphism** (Method Overriding)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
