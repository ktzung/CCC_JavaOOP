# Bài 17: Tính kế thừa (Inheritance)

> **Mục tiêu**: Hiểu được tính kế thừa trong Java, cách sử dụng từ khóa `extends`, `super`, và lợi ích của việc sử dụng kế thừa trong lập trình.

## I. Giới thiệu về tính kế thừa

### Kế thừa là gì?

**Kế thừa (Inheritance)** là một trong bốn tính chất cơ bản của lập trình hướng đối tượng. Đây là cơ chế cho phép một lớp **nhận** (inherit) các thuộc tính và phương thức từ một lớp khác.

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một gia đình:

- **Lớp cha (Parent/Superclass)**: `Person` (Người)
  - Có: tên, ngày sinh, địa chỉ
  
- **Lớp con (Child/Subclass)**: `Student` (Sinh viên)
  - **Kế thừa** từ `Person`: tên, ngày sinh, địa chỉ
  - **Bổ sung thêm**: mã sinh viên, điểm trung bình

- **Lớp con khác**: `Employee` (Nhân viên)
  - **Kế thừa** từ `Person`: tên, ngày sinh, địa chỉ
  - **Bổ sung thêm**: mã nhân viên, lương

**Lợi ích**: 
- Không cần viết lại các thuộc tính chung (tên, ngày sinh, địa chỉ)
- Dễ bảo trì: Thay đổi `Person` thì tự động ảnh hưởng đến `Student` và `Employee`
- Code ngắn gọn, dễ hiểu

### Thuật ngữ trong kế thừa

| Thuật ngữ | Tiếng Anh | Ý nghĩa |
|-----------|-----------|---------|
| **Lớp cha** | Parent class, Superclass, Base class | Lớp được kế thừa |
| **Lớp con** | Child class, Subclass, Derived class, Extended class | Lớp kế thừa từ lớp cha |
| **Kế thừa** | Inheritance, Extends | Quan hệ IS-A (là một) |

### Quan hệ IS-A

Kế thừa tạo ra quan hệ **IS-A** (là một):
- `Student` **IS-A** `Person` (Sinh viên là một Người)
- `Employee` **IS-A** `Person` (Nhân viên là một Người)
- `Car` **IS-A** `Vehicle` (Ô tô là một Phương tiện)

## II. Cú pháp kế thừa trong Java

### Từ khóa `extends`

Để kế thừa một lớp, sử dụng từ khóa `extends`:

```java
// Lớp cha (Superclass)
public class Person {
    String name;
    int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void displayInfo() {
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
    }
}

// Lớp con (Subclass) - Kế thừa từ Person
public class Student extends Person {
    String studentId;
    
    public Student(String name, int age, String studentId) {
        super(name, age);  // Gọi constructor của lớp cha
        this.studentId = studentId;
    }
    
    public void displayStudentInfo() {
        displayInfo();  // Sử dụng phương thức của lớp cha
        System.out.println("Mã SV: " + studentId);
    }
}
```

### Ví dụ hoàn chỉnh

```java
// Lớp cha
public class Animal {
    protected String name;  // protected để lớp con có thể truy cập
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ...");
    }
}

// Lớp con - Dog kế thừa từ Animal
public class Dog extends Animal {
    private String breed;  // Thêm thuộc tính riêng
    
    public Dog(String name, int age, String breed) {
        super(name, age);  // Gọi constructor của lớp cha
        this.breed = breed;
    }
    
    // Thêm phương thức riêng
    public void bark() {
        System.out.println(name + " đang sủa: Gâu gâu!");
    }
    
    // Override phương thức của lớp cha (sẽ học ở bài Polymorphism)
    @Override
    public void eat() {
        System.out.println(name + " đang ăn thức ăn cho chó...");
    }
}

// Sử dụng
public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog("Buddy", 3, "Golden Retriever");
        
        // Sử dụng phương thức kế thừa từ Animal
        dog.eat();      // Kế thừa từ Animal
        dog.sleep();    // Kế thừa từ Animal
        
        // Sử dụng phương thức riêng của Dog
        dog.bark();     // Phương thức riêng của Dog
    }
}
```

**Kết quả**:
```
Buddy đang ăn thức ăn cho chó...
Buddy đang ngủ...
Buddy đang sủa: Gâu gâu!
```

## III. Các kiểu kế thừa trong Java

### 1. Single Inheritance (Đơn kế thừa)

Một lớp con chỉ có thể kế thừa từ **một** lớp cha.

```java
public class A {
    // ...
}

public class B extends A {  // B kế thừa từ A
    // ...
}

public class C extends B {  // C kế thừa từ B (và gián tiếp từ A)
    // ...
}
```

**Sơ đồ**:
```
A
 ↓
B
 ↓
C
```

> **Lưu ý quan trọng**: Java **không hỗ trợ multiple inheritance** (kế thừa nhiều lớp cha) cho classes, nhưng hỗ trợ cho interfaces (sẽ học ở bài Abstraction).

### 2. Multilevel Inheritance (Kế thừa nhiều cấp)

Một lớp có thể kế thừa từ một lớp con khác, tạo thành chuỗi kế thừa:

```java
// Lớp cơ sở
public class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    public void start() {
        System.out.println(brand + " khởi động...");
    }
}

// Lớp con của Vehicle
public class Car extends Vehicle {
    private int doors;
    
    public Car(String brand, int doors) {
        super(brand);
        this.doors = doors;
    }
    
    public void drive() {
        System.out.println(brand + " đang chạy...");
    }
}

// Lớp con của Car (gián tiếp kế thừa từ Vehicle)
public class SportsCar extends Car {
    private int maxSpeed;
    
    public SportsCar(String brand, int doors, int maxSpeed) {
        super(brand, doors);
        this.maxSpeed = maxSpeed;
    }
    
    public void race() {
        System.out.println(brand + " đang đua với tốc độ " + maxSpeed + " km/h!");
    }
}
```

**Sơ đồ**:
```
Vehicle
   ↓
  Car
   ↓
SportsCar
```

**Sử dụng**:
```java
SportsCar sportsCar = new SportsCar("Ferrari", 2, 350);
sportsCar.start();   // Kế thừa từ Vehicle
sportsCar.drive();   // Kế thừa từ Car
sportsCar.race();    // Phương thức riêng của SportsCar
```

### 3. Hierarchical Inheritance (Kế thừa thứ bậc)

Nhiều lớp con cùng kế thừa từ một lớp cha:

```java
// Lớp cha
public class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn...");
    }
}

// Lớp con 1
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    public void bark() {
        System.out.println(name + " sủa: Gâu gâu!");
    }
}

// Lớp con 2
public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    public void meow() {
        System.out.println(name + " kêu: Meo meo!");
    }
}

// Lớp con 3
public class Bird extends Animal {
    public Bird(String name) {
        super(name);
    }
    
    public void fly() {
        System.out.println(name + " đang bay...");
    }
}
```

**Sơ đồ**:
```
       Animal
      /  |  \
     /   |   \
   Dog  Cat  Bird
```

## IV. Từ khóa `super`

### `super` là gì?

Từ khóa `super` dùng để:
1. **Gọi constructor của lớp cha**
2. **Truy cập thành viên (fields, methods) của lớp cha**

### 1. Gọi constructor của lớp cha

```java
public class Person {
    protected String name;
    protected int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Constructor của Person được gọi");
    }
}

public class Student extends Person {
    private String studentId;
    
    public Student(String name, int age, String studentId) {
        super(name, age);  // ✅ PHẢI gọi super() đầu tiên
        this.studentId = studentId;
        System.out.println("Constructor của Student được gọi");
    }
}
```

> **Quy tắc**: Lệnh `super()` **phải** là lệnh đầu tiên trong constructor của lớp con (nếu có gọi).

### 2. Truy cập thành viên của lớp cha

```java
public class Animal {
    protected String name = "Animal";
    
    public void eat() {
        System.out.println("Animal đang ăn...");
    }
}

public class Dog extends Animal {
    private String name = "Dog";  // Tên trùng với lớp cha
    
    public void display() {
        System.out.println(name);        // "Dog" - của lớp này
        System.out.println(super.name);  // "Animal" - của lớp cha
        
        eat();        // Gọi phương thức của lớp này (nếu có override)
        super.eat();  // Gọi phương thức của lớp cha
    }
    
    @Override
    public void eat() {
        System.out.println("Dog đang ăn thức ăn cho chó...");
        super.eat();  // Gọi phương thức eat() của lớp cha
    }
}
```

## V. Ví dụ thực tế: Hệ thống quản lý công ty

```java
// Lớp cơ sở: Person
public class Person {
    protected String name;
    protected String address;
    protected String phoneNumber;
    
    public Person(String name, String address, String phoneNumber) {
        this.name = name;
        this.address = address;
        this.phoneNumber = phoneNumber;
    }
    
    public void displayInfo() {
        System.out.println("=== THÔNG TIN ===");
        System.out.println("Tên: " + name);
        System.out.println("Địa chỉ: " + address);
        System.out.println("SĐT: " + phoneNumber);
    }
}

// Lớp con 1: Employee (Nhân viên)
public class Employee extends Person {
    private String employeeId;
    private double salary;
    
    public Employee(String name, String address, String phoneNumber, 
                    String employeeId, double salary) {
        super(name, address, phoneNumber);
        this.employeeId = employeeId;
        this.salary = salary;
    }
    
    public void displayEmployeeInfo() {
        displayInfo();  // Gọi phương thức của lớp cha
        System.out.println("Mã NV: " + employeeId);
        System.out.println("Lương: " + salary);
    }
    
    public double calculateAnnualSalary() {
        return salary * 12;
    }
}

// Lớp con 2: Manager (Quản lý) - kế thừa từ Employee
public class Manager extends Employee {
    private String department;
    private int numberOfEmployees;
    
    public Manager(String name, String address, String phoneNumber,
                   String employeeId, double salary, String department,
                   int numberOfEmployees) {
        super(name, address, phoneNumber, employeeId, salary);
        this.department = department;
        this.numberOfEmployees = numberOfEmployees;
    }
    
    public void displayManagerInfo() {
        displayEmployeeInfo();  // Gọi phương thức của lớp cha (Employee)
        System.out.println("Phòng ban: " + department);
        System.out.println("Số nhân viên: " + numberOfEmployees);
    }
    
    public void conductMeeting() {
        System.out.println(name + " đang họp với " + numberOfEmployees + " nhân viên...");
    }
}

// Sử dụng
public class CompanyManagement {
    public static void main(String[] args) {
        // Tạo đối tượng Employee
        Employee emp = new Employee("Nguyễn Văn A", "Hà Nội", "0901234567",
                                     "EMP001", 10000000);
        emp.displayEmployeeInfo();
        
        System.out.println("\n---\n");
        
        // Tạo đối tượng Manager
        Manager mgr = new Manager("Trần Thị B", "TP.HCM", "0912345678",
                                   "MGR001", 20000000, "Phát triển phần mềm",
                                   10);
        mgr.displayManagerInfo();
        mgr.conductMeeting();
    }
}
```

**Kết quả**:
```
=== THÔNG TIN ===
Tên: Nguyễn Văn A
Địa chỉ: Hà Nội
SĐT: 0901234567
Mã NV: EMP001
Lương: 10000000.0

---

=== THÔNG TIN ===
Tên: Trần Thị B
Địa chỉ: TP.HCM
SĐT: 0912345678
Mã NV: MGR001
Lương: 20000000.0
Phòng ban: Phát triển phần mềm
Số nhân viên: 10
Trần Thị B đang họp với 10 nhân viên...
```

## VI. Những gì lớp con có thể làm

### 1. Sử dụng các thành viên kế thừa

```java
public class Parent {
    protected int value = 10;
    
    public void method1() {
        System.out.println("Method 1 của Parent");
    }
}

public class Child extends Parent {
    public void test() {
        // ✅ Sử dụng field kế thừa
        System.out.println(value);  // 10
        
        // ✅ Sử dụng method kế thừa
        method1();  // "Method 1 của Parent"
    }
}
```

### 2. Thêm thành viên mới

```java
public class Child extends Parent {
    // ✅ Thêm field mới
    private int childValue = 20;
    
    // ✅ Thêm method mới
    public void childMethod() {
        System.out.println("Method riêng của Child");
    }
}
```

### 3. Ghi đè phương thức (Method Overriding)

```java
public class Parent {
    public void display() {
        System.out.println("Display của Parent");
    }
}

public class Child extends Parent {
    @Override  // Annotation để đánh dấu override
    public void display() {
        System.out.println("Display của Child");
    }
}
```

> **Lưu ý**: Method Overriding sẽ được học chi tiết ở bài Polymorphism.

### 4. Gọi constructor của lớp cha

```java
public class Child extends Parent {
    public Child() {
        super();  // Gọi constructor không tham số của Parent
    }
    
    public Child(int value) {
        super(value);  // Gọi constructor có tham số của Parent
    }
}
```

## VII. Access Modifiers và Kế thừa

### Các mức độ truy cập trong kế thừa

| Modifier | Lớp con trong cùng package | Lớp con khác package |
|----------|---------------------------|---------------------|
| `public` | ✅ Có thể truy cập | ✅ Có thể truy cập |
| `protected` | ✅ Có thể truy cập | ✅ Có thể truy cập |
| `default` (package-private) | ✅ Có thể truy cập | ❌ Không thể truy cập |
| `private` | ❌ Không thể truy cập | ❌ Không thể truy cập |

**Ví dụ**:
```java
public class Parent {
    public int publicField = 1;
    protected int protectedField = 2;
    int defaultField = 3;  // default (package-private)
    private int privateField = 4;  // ❌ Lớp con không thể truy cập
    
    public void publicMethod() { }
    protected void protectedMethod() { }
    void defaultMethod() { }
    private void privateMethod() { }  // ❌ Lớp con không thể truy cập
}

public class Child extends Parent {
    public void test() {
        System.out.println(publicField);      // ✅ OK
        System.out.println(protectedField);   // ✅ OK
        System.out.println(defaultField);     // ✅ OK (cùng package)
        // System.out.println(privateField);  // ❌ LỖI!
        
        publicMethod();      // ✅ OK
        protectedMethod();   // ✅ OK
        defaultMethod();     // ✅ OK (cùng package)
        // privateMethod();   // ❌ LỖI!
    }
}
```

## VIII. Lợi ích của tính kế thừa

### 1. Tái sử dụng code (Code Reusability)

- Không cần viết lại code đã có
- Giảm thiểu lỗi do copy-paste

### 2. Dễ bảo trì (Maintainability)

- Thay đổi ở lớp cha tự động ảnh hưởng đến các lớp con
- Sửa lỗi ở một nơi, áp dụng cho tất cả

### 3. Mở rộng dễ dàng (Extensibility)

- Dễ dàng thêm các lớp con mới
- Không cần sửa code cũ

### 4. Tổ chức code tốt hơn

- Phản ánh mối quan hệ thực tế
- Code dễ hiểu, dễ đọc

## IX. Lưu ý quan trọng

### 1. Java không hỗ trợ Multiple Inheritance cho classes

```java
// ❌ KHÔNG THỂ làm điều này!
public class Child extends Parent1, Parent2 {
    // LỖI! Java không cho phép kế thừa nhiều lớp cha
}
```

**Giải pháp**: Sử dụng interfaces (sẽ học ở bài Abstraction)

### 2. Constructor không được kế thừa

```java
public class Parent {
    public Parent(int value) {
        // ...
    }
}

public class Child extends Parent {
    // ❌ Không tự động có constructor Parent(int)
    // Phải tự tạo constructor mới
    public Child(int value) {
        super(value);  // Gọi constructor của Parent
    }
}
```

### 3. Tất cả các lớp đều kế thừa từ Object

```java
public class MyClass {
    // Mặc định: extends Object
}

// Tương đương với:
public class MyClass extends Object {
    // ...
}
```

### 4. Lớp `final` không thể bị kế thừa

```java
public final class FinalClass {
    // ...
}

// ❌ LỖI! Không thể kế thừa từ final class
public class Child extends FinalClass {
    // ...
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu tính kế thừa là gì và tại sao nó quan trọng
- ✅ Nắm được cú pháp sử dụng `extends` và `super`
- ✅ Biết các kiểu kế thừa: Single, Multilevel, Hierarchical
- ✅ Hiểu cách sử dụng `super` để gọi constructor và truy cập thành viên của lớp cha
- ✅ Nắm được các quy tắc về access modifiers trong kế thừa

## Bài tập thực hành

1. **Tạo hệ thống kế thừa cho phương tiện**:
   - Lớp cha: `Vehicle` (phương tiện) với các thuộc tính: brand, model, year
   - Lớp con 1: `Car` (ô tô) - thêm: số cửa
   - Lớp con 2: `Motorcycle` (xe máy) - thêm: dung tích động cơ

2. **Tạo hệ thống kế thừa cho hình học**:
   - Lớp cha: `Shape` (hình) với: color, filled
   - Lớp con 1: `Circle` (hình tròn) - thêm: radius
   - Lớp con 2: `Rectangle` (hình chữ nhật) - thêm: width, height

3. **Tạo hệ thống kế thừa 3 cấp**:
   - `Animal` → `Mammal` → `Dog`
   - Mỗi lớp thêm thuộc tính và phương thức riêng

## Tài liệu tham khảo

- [Oracle Java Tutorial - Inheritance](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)
- [Java Inheritance Examples](https://www.programiz.com/java-programming/inheritance)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
