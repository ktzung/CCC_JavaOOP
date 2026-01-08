# Bài 14: Tính đóng gói (Encapsulation)

> **Mục tiêu**: Hiểu được tính đóng gói trong Java, cách sử dụng access modifiers, và tại sao cần sử dụng getter/setter để bảo vệ dữ liệu.

## I. Giới thiệu về tính đóng gói

### Tính đóng gói là gì?

**Tính đóng gói (Encapsulation)** là một trong bốn tính chất cơ bản của lập trình hướng đối tượng (OOP). Đây là kỹ thuật **bọc gói** (wrapping) code và dữ liệu lại với nhau thành một đơn vị duy nhất để:

- **Bảo vệ dữ liệu** khỏi việc truy cập và sửa đổi không hợp lệ từ bên ngoài
- **Ẩn giấu chi tiết triển khai** - người dùng chỉ cần biết cách sử dụng, không cần biết cách hoạt động bên trong
- **Kiểm soát truy cập** - chỉ cho phép truy cập dữ liệu thông qua các phương thức được định nghĩa sẵn

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **chiếc xe ô tô**:

- **Dữ liệu bên trong** (engine, fuel level, speed) = Các trường (fields) của lớp
- **Bảng điều khiển** (pedal, steering wheel, buttons) = Các phương thức public (getter/setter)
- **Hộp máy động cơ** (engine compartment) = Được bảo vệ bằng `private`

Bạn **không thể** mở trực tiếp vào hộp máy để sửa động cơ (truy cập trực tiếp fields), nhưng bạn **có thể** sử dụng bàn đạp ga (method) để tăng tốc. Điều này đảm bảo:
- An toàn: Bạn không thể làm hỏng động cơ bằng cách thay đổi trực tiếp
- Dễ sử dụng: Chỉ cần biết cách sử dụng bàn đạp
- Bảo mật: Chi tiết hoạt động của động cơ được ẩn giấu

## II. Access Modifiers (Bổ từ truy cập)

Để hiểu về tính đóng gói, trước tiên chúng ta cần hiểu về **Access Modifiers** - các từ khóa xác định **phạm vi truy cập** của các thành phần trong Java.

### Các loại Access Modifiers

Java có **4 mức độ truy cập**:

| Access Modifier | Mô tả | Ví dụ |
|----------------|--------|-------|
| `public` | Có thể truy cập từ bất kỳ đâu | `public String name;` |
| `protected` | Có thể truy cập trong cùng package hoặc lớp con | `protected int age;` |
| `default` (package-private) | Có thể truy cập trong cùng package | `String address;` (không có modifier) |
| `private` | Chỉ có thể truy cập trong cùng lớp | `private double salary;` |

### Bảng chi tiết phạm vi truy cập

| Vị trí truy cập | `public` | `protected` | `default` | `private` |
|----------------|:--------:|:-----------:|:---------:|:---------:|
| **Cùng lớp** (Same class) | ✅ | ✅ | ✅ | ✅ |
| **Cùng package, lớp con** (Same package subclass) | ✅ | ✅ | ✅ | ❌ |
| **Cùng package, không phải lớp con** (Same package non-subclass) | ✅ | ✅ | ✅ | ❌ |
| **Khác package, lớp con** (Different package subclass) | ✅ | ✅ | ❌ | ❌ |
| **Khác package, không phải lớp con** (Different package non-subclass) | ✅ | ❌ | ❌ | ❌ |

### Ví dụ minh họa

```java
package com.cccacademy.student;

public class Student {
    // public - ai cũng có thể truy cập
    public String name;
    
    // protected - chỉ lớp con hoặc cùng package
    protected int age;
    
    // default - chỉ cùng package
    String address;
    
    // private - chỉ trong lớp này
    private double gpa; // Điểm trung bình
    
    // Constructor
    public Student(String name, int age, String address, double gpa) {
        this.name = name;
        this.age = age;
        this.address = address;
        this.gpa = gpa;
    }
}
```

```java
// Trong cùng package
package com.cccacademy.student;

public class Test {
    public static void main(String[] args) {
        Student s = new Student("Nguyễn Văn A", 20, "Hà Nội", 8.5);
        
        s.name = "Nguyễn Văn B";        // ✅ OK - public
        s.age = 21;                      // ✅ OK - protected, cùng package
        s.address = "TP.HCM";           // ✅ OK - default, cùng package
        // s.gpa = 9.0;                 // ❌ LỖI! - private, không thể truy cập
    }
}
```

```java
// Ở package khác
package com.cccacademy.other;

import com.cccacademy.student.Student;

public class TestOther {
    public static void main(String[] args) {
        Student s = new Student("Nguyễn Văn A", 20, "Hà Nội", 8.5);
        
        s.name = "Nguyễn Văn B";        // ✅ OK - public
        // s.age = 21;                  // ❌ LỖI! - protected, khác package
        // s.address = "TP.HCM";        // ❌ LỖI! - default, khác package
        // s.gpa = 9.0;                 // ❌ LỖI! - private, không thể truy cập
    }
}
```

> **Lưu ý**: `protected` sẽ được giải thích chi tiết hơn trong bài Kế thừa (Inheritance).

## III. Tính đóng gói trong thực tế

### Vấn đề khi không sử dụng đóng gói

Xem ví dụ sau về một lớp `BankAccount` **không** sử dụng đóng gói:

```java
public class BankAccount {
    // ❌ Tất cả đều public - ai cũng có thể truy cập và sửa đổi
    public String accountNumber;
    public double balance;
    public String ownerName;
    
    public BankAccount(String accountNumber, double balance, String ownerName) {
        this.accountNumber = accountNumber;
        this.balance = balance;
        this.ownerName = ownerName;
    }
}

// Vấn đề: Bất kỳ ai cũng có thể thay đổi số dư tài khoản!
public class Test {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("ACC001", 1000.0, "Nguyễn Văn A");
        
        // ❌ Nguy hiểm! Bất kỳ ai cũng có thể tự ý thay đổi số dư
        account.balance = 1000000.0; // Thêm tiền "từ không đâu"
        account.balance = -500.0;    // Số dư âm - không hợp lệ!
        
        System.out.println("Số dư: " + account.balance); // -500.0 (SAI!)
    }
}
```

**Vấn đề**:
- ❌ Không kiểm soát được việc thay đổi dữ liệu
- ❌ Có thể gán giá trị không hợp lệ (số dư âm, v.v.)
- ❌ Không thể theo dõi lịch sử giao dịch
- ❌ Dễ gây lỗi và khó debug

### Giải pháp: Sử dụng tính đóng gói

Cùng một lớp nhưng **có** sử dụng đóng gói:

```java
public class BankAccount {
    // ✅ Private - không thể truy cập trực tiếp từ bên ngoài
    private String accountNumber;
    private double balance;
    private String ownerName;
    
    // Constructor
    public BankAccount(String accountNumber, double balance, String ownerName) {
        this.accountNumber = accountNumber;
        // ✅ Kiểm tra số dư ban đầu hợp lệ
        if (balance >= 0) {
            this.balance = balance;
        } else {
            this.balance = 0;
            System.out.println("Cảnh báo: Số dư ban đầu không hợp lệ, đặt về 0");
        }
        this.ownerName = ownerName;
    }
    
    // ✅ Getter - Lấy giá trị
    public String getAccountNumber() {
        return accountNumber;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public String getOwnerName() {
        return ownerName;
    }
    
    // ✅ Setter - Thay đổi giá trị với kiểm tra
    public void setOwnerName(String ownerName) {
        if (ownerName != null && !ownerName.trim().isEmpty()) {
            this.ownerName = ownerName;
        } else {
            System.out.println("Lỗi: Tên chủ tài khoản không hợp lệ");
        }
    }
    
    // ✅ Không có setter cho balance - không cho phép thay đổi trực tiếp
    // Thay vào đó, sử dụng các phương thức rút/nạp tiền
    
    // Phương thức nạp tiền
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Đã nạp " + amount + ". Số dư hiện tại: " + balance);
        } else {
            System.out.println("Lỗi: Số tiền nạp phải lớn hơn 0");
        }
    }
    
    // Phương thức rút tiền
    public void withdraw(double amount) {
        if (amount > 0) {
            if (balance >= amount) {
                balance -= amount;
                System.out.println("Đã rút " + amount + ". Số dư hiện tại: " + balance);
            } else {
                System.out.println("Lỗi: Số dư không đủ. Số dư hiện tại: " + balance);
            }
        } else {
            System.out.println("Lỗi: Số tiền rút phải lớn hơn 0");
        }
    }
    
    // Hiển thị thông tin
    public void displayInfo() {
        System.out.println("=== THÔNG TIN TÀI KHOẢN ===");
        System.out.println("Số tài khoản: " + accountNumber);
        System.out.println("Chủ tài khoản: " + ownerName);
        System.out.println("Số dư: " + balance);
    }
}

// Sử dụng
public class Test {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("ACC001", 1000.0, "Nguyễn Văn A");
        
        // ✅ Chỉ có thể xem số dư
        System.out.println("Số dư: " + account.getBalance()); // 1000.0
        
        // ✅ Không thể thay đổi trực tiếp
        // account.balance = 1000000.0; // ❌ LỖI! - balance là private
        
        // ✅ Phải sử dụng phương thức được cung cấp
        account.deposit(500.0);   // Nạp tiền hợp lệ
        account.withdraw(200.0);  // Rút tiền hợp lệ
        account.withdraw(2000.0); // Rút tiền không hợp lệ - bị từ chối
        
        account.displayInfo();
    }
}
```

**Kết quả**:
```
Đã nạp 500.0. Số dư hiện tại: 1500.0
Đã rút 200.0. Số dư hiện tại: 1300.0
Lỗi: Số dư không đủ. Số dư hiện tại: 1300.0
=== THÔNG TIN TÀI KHOẢN ===
Số tài khoản: ACC001
Chủ tài khoản: Nguyễn Văn A
Số dư: 1300.0
```

**Lợi ích**:
- ✅ Kiểm soát hoàn toàn việc thay đổi dữ liệu
- ✅ Đảm bảo dữ liệu luôn hợp lệ
- ✅ Dễ bảo trì và mở rộng (có thể thêm log, kiểm tra, v.v.)
- ✅ Ẩn giấu chi tiết triển khai

## IV. Getter và Setter

### Getter là gì?

**Getter** (phương thức get) là phương thức **lấy giá trị** của một trường private.

**Quy tắc đặt tên**: `get` + tên trường (viết hoa chữ đầu)

```java
public class Student {
    private String name;
    private int age;
    
    // Getter cho name
    public String getName() {
        return name;
    }
    
    // Getter cho age
    public int getAge() {
        return age;
    }
}
```

### Setter là gì?

**Setter** (phương thức set) là phương thức **gán giá trị** cho một trường private.

**Quy tắc đặt tên**: `set` + tên trường (viết hoa chữ đầu)

```java
public class Student {
    private String name;
    private int age;
    
    // Setter cho name - có kiểm tra
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name;
        } else {
            System.out.println("Lỗi: Tên không hợp lệ");
        }
    }
    
    // Setter cho age - có kiểm tra
    public void setAge(int age) {
        if (age >= 0 && age <= 150) { // Kiểm tra tuổi hợp lệ
            this.age = age;
        } else {
            System.out.println("Lỗi: Tuổi phải từ 0 đến 150");
        }
    }
}
```

### Ví dụ hoàn chỉnh với Getter/Setter

```java
public class Car {
    // ✅ Private fields - được bảo vệ
    private String licensePlate;
    private double price;
    private double horsepower;
    
    // Constructor
    public Car(String licensePlate, double price, double horsepower) {
        setLicensePlate(licensePlate); // Gọi setter để kiểm tra
        setPrice(price);
        setHorsepower(horsepower);
    }
    
    // ✅ Getter methods
    public String getLicensePlate() {
        return licensePlate;
    }
    
    public double getPrice() {
        return price;
    }
    
    public double getHorsepower() {
        return horsepower;
    }
    
    // ✅ Setter methods với kiểm tra
    public void setLicensePlate(String licensePlate) {
        if (licensePlate != null && licensePlate.length() == 7) {
            // Kiểm tra định dạng: 2 chữ cái, 4 số, 2 chữ cái
            if (licensePlate.matches("[A-Z]{2}\\d{4}[A-Z]{2}")) {
                this.licensePlate = licensePlate;
            } else {
                System.out.println("Lỗi: Biển số không đúng định dạng");
            }
        } else {
            System.out.println("Lỗi: Biển số phải có 7 ký tự");
        }
    }
    
    public void setPrice(double price) {
        if (price > 0) {
            this.price = price;
        } else {
            System.out.println("Lỗi: Giá phải lớn hơn 0");
        }
    }
    
    public void setHorsepower(double horsepower) {
        if (horsepower > 0) {
            this.horsepower = horsepower;
        } else {
            System.out.println("Lỗi: Mã lực phải lớn hơn 0");
        }
    }
    
    // Phương thức hiển thị thông tin
    public void displayInfo() {
        System.out.println("=== THÔNG TIN XE ===");
        System.out.println("Biển số: " + licensePlate);
        System.out.println("Giá: " + price);
        System.out.println("Mã lực: " + horsepower);
    }
}

// Sử dụng
public class Test {
    public static void main(String[] args) {
        Car car = new Car("AB1234CD", 500000000, 150);
        
        // ✅ Sử dụng getter để lấy giá trị
        System.out.println("Giá xe: " + car.getPrice());
        
        // ✅ Sử dụng setter để thay đổi giá trị (có kiểm tra)
        car.setPrice(600000000); // Hợp lệ
        car.setPrice(-1000);     // Không hợp lệ - bị từ chối
        
        car.displayInfo();
    }
}
```

### Lợi ích của Getter/Setter

1. **Kiểm soát truy cập**: Kiểm tra dữ liệu trước khi gán
2. **Tính linh hoạt**: Có thể thay đổi cách lưu trữ dữ liệu mà không ảnh hưởng đến người dùng
3. **Tính bảo mật**: Ẩn giấu chi tiết triển khai
4. **Dễ debug**: Có thể thêm log, kiểm tra tại một nơi

## V. Các đặc điểm của tính đóng gói

### 1. Bảo vệ dữ liệu

Dữ liệu private không thể truy cập trực tiếp từ bên ngoài:

```java
public class Person {
    private int age; // Private - được bảo vệ
    
    // Chỉ có thể thay đổi qua setter
    public void setAge(int age) {
        if (age >= 0 && age <= 150) {
            this.age = age;
        }
    }
}
```

### 2. Kiểm soát truy cập

Ngăn chặn việc gán giá trị không hợp lệ:

```java
public class Student {
    private double gpa; // Điểm trung bình (0-10)
    
    public void setGpa(double gpa) {
        // Kiểm tra giá trị hợp lệ
        if (gpa >= 0 && gpa <= 10) {
            this.gpa = gpa;
        } else {
            System.out.println("Lỗi: Điểm phải từ 0 đến 10");
        }
    }
}
```

### 3. Ẩn giấu chi tiết triển khai

Người dùng không cần biết dữ liệu được lưu trữ như thế nào:

```java
public class Account {
    // Chi tiết triển khai - người dùng không cần biết
    private double balanceInVND; // Lưu bằng VNĐ
    
    // Giao diện công khai - người dùng chỉ cần biết cách sử dụng
    public void depositUSD(double usdAmount) {
        double vndAmount = usdAmount * 24000; // Tỷ giá
        balanceInVND += vndAmount;
    }
    
    public double getBalanceInUSD() {
        return balanceInVND / 24000;
    }
}
```

### 4. Dễ bảo trì

Thay đổi cách triển khai mà không ảnh hưởng đến người dùng:

```java
public class Student {
    // Trước đây: Lưu tên đầy đủ trong 1 field
    // private String fullName;
    
    // Sau này: Tách thành firstName và lastName
    private String firstName;
    private String lastName;
    
    // Nhưng getter/setter vẫn giữ nguyên - người dùng không bị ảnh hưởng
    public String getFullName() {
        return firstName + " " + lastName;
    }
    
    public void setFullName(String fullName) {
        String[] parts = fullName.split(" ");
        this.firstName = parts[0];
        this.lastName = parts.length > 1 ? parts[1] : "";
    }
}
```

## VI. Lợi ích của tính đóng gói

### 1. Bảo mật dữ liệu

- Dữ liệu không thể bị thay đổi bất hợp pháp
- Chỉ có thể truy cập thông qua các phương thức được kiểm soát

### 2. Dễ bảo trì và mở rộng

- Có thể thay đổi cách triển khai mà không ảnh hưởng đến code khác
- Dễ thêm các tính năng mới (log, validation, v.v.)

### 3. Code rõ ràng và dễ hiểu

- Người dùng chỉ cần biết cách sử dụng, không cần hiểu chi tiết
- Giảm độ phức tạp của code

### 4. Tái sử dụng

- Có thể sử dụng lại code ở nhiều nơi
- Dễ test và debug

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu tính đóng gói là gì và tại sao nó quan trọng
- ✅ Nắm được 4 mức độ access modifiers: public, protected, default, private
- ✅ Biết cách sử dụng getter và setter
- ✅ Hiểu lợi ích của tính đóng gói trong lập trình

## Bài tập thực hành

1. **Tạo lớp `Product` (Sản phẩm) với tính đóng gói**:
   - Fields: `name`, `price`, `quantity` (private)
   - Getter/Setter cho tất cả fields
   - Kiểm tra: price > 0, quantity >= 0
   - Phương thức `displayInfo()` để hiển thị thông tin

2. **Tạo lớp `Employee` (Nhân viên)**:
   - Fields: `id`, `name`, `salary` (private)
   - Getter/Setter
   - Kiểm tra: salary > 0
   - Phương thức `calculateAnnualSalary()` tính lương năm

3. **Tạo lớp `Rectangle` (Hình chữ nhật)**:
   - Fields: `width`, `height` (private)
   - Getter/Setter với kiểm tra > 0
   - Phương thức `calculateArea()` và `calculatePerimeter()`

## Tài liệu tham khảo

- [Oracle Java Tutorial - Encapsulation](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html)
- [Java Access Modifiers](https://www.javatpoint.com/access-modifiers-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
