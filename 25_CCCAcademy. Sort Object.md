# Bài 25: Sắp xếp đối tượng (Sort Object) trong Java

> **Mục tiêu**: Hiểu cách sắp xếp đối tượng trong Java, sử dụng Comparable và Comparator, và áp dụng vào các ví dụ thực tế.

## I. Giới thiệu về sắp xếp đối tượng

### Vấn đề khi sắp xếp đối tượng

Khi làm việc với danh sách các đối tượng, chúng ta thường cần **sắp xếp** chúng theo một tiêu chí nào đó:

- Sắp xếp sinh viên theo **điểm trung bình** (tăng dần/giảm dần)
- Sắp xếp sản phẩm theo **giá tiền** (từ thấp đến cao)
- Sắp xếp nhân viên theo **tên** (alphabetically)
- Sắp xếp theo **nhiều tiêu chí** (tên, nếu trùng tên thì sắp xếp theo tuổi)

### Vấn đề: So sánh đối tượng như thế nào?

**Với số nguyên**: Rõ ràng (10 < 20, 30 > 25)

**Với đối tượng**: Không rõ ràng!
- `student1 < student2`? → So sánh cái gì? Điểm? Tên? Tuổi?

**Giải pháp**: Java cung cấp 2 interface để so sánh:
1. **Comparable** - Đối tượng tự so sánh với nhau
2. **Comparator** - So sánh từ bên ngoài (linh hoạt hơn)

## II. Comparable Interface

### Comparable là gì?

**Comparable** là một interface trong Java cho phép đối tượng **tự so sánh** với đối tượng khác cùng loại.

### Cách sử dụng

**1. Cho class implement Comparable**:
```java
public class Student implements Comparable<Student> {
    private String name;
    private int age;
    private double gpa;
    
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Getters
    public String getName() { return name; }
    public int getAge() { return age; }
    public double getGpa() { return gpa; }
}
```

**2. Override compareTo()**:
```java
@Override
public int compareTo(Student other) {
    // So sánh theo GPA (tăng dần)
    return Double.compare(this.gpa, other.gpa);
    
    // Hoặc:
    // if (this.gpa < other.gpa) return -1;
    // if (this.gpa > other.gpa) return 1;
    // return 0;
}
```

**3. Sử dụng Collections.sort()**:
```java
List<Student> students = new ArrayList<>();
students.add(new Student("Alice", 20, 8.5));
students.add(new Student("Bob", 21, 7.5));
students.add(new Student("Charlie", 19, 9.0));

Collections.sort(students);  // ✅ Tự động sắp xếp theo compareTo()
```

### Giá trị trả về của compareTo()

| Giá trị | Ý nghĩa |
|---------|---------|
| **Âm** (< 0) | Đối tượng này **nhỏ hơn** đối tượng kia |
| **0** | Đối tượng này **bằng** đối tượng kia |
| **Dương** (> 0) | Đối tượng này **lớn hơn** đối tượng kia |

**Công thức nhớ**:
```java
this.compareTo(other):
- < 0: this < other (this đứng trước other)
- = 0: this == other (bằng nhau)
- > 0: this > other (this đứng sau other)
```

### Ví dụ hoàn chỉnh với Comparable

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Student implements Comparable<Student> {
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
    
    // Override compareTo() - Sắp xếp theo GPA tăng dần
    @Override
    public int compareTo(Student other) {
        // So sánh theo GPA
        return Double.compare(this.gpa, other.gpa);
        
        // Cách viết tương đương:
        // if (this.gpa < other.gpa) return -1;
        // if (this.gpa > other.gpa) return 1;
        // return 0;
    }
    
    @Override
    public String toString() {
        return String.format("ID: %s, Tên: %s, Tuổi: %d, GPA: %.2f",
                            studentId, name, age, gpa);
    }
    
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        students.add(new Student("SV004", "Phạm Thị D", 20, 8.2));
        
        System.out.println("=== TRƯỚC KHI SẮP XẾP ===");
        for (Student s : students) {
            System.out.println(s);
        }
        
        // Sắp xếp - Sử dụng compareTo()
        Collections.sort(students);
        
        System.out.println("\n=== SAU KHI SẮP XẾP (theo GPA tăng dần) ===");
        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

**Kết quả**:
```
=== TRƯỚC KHI SẮP XẾP ===
ID: SV001, Tên: Nguyễn Văn A, Tuổi: 20, GPA: 8.50
ID: SV002, Tên: Trần Thị B, Tuổi: 21, GPA: 9.00
ID: SV003, Tên: Lê Văn C, Tuổi: 19, GPA: 7.80
ID: SV004, Tên: Phạm Thị D, Tuổi: 20, GPA: 8.20

=== SAU KHI SẮP XẾP (theo GPA tăng dần) ===
ID: SV003, Tên: Lê Văn C, Tuổi: 19, GPA: 7.80
ID: SV004, Tên: Phạm Thị D, Tuổi: 20, GPA: 8.20
ID: SV001, Tên: Nguyễn Văn A, Tuổi: 20, GPA: 8.50
ID: SV002, Tên: Trần Thị B, Tuổi: 21, GPA: 9.00
```

### Sắp xếp giảm dần với Comparable

**Cách 1: Đảo ngược logic**:
```java
@Override
public int compareTo(Student other) {
    // Giảm dần: Đảo ngược thứ tự so sánh
    return Double.compare(other.gpa, this.gpa);  // other trước this
}
```

**Cách 2: Đảo ngược sau khi sắp xếp**:
```java
Collections.sort(students);
Collections.reverse(students);  // Đảo ngược danh sách
```

## III. Comparator Interface

### Comparator là gì?

**Comparator** là một interface trong Java cho phép **so sánh 2 đối tượng từ bên ngoài** (không cần đối tượng implement Comparable).

### Ưu điểm của Comparator

- ✅ **Linh hoạt hơn**: Có thể so sánh theo nhiều tiêu chí khác nhau
- ✅ **Không cần sửa class gốc**: Không cần implement trong class
- ✅ **Nhiều Comparator**: Có thể tạo nhiều Comparator cho cùng một class
- ✅ **Reverse order**: Dễ dàng sắp xếp ngược

### Cách sử dụng Comparator

**1. Tạo Comparator class**:
```java
import java.util.Comparator;

public class StudentNameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        // So sánh theo tên (tăng dần)
        return s1.getName().compareTo(s2.getName());
    }
}
```

**2. Sử dụng Comparator khi sắp xếp**:
```java
List<Student> students = new ArrayList<>();
// ... thêm sinh viên ...

// Sắp xếp theo tên
Collections.sort(students, new StudentNameComparator());

// Hoặc dùng list.sort() (Java 8+)
students.sort(new StudentNameComparator());
```

### Ví dụ với nhiều Comparator

```java
import java.util.ArrayList;
import java.util.Collections;
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

// Comparator 1: Sắp xếp theo tên
class StudentNameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName());
    }
}

// Comparator 2: Sắp xếp theo tuổi
class StudentAgeComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.getAge(), s2.getAge());
    }
}

// Comparator 3: Sắp xếp theo GPA (giảm dần)
class StudentGpaDescComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        // Giảm dần: Đảo ngược thứ tự
        return Double.compare(s2.getGpa(), s1.getGpa());
    }
}

// Sử dụng
public class ComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        System.out.println("=== SẮP XẾP THEO TÊN ===");
        Collections.sort(students, new StudentNameComparator());
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TUỔI ===");
        Collections.sort(students, new StudentAgeComparator());
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GPA (GIẢM DẦN) ===");
        Collections.sort(students, new StudentGpaDescComparator());
        students.forEach(System.out::println);
    }
}
```

## IV. Anonymous Comparator và Lambda (Java 8+)

### Anonymous Inner Class (Trước Java 8)

```java
// Sắp xếp theo tên - Anonymous inner class
Collections.sort(students, new Comparator<Student>() {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName());
    }
});
```

### Lambda Expression (Java 8+)

**Cú pháp**:
```java
Comparator<Student> comparator = (s1, s2) -> s1.getName().compareTo(s2.getName());
```

**Ví dụ**:
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class LambdaSort {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        // Cách 1: Lambda expression
        students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
        
        // Cách 2: Method reference (nếu có getter)
        // students.sort(Comparator.comparing(Student::getName));
        
        // Cách 3: Lambda với nhiều dòng
        students.sort((s1, s2) -> {
            int nameCompare = s1.getName().compareTo(s2.getName());
            if (nameCompare != 0) {
                return nameCompare;
            }
            // Nếu tên giống nhau, sắp xếp theo tuổi
            return Integer.compare(s1.getAge(), s2.getAge());
        });
        
        students.forEach(System.out::println);
    }
}
```

### Comparator.comparing() (Java 8+)

**Cách ngắn gọn hơn**:
```java
import java.util.Comparator;

// Sắp xếp theo tên
students.sort(Comparator.comparing(Student::getName));

// Sắp xếp theo GPA
students.sort(Comparator.comparing(Student::getGpa));

// Sắp xếp giảm dần
students.sort(Comparator.comparing(Student::getGpa).reversed());

// Sắp xếp theo nhiều tiêu chí
students.sort(Comparator.comparing(Student::getName)
                        .thenComparing(Student::getAge)
                        .thenComparing(Student::getGpa));
```

**Ví dụ**:
```java
public class ComparingExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Nguyễn Văn A", 21, 9.0));  // Trùng tên
        students.add(new Student("SV003", "Trần Thị B", 19, 7.8));
        
        // Sắp xếp theo tên, nếu trùng tên thì sắp xếp theo tuổi
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparing(Student::getAge));
        
        students.forEach(System.out::println);
    }
}
```

## V. Sắp xếp theo nhiều tiêu chí

### Ví dụ: Sắp xếp theo nhiều tiêu chí

```java
// Sắp xếp: Tên → Tuổi → GPA
students.sort((s1, s2) -> {
    // Tiêu chí 1: Tên
    int nameCompare = s1.getName().compareTo(s2.getName());
    if (nameCompare != 0) {
        return nameCompare;
    }
    
    // Tiêu chí 2: Tuổi (nếu tên giống nhau)
    int ageCompare = Integer.compare(s1.getAge(), s2.getAge());
    if (ageCompare != 0) {
        return ageCompare;
    }
    
    // Tiêu chí 3: GPA (nếu tên và tuổi giống nhau)
    return Double.compare(s1.getGpa(), s2.getGpa());
});

// Hoặc dùng thenComparing() (Java 8+)
students.sort(Comparator.comparing(Student::getName)
                       .thenComparing(Student::getAge)
                       .thenComparing(Student::getGpa));
```

### Ví dụ thực tế: Sắp xếp sinh viên

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class StudentSorting {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Nguyễn Văn A", 19, 8.5));  // Trùng tên
        students.add(new Student("SV004", "Lê Văn C", 20, 7.8));
        
        System.out.println("=== SẮP XẾP THEO TÊN (tăng dần) ===");
        students.sort(Comparator.comparing(Student::getName));
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TÊN, SAU ĐÓ THEO TUỔI ===");
        students.sort(Comparator.comparing(Student::getName)
                               .thenComparing(Student::getAge));
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GPA (giảm dần) ===");
        students.sort(Comparator.comparing(Student::getGpa).reversed());
        students.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TÊN (giảm dần) ===");
        students.sort((s1, s2) -> s2.getName().compareTo(s1.getName()));
        students.forEach(System.out::println);
    }
}
```

## VI. So sánh Comparable vs Comparator

### Bảng so sánh

| Đặc điểm | Comparable | Comparator |
|----------|-----------|------------|
| **Package** | `java.lang.Comparable` | `java.util.Comparator` |
| **Method** | `compareTo(T o)` - 1 tham số | `compare(T o1, T o2)` - 2 tham số |
| **Implementation** | Trong class cần so sánh | Tách riêng (class riêng, anonymous, lambda) |
| **Sắp xếp** | 1 cách (theo compareTo) | Nhiều cách (nhiều Comparator) |
| **Sửa class gốc** | ✅ Cần sửa class | ❌ Không cần |
| **Tên gọi** | Natural ordering | Custom ordering |

### Khi nào dùng gì?

**Dùng Comparable khi**:
- ✅ Class có **một cách sắp xếp tự nhiên** (natural ordering)
- ✅ Có quyền **sửa class gốc**
- ✅ Ví dụ: String (theo alphabet), Integer (theo giá trị số)

**Dùng Comparator khi**:
- ✅ Cần **nhiều cách sắp xếp** khác nhau
- ✅ **Không thể sửa class gốc** (class của thư viện)
- ✅ Sắp xếp **tạm thời** (không cần thay đổi class)

### Ví dụ tổng hợp

```java
// Student implement Comparable (sắp xếp tự nhiên: theo GPA)
public class Student implements Comparable<Student> {
    // ...
    
    @Override
    public int compareTo(Student other) {
        return Double.compare(this.gpa, other.gpa);  // Tự nhiên: theo GPA
    }
}

// Sử dụng Comparable
Collections.sort(students);  // Sắp xếp theo GPA (compareTo)

// Sử dụng Comparator (nhiều cách khác)
Collections.sort(students, Comparator.comparing(Student::getName));  // Theo tên
Collections.sort(students, Comparator.comparing(Student::getAge));   // Theo tuổi
Collections.sort(students, Comparator.comparing(Student::getGpa).reversed());  // Theo GPA giảm dần
```

## VII. Ví dụ thực tế

### Ví dụ 1: Quản lý danh sách sản phẩm

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Product implements Comparable<Product> {
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
    
    // Comparable - Sắp xếp tự nhiên theo giá (tăng dần)
    @Override
    public int compareTo(Product other) {
        return Double.compare(this.price, other.price);
    }
    
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
        
        System.out.println("=== SẮP XẾP THEO GIÁ (Tăng dần - Comparable) ===");
        products.sort(null);  // null = dùng compareTo()
        products.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TÊN (Comparator) ===");
        products.sort(Comparator.comparing(Product::getName));
        products.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO GIÁ (Giảm dần) ===");
        products.sort(Comparator.comparing(Product::getPrice).reversed());
        products.forEach(System.out::println);
        
        System.out.println("\n=== SẮP XẾP THEO TÊN, SAU ĐÓ THEO GIÁ ===");
        products.sort(Comparator.comparing(Product::getName)
                               .thenComparing(Product::getPrice));
        products.forEach(System.out::println);
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu vấn đề khi sắp xếp đối tượng
- ✅ Nắm được Comparable interface và cách sử dụng
- ✅ Nắm được Comparator interface và cách sử dụng
- ✅ So sánh được Comparable vs Comparator
- ✅ Sắp xếp theo nhiều tiêu chí
- ✅ Sử dụng Lambda và Method Reference (Java 8+)
- ✅ Áp dụng vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo class Student với Comparable**:
   - Implement Comparable
   - Override compareTo() theo GPA
   - Sắp xếp danh sách sinh viên

2. **Tạo các Comparator**:
   - Comparator sắp xếp theo tên
   - Comparator sắp xếp theo tuổi
   - Comparator sắp xếp theo GPA (giảm dần)

3. **Sắp xếp theo nhiều tiêu chí**:
   - Theo tên, nếu trùng tên thì theo tuổi
   - Theo GPA, nếu trùng GPA thì theo tên

## Tài liệu tham khảo

- [Oracle Java Tutorial - Object Ordering](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html)
- [Java Comparable](https://www.javatpoint.com/Comparable-in-java)
- [Java Comparator](https://www.javatpoint.com/Comparator-interface-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
