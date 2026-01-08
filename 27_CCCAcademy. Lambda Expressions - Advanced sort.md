# Bài 27: Lambda Expressions - Sắp xếp nâng cao với Lambda

> **Mục tiêu**: Sử dụng Lambda để sắp xếp danh sách một cách nâng cao, Comparator.comparing(), sắp xếp theo nhiều tiêu chí, và áp dụng vào các ví dụ thực tế.

## I. Sắp xếp cơ bản với Lambda

### So sánh: Trước và sau Java 8

**Trước Java 8** (Anonymous Inner Class):
```java
List<Student> students = new ArrayList<>();
students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
students.add(new Student("SV002", "Trần Thị B", 21, 9.0));

Collections.sort(students, new Comparator<Student>() {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName());
    }
});
```

**Sau Java 8** (Lambda Expression):
```java
List<Student> students = new ArrayList<>();
students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
students.add(new Student("SV002", "Trần Thị B", 21, 9.0));

// Ngắn gọn hơn nhiều!
students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
```

**Sau Java 8** (Method Reference):
```java
// Ngắn gọn nhất!
students.sort(Comparator.comparing(Student::getName));
```

## II. Comparator.comparing() - Cú pháp ngắn gọn

### Comparator.comparing() là gì?

`Comparator.comparing()` là một static method trong lớp `Comparator` (Java 8+) cho phép tạo Comparator một cách **ngắn gọn** bằng cách chỉ định **key extractor** (hàm trích xuất khóa sắp xếp).

### Cú pháp

```java
Comparator.comparing(Function<? super T, ? extends U> keyExtractor)
```

**Trong đó**:
- `T`: Kiểu của đối tượng cần sắp xếp
- `U`: Kiểu của khóa sắp xếp (phải implement Comparable)

### Ví dụ cơ bản

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Student {
    private String studentId;
    private String name;
    private int age;
    private double gpa;
    
    public Student(String studentId, String name, int age, double gpa) {
        this.studentId = studentId;
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Getters
    public String getStudentId() { return studentId; }
    public String getName() { return name; }
    public int getAge() { return age; }
    public double getGpa() { return gpa; }
    
    @Override
    public String toString() {
        return String.format("ID: %s, Tên: %s, Tuổi: %d, GPA: %.2f",
                            studentId, name, age, gpa);
    }
}

public class ComparingExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        // Cách 1: Lambda (đầy đủ)
        students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
        
        // Cách 2: Method Reference (ngắn gọn nhất)
        students.sort(Comparator.comparing(Student::getName));
        
        // Cách 3: Lambda với Comparator.comparing
        students.sort(Comparator.comparing(s -> s.getName()));
        
        students.forEach(System.out::println);
    }
}
```

### Sắp xếp theo các trường khác nhau

```java
public class ComparingDifferentFields {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        System.out.println("=== SẮP XẾP THEO TÊN ===");
        students.sort(Comparator.comparing(Student::getName));
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TUỔI ===");
        students.sort(Comparator.comparingInt(Student::getAge));
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GPA ===");
        students.sort(Comparator.comparingDouble(Student::getGpa));
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO ID ===");
        students.sort(Comparator.comparing(Student::getStudentId));
        students.forEach(System.out::println);
    }
}
```

## III. Comparator.comparing() với Primitive Types

### Comparator.comparingInt() - Cho int

```java
// Thay vì: Comparator.comparing(Student::getAge)
// Dùng: Comparator.comparingInt() (hiệu quả hơn cho int)
students.sort(Comparator.comparingInt(Student::getAge));
```

### Comparator.comparingDouble() - Cho double

```java
// Thay vì: Comparator.comparing(Student::getGpa)
// Dùng: Comparator.comparingDouble() (hiệu quả hơn cho double)
students.sort(Comparator.comparingDouble(Student::getGpa));
```

### Comparator.comparingLong() - Cho long

```java
// Tương tự cho long
students.sort(Comparator.comparingLong(Student::getId));
```

### Ví dụ

```java
public class ComparingPrimitives {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        // Sắp xếp theo tuổi (int)
        students.sort(Comparator.comparingInt(Student::getAge));
        
        // Sắp xếp theo GPA (double)
        students.sort(Comparator.comparingDouble(Student::getGpa));
        
        // Sắp xếp theo tên (String - không có comparingString, dùng comparing)
        students.sort(Comparator.comparing(Student::getName));
        
        students.forEach(System.out::println);
    }
}
```

## IV. Sắp xếp giảm dần (Reversed Order)

### Sử dụng .reversed()

```java
// Sắp xếp theo GPA giảm dần
students.sort(Comparator.comparingDouble(Student::getGpa).reversed());

// Sắp xếp theo tên giảm dần (Z → A)
students.sort(Comparator.comparing(Student::getName).reversed());

// Sắp xếp theo tuổi giảm dần
students.sort(Comparator.comparingInt(Student::getAge).reversed());
```

### Ví dụ

```java
public class ReversedSorting {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        System.out.println("=== SẮP XẾP THEO GPA (Tăng dần) ===");
        students.sort(Comparator.comparingDouble(Student::getGpa));
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GPA (Giảm dần) ===");
        students.sort(Comparator.comparingDouble(Student::getGpa).reversed());
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TÊN (Z → A) ===");
        students.sort(Comparator.comparing(Student::getName).reversed());
        students.forEach(System.out::println);
    }
}
```

## V. Sắp xếp theo nhiều tiêu chí (Multiple Criteria)

### Sử dụng thenComparing()

**`thenComparing()`** cho phép sắp xếp theo **nhiều tiêu chí** (tiêu chí phụ khi tiêu chí chính bằng nhau).

### Cú pháp

```java
Comparator.comparing(keyExtractor1)
          .thenComparing(keyExtractor2)
          .thenComparing(keyExtractor3)
```

### Ví dụ: Sắp xếp theo tên, sau đó theo tuổi

```java
public class MultipleCriteria {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Nguyễn Văn A", 19, 9.0));  // Trùng tên
        students.add(new Student("SV003", "Trần Thị B", 21, 7.8));
        students.add(new Student("SV004", "Lê Văn C", 20, 8.2));
        
        System.out.println("=== TRƯỚC KHI SẮP XẾP ===");
        students.forEach(System.out::println);
        
        // Sắp xếp: Tên → Tuổi
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparingInt(Student::getAge));
        
        System.out.println("\n=== SAU KHI SẮP XẾP (Tên → Tuổi) ===");
        students.forEach(System.out::println);
        
        // Sắp xếp: Tên → Tuổi → GPA
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparingInt(Student::getAge)
                               .thenComparingDouble(Student::getGpa));
        
        System.out.println("\n=== SAU KHI SẮP XẾP (Tên → Tuổi → GPA) ===");
        students.forEach(System.out::println);
    }
}
```

**Kết quả**:
```
=== TRƯỚC KHI SẮP XẾP ===
ID: SV001, Tên: Nguyễn Văn A, Tuổi: 20, GPA: 8.50
ID: SV002, Tên: Nguyễn Văn A, Tuổi: 19, GPA: 9.00
ID: SV003, Tên: Trần Thị B, Tuổi: 21, GPA: 7.80
ID: SV004, Tên: Lê Văn C, Tuổi: 20, GPA: 8.20

=== SAU KHI SẮP XẾP (Tên → Tuổi) ===
ID: SV002, Tên: Nguyễn Văn A, Tuổi: 19, GPA: 9.00  (tên giống, tuổi nhỏ hơn)
ID: SV001, Tên: Nguyễn Văn A, Tuổi: 20, GPA: 8.50
ID: SV003, Tên: Trần Thị B, Tuổi: 21, GPA: 7.80
ID: SV004, Tên: Lê Văn C, Tuổi: 20, GPA: 8.20
```

### Các biến thể của thenComparing()

```java
// thenComparing() - Với method reference
students.sort(Comparator.comparing(Student::getName)
                       .thenComparing(Student::getAge));

// thenComparingInt() - Với int
students.sort(Comparator.comparing(Student::getName)
                       .thenComparingInt(Student::getAge));

// thenComparingDouble() - Với double
students.sort(Comparator.comparing(Student::getName)
                       .thenComparingDouble(Student::getGpa));

// thenComparing() với Comparator tùy chỉnh
students.sort(Comparator.comparing(Student::getName)
                       .thenComparing((s1, s2) -> 
                           Integer.compare(s1.getAge(), s2.getAge())));
```

## VI. Comparator.comparing() với Custom Comparator

### So sánh tùy chỉnh cho key

`Comparator.comparing()` có thể nhận thêm một Comparator tùy chỉnh để so sánh key:

```java
// Cú pháp
Comparator.comparing(keyExtractor, customComparator)
```

### Ví dụ

```java
public class CustomComparator {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        // Sắp xếp theo tên (giảm dần - Z → A)
        students.sort(Comparator.comparing(
            Student::getName,
            (s1, s2) -> s2.compareTo(s1)  // Comparator tùy chỉnh
        ));
        
        // Hoặc dùng reversed()
        students.sort(Comparator.comparing(Student::getName).reversed());
        
        // Sắp xếp theo tên (không phân biệt hoa thường)
        students.sort(Comparator.comparing(
            Student::getName,
            String.CASE_INSENSITIVE_ORDER
        ));
        
        // Sắp xếp theo GPA (giảm dần)
        students.sort(Comparator.comparing(
            Student::getGpa,
            (gpa1, gpa2) -> Double.compare(gpa2, gpa1)  // Giảm dần
        ));
        
        students.forEach(System.out::println);
    }
}
```

## VII. Ví dụ thực tế

### Ví dụ 1: Sắp xếp danh sách sản phẩm

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;
    
    public Product(String id, String name, double price, int quantity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }
    
    // Getters
    public String getId() { return id; }
    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }
    
    @Override
    public String toString() {
        return String.format("ID: %s, Tên: %s, Giá: %.2f, SL: %d",
                            id, name, price, quantity);
    }
    
    public static void main(String[] args) {
        List<Product> products = new ArrayList<>();
        products.add(new Product("P001", "Laptop", 15000000, 5));
        products.add(new Product("P002", "Mouse", 500000, 10));
        products.add(new Product("P003", "Keyboard", 1000000, 8));
        products.add(new Product("P004", "Monitor", 3000000, 3));
        
        System.out.println("=== SẮP XẾP THEO TÊN (A-Z) ===");
        products.sort(Comparator.comparing(Product::getName));
        products.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GIÁ (Tăng dần) ===");
        products.sort(Comparator.comparingDouble(Product::getPrice));
        products.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GIÁ (Giảm dần) ===");
        products.sort(Comparator.comparingDouble(Product::getPrice).reversed());
        products.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TÊN → GIÁ ===");
        products.sort(Comparator.comparing(Product::getName)
                               .thenComparingDouble(Product::getPrice));
        products.forEach(System.out::println);
    }
}
```

### Ví dụ 2: Sắp xếp danh sách nhân viên

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Employee {
    private String employeeId;
    private String name;
    private String department;
    private double salary;
    private int yearsOfExperience;
    
    public Employee(String employeeId, String name, String department,
                   double salary, int yearsOfExperience) {
        this.employeeId = employeeId;
        this.name = name;
        this.department = department;
        this.salary = salary;
        this.yearsOfExperience = yearsOfExperience;
    }
    
    // Getters
    public String getEmployeeId() { return employeeId; }
    public String getName() { return name; }
    public String getDepartment() { return department; }
    public double getSalary() { return salary; }
    public int getYearsOfExperience() { return yearsOfExperience; }
    
    @Override
    public String toString() {
        return String.format("ID: %s, Tên: %s, Phòng: %s, Lương: %.2f, Kinh nghiệm: %d năm",
                            employeeId, name, department, salary, yearsOfExperience);
    }
    
    public static void main(String[] args) {
        List<Employee> employees = new ArrayList<>();
        employees.add(new Employee("E001", "Nguyễn Văn A", "IT", 15000000, 3));
        employees.add(new Employee("E002", "Trần Thị B", "HR", 12000000, 2));
        employees.add(new Employee("E003", "Lê Văn C", "IT", 18000000, 5));
        employees.add(new Employee("E004", "Phạm Thị D", "IT", 15000000, 3));
        
        System.out.println("=== SẮP XẾP THEO PHÒNG → LƯƠNG (Giảm dần) ===");
        employees.sort(Comparator.comparing(Employee::getDepartment)
                                 .thenComparingDouble(Employee::getSalary).reversed());
        employees.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO PHÒNG → KINH NGHIỆM → LƯƠNG ===");
        employees.sort(Comparator.comparing(Employee::getDepartment)
                                 .thenComparingInt(Employee::getYearsOfExperience).reversed()
                                 .thenComparingDouble(Employee::getSalary).reversed());
        employees.forEach(System.out::println);
    }
}
```

### Ví dụ 3: Sắp xếp với null handling

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class NullHandling {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add(null);
        names.add("Bob");
        names.add(null);
        names.add("Charlie");
        
        // ❌ LỖI: NullPointerException khi so sánh với null
        // names.sort(Comparator.comparing(String::toString));
        
        // ✅ OK: Xử lý null - null đứng đầu
        names.sort(Comparator.nullsFirst(Comparator.naturalOrder()));
        System.out.println("Nulls first: " + names);
        // [null, null, Alice, Bob, Charlie]
        
        // ✅ OK: Xử lý null - null đứng cuối
        names.sort(Comparator.nullsLast(Comparator.naturalOrder()));
        System.out.println("Nulls last: " + names);
        // [Alice, Bob, Charlie, null, null]
    }
}
```

## VIII. So sánh các cách sắp xếp

### Bảng so sánh

| Cách | Cú pháp | Độ dài | Dễ đọc |
|------|---------|--------|--------|
| **Anonymous Inner Class** | `new Comparator<>() { ... }` | 🔴 Rất dài | ❌ Khó đọc |
| **Lambda Expression** | `(s1, s2) -> s1.getName().compareTo(s2.getName())` | 🟡 Trung bình | ✅ Dễ đọc |
| **Method Reference** | `Comparator.comparing(Student::getName)` | 🟢 Ngắn | ✅✅ Rất dễ đọc |
| **Method Reference + Chain** | `Comparator.comparing(...).thenComparing(...)` | 🟢 Ngắn | ✅✅✅ Cực kỳ dễ đọc |

### Ví dụ so sánh

```java
public class CompareSortingMethods {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        
        // Cách 1: Anonymous Inner Class (Trước Java 8)
        Collections.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student s1, Student s2) {
                int nameCompare = s1.getName().compareTo(s2.getName());
                if (nameCompare != 0) {
                    return nameCompare;
                }
                return Integer.compare(s1.getAge(), s2.getAge());
            }
        });
        
        // Cách 2: Lambda Expression (Java 8+)
        students.sort((s1, s2) -> {
            int nameCompare = s1.getName().compareTo(s2.getName());
            if (nameCompare != 0) {
                return nameCompare;
            }
            return Integer.compare(s1.getAge(), s2.getAge());
        });
        
        // Cách 3: Method Reference với Chain (Java 8+) - ✅ Khuyến nghị
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparingInt(Student::getAge));
        
        // Rõ ràng là Cách 3 ngắn gọn và dễ đọc nhất!
    }
}
```

## IX. Best Practices

### 1. Ưu tiên Method Reference khi có thể

```java
// ✅ TỐT: Method Reference
students.sort(Comparator.comparing(Student::getName));

// ❌ KHÔNG TỐT: Lambda không cần thiết
students.sort(Comparator.comparing(s -> s.getName()));
```

### 2. Sử dụng thenComparing() cho nhiều tiêu chí

```java
// ✅ TỐT: Rõ ràng, dễ đọc
students.sort(Comparator.comparing(Student::getName)
                       .thenComparingInt(Student::getAge)
                       .thenComparingDouble(Student::getGpa));

// ❌ KHÔNG TỐT: Logic phức tạp trong Lambda
students.sort((s1, s2) -> {
    int nameCompare = s1.getName().compareTo(s2.getName());
    if (nameCompare != 0) return nameCompare;
    int ageCompare = Integer.compare(s1.getAge(), s2.getAge());
    if (ageCompare != 0) return ageCompare;
    return Double.compare(s1.getGpa(), s2.getGpa());
});
```

### 3. Sử dụng comparingInt/Double/Long cho primitives

```java
// ✅ TỐT: Hiệu quả hơn
students.sort(Comparator.comparingInt(Student::getAge));

// ⚠️ OK: Cũng được, nhưng kém hiệu quả hơn một chút
students.sort(Comparator.comparing(Student::getAge));
```

### 4. Kết hợp với null handling khi cần

```java
// Nếu có thể có null
names.sort(Comparator.nullsLast(Comparator.comparing(String::toString)));
```

## X. Ví dụ tổng hợp

### Ví dụ: Hệ thống quản lý sinh viên với sắp xếp

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class StudentManagement {
    private List<Student> students;
    
    public StudentManagement() {
        this.students = new ArrayList<>();
    }
    
    public void addStudent(Student student) {
        students.add(student);
    }
    
    // Sắp xếp theo GPA (tăng dần)
    public void sortByGpaAscending() {
        students.sort(Comparator.comparingDouble(Student::getGpa));
        System.out.println("✅ Đã sắp xếp theo GPA (tăng dần)");
    }
    
    // Sắp xếp theo GPA (giảm dần)
    public void sortByGpaDescending() {
        students.sort(Comparator.comparingDouble(Student::getGpa).reversed());
        System.out.println("✅ Đã sắp xếp theo GPA (giảm dần)");
    }
    
    // Sắp xếp theo tên
    public void sortByName() {
        students.sort(Comparator.comparing(Student::getName));
        System.out.println("✅ Đã sắp xếp theo tên");
    }
    
    // Sắp xếp theo tên → tuổi
    public void sortByNameThenAge() {
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparingInt(Student::getAge));
        System.out.println("✅ Đã sắp xếp theo tên → tuổi");
    }
    
    // Sắp xếp theo nhiều tiêu chí
    public void sortByNameThenAgeThenGpa() {
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparingInt(Student::getAge)
                               .thenComparingDouble(Student::getGpa));
        System.out.println("✅ Đã sắp xếp theo tên → tuổi → GPA");
    }
    
    // Hiển thị danh sách
    public void displayStudents() {
        if (students.isEmpty()) {
            System.out.println("Danh sách rỗng!");
            return;
        }
        
        System.out.println("\n=== DANH SÁCH SINH VIÊN ===");
        for (int i = 0; i < students.size(); i++) {
            System.out.println((i + 1) + ". " + students.get(i));
        }
        System.out.println("Tổng số: " + students.size() + "\n");
    }
    
    public static void main(String[] args) {
        StudentManagement manager = new StudentManagement();
        
        // Thêm sinh viên
        manager.addStudent(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        manager.addStudent(new Student("SV002", "Trần Thị B", 21, 9.0));
        manager.addStudent(new Student("SV003", "Nguyễn Văn A", 19, 8.2));  // Trùng tên
        manager.addStudent(new Student("SV004", "Lê Văn C", 20, 7.8));
        
        manager.displayStudents();
        
        // Các cách sắp xếp khác nhau
        manager.sortByGpaAscending();
        manager.displayStudents();
        
        manager.sortByGpaDescending();
        manager.displayStudents();
        
        manager.sortByName();
        manager.displayStudents();
        
        manager.sortByNameThenAge();
        manager.displayStudents();
        
        manager.sortByNameThenAgeThenGpa();
        manager.displayStudents();
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Sử dụng Lambda để sắp xếp danh sách một cách ngắn gọn
- ✅ Nắm được `Comparator.comparing()` và các biến thể
- ✅ Sắp xếp giảm dần với `.reversed()`
- ✅ Sắp xếp theo nhiều tiêu chí với `thenComparing()`
- ✅ Sử dụng method reference trong sắp xếp
- ✅ Xử lý null khi sắp xếp
- ✅ Áp dụng vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo danh sách sản phẩm và sắp xếp**:
   - Theo giá (tăng dần/giảm dần)
   - Theo tên
   - Theo giá → số lượng

2. **Tạo danh sách nhân viên và sắp xếp**:
   - Theo phòng ban → lương
   - Theo kinh nghiệm → lương
   - Theo phòng ban → kinh nghiệm → lương

3. **Tạo hệ thống sắp xếp linh hoạt**:
   - Cho phép người dùng chọn tiêu chí sắp xếp
   - Hỗ trợ sắp xếp theo nhiều tiêu chí

## Tài liệu tham khảo

- [Oracle Java Tutorial - Comparator](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)
- [Java Lambda Expressions](https://www.javatpoint.com/java-lambda-expressions)
- [Java Comparator.comparing()](https://www.baeldung.com/java-8-comparator-comparing)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
