# Bài 23: Project - Phase 4: Tạo Menu và Áp dụng Abstraction

> **Mục tiêu**: Tạo menu quản lý đầy đủ, chuyển Person thành Abstract Class, tạo Interfaces cho business logic, và áp dụng Abstraction vào project.

## I. Giới thiệu về Phase 4

### Mục tiêu

Trong Phase 4, chúng ta sẽ:
1. Xác định các chức năng cần có trong hệ thống
2. Tạo menu quản lý đầy đủ
3. Chuyển Person thành **Abstract Class**
4. Tạo **Interfaces** cho business logic
5. Áp dụng **Abstraction** vào project

### Các chức năng cần có

Một hệ thống quản lý thường có các chức năng cơ bản:

| Chức năng | Mô tả |
|-----------|-------|
| **Display** | Hiển thị danh sách |
| **Add** | Thêm đối tượng mới |
| **Update** | Chỉnh sửa thông tin |
| **Delete** | Xóa đối tượng |
| **Search** | Tìm kiếm |
| **Sort** | Sắp xếp |
| **Save** | Lưu dữ liệu vào file |
| **Load** | Đọc dữ liệu từ file |

## II. Chuyển Person thành Abstract Class

### Tại sao cần Abstract Class?

Trong thực tế, chúng ta **không bao giờ** tạo đối tượng `Person` trực tiếp. Chúng ta chỉ tạo `Student` hoặc `Staff`. Vì vậy, `Person` nên là **Abstract Class**.

### Sửa Person thành Abstract

```java
package entity;

import java.util.Scanner;

// ✅ Chuyển thành abstract class
public abstract class Person {
    // Private fields
    private String rollNumber;
    private String name;
    private boolean gender;
    private String dob;
    private String email;
    private String mobile;
    private String address;
    
    // ... getters và setters ...
    
    // Concrete method - Có implementation
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
    
    // Abstract method - Phải override trong lớp con
    public abstract void display();
}
```

**Lợi ích**:
- ✅ Không thể tạo `new Person()` → Bắt buộc tạo Student hoặc Staff
- ✅ Đảm bảo mỗi lớp con phải override `display()`
- ✅ Code rõ ràng hơn về ý định thiết kế

## III. Tạo Menu Quản lý

### Tạo StudentMain.java

Trong package `main`, tạo class `StudentMain.java`:

```java
package main;

import java.util.Scanner;

public class StudentMain {
    private static Scanner scanner = new Scanner(System.in);
    
    public static void main(String[] args) {
        boolean running = true;
        
        do {
            showMenu();
            int choice = getChoice();
            
            switch (choice) {
                case 1:
                    System.out.println("Hiển thị danh sách sinh viên");
                    // Sẽ implement ở Phase 5
                    break;
                case 2:
                    System.out.println("Thêm sinh viên mới");
                    // Sẽ implement ở Phase 5
                    break;
                case 3:
                    System.out.println("Cập nhật sinh viên");
                    // Sẽ implement ở Phase 5
                    break;
                case 4:
                    System.out.println("Xóa sinh viên");
                    // Sẽ implement ở Phase 5
                    break;
                case 5:
                    System.out.println("Tìm kiếm sinh viên");
                    // Sẽ implement ở Phase 5
                    break;
                case 6:
                    System.out.println("Sắp xếp danh sách");
                    // Sẽ implement ở Phase 5
                    break;
                case 7:
                    System.out.println("Lưu dữ liệu");
                    // Sẽ implement ở Phase 6
                    break;
                case 8:
                    System.out.println("Đọc dữ liệu");
                    // Sẽ implement ở Phase 6
                    break;
                case 9:
                    System.out.println("Tạm biệt!");
                    running = false;
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ! Vui lòng chọn 1-9.");
            }
            
            // Dừng màn hình để người dùng xem kết quả
            if (running && choice != 9) {
                System.out.println("\nNhấn Enter để tiếp tục...");
                scanner.nextLine();
            }
            
        } while (running);
        
        scanner.close();
    }
    
    private static void showMenu() {
        System.out.println("\n╔════════════════════════════════════╗");
        System.out.println("║    HỆ THỐNG QUẢN LÝ SINH VIÊN      ║");
        System.out.println("╠════════════════════════════════════╣");
        System.out.println("║  1. Hiển thị danh sách            ║");
        System.out.println("║  2. Thêm sinh viên mới            ║");
        System.out.println("║  3. Cập nhật thông tin             ║");
        System.out.println("║  4. Xóa sinh viên                 ║");
        System.out.println("║  5. Tìm kiếm                      ║");
        System.out.println("║  6. Sắp xếp                        ║");
        System.out.println("║  7. Lưu dữ liệu                   ║");
        System.out.println("║  8. Đọc dữ liệu                   ║");
        System.out.println("║  9. Thoát                          ║");
        System.out.println("╚════════════════════════════════════╝");
        System.out.print("Chọn chức năng (1-9): ");
    }
    
    private static int getChoice() {
        try {
            return Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            return -1;  // Invalid choice
        }
    }
}
```

### Tạo StaffMain.java (Tương tự)

```java
package main;

import java.util.Scanner;

public class StaffMain {
    private static Scanner scanner = new Scanner(System.in);
    
    public static void main(String[] args) {
        boolean running = true;
        
        do {
            showMenu();
            int choice = getChoice();
            
            switch (choice) {
                case 1:
                    System.out.println("Hiển thị danh sách nhân viên");
                    break;
                case 2:
                    System.out.println("Thêm nhân viên mới");
                    break;
                case 3:
                    System.out.println("Cập nhật thông tin");
                    break;
                case 4:
                    System.out.println("Xóa nhân viên");
                    break;
                case 5:
                    System.out.println("Tìm kiếm");
                    break;
                case 6:
                    System.out.println("Sắp xếp");
                    break;
                case 7:
                    System.out.println("Lưu dữ liệu");
                    break;
                case 8:
                    System.out.println("Đọc dữ liệu");
                    break;
                case 9:
                    System.out.println("Tạm biệt!");
                    running = false;
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ!");
            }
            
            if (running && choice != 9) {
                System.out.println("\nNhấn Enter để tiếp tục...");
                scanner.nextLine();
            }
            
        } while (running);
        
        scanner.close();
    }
    
    private static void showMenu() {
        System.out.println("\n╔════════════════════════════════════╗");
        System.out.println("║    HỆ THỐNG QUẢN LÝ NHÂN VIÊN      ║");
        System.out.println("╠════════════════════════════════════╣");
        System.out.println("║  1. Hiển thị danh sách            ║");
        System.out.println("║  2. Thêm nhân viên mới            ║");
        System.out.println("║  3. Cập nhật thông tin           ║");
        System.out.println("║  4. Xóa nhân viên                 ║");
        System.out.println("║  5. Tìm kiếm                      ║");
        System.out.println("║  6. Sắp xếp                        ║");
        System.out.println("║  7. Lưu dữ liệu                  ║");
        System.out.println("║  8. Đọc dữ liệu                  ║");
        System.out.println("║  9. Thoát                         ║");
        System.out.println("╚════════════════════════════════════╝");
        System.out.print("Chọn chức năng (1-9): ");
    }
    
    private static int getChoice() {
        try {
            return Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            return -1;
        }
    }
}
```

## IV. Tạo Interface cho Business Logic

### Interface IManageable

Tạo interface `IManageable` trong package `bo` (business object) để định nghĩa các chức năng quản lý:

```java
package bo;

import java.util.List;

/**
 * Interface định nghĩa các chức năng quản lý chung
 * @param <E> Kiểu đối tượng cần quản lý (Student, Staff, v.v.)
 */
public interface IManageable<E> {
    /**
     * Hiển thị danh sách
     */
    void display();
    
    /**
     * Thêm đối tượng mới
     * @return true nếu thêm thành công
     */
    boolean add();
    
    /**
     * Cập nhật thông tin đối tượng
     * @param rollNumber Mã số của đối tượng cần cập nhật
     * @return true nếu cập nhật thành công
     */
    boolean update(String rollNumber);
    
    /**
     * Xóa đối tượng
     * @param rollNumber Mã số của đối tượng cần xóa
     * @return true nếu xóa thành công
     */
    boolean remove(String rollNumber);
    
    /**
     * Tìm kiếm đối tượng
     * @param text Từ khóa tìm kiếm
     * @return Danh sách các đối tượng tìm thấy
     */
    List<E> search(String text);
    
    /**
     * Sắp xếp danh sách
     */
    void sort();
    
    /**
     * Lưu dữ liệu vào file
     * @param filePath Đường dẫn file
     * @return true nếu lưu thành công
     */
    boolean save(String filePath);
    
    /**
     * Đọc dữ liệu từ file
     * @param filePath Đường dẫn file
     * @return true nếu đọc thành công
     */
    boolean load(String filePath);
}
```

## V. Tạo Business Object Classes

### Tạo Package `bo`

Tạo package `bo` (business object) để chứa các class xử lý business logic.

### Tạo StudentBo.java (Skeleton)

```java
package bo;

import entity.Student;
import java.util.ArrayList;
import java.util.List;

/**
 * Class xử lý business logic cho Student
 */
public class StudentBo implements IManageable<Student> {
    private List<Student> list;
    
    public StudentBo() {
        this.list = new ArrayList<>();
    }
    
    public List<Student> getList() {
        return list;
    }
    
    public void setList(List<Student> list) {
        this.list = list;
    }
    
    // Helper method - Tìm index theo rollNumber
    private int getIndex(String rollNumber) {
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).getRollNumber().equalsIgnoreCase(rollNumber.trim())) {
                return i;
            }
        }
        return -1;  // Không tìm thấy
    }
    
    // ========== IMPLEMENT INTERFACE METHODS ==========
    
    @Override
    public void display() {
        // Sẽ implement ở Phase 5
        System.out.println("Chức năng hiển thị danh sách (sẽ implement ở Phase 5)");
    }
    
    @Override
    public boolean add() {
        // Sẽ implement ở Phase 5
        System.out.println("Chức năng thêm (sẽ implement ở Phase 5)");
        return false;
    }
    
    @Override
    public boolean update(String rollNumber) {
        // Sẽ implement ở Phase 5
        System.out.println("Chức năng cập nhật (sẽ implement ở Phase 5)");
        return false;
    }
    
    @Override
    public boolean remove(String rollNumber) {
        // Sẽ implement ở Phase 5
        System.out.println("Chức năng xóa (sẽ implement ở Phase 5)");
        return false;
    }
    
    @Override
    public List<Student> search(String text) {
        // Sẽ implement ở Phase 5
        System.out.println("Chức năng tìm kiếm (sẽ implement ở Phase 5)");
        return new ArrayList<>();
    }
    
    @Override
    public void sort() {
        // Sẽ implement ở Phase 5
        System.out.println("Chức năng sắp xếp (sẽ implement ở Phase 5)");
    }
    
    @Override
    public boolean save(String filePath) {
        // Sẽ implement ở Phase 6
        System.out.println("Chức năng lưu (sẽ implement ở Phase 6)");
        return false;
    }
    
    @Override
    public boolean load(String filePath) {
        // Sẽ implement ở Phase 6
        System.out.println("Chức năng đọc (sẽ implement ở Phase 6)");
        return false;
    }
}
```

### Tạo StaffBo.java (Tương tự)

```java
package bo;

import entity.Staff;
import java.util.ArrayList;
import java.util.List;

public class StaffBo implements IManageable<Staff> {
    private List<Staff> list;
    
    public StaffBo() {
        this.list = new ArrayList<>();
    }
    
    public List<Staff> getList() {
        return list;
    }
    
    public void setList(List<Staff> list) {
        this.list = list;
    }
    
    private int getIndex(String rollNumber) {
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).getRollNumber().equalsIgnoreCase(rollNumber.trim())) {
                return i;
            }
        }
        return -1;
    }
    
    // Implement tất cả methods từ IManageable<Staff>
    // (Tương tự StudentBo)
    
    @Override
    public void display() {
        System.out.println("Chức năng hiển thị (sẽ implement ở Phase 5)");
    }
    
    // ... các methods khác tương tự ...
}
```

## VI. Kết nối Menu với Business Logic

### Cập nhật StudentMain.java

```java
package main;

import bo.StudentBo;
import java.util.Scanner;

public class StudentMain {
    private static Scanner scanner = new Scanner(System.in);
    private static StudentBo studentBo = new StudentBo();  // Business Object
    
    public static void main(String[] args) {
        boolean running = true;
        
        do {
            showMenu();
            int choice = getChoice();
            
            switch (choice) {
                case 1:
                    studentBo.display();
                    break;
                case 2:
                    if (studentBo.add()) {
                        System.out.println("✅ Đã thêm sinh viên thành công!");
                    } else {
                        System.out.println("❌ Thêm sinh viên thất bại!");
                    }
                    break;
                case 3:
                    System.out.print("Nhập mã số sinh viên cần cập nhật: ");
                    String updateId = scanner.nextLine();
                    if (studentBo.update(updateId)) {
                        System.out.println("✅ Đã cập nhật thành công!");
                    } else {
                        System.out.println("❌ Không tìm thấy sinh viên!");
                    }
                    break;
                case 4:
                    System.out.print("Nhập mã số sinh viên cần xóa: ");
                    String deleteId = scanner.nextLine();
                    if (studentBo.remove(deleteId)) {
                        System.out.println("✅ Đã xóa thành công!");
                    } else {
                        System.out.println("❌ Không tìm thấy sinh viên!");
                    }
                    break;
                case 5:
                    System.out.print("Nhập từ khóa tìm kiếm: ");
                    String searchText = scanner.nextLine();
                    var results = studentBo.search(searchText);
                    if (results.isEmpty()) {
                        System.out.println("❌ Không tìm thấy!");
                    } else {
                        System.out.println("Tìm thấy " + results.size() + " kết quả:");
                        results.forEach(Student::display);
                    }
                    break;
                case 6:
                    studentBo.sort();
                    System.out.println("✅ Đã sắp xếp!");
                    break;
                case 7:
                    System.out.print("Nhập đường dẫn file: ");
                    String savePath = scanner.nextLine();
                    if (studentBo.save(savePath)) {
                        System.out.println("✅ Đã lưu thành công!");
                    } else {
                        System.out.println("❌ Lưu thất bại!");
                    }
                    break;
                case 8:
                    System.out.print("Nhập đường dẫn file: ");
                    String loadPath = scanner.nextLine();
                    if (studentBo.load(loadPath)) {
                        System.out.println("✅ Đã đọc thành công!");
                    } else {
                        System.out.println("❌ Đọc thất bại!");
                    }
                    break;
                case 9:
                    System.out.println("Tạm biệt!");
                    running = false;
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ! Vui lòng chọn 1-9.");
            }
            
            if (running && choice != 9) {
                System.out.println("\nNhấn Enter để tiếp tục...");
                scanner.nextLine();
            }
            
        } while (running);
        
        scanner.close();
    }
    
    private static void showMenu() {
        System.out.println("\n╔════════════════════════════════════╗");
        System.out.println("║    HỆ THỐNG QUẢN LÝ SINH VIÊN      ║");
        System.out.println("╠════════════════════════════════════╣");
        System.out.println("║  1. Hiển thị danh sách            ║");
        System.out.println("║  2. Thêm sinh viên mới            ║");
        System.out.println("║  3. Cập nhật thông tin             ║");
        System.out.println("║  4. Xóa sinh viên                 ║");
        System.out.println("║  5. Tìm kiếm                      ║");
        System.out.println("║  6. Sắp xếp                        ║");
        System.out.println("║  7. Lưu dữ liệu                   ║");
        System.out.println("║  8. Đọc dữ liệu                   ║");
        System.out.println("║  9. Thoát                          ║");
        System.out.println("╚════════════════════════════════════╝");
        System.out.print("Chọn chức năng (1-9): ");
    }
    
    private static int getChoice() {
        try {
            return Integer.parseInt(scanner.nextLine());
        } catch (NumberFormatException e) {
            return -1;
        }
    }
}
```

## VII. Lợi ích của Abstraction trong Project

### 1. Interface định nghĩa Contract

```java
// Interface định nghĩa "CÁI GÌ" cần làm
public interface IManageable<E> {
    void display();
    boolean add();
    // ...
}

// Class implement định nghĩa "LÀM THẾ NÀO"
public class StudentBo implements IManageable<Student> {
    @Override
    public void display() {
        // Implementation cụ thể
    }
}
```

### 2. Dễ mở rộng

Thêm class mới (ví dụ: `TeacherBo`) rất dễ:

```java
public class TeacherBo implements IManageable<Teacher> {
    // Implement tất cả methods từ interface
    // Code tương tự StudentBo
}
```

### 3. Polymorphism với Interface

```java
// Có thể xử lý nhiều loại business objects cùng lúc
public void processManager(IManageable<?> manager) {
    manager.display();  // Polymorphism
    manager.sort();     // Polymorphism
}
```

## VIII. Cấu trúc Project sau Phase 4

```
StudentManagementSystem/
└── src/
    ├── bo/                    ✅ Business Object (mới)
    │   ├── IManageable.java  ✅ Interface
    │   ├── StudentBo.java    ✅ Skeleton
    │   └── StaffBo.java       ✅ Skeleton
    ├── entity/
    │   ├── Person.java       ✅ Abstract Class
    │   ├── Student.java      ✅ Extends Person
    │   └── Staff.java        ✅ Extends Person
    └── main/
        ├── Main.java
        ├── StudentMain.java   ✅ Menu đầy đủ
        └── StaffMain.java    ✅ Menu đầy đủ
```

## IX. Best Practices

### 1. Tổ chức Package Structure

```
src/
├── entity/     # Entities (đối tượng)
├── bo/          # Business Objects (xử lý logic)
├── service/     # Services (có thể thêm sau)
├── util/        # Utilities (có thể thêm sau)
└── main/        # Main classes
```

### 2. Interface cho Contract

```java
// ✅ TỐT: Interface định nghĩa contract rõ ràng
public interface IManageable<E> {
    void display();
    boolean add();
    // ...
}
```

### 3. Abstract Class cho Common Code

```java
// ✅ TỐT: Abstract class chứa code chung
public abstract class Person {
    // Common fields
    // Common methods (input)
    // Abstract methods (display - phải override)
}
```

## X. Bài tập thực hành

### Bài tập 1: Hoàn thiện Menu

1. Thêm validation cho choice (1-9)
2. Thêm confirmation trước khi xóa
3. Cải thiện giao diện menu

### Bài tập 2: Tạo Interface mới

Tạo interface `IExportable` với method `exportToCSV()`:
- StudentBo và StaffBo implement interface này
- Export dữ liệu ra file CSV

### Bài tập 3: Tạo Main Menu

Tạo menu chính cho phép chọn:
- Quản lý Sinh viên
- Quản lý Nhân viên
- Thoát

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Xác định các chức năng cần có trong hệ thống
- ✅ Tạo menu quản lý đầy đủ với switch-case
- ✅ Chuyển Person thành Abstract Class
- ✅ Tạo Interface IManageable cho business logic
- ✅ Tạo Business Object classes (StudentBo, StaffBo)
- ✅ Kết nối menu với business logic
- ✅ Áp dụng Abstraction vào project

## Cấu trúc Project hiện tại

```
StudentManagementSystem/
└── src/
    ├── bo/
    │   ├── IManageable.java  ✅ Interface
    │   ├── StudentBo.java    ✅ Skeleton
    │   └── StaffBo.java      ✅ Skeleton
    ├── entity/
    │   ├── Person.java       ✅ Abstract
    │   ├── Student.java      ✅ Extends Person
    │   └── Staff.java        ✅ Extends Person
    └── main/
        ├── StudentMain.java  ✅ Menu đầy đủ
        └── StaffMain.java    ✅ Menu đầy đủ
```

## Bước tiếp theo

Ở **Phase 5**, chúng ta sẽ:
- Implement đầy đủ các methods trong StudentBo và StaffBo
- Sử dụng ArrayList để quản lý danh sách
- Implement các chức năng: add, update, delete, search, sort

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
