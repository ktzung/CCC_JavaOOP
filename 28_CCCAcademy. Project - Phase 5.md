# Bài 28: Project - Phase 5: Implement Business Logic với ArrayList

> **Mục tiêu**: Implement đầy đủ các methods trong StudentBo và StaffBo, sử dụng ArrayList để quản lý danh sách, và hoàn thiện các chức năng CRUD.

## I. Giới thiệu về Phase 5

### Mục tiêu

Trong Phase 5, chúng ta sẽ:
1. Implement đầy đủ các methods trong `StudentBo` và `StaffBo`
2. Sử dụng **ArrayList** để lưu trữ danh sách
3. Implement các chức năng: **Add, Update, Delete, Search, Sort, Display**
4. Kết nối menu với business logic hoàn chỉnh

### Các chức năng cần implement

| Method | Mô tả | Return Type |
|--------|-------|-------------|
| `display()` | Hiển thị tất cả đối tượng trong danh sách | `void` |
| `add()` | Thêm đối tượng mới vào danh sách | `boolean` |
| `update(rollNumber)` | Cập nhật thông tin đối tượng | `boolean` |
| `remove(rollNumber)` | Xóa đối tượng khỏi danh sách | `boolean` |
| `search(text)` | Tìm kiếm đối tượng theo từ khóa | `List<E>` |
| `sort()` | Sắp xếp danh sách | `void` |

## II. Implement StudentBo đầy đủ

### Code hoàn chỉnh StudentBo.java

```java
package bo;

import entity.Student;
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
        if (list.isEmpty()) {
            System.out.println("⚠️ Danh sách rỗng!");
            return;
        }
        
        System.out.println("\n╔════════════════════════════════════════════════════════════════════════════════════╗");
        System.out.println("║                          DANH SÁCH SINH VIÊN                                      ║");
        System.out.println("╠════════════════════════════════════════════════════════════════════════════════════╣");
        System.out.printf("║ %-10s │ %-20s │ %-5s │ %-12s │ %-12s │ %-10s ║%n",
                         "Mã SV", "Tên", "Giới tính", "Ngày sinh", "SĐT", "Điểm TB");
        System.out.println("╠════════════════════════════════════════════════════════════════════════════════════╣");
        
        for (Student student : list) {
            System.out.printf("║ %-10s │ %-20s │ %-5s │ %-12s │ %-12s │ %-10.2f ║%n",
                student.getRollNumber(),
                student.getName(),
                student.isGender() ? "Nam" : "Nữ",
                student.getDob(),
                student.getMobile(),
                student.getMark());
        }
        
        System.out.println("╚════════════════════════════════════════════════════════════════════════════════════╝");
        System.out.println("Tổng số: " + list.size() + " sinh viên");
    }
    
    @Override
    public boolean add() {
        System.out.println("\n=== THÊM SINH VIÊN MỚI ===");
        Student student = new Student();
        
        // Kiểm tra mã số đã tồn tại chưa
        System.out.print("Nhập mã số sinh viên: ");
        String rollNumber = scanner.nextLine().trim();
        
        if (getIndex(rollNumber) >= 0) {
            System.out.println("❌ Mã số sinh viên đã tồn tại!");
            return false;
        }
        
        student.setRollNumber(rollNumber);
        student.input();  // Nhập các thông tin còn lại
        
        // Thêm vào danh sách
        return list.add(student);
    }
    
    @Override
    public boolean update(String rollNumber) {
        int index = getIndex(rollNumber);
        if (index < 0) {
            System.out.println("❌ Không tìm thấy sinh viên với mã số: " + rollNumber);
            return false;
        }
        
        Student student = list.get(index);
        System.out.println("\n=== CẬP NHẬT THÔNG TIN SINH VIÊN ===");
        System.out.println("Thông tin hiện tại:");
        student.display();
        
        System.out.println("\nNhập thông tin mới (Enter để giữ nguyên):");
        
        System.out.print("Tên mới: ");
        String name = scanner.nextLine().trim();
        if (!name.isEmpty()) {
            student.setName(name);
        }
        
        System.out.print("Giới tính mới (true=Nam, false=Nữ): ");
        String genderStr = scanner.nextLine().trim();
        if (!genderStr.isEmpty()) {
            student.setGender(Boolean.parseBoolean(genderStr));
        }
        
        System.out.print("Ngày sinh mới: ");
        String dob = scanner.nextLine().trim();
        if (!dob.isEmpty()) {
            student.setDob(dob);
        }
        
        System.out.print("Email mới: ");
        String email = scanner.nextLine().trim();
        if (!email.isEmpty()) {
            student.setEmail(email);
        }
        
        System.out.print("SĐT mới: ");
        String mobile = scanner.nextLine().trim();
        if (!mobile.isEmpty()) {
            student.setMobile(mobile);
        }
        
        System.out.print("Địa chỉ mới: ");
        String address = scanner.nextLine().trim();
        if (!address.isEmpty()) {
            student.setAddress(address);
        }
        
        System.out.print("Điểm TB mới: ");
        String markStr = scanner.nextLine().trim();
        if (!markStr.isEmpty()) {
            try {
                student.setMark(Double.parseDouble(markStr));
            } catch (NumberFormatException e) {
                System.out.println("⚠️ Điểm không hợp lệ!");
            }
        }
        
        return true;
    }
    
    @Override
    public boolean remove(String rollNumber) {
        int index = getIndex(rollNumber);
        if (index < 0) {
            System.out.println("❌ Không tìm thấy sinh viên với mã số: " + rollNumber);
            return false;
        }
        
        Student student = list.get(index);
        System.out.println("\nThông tin sinh viên sẽ bị xóa:");
        student.display();
        
        System.out.print("\nBạn có chắc chắn muốn xóa? (yes/no): ");
        String confirm = scanner.nextLine().trim().toLowerCase();
        
        if ("yes".equals(confirm) || "y".equals(confirm)) {
            Student removed = list.remove(index);
            System.out.println("✅ Đã xóa sinh viên: " + removed.getName());
            return true;
        } else {
            System.out.println("❌ Đã hủy xóa!");
            return false;
        }
    }
    
    @Override
    public List<Student> search(String text) {
        if (text == null || text.trim().isEmpty()) {
            return new ArrayList<>();
        }
        
        String searchText = text.toLowerCase().trim();
        return list.stream()
                   .filter(student -> 
                       student.getRollNumber().toLowerCase().contains(searchText) ||
                       student.getName().toLowerCase().contains(searchText) ||
                       student.getEmail().toLowerCase().contains(searchText) ||
                       student.getMobile().contains(searchText))
                   .collect(Collectors.toList());
    }
    
    @Override
    public void sort() {
        if (list.isEmpty()) {
            System.out.println("⚠️ Danh sách rỗng, không thể sắp xếp!");
            return;
        }
        
        System.out.println("\n=== SẮP XẾP DANH SÁCH ===");
        System.out.println("1. Theo mã số (tăng dần)");
        System.out.println("2. Theo tên (A-Z)");
        System.out.println("3. Theo điểm TB (giảm dần)");
        System.out.println("4. Theo điểm TB (tăng dần)");
        System.out.print("Chọn tiêu chí sắp xếp (1-4): ");
        
        try {
            int choice = Integer.parseInt(scanner.nextLine());
            
            switch (choice) {
                case 1:
                    list.sort(Comparator.comparing(Student::getRollNumber));
                    System.out.println("✅ Đã sắp xếp theo mã số (tăng dần)");
                    break;
                case 2:
                    list.sort(Comparator.comparing(Student::getName));
                    System.out.println("✅ Đã sắp xếp theo tên (A-Z)");
                    break;
                case 3:
                    list.sort(Comparator.comparingDouble(Student::getMark).reversed());
                    System.out.println("✅ Đã sắp xếp theo điểm TB (giảm dần)");
                    break;
                case 4:
                    list.sort(Comparator.comparingDouble(Student::getMark));
                    System.out.println("✅ Đã sắp xếp theo điểm TB (tăng dần)");
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ!");
            }
        } catch (NumberFormatException e) {
            System.out.println("⚠️ Lựa chọn không hợp lệ!");
        }
    }
    
    @Override
    public boolean save(String filePath) {
        // Sẽ implement ở Phase 6
        System.out.println("Chức năng lưu sẽ được implement ở Phase 6");
        return false;
    }
    
    @Override
    public boolean load(String filePath) {
        // Sẽ implement ở Phase 6
        System.out.println("Chức năng đọc sẽ được implement ở Phase 6");
        return false;
    }
}
```

## III. Implement StaffBo đầy đủ

### Code hoàn chỉnh StaffBo.java

```java
package bo;

import entity.Staff;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Scanner;
import java.util.stream.Collectors;

public class StaffBo implements IManageable<Staff> {
    private List<Staff> list;
    private Scanner scanner;
    
    public StaffBo() {
        this.list = new ArrayList<>();
        this.scanner = new Scanner(System.in);
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
    
    @Override
    public void display() {
        if (list.isEmpty()) {
            System.out.println("⚠️ Danh sách rỗng!");
            return;
        }
        
        System.out.println("\n╔══════════════════════════════════════════════════════════════════════════════════════════╗");
        System.out.println("║                              DANH SÁCH NHÂN VIÊN                                        ║");
        System.out.println("╠══════════════════════════════════════════════════════════════════════════════════════════╣");
        System.out.printf("║ %-10s │ %-20s │ %-5s │ %-12s │ %-12s │ %-15s ║%n",
                         "Mã NV", "Tên", "Giới tính", "Ngày sinh", "SĐT", "Lương");
        System.out.println("╠══════════════════════════════════════════════════════════════════════════════════════════╣");
        
        for (Staff staff : list) {
            System.out.printf("║ %-10s │ %-20s │ %-5s │ %-12s │ %-12s │ %-15s ║%n",
                staff.getRollNumber(),
                staff.getName(),
                staff.isGender() ? "Nam" : "Nữ",
                staff.getDob(),
                staff.getMobile(),
                String.format("%,d VNĐ", staff.getSalary()));
        }
        
        System.out.println("╚══════════════════════════════════════════════════════════════════════════════════════════╝");
        System.out.println("Tổng số: " + list.size() + " nhân viên");
    }
    
    @Override
    public boolean add() {
        System.out.println("\n=== THÊM NHÂN VIÊN MỚI ===");
        Staff staff = new Staff();
        
        System.out.print("Nhập mã số nhân viên: ");
        String rollNumber = scanner.nextLine().trim();
        
        if (getIndex(rollNumber) >= 0) {
            System.out.println("❌ Mã số nhân viên đã tồn tại!");
            return false;
        }
        
        staff.setRollNumber(rollNumber);
        staff.input();
        
        return list.add(staff);
    }
    
    @Override
    public boolean update(String rollNumber) {
        int index = getIndex(rollNumber);
        if (index < 0) {
            System.out.println("❌ Không tìm thấy nhân viên với mã số: " + rollNumber);
            return false;
        }
        
        Staff staff = list.get(index);
        System.out.println("\n=== CẬP NHẬT THÔNG TIN NHÂN VIÊN ===");
        System.out.println("Thông tin hiện tại:");
        staff.display();
        
        System.out.println("\nNhập thông tin mới (Enter để giữ nguyên):");
        
        System.out.print("Tên mới: ");
        String name = scanner.nextLine().trim();
        if (!name.isEmpty()) {
            staff.setName(name);
        }
        
        System.out.print("Giới tính mới (true=Nam, false=Nữ): ");
        String genderStr = scanner.nextLine().trim();
        if (!genderStr.isEmpty()) {
            staff.setGender(Boolean.parseBoolean(genderStr));
        }
        
        System.out.print("Ngày sinh mới: ");
        String dob = scanner.nextLine().trim();
        if (!dob.isEmpty()) {
            staff.setDob(dob);
        }
        
        System.out.print("Email mới: ");
        String email = scanner.nextLine().trim();
        if (!email.isEmpty()) {
            staff.setEmail(email);
        }
        
        System.out.print("SĐT mới: ");
        String mobile = scanner.nextLine().trim();
        if (!mobile.isEmpty()) {
            staff.setMobile(mobile);
        }
        
        System.out.print("SĐT công việc mới: ");
        String workMobile = scanner.nextLine().trim();
        if (!workMobile.isEmpty()) {
            staff.setWorkMobile(workMobile);
        }
        
        System.out.print("Địa chỉ mới: ");
        String address = scanner.nextLine().trim();
        if (!address.isEmpty()) {
            staff.setAddress(address);
        }
        
        System.out.print("Lương mới: ");
        String salaryStr = scanner.nextLine().trim();
        if (!salaryStr.isEmpty()) {
            try {
                staff.setSalary(Long.parseLong(salaryStr));
            } catch (NumberFormatException e) {
                System.out.println("⚠️ Lương không hợp lệ!");
            }
        }
        
        return true;
    }
    
    @Override
    public boolean remove(String rollNumber) {
        int index = getIndex(rollNumber);
        if (index < 0) {
            System.out.println("❌ Không tìm thấy nhân viên với mã số: " + rollNumber);
            return false;
        }
        
        Staff staff = list.get(index);
        System.out.println("\nThông tin nhân viên sẽ bị xóa:");
        staff.display();
        
        System.out.print("\nBạn có chắc chắn muốn xóa? (yes/no): ");
        String confirm = scanner.nextLine().trim().toLowerCase();
        
        if ("yes".equals(confirm) || "y".equals(confirm)) {
            Staff removed = list.remove(index);
            System.out.println("✅ Đã xóa nhân viên: " + removed.getName());
            return true;
        } else {
            System.out.println("❌ Đã hủy xóa!");
            return false;
        }
    }
    
    @Override
    public List<Staff> search(String text) {
        if (text == null || text.trim().isEmpty()) {
            return new ArrayList<>();
        }
        
        String searchText = text.toLowerCase().trim();
        return list.stream()
                   .filter(staff -> 
                       staff.getRollNumber().toLowerCase().contains(searchText) ||
                       staff.getName().toLowerCase().contains(searchText) ||
                       staff.getEmail().toLowerCase().contains(searchText) ||
                       staff.getMobile().contains(searchText))
                   .collect(Collectors.toList());
    }
    
    @Override
    public void sort() {
        if (list.isEmpty()) {
            System.out.println("⚠️ Danh sách rỗng, không thể sắp xếp!");
            return;
        }
        
        System.out.println("\n=== SẮP XẾP DANH SÁCH ===");
        System.out.println("1. Theo mã số (tăng dần)");
        System.out.println("2. Theo tên (A-Z)");
        System.out.println("3. Theo lương (giảm dần)");
        System.out.println("4. Theo lương (tăng dần)");
        System.out.print("Chọn tiêu chí sắp xếp (1-4): ");
        
        try {
            int choice = Integer.parseInt(scanner.nextLine());
            
            switch (choice) {
                case 1:
                    list.sort(Comparator.comparing(Staff::getRollNumber));
                    System.out.println("✅ Đã sắp xếp theo mã số (tăng dần)");
                    break;
                case 2:
                    list.sort(Comparator.comparing(Staff::getName));
                    System.out.println("✅ Đã sắp xếp theo tên (A-Z)");
                    break;
                case 3:
                    list.sort(Comparator.comparingLong(Staff::getSalary).reversed());
                    System.out.println("✅ Đã sắp xếp theo lương (giảm dần)");
                    break;
                case 4:
                    list.sort(Comparator.comparingLong(Staff::getSalary));
                    System.out.println("✅ Đã sắp xếp theo lương (tăng dần)");
                    break;
                default:
                    System.out.println("⚠️ Lựa chọn không hợp lệ!");
            }
        } catch (NumberFormatException e) {
            System.out.println("⚠️ Lựa chọn không hợp lệ!");
        }
    }
    
    @Override
    public boolean save(String filePath) {
        System.out.println("Chức năng lưu sẽ được implement ở Phase 6");
        return false;
    }
    
    @Override
    public boolean load(String filePath) {
        System.out.println("Chức năng đọc sẽ được implement ở Phase 6");
        return false;
    }
}
```

## IV. Cập nhật StudentMain và StaffMain

### Cập nhật StudentMain.java (Hoàn chỉnh)

```java
package main;

import bo.StudentBo;
import entity.Student;
import java.util.List;
import java.util.Scanner;

public class StudentMain {
    private static Scanner scanner = new Scanner(System.in);
    private static StudentBo studentBo = new StudentBo();
    
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
                    handleAdd();
                    break;
                case 3:
                    handleUpdate();
                    break;
                case 4:
                    handleDelete();
                    break;
                case 5:
                    handleSearch();
                    break;
                case 6:
                    studentBo.sort();
                    studentBo.display();
                    break;
                case 7:
                    handleSave();
                    break;
                case 8:
                    handleLoad();
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
        System.out.println("║  3. Cập nhật thông tin           ║");
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
    
    private static void handleAdd() {
        if (studentBo.add()) {
            System.out.println("✅ Đã thêm sinh viên thành công!");
        } else {
            System.out.println("❌ Thêm sinh viên thất bại!");
        }
    }
    
    private static void handleUpdate() {
        System.out.print("Nhập mã số sinh viên cần cập nhật: ");
        String rollNumber = scanner.nextLine();
        if (studentBo.update(rollNumber)) {
            System.out.println("✅ Đã cập nhật thành công!");
        } else {
            System.out.println("❌ Không tìm thấy sinh viên!");
        }
    }
    
    private static void handleDelete() {
        System.out.print("Nhập mã số sinh viên cần xóa: ");
        String rollNumber = scanner.nextLine();
        if (studentBo.remove(rollNumber)) {
            System.out.println("✅ Đã xóa thành công!");
        } else {
            System.out.println("❌ Không tìm thấy sinh viên!");
        }
    }
    
    private static void handleSearch() {
        System.out.print("Nhập từ khóa tìm kiếm: ");
        String searchText = scanner.nextLine();
        List<Student> results = studentBo.search(searchText);
        
        if (results.isEmpty()) {
            System.out.println("❌ Không tìm thấy kết quả!");
        } else {
            System.out.println("\n=== KẾT QUẢ TÌM KIẾM (" + results.size() + " kết quả) ===");
            for (Student student : results) {
                student.display();
                System.out.println();
            }
        }
    }
    
    private static void handleSave() {
        System.out.print("Nhập đường dẫn file để lưu: ");
        String filePath = scanner.nextLine();
        if (studentBo.save(filePath)) {
            System.out.println("✅ Đã lưu thành công!");
        } else {
            System.out.println("❌ Lưu thất bại!");
        }
    }
    
    private static void handleLoad() {
        System.out.print("Nhập đường dẫn file để đọc: ");
        String filePath = scanner.nextLine();
        if (studentBo.load(filePath)) {
            System.out.println("✅ Đã đọc thành công!");
        } else {
            System.out.println("❌ Đọc thất bại!");
        }
    }
}
```

## V. Ví dụ sử dụng hệ thống

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
```

## VI. Best Practices

### 1. Validation trong Business Logic

```java
// ✅ TỐT: Kiểm tra trùng lặp trước khi thêm
if (getIndex(rollNumber) >= 0) {
    System.out.println("❌ Mã số đã tồn tại!");
    return false;
}
```

### 2. User-friendly Messages

```java
// ✅ TỐT: Thông báo rõ ràng
System.out.println("✅ Đã thêm thành công!");
System.out.println("❌ Thêm thất bại!");

// ❌ KHÔNG TỐT: Thông báo mơ hồ
System.out.println("Done");
System.out.println("Error");
```

### 3. Error Handling

```java
// ✅ TỐT: Xử lý lỗi đầy đủ
try {
    int choice = Integer.parseInt(scanner.nextLine());
} catch (NumberFormatException e) {
    System.out.println("⚠️ Lựa chọn không hợp lệ!");
    return -1;
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Implement đầy đủ các methods trong StudentBo và StaffBo
- ✅ Sử dụng ArrayList để quản lý danh sách
- ✅ Implement các chức năng: add, update, delete, search, sort, display
- ✅ Kết nối menu với business logic hoàn chỉnh
- ✅ Tạo chương trình quản lý hoàn chỉnh

## Cấu trúc Project hiện tại

```
StudentManagementSystem/
└── src/
    ├── bo/
    │   ├── IManageable.java  ✅ Interface
    │   ├── StudentBo.java    ✅ Implement đầy đủ
    │   └── StaffBo.java      ✅ Implement đầy đủ
    ├── entity/
    │   ├── Person.java       ✅ Abstract
    │   ├── Student.java      ✅ Extends Person
    │   └── Staff.java        ✅ Extends Person
    └── main/
        ├── StudentMain.java  ✅ Menu + Logic
        └── StaffMain.java    ✅ Menu + Logic
```

## Bước tiếp theo

Ở **Phase 6**, chúng ta sẽ:
- Implement methods `save()` và `load()` với Java IO
- Lưu dữ liệu vào file
- Đọc dữ liệu từ file
- Hoàn thiện hệ thống quản lý

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
