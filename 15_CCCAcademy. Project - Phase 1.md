# Bài 15: Project - Phase 1: Tạo Class và Áp dụng Encapsulation

> **Mục tiêu**: Tạo class đầu tiên trong dự án quản lý sinh viên, áp dụng Encapsulation với private fields và public getters/setters, và hiểu cách tổ chức project structure.

## I. Giới thiệu về Project

### Mục tiêu Project

Trong các bài Project này, chúng ta sẽ xây dựng một **hệ thống quản lý sinh viên** (Student Management System) để áp dụng các kiến thức đã học:

- **Phase 1**: Tạo class Student với Encapsulation
- **Phase 2**: Áp dụng Inheritance (tạo class Person)
- **Phase 3**: Thêm methods (input, display) với Polymorphism
- **Phase 4**: Áp dụng Abstraction (Abstract classes, Interfaces)
- **Phase 5**: Sử dụng Collections (ArrayList)
- **Phase 6**: Lưu trữ dữ liệu vào file (Java IO)

### Project Structure

Chúng ta sẽ tổ chức project theo cấu trúc sau:

```
StudentManagementSystem/
└── src/
    ├── entity/          # Các class đại diện cho đối tượng
    │   ├── Person.java
    │   ├── Student.java
    │   └── Staff.java
    ├── service/         # Các class xử lý business logic (sẽ học sau)
    ├── util/            # Các class tiện ích (sẽ học sau)
    └── main/            # Class chính để chạy chương trình
        └── Main.java
```

## II. Xác định đối tượng và thuộc tính

### Đối tượng: Sinh viên (Student)

Trong hệ thống quản lý sinh viên, đối tượng chính là **Sinh viên (Student)**.

### Thuộc tính của Student

Dựa trên yêu cầu thực tế, một sinh viên cần có các thông tin sau:

| Thuộc tính | Kiểu dữ liệu | Mô tả | Ví dụ |
|------------|--------------|-------|-------|
| **rollNumber** | `String` | Mã số sinh viên | "SV001", "HE150345" |
| **name** | `String` | Họ và tên | "Nguyễn Văn A" |
| **gender** | `boolean` | Giới tính | `true` = Nam, `false` = Nữ |
| **dob** | `String` | Ngày sinh (DD/MM/YYYY) | "11/11/2000" |
| **email** | `String` | Email | "student@example.com" |
| **mobile** | `String` | Số điện thoại | "0912345678" |
| **address** | `String` | Địa chỉ | "Hà Nội" |
| **mark** | `double` | Điểm trung bình | 8.5 |

> **Lưu ý**: Trong thực tế, có thể dùng `LocalDate` cho ngày sinh, nhưng để đơn giản, chúng ta dùng `String` trong giai đoạn đầu.

## III. Tạo Project Structure

### Bước 1: Tạo Project trong IDE

1. Tạo **Java Project** mới trong IDE (Eclipse, IntelliJ IDEA, NetBeans)
2. Đặt tên project: `StudentManagementSystem`

### Bước 2: Tạo Packages

Trong thư mục `src`, tạo các packages:

1. **`entity`** - Chứa các class đại diện cho đối tượng
2. **`main`** - Chứa class Main để chạy chương trình

**Cấu trúc sau bước 2**:
```
StudentManagementSystem/
└── src/
    ├── entity/
    └── main/
```

### Bước 3: Tạo Class Student

Trong package `entity`, tạo class `Student.java`:

```java
package entity;

public class Student {
    // Các thuộc tính sẽ được khai báo ở đây
}
```

## IV. Triển khai Class Student với Encapsulation

### Bước 1: Khai báo các thuộc tính (Private Fields)

Áp dụng **Encapsulation** - tất cả fields đều là **private**:

```java
package entity;

public class Student {
    // Private fields - Encapsulation
    private String rollNumber;
    private String name;
    private boolean gender;  // true = Nam, false = Nữ
    private String dob;      // Date of Birth (DD/MM/YYYY)
    private String email;
    private String mobile;
    private String address;
    private double mark;     // Điểm trung bình
}
```

**Giải thích**:
- ✅ Tất cả fields đều là **private** → Bảo vệ dữ liệu
- ✅ Không thể truy cập trực tiếp từ bên ngoài
- ✅ Phải thông qua getters/setters

### Bước 2: Tạo Getters và Setters

**Getters** - Lấy giá trị (read-only access):
```java
// Getter cho rollNumber
public String getRollNumber() {
    return rollNumber;
}

// Getter cho name
public String getName() {
    return name;
}

// Getter cho gender (boolean dùng is thay vì get)
public boolean isGender() {
    return gender;
}

// Getter cho mark
public double getMark() {
    return mark;
}
```

**Setters** - Đặt giá trị (write access) với validation:
```java
// Setter cho rollNumber với validation
public void setRollNumber(String rollNumber) {
    if (rollNumber != null && !rollNumber.trim().isEmpty()) {
        this.rollNumber = rollNumber.trim();
    } else {
        System.out.println("⚠️ Cảnh báo: Mã số sinh viên không hợp lệ!");
    }
}

// Setter cho name với validation
public void setName(String name) {
    if (name != null && !name.trim().isEmpty()) {
        this.name = name.trim();
    } else {
        System.out.println("⚠️ Cảnh báo: Tên không hợp lệ!");
    }
}

// Setter cho mark với validation
public void setMark(double mark) {
    if (mark >= 0 && mark <= 10) {
        this.mark = mark;
    } else {
        System.out.println("⚠️ Cảnh báo: Điểm phải trong khoảng 0-10!");
    }
}
```

### Code hoàn chỉnh của Student.java

```java
package entity;

public class Student {
    // Private fields - Encapsulation
    private String rollNumber;
    private String name;
    private boolean gender;  // true = Nam, false = Nữ
    private String dob;      // Date of Birth (DD/MM/YYYY)
    private String email;
    private String mobile;
    private String address;
    private double mark;     // Điểm trung bình
    
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
    
    public double getMark() {
        return mark;
    }
    
    // ========== SETTERS ==========
    
    public void setRollNumber(String rollNumber) {
        if (rollNumber != null && !rollNumber.trim().isEmpty()) {
            this.rollNumber = rollNumber.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Mã số sinh viên không hợp lệ!");
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
    
    public void setMark(double mark) {
        if (mark >= 0 && mark <= 10) {
            this.mark = mark;
        } else {
            System.out.println("⚠️ Cảnh báo: Điểm phải trong khoảng 0-10!");
        }
    }
}
```

## V. Tạo Main Class để Test

### Tạo Main.java

Trong package `main`, tạo class `Main.java`:

```java
package main;

import entity.Student;

public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng Student
        Student student = new Student();
        
        // Sử dụng setters để đặt giá trị
        student.setRollNumber("SV001");
        student.setName("Nguyễn Văn A");
        student.setGender(true);  // Nam
        student.setDob("11/11/2000");
        student.setEmail("nguyenvana@example.com");
        student.setMobile("0912345678");
        student.setAddress("Hà Nội");
        student.setMark(8.5);
        
        // Sử dụng getters để lấy giá trị
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Mã SV: " + student.getRollNumber());
        System.out.println("Tên: " + student.getName());
        System.out.println("Giới tính: " + (student.isGender() ? "Nam" : "Nữ"));
        System.out.println("Ngày sinh: " + student.getDob());
        System.out.println("Email: " + student.getEmail());
        System.out.println("SĐT: " + student.getMobile());
        System.out.println("Địa chỉ: " + student.getAddress());
        System.out.println("Điểm TB: " + student.getMark());
        
        // Test validation
        System.out.println("\n=== TEST VALIDATION ===");
        student.setMark(15.0);  // Điểm không hợp lệ → Cảnh báo
        student.setName("");    // Tên rỗng → Cảnh báo
    }
}
```

**Kết quả**:
```
=== THÔNG TIN SINH VIÊN ===
Mã SV: SV001
Tên: Nguyễn Văn A
Giới tính: Nam
Ngày sinh: 11/11/2000
Email: nguyenvana@example.com
SĐT: 0912345678
Địa chỉ: Hà Nội
Điểm TB: 8.5

=== TEST VALIDATION ===
⚠️ Cảnh báo: Điểm phải trong khoảng 0-10!
⚠️ Cảnh báo: Tên không hợp lệ!
```

## VI. Lợi ích của Encapsulation trong Project

### 1. Bảo vệ dữ liệu

```java
Student student = new Student();

// ❌ KHÔNG THỂ: Truy cập trực tiếp
// student.mark = -5;  // Lỗi! mark là private

// ✅ PHẢI: Thông qua setter (có validation)
student.setMark(-5);  // Cảnh báo: Điểm không hợp lệ → Không được set
```

### 2. Validation tự động

Mọi lần set giá trị đều được kiểm tra:

```java
student.setMark(8.5);   // ✅ OK
student.setMark(15.0);  // ⚠️ Cảnh báo - Không được set
student.setMark(-1);    // ⚠️ Cảnh báo - Không được set
```

### 3. Dễ thay đổi implementation

Nếu muốn thay đổi cách lưu trữ (ví dụ: mark thành Integer), chỉ cần sửa trong class:

```java
// Trước: private double mark;
// Sau: private int mark;  // Chỉ cần sửa trong class, không ảnh hưởng code bên ngoài
```

## VII. Best Practices

### 1. Naming Convention

- **Fields**: camelCase, private
- **Getters**: `getFieldName()` hoặc `isFieldName()` (cho boolean)
- **Setters**: `setFieldName()`

```java
private String rollNumber;
public String getRollNumber() { return rollNumber; }
public void setRollNumber(String rollNumber) { this.rollNumber = rollNumber; }

private boolean gender;
public boolean isGender() { return gender; }  // boolean dùng is
public void setGender(boolean gender) { this.gender = gender; }
```

### 2. Validation trong Setters

Luôn validate dữ liệu trong setters:

```java
public void setMark(double mark) {
    if (mark >= 0 && mark <= 10) {
        this.mark = mark;
    } else {
        // Có thể throw exception hoặc chỉ cảnh báo
        System.out.println("⚠️ Điểm không hợp lệ!");
        // Hoặc: throw new IllegalArgumentException("Điểm phải trong khoảng 0-10");
    }
}
```

### 3. Trim() cho String

Luôn trim() để loại bỏ khoảng trắng thừa:

```java
public void setName(String name) {
    if (name != null && !name.trim().isEmpty()) {
        this.name = name.trim();  // Loại bỏ khoảng trắng đầu/cuối
    }
}
```

## VIII. Bài tập thực hành

### Bài tập 1: Hoàn thiện Class Student

1. Thêm validation cho email (kiểm tra có chứa @)
2. Thêm validation cho mobile (kiểm tra 10 số, bắt đầu bằng 0)
3. Thêm validation cho dob (kiểm tra format DD/MM/YYYY)

### Bài tập 2: Tạo Class Product

Tạo class `Product` trong package `entity` với:
- Fields: id, name, price, quantity, category
- Tất cả fields là private
- Getters và Setters với validation
- Test trong Main class

### Bài tập 3: Tạo Class BankAccount

Tạo class `BankAccount` với:
- Fields: accountNumber, ownerName, balance
- Validation: balance >= 0, accountNumber không rỗng
- Methods: deposit(), withdraw() (sẽ học ở bài sau)

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu cách tổ chức project structure
- ✅ Tạo class Student với Encapsulation
- ✅ Sử dụng private fields và public getters/setters
- ✅ Thêm validation trong setters
- ✅ Test class trong Main
- ✅ Áp dụng best practices

## Cấu trúc Project hiện tại

```
StudentManagementSystem/
└── src/
    ├── entity/
    │   └── Student.java    ✅ Đã tạo
    └── main/
        └── Main.java       ✅ Đã tạo
```

## Bước tiếp theo

Ở **Phase 2**, chúng ta sẽ:
- Tạo class `Person` (lớp cha)
- Áp dụng **Inheritance** để `Student` kế thừa từ `Person`
- Tạo class `Staff` cũng kế thừa từ `Person`

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
