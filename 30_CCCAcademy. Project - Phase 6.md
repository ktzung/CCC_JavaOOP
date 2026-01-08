# Bài 30: Project - Phase 6: Lưu trữ dữ liệu với Java IO

> **Mục tiêu**: Implement methods `save()` và `load()` sử dụng Java IO, lưu và đọc dữ liệu từ file, hoàn thiện hệ thống quản lý.

## I. Giới thiệu về Phase 6

### Mục tiêu

Trong Phase 6, chúng ta sẽ:
1. Implement methods `save()` và `load()` trong StudentBo và StaffBo
2. Sử dụng **Java IO** để lưu và đọc dữ liệu
3. Lưu dữ liệu vào file text
4. Đọc dữ liệu từ file text
5. **Hoàn thiện** hệ thống quản lý

### Tại sao cần lưu trữ dữ liệu?

- ✅ **Dữ liệu tồn tại lâu dài**: Không mất khi tắt chương trình
- ✅ **Chia sẻ dữ liệu**: Có thể mở lại sau
- ✅ **Backup**: Có thể sao lưu dữ liệu

## II. Implement save() Method

### Lưu danh sách Student vào file

Cập nhật method `save()` trong `StudentBo.java`:

```java
@Override
public boolean save(String filePath) {
    if (filePath == null || filePath.trim().isEmpty()) {
        System.out.println("⚠️ Đường dẫn file không hợp lệ!");
        return false;
    }
    
    try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
        // Ghi header
        writer.write("=== DANH SÁCH SINH VIÊN ===");
        writer.newLine();
        writer.write(String.format("%-10s | %-20s | %-5s | %-12s | %-30s | %-12s | %-20s | %-10s",
                                   "Mã SV", "Tên", "Giới tính", "Ngày sinh", "Email", "SĐT", "Địa chỉ", "Điểm TB"));
        writer.newLine();
        writer.write("--------------------------------------------------------------------------------------------------------");
        writer.newLine();
        
        // Ghi từng sinh viên
        for (Student student : list) {
            writer.write(String.format("%s|%s|%s|%s|%s|%s|%s|%.2f",
                student.getRollNumber(),
                student.getName(),
                student.isGender() ? "Nam" : "Nữ",
                student.getDob(),
                student.getEmail(),
                student.getMobile(),
                student.getAddress(),
                student.getMark()));
            writer.newLine();
        }
        
        System.out.println("✅ Đã lưu " + list.size() + " sinh viên vào file: " + filePath);
        return true;
        
    } catch (IOException e) {
        System.out.println("❌ Lỗi khi lưu file: " + e.getMessage());
        return false;
    }
}
```

### Format đơn giản hơn (CSV-like)

```java
@Override
public boolean save(String filePath) {
    if (filePath == null || filePath.trim().isEmpty()) {
        System.out.println("⚠️ Đường dẫn file không hợp lệ!");
        return false;
    }
    
    try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
        // Ghi số lượng sinh viên
        writer.write(String.valueOf(list.size()));
        writer.newLine();
        
        // Ghi từng sinh viên (mỗi dòng một sinh viên)
        for (Student student : list) {
            // Format: rollNumber|name|gender|dob|email|mobile|address|mark
            writer.write(String.format("%s|%s|%s|%s|%s|%s|%s|%.2f",
                student.getRollNumber(),
                student.getName(),
                student.isGender(),
                student.getDob(),
                student.getEmail(),
                student.getMobile(),
                student.getAddress(),
                student.getMark()));
            writer.newLine();
        }
        
        System.out.println("✅ Đã lưu " + list.size() + " sinh viên vào file: " + filePath);
        return true;
        
    } catch (IOException e) {
        System.out.println("❌ Lỗi khi lưu file: " + e.getMessage());
        e.printStackTrace();
        return false;
    }
}
```

## III. Implement load() Method

### Đọc danh sách Student từ file

Cập nhật method `load()` trong `StudentBo.java`:

```java
@Override
public boolean load(String filePath) {
    if (filePath == null || filePath.trim().isEmpty()) {
        System.out.println("⚠️ Đường dẫn file không hợp lệ!");
        return false;
    }
    
    File file = new File(filePath);
    if (!file.exists()) {
        System.out.println("❌ File không tồn tại: " + filePath);
        return false;
    }
    
    try (BufferedReader reader = new BufferedReader(new FileReader(file))) {
        // Xóa danh sách cũ (nếu muốn)
        // list.clear();  // Hoặc hỏi người dùng
        
        // Đọc số lượng
        String countStr = reader.readLine();
        if (countStr == null) {
            System.out.println("⚠️ File rỗng!");
            return false;
        }
        
        int count = Integer.parseInt(countStr.trim());
        
        // Đọc từng sinh viên
        for (int i = 0; i < count; i++) {
            String line = reader.readLine();
            if (line == null) {
                break;
            }
            
            // Parse dữ liệu: rollNumber|name|gender|dob|email|mobile|address|mark
            String[] parts = line.split("\\|");
            if (parts.length >= 8) {
                Student student = new Student();
                student.setRollNumber(parts[0]);
                student.setName(parts[1]);
                student.setGender(Boolean.parseBoolean(parts[2]));
                student.setDob(parts[3]);
                student.setEmail(parts[4]);
                student.setMobile(parts[5]);
                student.setAddress(parts[6]);
                student.setMark(Double.parseDouble(parts[7]));
                
                list.add(student);
            }
        }
        
        System.out.println("✅ Đã đọc " + list.size() + " sinh viên từ file: " + filePath);
        return true;
        
    } catch (IOException e) {
        System.out.println("❌ Lỗi khi đọc file: " + e.getMessage());
        e.printStackTrace();
        return false;
    } catch (NumberFormatException e) {
        System.out.println("❌ Lỗi định dạng dữ liệu trong file!");
        return false;
    }
}
```

## IV. Code hoàn chỉnh StudentBo với IO

### StudentBo.java (với save/load)

```java
package bo;

import entity.Student;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Scanner;
import java.util.stream.Collectors;

public class StudentBo implements IManageable<Student> {
    private List<Student> list;
    private Scanner scanner;
    
    public StudentBo() {
        this.list = new ArrayList<>();
        this.scanner = new Scanner(System.in);
    }
    
    // ... các methods khác (display, add, update, remove, search, sort) ...
    
    @Override
    public boolean save(String filePath) {
        if (filePath == null || filePath.trim().isEmpty()) {
            System.out.println("⚠️ Đường dẫn file không hợp lệ!");
            return false;
        }
        
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            // Ghi số lượng
            writer.write(String.valueOf(list.size()));
            writer.newLine();
            
            // Ghi từng sinh viên
            for (Student student : list) {
                writer.write(String.format("%s|%s|%s|%s|%s|%s|%s|%.2f",
                    student.getRollNumber(),
                    student.getName(),
                    student.isGender(),
                    student.getDob(),
                    student.getEmail(),
                    student.getMobile(),
                    student.getAddress(),
                    student.getMark()));
                writer.newLine();
            }
            
            System.out.println("✅ Đã lưu " + list.size() + " sinh viên vào file: " + filePath);
            return true;
            
        } catch (IOException e) {
            System.out.println("❌ Lỗi khi lưu file: " + e.getMessage());
            return false;
        }
    }
    
    @Override
    public boolean load(String filePath) {
        if (filePath == null || filePath.trim().isEmpty()) {
            System.out.println("⚠️ Đường dẫn file không hợp lệ!");
            return false;
        }
        
        File file = new File(filePath);
        if (!file.exists()) {
            System.out.println("❌ File không tồn tại: " + filePath);
            return false;
        }
        
        try (BufferedReader reader = new BufferedReader(new FileReader(file))) {
            // Hỏi người dùng: Xóa danh sách cũ hay thêm vào?
            if (!list.isEmpty()) {
                System.out.print("Danh sách hiện tại có " + list.size() + " sinh viên. ");
                System.out.print("Bạn muốn (1) Thêm vào danh sách hiện tại, (2) Thay thế danh sách: ");
                String choice = scanner.nextLine().trim();
                if ("2".equals(choice)) {
                    list.clear();
                }
            }
            
            // Đọc số lượng
            String countStr = reader.readLine();
            if (countStr == null) {
                System.out.println("⚠️ File rỗng!");
                return false;
            }
            
            int count = Integer.parseInt(countStr.trim());
            int loaded = 0;
            
            // Đọc từng sinh viên
            for (int i = 0; i < count; i++) {
                String line = reader.readLine();
                if (line == null) {
                    break;
                }
                
                String[] parts = line.split("\\|");
                if (parts.length >= 8) {
                    Student student = new Student();
                    student.setRollNumber(parts[0]);
                    student.setName(parts[1]);
                    student.setGender(Boolean.parseBoolean(parts[2]));
                    student.setDob(parts[3]);
                    student.setEmail(parts[4]);
                    student.setMobile(parts[5]);
                    student.setAddress(parts[6]);
                    student.setMark(Double.parseDouble(parts[7]));
                    
                    list.add(student);
                    loaded++;
                }
            }
            
            System.out.println("✅ Đã đọc " + loaded + " sinh viên từ file: " + filePath);
            return true;
            
        } catch (IOException e) {
            System.out.println("❌ Lỗi khi đọc file: " + e.getMessage());
            return false;
        } catch (NumberFormatException e) {
            System.out.println("❌ Lỗi định dạng dữ liệu trong file!");
            return false;
        }
    }
}
```

## V. Implement tương tự cho StaffBo

### StaffBo.java (với save/load)

```java
// Tương tự StudentBo, nhưng format khác một chút (có workMobile và salary)

@Override
public boolean save(String filePath) {
    if (filePath == null || filePath.trim().isEmpty()) {
        System.out.println("⚠️ Đường dẫn file không hợp lệ!");
        return false;
    }
    
    try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
        writer.write(String.valueOf(list.size()));
        writer.newLine();
        
        for (Staff staff : list) {
            // Format: rollNumber|name|gender|dob|email|mobile|workMobile|address|salary
            writer.write(String.format("%s|%s|%s|%s|%s|%s|%s|%s|%d",
                staff.getRollNumber(),
                staff.getName(),
                staff.isGender(),
                staff.getDob(),
                staff.getEmail(),
                staff.getMobile(),
                staff.getWorkMobile(),
                staff.getAddress(),
                staff.getSalary()));
            writer.newLine();
        }
        
        System.out.println("✅ Đã lưu " + list.size() + " nhân viên vào file: " + filePath);
        return true;
        
    } catch (IOException e) {
        System.out.println("❌ Lỗi khi lưu file: " + e.getMessage());
        return false;
    }
}

@Override
public boolean load(String filePath) {
    // Tương tự StudentBo, nhưng parse 9 phần tử thay vì 8
    // (thêm workMobile và salary)
}
```

## VI. Cải thiện Menu với Default Path

### Cập nhật StudentMain.java

```java
private static final String DEFAULT_FILE_PATH = "students.txt";

private static void handleSave() {
    System.out.print("Nhập đường dẫn file (Enter để dùng mặc định: " + DEFAULT_FILE_PATH + "): ");
    String filePath = scanner.nextLine().trim();
    
    if (filePath.isEmpty()) {
        filePath = DEFAULT_FILE_PATH;
    }
    
    if (studentBo.save(filePath)) {
        System.out.println("✅ Đã lưu thành công!");
    } else {
        System.out.println("❌ Lưu thất bại!");
    }
}

private static void handleLoad() {
    System.out.print("Nhập đường dẫn file (Enter để dùng mặc định: " + DEFAULT_FILE_PATH + "): ");
    String filePath = scanner.nextLine().trim();
    
    if (filePath.isEmpty()) {
        filePath = DEFAULT_FILE_PATH;
    }
    
    if (studentBo.load(filePath)) {
        System.out.println("✅ Đã đọc thành công!");
    } else {
        System.out.println("❌ Đọc thất bại!");
    }
}
```

## VII. Ví dụ sử dụng hệ thống hoàn chỉnh

### Demo Flow

```
=== HỆ THỐNG QUẢN LÝ SINH VIÊN ===
1. Hiển thị danh sách
2. Thêm sinh viên mới
3. Cập nhật thông tin
4. Xóa sinh viên
5. Tìm kiếm
6. Sắp xếp
7. Lưu dữ liệu
8. Đọc dữ liệu
9. Thoát
Chọn chức năng (1-9): 2

=== THÊM SINH VIÊN MỚI ===
Nhập mã số sinh viên: SV001
...
✅ Đã thêm sinh viên thành công!

Chọn chức năng (1-9): 7
Nhập đường dẫn file: students.txt
✅ Đã lưu 1 sinh viên vào file: students.txt

Chọn chức năng (1-9): 8
Nhập đường dẫn file: students.txt
✅ Đã đọc 1 sinh viên từ file: students.txt
```

## VIII. Best Practices cho File I/O

### 1. Luôn dùng try-with-resources

```java
// ✅ TỐT: Tự động đóng
try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
    // Code
}

// ❌ KHÔNG TỐT: Phải đóng thủ công
BufferedWriter writer = new BufferedWriter(new FileWriter(filePath));
// ... code ...
writer.close();  // Có thể quên!
```

### 2. Kiểm tra file tồn tại trước khi đọc

```java
File file = new File(filePath);
if (!file.exists()) {
    System.out.println("❌ File không tồn tại!");
    return false;
}
```

### 3. Xử lý lỗi đầy đủ

```java
try {
    // Code đọc/ghi file
} catch (IOException e) {
    System.out.println("❌ Lỗi I/O: " + e.getMessage());
    e.printStackTrace();  // In stack trace để debug
} catch (NumberFormatException e) {
    System.out.println("❌ Lỗi định dạng dữ liệu!");
}
```

## IX. Cấu trúc Project hoàn chỉnh

```
StudentManagementSystem/
└── src/
    ├── bo/
    │   ├── IManageable.java  ✅ Interface
    │   ├── StudentBo.java     ✅ Implement đầy đủ (có save/load)
    │   └── StaffBo.java       ✅ Implement đầy đủ (có save/load)
    ├── entity/
    │   ├── Person.java        ✅ Abstract Class
    │   ├── Student.java       ✅ Extends Person
    │   └── Staff.java         ✅ Extends Person
    └── main/
        ├── StudentMain.java   ✅ Menu + Logic + IO
        └── StaffMain.java      ✅ Menu + Logic + IO
```

## X. Tính năng nâng cao (Optional)

### 1. Auto-save

Tự động lưu sau mỗi thao tác:

```java
private void autoSave() {
    studentBo.save("students_autosave.txt");
}
```

### 2. Backup

Tạo backup trước khi load:

```java
private void backup() {
    String backupPath = "students_backup_" + System.currentTimeMillis() + ".txt";
    studentBo.save(backupPath);
}
```

### 3. Export CSV

Export ra định dạng CSV để mở bằng Excel:

```java
public boolean exportToCSV(String filePath) {
    try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
        // Header CSV
        writer.write("Mã SV,Tên,Giới tính,Ngày sinh,Email,SĐT,Địa chỉ,Điểm TB");
        writer.newLine();
        
        // Data
        for (Student student : list) {
            writer.write(String.format("%s,%s,%s,%s,%s,%s,%s,%.2f",
                student.getRollNumber(),
                student.getName(),
                student.isGender() ? "Nam" : "Nữ",
                student.getDob(),
                student.getEmail(),
                student.getMobile(),
                student.getAddress(),
                student.getMark()));
            writer.newLine();
        }
        
        return true;
    } catch (IOException e) {
        return false;
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Implement methods `save()` và `load()` với Java IO
- ✅ Lưu danh sách vào file text
- ✅ Đọc danh sách từ file text
- ✅ Xử lý lỗi đầy đủ
- ✅ **Hoàn thiện** hệ thống quản lý sinh viên/nhân viên

## Hệ thống hoàn chỉnh

Bây giờ bạn đã có một **hệ thống quản lý hoàn chỉnh** với:

- ✅ **Encapsulation**: Private fields, public getters/setters
- ✅ **Inheritance**: Person → Student, Staff
- ✅ **Polymorphism**: Method Overriding
- ✅ **Abstraction**: Abstract Class, Interfaces
- ✅ **Collections**: ArrayList để quản lý danh sách
- ✅ **I/O**: Lưu và đọc dữ liệu từ file

## Bài tập mở rộng

1. **Thêm tính năng**:
   - Thống kê (số lượng, điểm trung bình, lương trung bình)
   - Export ra Excel (CSV)
   - Import từ Excel (CSV)

2. **Cải thiện**:
   - Validation đầy đủ hơn
   - Giao diện đẹp hơn
   - Xử lý lỗi tốt hơn

3. **Mở rộng**:
   - Thêm class Teacher
   - Thêm class Manager
   - Quản lý nhiều loại đối tượng cùng lúc

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
