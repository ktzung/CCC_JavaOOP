# Đáp án Gợi ý - Hệ thống Bài tập Thực hành

## 📚 Mục đích

Tài liệu này cung cấp đáp án gợi ý cho một số bài tập quan trọng trong hệ thống bài tập thực hành. **Lưu ý**: Đây chỉ là gợi ý, có nhiều cách giải khác nhau.

---

## 📖 PHẦN 1: NHẬP MÔN JAVA

### Bài tập 1.1: Calculator Cơ bản

**Đáp án gợi ý**:

```java
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== MÁY TÍNH ĐƠN GIẢN ===");
        System.out.print("Nhập số thứ nhất: ");
        double num1 = scanner.nextDouble();
        
        System.out.print("Nhập số thứ hai: ");
        double num2 = scanner.nextDouble();
        
        System.out.println("\nChọn phép tính:");
        System.out.println("1. Cộng (+)");
        System.out.println("2. Trừ (-)");
        System.out.println("3. Nhân (*)");
        System.out.println("4. Chia (/)");
        System.out.print("Lựa chọn: ");
        int choice = scanner.nextInt();
        
        double result = 0;
        String operation = "";
        
        switch (choice) {
            case 1:
                result = add(num1, num2);
                operation = "+";
                break;
            case 2:
                result = subtract(num1, num2);
                operation = "-";
                break;
            case 3:
                result = multiply(num1, num2);
                operation = "*";
                break;
            case 4:
                if (num2 != 0) {
                    result = divide(num1, num2);
                    operation = "/";
                } else {
                    System.out.println("❌ Lỗi: Không thể chia cho 0!");
                    return;
                }
                break;
            default:
                System.out.println("❌ Lựa chọn không hợp lệ!");
                return;
        }
        
        System.out.printf("\nKết quả: %.2f %s %.2f = %.2f%n", 
                         num1, operation, num2, result);
        
        scanner.close();
    }
    
    public static double add(double a, double b) {
        return a + b;
    }
    
    public static double subtract(double a, double b) {
        return a - b;
    }
    
    public static double multiply(double a, double b) {
        return a * b;
    }
    
    public static double divide(double a, double b) {
        return a / b;
    }
}
```

---

### Bài tập 1.2: Quản lý Thông tin Cá nhân

**Đáp án gợi ý**:

```java
import java.util.Scanner;

public class PersonalInfo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== NHẬP THÔNG TIN CÁ NHÂN ===");
        
        System.out.print("Họ và tên: ");
        String fullName = scanner.nextLine();
        
        System.out.print("Tuổi: ");
        int age = Integer.parseInt(scanner.nextLine());
        
        System.out.print("Email: ");
        String email = scanner.nextLine();
        
        // Kiểm tra email
        if (!email.contains("@")) {
            System.out.println("⚠️ Cảnh báo: Email không hợp lệ!");
        }
        
        System.out.print("Số điện thoại: ");
        String phone = scanner.nextLine();
        
        System.out.print("Địa chỉ: ");
        String address = scanner.nextLine();
        
        // Hiển thị thông tin
        System.out.println("\n╔════════════════════════════════════╗");
        System.out.println("║      THÔNG TIN CÁ NHÂN            ║");
        System.out.println("╠════════════════════════════════════╣");
        System.out.printf("║ Họ tên: %-25s ║%n", fullName);
        System.out.printf("║ Tuổi: %-27d ║%n", age);
        System.out.printf("║ Email: %-26s ║%n", email);
        System.out.printf("║ SĐT: %-28s ║%n", phone);
        System.out.printf("║ Địa chỉ: %-24s ║%n", address);
        System.out.println("╚════════════════════════════════════╝");
        
        scanner.close();
    }
}
```

---

## 🎓 PHẦN 2: LẬP TRÌNH HƯỚNG ĐỐI TƯỢNG

### Bài tập 4.1: Hệ thống Quản lý Sản phẩm

**Đáp án gợi ý**:

```java
public class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;
    private String category;
    
    // Constructors
    public Product() {
    }
    
    public Product(String id, String name, double price, int quantity, String category) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
        this.category = category;
    }
    
    // Getters
    public String getId() {
        return id;
    }
    
    public String getName() {
        return name;
    }
    
    public double getPrice() {
        return price;
    }
    
    public int getQuantity() {
        return quantity;
    }
    
    public String getCategory() {
        return category;
    }
    
    // Setters với validation
    public void setId(String id) {
        if (id != null && !id.trim().isEmpty()) {
            this.id = id.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: ID không hợp lệ!");
        }
    }
    
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name.trim();
        } else {
            System.out.println("⚠️ Cảnh báo: Tên không hợp lệ!");
        }
    }
    
    public void setPrice(double price) {
        if (price > 0) {
            this.price = price;
        } else {
            System.out.println("⚠️ Cảnh báo: Giá phải > 0!");
        }
    }
    
    public void setQuantity(int quantity) {
        if (quantity >= 0) {
            this.quantity = quantity;
        } else {
            System.out.println("⚠️ Cảnh báo: Số lượng phải >= 0!");
        }
    }
    
    public void setCategory(String category) {
        if (category != null) {
            this.category = category.trim();
        }
    }
    
    // Methods
    public void displayInfo() {
        System.out.println("\n=== THÔNG TIN SẢN PHẨM ===");
        System.out.println("ID: " + id);
        System.out.println("Tên: " + name);
        System.out.println("Giá: " + String.format("%,.0f VNĐ", price));
        System.out.println("Số lượng: " + quantity);
        System.out.println("Danh mục: " + category);
    }
    
    public double calculateTotalValue() {
        return price * quantity;
    }
    
    public void applyDiscount(double percent) {
        if (percent > 0 && percent <= 100) {
            this.price = price * (1 - percent / 100);
            System.out.println("✅ Đã áp dụng giảm giá " + percent + "%");
        } else {
            System.out.println("⚠️ Phần trăm giảm giá không hợp lệ!");
        }
    }
    
    public boolean isLowStock() {
        return quantity < 10;
    }
}
```

**Test class**:

```java
public class ProductTest {
    public static void main(String[] args) {
        Product product1 = new Product("P001", "Laptop", 15000000, 5, "Electronics");
        product1.displayInfo();
        System.out.println("Tổng giá trị: " + String.format("%,.0f VNĐ", product1.calculateTotalValue()));
        System.out.println("Hàng sắp hết: " + product1.isLowStock());
        
        Product product2 = new Product();
        product2.setId("P002");
        product2.setName("Mouse");
        product2.setPrice(500000);
        product2.setQuantity(20);
        product2.setCategory("Accessories");
        product2.displayInfo();
    }
}
```

---

### Bài tập 5.1: Hệ thống Quản lý Phương tiện

**Đáp án gợi ý**:

```java
// Vehicle.java
public class Vehicle {
    protected String brand;
    protected String model;
    protected int year;
    protected double price;
    
    // Default constructor
    public Vehicle() {
    }
    
    // Parameterized constructor
    public Vehicle(String brand, String model, int year, double price) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.price = price;
    }
    
    // Getters
    public String getBrand() {
        return brand;
    }
    
    public String getModel() {
        return model;
    }
    
    public int getYear() {
        return year;
    }
    
    public double getPrice() {
        return price;
    }
    
    // Setters
    public void setBrand(String brand) {
        this.brand = brand;
    }
    
    public void setModel(String model) {
        this.model = model;
    }
    
    public void setYear(int year) {
        this.year = year;
    }
    
    public void setPrice(double price) {
        this.price = price;
    }
    
    // Methods
    public void displayInfo() {
        System.out.println("\n=== THÔNG TIN PHƯƠNG TIỆN ===");
        System.out.println("Hãng: " + brand);
        System.out.println("Model: " + model);
        System.out.println("Năm sản xuất: " + year);
        System.out.println("Giá: " + String.format("%,.0f VNĐ", price));
    }
    
    public double calculateDepreciation(int currentYear) {
        int age = currentYear - year;
        double depreciationRate = 0.1; // 10% mỗi năm
        return price * depreciationRate * age;
    }
    
    public boolean isVintage(int currentYear) {
        return (currentYear - year) > 25;
    }
}

// Car.java
public class Car extends Vehicle {
    private int numberOfSeats;
    
    // Constructor với super()
    public Car(String brand, String model, int year, double price, int numberOfSeats) {
        super(brand, model, year, price);
        this.numberOfSeats = numberOfSeats;
    }
    
    // Getter và Setter
    public int getNumberOfSeats() {
        return numberOfSeats;
    }
    
    public void setNumberOfSeats(int numberOfSeats) {
        this.numberOfSeats = numberOfSeats;
    }
    
    // Override displayInfo()
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Số ghế: " + numberOfSeats);
    }
}

// Motorcycle.java
public class Motorcycle extends Vehicle {
    private int engineCapacity; // cc
    
    public Motorcycle(String brand, String model, int year, double price, int engineCapacity) {
        super(brand, model, year, price);
        this.engineCapacity = engineCapacity;
    }
    
    public int getEngineCapacity() {
        return engineCapacity;
    }
    
    public void setEngineCapacity(int engineCapacity) {
        this.engineCapacity = engineCapacity;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Dung tích động cơ: " + engineCapacity + " cc");
    }
}

// Test class
public class VehicleTest {
    public static void main(String[] args) {
        Car car = new Car("Toyota", "Camry", 2020, 1000000000, 5);
        car.displayInfo();
        
        Motorcycle bike = new Motorcycle("Honda", "CBR", 2021, 500000000, 150);
        bike.displayInfo();
        
        // Test methods từ Vehicle
        System.out.println("\nDepreciation (2024): " + 
                         String.format("%,.0f VNĐ", car.calculateDepreciation(2024)));
        System.out.println("Is Vintage: " + car.isVintage(2024));
    }
}
```

---

### Bài tập 6.1: Hệ thống Hình học

**Đáp án gợi ý**:

```java
// Shape.java
public abstract class Shape {
    public abstract double calculateArea();
    public abstract double calculatePerimeter();
    
    public void displayInfo() {
        System.out.println("\n=== THÔNG TIN HÌNH ===");
        System.out.println("Diện tích: " + String.format("%.2f", calculateArea()));
        System.out.println("Chu vi: " + String.format("%.2f", calculatePerimeter()));
    }
}

// Circle.java
public class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    public double getRadius() {
        return radius;
    }
    
    public void setRadius(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

// Rectangle.java
public class Rectangle extends Shape {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    public double getWidth() {
        return width;
    }
    
    public void setWidth(double width) {
        this.width = width;
    }
    
    public double getHeight() {
        return height;
    }
    
    public void setHeight(double height) {
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
    
    @Override
    public double calculatePerimeter() {
        return 2 * (width + height);
    }
}

// Triangle.java
public class Triangle extends Shape {
    private double a, b, c;
    
    public Triangle(double a, double b, double c) {
        this.a = a;
        this.b = b;
        this.c = c;
    }
    
    @Override
    public double calculateArea() {
        // Heron's formula
        double s = calculatePerimeter() / 2;
        return Math.sqrt(s * (s - a) * (s - b) * (s - c));
    }
    
    @Override
    public double calculatePerimeter() {
        return a + b + c;
    }
}

// Test với Polymorphism
import java.util.ArrayList;
import java.util.List;

public class ShapeTest {
    public static void main(String[] args) {
        List<Shape> shapes = new ArrayList<>();
        
        shapes.add(new Circle(5));
        shapes.add(new Rectangle(4, 6));
        shapes.add(new Triangle(3, 4, 5));
        
        double totalArea = 0;
        for (Shape shape : shapes) {
            shape.displayInfo();
            totalArea += shape.calculateArea();
        }
        
        System.out.println("\nTổng diện tích tất cả hình: " + 
                         String.format("%.2f", totalArea));
        
        // Sắp xếp theo diện tích
        shapes.sort((s1, s2) -> Double.compare(s1.calculateArea(), s2.calculateArea()));
        System.out.println("\nSắp xếp theo diện tích (tăng dần):");
        for (Shape shape : shapes) {
            System.out.println("Area: " + String.format("%.2f", shape.calculateArea()));
        }
    }
}
```

---

### Bài tập 7.1: Hệ thống Quản lý Danh sách Sinh viên

**Đáp án gợi ý**:

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

// Student.java
public class Student implements Comparable<Student> {
    private String id;
    private String name;
    private int age;
    private double gpa;
    
    public Student(String id, String name, int age, double gpa) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.gpa = gpa;
    }
    
    // Getters
    public String getId() { return id; }
    public String getName() { return name; }
    public int getAge() { return age; }
    public double getGpa() { return gpa; }
    
    // Implement Comparable - sort by GPA (descending)
    @Override
    public int compareTo(Student other) {
        return Double.compare(other.gpa, this.gpa);
    }
    
    @Override
    public String toString() {
        return String.format("ID: %s, Name: %s, Age: %d, GPA: %.2f", 
                           id, name, age, gpa);
    }
}

// StudentManager.java
public class StudentManager {
    private List<Student> students = new ArrayList<>();
    
    public void addStudent(Student student) {
        students.add(student);
        System.out.println("✅ Đã thêm sinh viên: " + student.getName());
    }
    
    public boolean removeStudent(String id) {
        for (int i = 0; i < students.size(); i++) {
            if (students.get(i).getId().equals(id)) {
                Student removed = students.remove(i);
                System.out.println("✅ Đã xóa sinh viên: " + removed.getName());
                return true;
            }
        }
        System.out.println("❌ Không tìm thấy sinh viên với ID: " + id);
        return false;
    }
    
    public Student findStudent(String id) {
        for (Student student : students) {
            if (student.getId().equals(id)) {
                return student;
            }
        }
        return null;
    }
    
    public void sortByGPA() {
        Collections.sort(students);
        System.out.println("✅ Đã sắp xếp theo GPA (giảm dần)");
    }
    
    public void sortByName() {
        students.sort(Comparator.comparing(Student::getName));
        System.out.println("✅ Đã sắp xếp theo tên (A-Z)");
    }
    
    public void displayAll() {
        if (students.isEmpty()) {
            System.out.println("⚠️ Danh sách rỗng!");
            return;
        }
        
        System.out.println("\n=== DANH SÁCH SINH VIÊN ===");
        for (Student student : students) {
            System.out.println(student);
        }
    }
    
    public List<Student> getTopStudents(int n) {
        sortByGPA();
        int size = Math.min(n, students.size());
        return students.subList(0, size);
    }
    
    public double getAverageGPA() {
        if (students.isEmpty()) {
            return 0;
        }
        double sum = students.stream()
                             .mapToDouble(Student::getGpa)
                             .sum();
        return sum / students.size();
    }
}

// Test class
public class StudentManagerTest {
    public static void main(String[] args) {
        StudentManager manager = new StudentManager();
        
        manager.addStudent(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        manager.addStudent(new Student("SV002", "Trần Thị B", 21, 9.0));
        manager.addStudent(new Student("SV003", "Lê Văn C", 19, 7.5));
        
        manager.displayAll();
        
        System.out.println("\n=== TOP 2 SINH VIÊN ===");
        List<Student> topStudents = manager.getTopStudents(2);
        for (Student student : topStudents) {
            System.out.println(student);
        }
        
        System.out.println("\nĐiểm trung bình: " + 
                         String.format("%.2f", manager.getAverageGPA()));
    }
}
```

---

## 💡 Lưu ý

1. **Đây chỉ là gợi ý**: Có nhiều cách giải khác nhau
2. **Nên tự code**: Đừng copy-paste, hãy tự viết để hiểu rõ
3. **Test kỹ**: Kiểm tra các trường hợp edge cases
4. **Cải thiện**: Thêm validation, error handling, comments

---

*Tài liệu này cung cấp đáp án gợi ý cho một số bài tập quan trọng*
*Cập nhật: 2025-01-XX*
