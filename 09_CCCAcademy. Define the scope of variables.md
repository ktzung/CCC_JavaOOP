# Bài 9: Phạm vi biến (Scope of Variables) trong Java

> **Mục tiêu**: Hiểu được phạm vi (scope) của biến trong Java, phân biệt các loại biến (instance, local, static), và cách sử dụng chúng đúng cách.

## I. Giới thiệu về Phạm vi biến (Scope)

### Scope là gì?

**Scope (Phạm vi)** của biến là **vùng code** trong đó biến có thể được truy cập và sử dụng.

### Tại sao cần hiểu Scope?

Hiểu scope giúp bạn:
- ✅ Biết biến có thể sử dụng ở đâu
- ✅ Tránh lỗi "variable not found"
- ✅ Tổ chức code tốt hơn
- ✅ Tránh xung đột tên biến

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **ngôi nhà**:
- **Căn phòng (Block)** = Vùng code giữa `{ }`
- **Ngôi nhà (Class)** = Toàn bộ class
- **Khu vực chung (Static)** = Dùng chung cho cả khu vực

**Ví dụ**:
- **Biến trong phòng** (local) = Chỉ dùng trong phòng đó
- **Biến trong nhà** (instance) = Dùng được ở mọi phòng trong nhà
- **Biến khu vực chung** (static) = Dùng chung cho cả khu vực

## II. Các loại Scope trong Java

Java có **3 loại scope** chính:

1. **Class-level scope** (Phạm vi lớp) - Instance và Static variables
2. **Method-level scope** (Phạm vi phương thức) - Local variables
3. **Block-level scope** (Phạm vi khối) - Variables trong khối `{ }`

### Sơ đồ tổng quan

```
Class {
    // Class-level scope (Instance variables)
    private int instanceVar;
    private static int staticVar;
    
    Method() {
        // Method-level scope (Local variables)
        int localVar;
        
        {
            // Block-level scope
            int blockVar;
        }
    }
}
```

## III. Class-level Scope (Phạm vi lớp)

### Instance Variables (Biến instance)

**Instance variables** là biến được khai báo **trong class** nhưng **ngoài methods, constructors, và blocks**.

**Đặc điểm**:
- ✅ Thuộc về **từng đối tượng** riêng lẻ
- ✅ Mỗi đối tượng có **một bản sao** riêng
- ✅ Có thể truy cập từ **bất kỳ đâu trong class** (tùy access modifier)
- ✅ Có **giá trị mặc định** (0, null, false)
- ✅ Tồn tại **trong suốt vòng đời đối tượng**
- ✅ Có thể dùng **access modifiers** (public, private, protected)

**Ví dụ**:
```java
public class Student {
    // Instance variables - Class-level scope
    private String name;       // Thuộc về từng đối tượng
    private int age;           // Mỗi Student có age riêng
    private double gpa;        // Mỗi Student có gpa riêng
    
    // Constructor - Có thể truy cập instance variables
    public Student(String name, int age, double gpa) {
        this.name = name;  // ✅ Có thể truy cập
        this.age = age;    // ✅ Có thể truy cập
        this.gpa = gpa;    // ✅ Có thể truy cập
    }
    
    // Method - Có thể truy cập instance variables
    public void displayInfo() {
        System.out.println("Tên: " + name);   // ✅ Có thể truy cập
        System.out.println("Tuổi: " + age);   // ✅ Có thể truy cập
        System.out.println("Điểm TB: " + gpa); // ✅ Có thể truy cập
    }
    
    // Static method - KHÔNG THỂ truy cập instance variables trực tiếp
    public static void staticMethod() {
        // System.out.println(name);  // ❌ LỖI! Không thể truy cập
        // Phải có đối tượng để truy cập:
        Student s = new Student("Test", 0, 0.0);
        System.out.println(s.name);  // ✅ OK (qua đối tượng)
    }
    
    public static void main(String[] args) {
        Student s1 = new Student("Nguyễn Văn A", 20, 8.5);
        Student s2 = new Student("Trần Thị B", 21, 9.0);
        
        // Mỗi đối tượng có giá trị riêng
        s1.displayInfo();  // Tên: Nguyễn Văn A, Tuổi: 20, Điểm TB: 8.5
        s2.displayInfo();  // Tên: Trần Thị B, Tuổi: 21, Điểm TB: 9.0
    }
}
```

### Static Variables (Biến tĩnh)

**Static variables** là biến được khai báo với từ khóa `static` trong class.

**Đặc điểm**:
- ✅ Thuộc về **lớp**, không thuộc về đối tượng
- ✅ Chỉ có **một bản sao** cho cả lớp (dùng chung)
- ✅ Có thể truy cập từ **bất kỳ đâu trong class**
- ✅ Có **giá trị mặc định** (0, null, false)
- ✅ Tồn tại **trong suốt chương trình**
- ✅ Có thể truy cập **qua tên lớp** (không cần đối tượng)

**Ví dụ**:
```java
public class Counter {
    // Instance variable - Mỗi đối tượng có một bản sao
    private int instanceCounter = 0;
    
    // Static variable - Cả lớp dùng chung một bản sao
    private static int staticCounter = 0;
    
    public Counter() {
        instanceCounter++;  // Tăng biến riêng của đối tượng này
        staticCounter++;    // Tăng biến chung của lớp
    }
    
    public void display() {
        System.out.println("Instance: " + instanceCounter + ", Static: " + staticCounter);
    }
    
    public static int getStaticCounter() {
        return staticCounter;  // ✅ Có thể truy cập static variable
    }
    
    public static void main(String[] args) {
        System.out.println("Ban đầu: " + Counter.getStaticCounter());  // 0
        
        Counter c1 = new Counter();
        c1.display();  // Instance: 1, Static: 1
        
        Counter c2 = new Counter();
        c2.display();  // Instance: 1, Static: 2
        
        Counter c3 = new Counter();
        c3.display();  // Instance: 1, Static: 3
        
        // Tất cả đối tượng thấy cùng giá trị static
        System.out.println("Tổng (từ c1): " + c1.getStaticCounter());  // 3
        System.out.println("Tổng (từ c2): " + c2.getStaticCounter());  // 3
        System.out.println("Tổng (từ lớp): " + Counter.getStaticCounter());  // 3
    }
}
```

**Kết quả**:
```
Ban đầu: 0
Instance: 1, Static: 1
Instance: 1, Static: 2
Instance: 1, Static: 3
Tổng (từ c1): 3
Tổng (từ c2): 3
Tổng (từ lớp): 3
```

## IV. Method-level Scope (Phạm vi phương thức)

### Local Variables (Biến cục bộ)

**Local variables** (Biến cục bộ) là biến được khai báo **bên trong** một method, constructor, hoặc block.

**Đặc điểm**:
- ✅ Chỉ tồn tại **trong method/constructor/block** được khai báo
- ✅ **Không có giá trị mặc định** - **phải khởi tạo** trước khi sử dụng
- ✅ **Không thể** dùng access modifiers (public, private, v.v.)
- ✅ Tồn tại **từ khi khai báo đến khi method kết thúc**
- ✅ **Parameters** (tham số) cũng là local variables

### Ví dụ Local Variables

```java
public class LocalVariables {
    // Instance variable
    private String name = "Default";
    
    // Method với local variables
    public void method1(int param) {  // param là local variable
        // Local variable
        int localVar = 10;  // ✅ Phải khởi tạo
        
        // ✅ Có thể truy cập local variable
        System.out.println("Local: " + localVar);
        System.out.println("Param: " + param);
        
        // ✅ Có thể truy cập instance variable
        System.out.println("Instance: " + name);
        
        // localVar và param chỉ tồn tại trong method1
    }
    
    public void method2() {
        // ❌ KHÔNG THỂ truy cập local variable của method1
        // System.out.println(localVar);  // Lỗi!
        
        // Local variable riêng của method2
        int localVar = 20;  // ✅ OK - Tên giống nhưng khác scope
        System.out.println("Local: " + localVar);
    }
    
    public static void main(String[] args) {
        LocalVariables obj = new LocalVariables();
        obj.method1(100);
        obj.method2();
    }
}
```

### Parameters là Local Variables

**Parameters** (Tham số) của method cũng là **local variables**:

```java
public class Parameters {
    public void method(int param1, String param2) {
        // param1 và param2 là local variables
        System.out.println("Param1: " + param1);   // ✅ OK
        System.out.println("Param2: " + param2);   // ✅ OK
        
        // Có thể gán giá trị mới (nhưng không ảnh hưởng đến caller)
        param1 = 999;  // ✅ OK - Chỉ thay đổi local copy
        param2 = "New";  // ✅ OK
    }
    
    public static void main(String[] args) {
        Parameters obj = new Parameters();
        int a = 10;
        String s = "Original";
        
        obj.method(a, s);
        
        // a và s không bị thay đổi
        System.out.println("a: " + a);        // 10 (không đổi)
        System.out.println("s: " + s);        // Original (không đổi)
    }
}
```

### Lưu ý quan trọng về Local Variables

**1. Phải khởi tạo trước khi sử dụng**:
```java
public class LocalVariableInit {
    public void method() {
        int x;  // Khai báo nhưng chưa khởi tạo
        
        // ❌ LỖI: Phải khởi tạo trước khi sử dụng
        // System.out.println(x);  // Lỗi!
        
        x = 10;  // Khởi tạo
        System.out.println(x);  // ✅ OK
    }
}
```

**2. Không có giá trị mặc định**:
```java
public class NoDefaultValue {
    // Instance variable - Có giá trị mặc định
    private int instanceVar;  // 0 (mặc định)
    
    public void method() {
        // Local variable - KHÔNG có giá trị mặc định
        int localVar;  // ❌ LỖI nếu sử dụng trước khi khởi tạo
        
        // System.out.println(localVar);  // Lỗi!
        
        localVar = 10;  // Phải khởi tạo
        System.out.println(localVar);  // ✅ OK
    }
}
```

**3. Không thể dùng access modifiers**:
```java
public class NoAccessModifier {
    public void method() {
        // ❌ LỖI: Local variable không thể dùng access modifier
        // public int x;      // Lỗi!
        // private int y;     // Lỗi!
        // protected int z;   // Lỗi!
        
        // ✅ OK: Không có modifier
        int x = 10;
    }
}
```

## V. Block-level Scope (Phạm vi khối)

### Block-level Scope là gì?

**Block-level scope** là phạm vi được xác định bởi cặp dấu ngoặc nhọn `{ }`.

**Đặc điểm**:
- ✅ Biến chỉ tồn tại **trong khối `{ }`** được khai báo
- ✅ **Không có giá trị mặc định** - Phải khởi tạo trước khi sử dụng
- ✅ **Không thể** truy cập từ bên ngoài khối

### Ví dụ Block-level Scope

```java
public class BlockScope {
    public void method() {
        // Method-level scope
        int methodVar = 10;
        System.out.println("Method var: " + methodVar);  // ✅ OK
        
        // Block 1
        {
            // Block-level scope
            int blockVar1 = 20;
            System.out.println("Block 1 var: " + blockVar1);  // ✅ OK
            System.out.println("Method var: " + methodVar);   // ✅ OK (truy cập từ ngoài vào)
        }
        
        // ❌ KHÔNG THỂ truy cập blockVar1 từ ngoài block
        // System.out.println(blockVar1);  // Lỗi!
        
        // Block 2
        {
            // Block-level scope
            int blockVar2 = 30;
            System.out.println("Block 2 var: " + blockVar2);  // ✅ OK
            
            // ❌ KHÔNG THỂ truy cập blockVar1 từ block khác
            // System.out.println(blockVar1);  // Lỗi!
        }
    }
    
    public static void main(String[] args) {
        BlockScope obj = new BlockScope();
        obj.method();
    }
}
```

### Block Scope trong vòng lặp và điều kiện

```java
public class LoopBlockScope {
    public static void main(String[] args) {
        // For loop - Biến trong loop chỉ tồn tại trong loop
        for (int i = 0; i < 5; i++) {
            System.out.println("i: " + i);  // ✅ OK
        }
        // ❌ KHÔNG THỂ truy cập i từ ngoài loop
        // System.out.println(i);  // Lỗi!
        
        // If statement - Biến trong block chỉ tồn tại trong block
        if (true) {
            int ifVar = 10;
            System.out.println("If var: " + ifVar);  // ✅ OK
        }
        // ❌ KHÔNG THỂ truy cập ifVar từ ngoài if
        // System.out.println(ifVar);  // Lỗi!
        
        // While loop
        int j = 0;
        while (j < 5) {
            int whileVar = j * 2;
            System.out.println("While var: " + whileVar);  // ✅ OK
            j++;
        }
        // ❌ KHÔNG THỂ truy cập whileVar từ ngoài while
        // System.out.println(whileVar);  // Lỗi!
    }
}
```

## VI. Variable Shadowing (Ẩn biến)

### Variable Shadowing là gì?

**Variable Shadowing** (Ẩn biến) xảy ra khi biến trong scope nhỏ hơn **che giấu** (hide/shadow) biến có cùng tên trong scope lớn hơn.

### Ví dụ

```java
public class VariableShadowing {
    // Instance variable
    private String name = "Instance Name";
    
    public void method() {
        // Local variable - Shadow instance variable
        String name = "Local Name";  // Che giấu instance variable
        
        System.out.println("Local name: " + name);      // "Local Name" (local)
        System.out.println("Instance name: " + this.name);  // "Instance Name" (instance)
    }
    
    public void method2() {
        // Không có local variable → Sử dụng instance variable
        System.out.println("Name: " + name);  // "Instance Name"
    }
    
    public static void main(String[] args) {
        VariableShadowing obj = new VariableShadowing();
        obj.method();
        System.out.println();
        obj.method2();
    }
}
```

**Kết quả**:
```
Local name: Local Name
Instance name: Instance Name

Name: Instance Name
```

### Khi nào xảy ra Shadowing?

1. **Local variable shadowing instance variable**:
```java
public class ShadowExample {
    private int value = 10;  // Instance variable
    
    public void method() {
        int value = 20;  // Local variable che giấu instance variable
        
        System.out.println(value);       // 20 (local)
        System.out.println(this.value);  // 10 (instance - dùng this)
    }
}
```

2. **Block variable shadowing method variable**:
```java
public class BlockShadow {
    public void method() {
        int x = 10;  // Method variable
        
        {
            int x = 20;  // ❌ LỖI! Không thể shadow trong cùng scope
            System.out.println(x);
        }
    }
}
```

**Lưu ý**: Không thể shadow trong **cùng scope**, chỉ có thể shadow từ **scope lớn hơn**.

## VII. So sánh các loại biến

### Bảng so sánh

| Đặc điểm | Instance Variable | Static Variable | Local Variable | Block Variable |
|----------|------------------|-----------------|----------------|----------------|
| **Khai báo** | Trong class, ngoài method | Trong class, ngoài method, có `static` | Trong method | Trong block `{ }` |
| **Thuộc về** | Đối tượng | Lớp | Method | Block |
| **Số lượng** | 1 cho mỗi đối tượng | 1 cho cả lớp | 1 cho mỗi lần gọi method | 1 cho mỗi lần vào block |
| **Giá trị mặc định** | ✅ Có (0, null, false) | ✅ Có (0, null, false) | ❌ Không (phải khởi tạo) | ❌ Không (phải khởi tạo) |
| **Access modifiers** | ✅ Có thể dùng | ✅ Có thể dùng | ❌ Không thể | ❌ Không thể |
| **Tồn tại** | Khi đối tượng được tạo đến khi bị GC | Khi lớp được nạp đến khi chương trình kết thúc | Khi method được gọi đến khi method kết thúc | Khi vào block đến khi ra khỏi block |
| **Truy cập từ static method** | ❌ Không (trừ qua đối tượng) | ✅ Có | ✅ Có (nếu trong method đó) | ✅ Có (nếu trong block đó) |

### Ví dụ tổng hợp

```java
public class ScopeExample {
    // Instance variable
    private int instanceVar = 1;
    
    // Static variable
    private static int staticVar = 10;
    
    public void instanceMethod(int param) {  // param là local variable
        // Local variable
        int localVar = 100;
        
        System.out.println("Instance var: " + instanceVar);   // ✅ OK
        System.out.println("Static var: " + staticVar);       // ✅ OK
        System.out.println("Local var: " + localVar);        // ✅ OK
        System.out.println("Param: " + param);               // ✅ OK
        
        // Block scope
        {
            int blockVar = 200;
            System.out.println("Block var: " + blockVar);     // ✅ OK
            System.out.println("Local var (từ block): " + localVar);  // ✅ OK
        }
        
        // ❌ KHÔNG THỂ: System.out.println(blockVar);  // Lỗi!
    }
    
    public static void staticMethod() {
        // ❌ KHÔNG THỂ: System.out.println(instanceVar);  // Lỗi!
        
        // ✅ CÓ THỂ: Truy cập static variable
        System.out.println("Static var: " + staticVar);
        
        // ✅ CÓ THỂ: Truy cập qua đối tượng
        ScopeExample obj = new ScopeExample();
        System.out.println("Instance var (qua obj): " + obj.instanceVar);
        
        // Local variable trong static method
        int localVar = 300;
        System.out.println("Local var: " + localVar);
    }
    
    public static void main(String[] args) {
        ScopeExample obj = new ScopeExample();
        obj.instanceMethod(50);
        System.out.println();
        staticMethod();
    }
}
```

## VIII. Lưu ý quan trọng

### 1. Local variables phải khởi tạo

```java
public class InitializationRule {
    // Instance variable - Có giá trị mặc định
    private int instanceVar;  // 0 (mặc định)
    
    public void method() {
        // Local variable - PHẢI khởi tạo
        int localVar;  // ❌ LỖI nếu sử dụng trước khi khởi tạo
        
        // System.out.println(localVar);  // Lỗi!
        
        localVar = 10;  // ✅ Phải khởi tạo trước
        System.out.println(localVar);  // OK
    }
}
```

### 2. Không thể truy cập từ scope nhỏ ra scope lớn

```java
public class ScopeAccess {
    public void method() {
        int methodVar = 10;
        
        {
            int blockVar = 20;
            
            // ✅ Có thể truy cập từ block ra method (scope lớn hơn)
            System.out.println(methodVar);  // OK
        }
        
        // ❌ KHÔNG THỂ truy cập từ method vào block (scope nhỏ hơn)
        // System.out.println(blockVar);  // Lỗi!
    }
}
```

### 3. Tên biến có thể trùng (nếu khác scope)

```java
public class SameNameDifferentScope {
    // Instance variable
    private int value = 1;
    
    public void method1() {
        // Local variable (khác scope)
        int value = 2;  // ✅ OK - Shadow instance variable
        
        System.out.println("Local value: " + value);       // 2
        System.out.println("Instance value: " + this.value);  // 1
    }
    
    public void method2() {
        // Local variable riêng (khác method)
        int value = 3;  // ✅ OK - Khác scope với method1
        
        System.out.println("Method2 value: " + value);  // 3
    }
}
```

## IX. Ví dụ thực tế

### Ví dụ 1: Quản lý điểm sinh viên

```java
public class StudentManager {
    // Static variable - Đếm tổng số sinh viên (dùng chung)
    private static int totalStudents = 0;
    
    // Instance variables - Thông tin riêng của từng sinh viên
    private int studentId;
    private String name;
    private double gpa;
    
    // Constructor
    public StudentManager(String name, double gpa) {
        this.studentId = ++totalStudents;  // Tự động tạo ID
        this.name = name;
        this.gpa = gpa;
    }
    
    // Method với local variables
    public void updateGpa(double newGpa) {
        // Local variable - Validate
        double validGpa = newGpa;  // Local variable
        
        if (validGpa < 0) {
            validGpa = 0;
        } else if (validGpa > 10) {
            validGpa = 10;
        }
        
        // Block scope - Tính toán xếp loại
        {
            String grade;  // Block variable
            if (validGpa >= 9) {
                grade = "Xuất sắc";
            } else if (validGpa >= 8) {
                grade = "Giỏi";
            } else if (validGpa >= 7) {
                grade = "Khá";
            } else {
                grade = "Trung bình";
            }
            System.out.println("Xếp loại: " + grade);
        }
        
        this.gpa = validGpa;  // Cập nhật instance variable
    }
    
    // Static method - Chỉ truy cập static variable
    public static int getTotalStudents() {
        return totalStudents;  // ✅ OK - Static variable
    }
    
    // Instance method - Truy cập cả instance và static
    public void displayInfo() {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("ID: " + studentId);          // Instance variable
        System.out.println("Tên: " + name);              // Instance variable
        System.out.println("Điểm TB: " + gpa);          // Instance variable
        System.out.println("Tổng số SV: " + totalStudents);  // Static variable
    }
    
    public static void main(String[] args) {
        StudentManager s1 = new StudentManager("Nguyễn Văn A", 8.5);
        StudentManager s2 = new StudentManager("Trần Thị B", 9.0);
        
        System.out.println("Tổng số sinh viên: " + StudentManager.getTotalStudents());
        System.out.println();
        
        s1.displayInfo();
        System.out.println();
        s2.displayInfo();
        
        s1.updateGpa(9.5);
        s1.displayInfo();
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu scope là gì và tại sao nó quan trọng
- ✅ Nắm được 3 loại scope: Class-level, Method-level, Block-level
- ✅ Phân biệt được instance variables, static variables, và local variables
- ✅ Hiểu về variable shadowing
- ✅ Nắm được các quy tắc và lưu ý về scope
- ✅ Áp dụng scope vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo class với các loại biến**:
   - Instance variables: name, age
   - Static variable: totalCount
   - Local variables trong methods
   - Block variables trong if/for

2. **Thực hành variable shadowing**:
   - Tạo instance variable và local variable cùng tên
   - Sử dụng `this` để phân biệt

3. **Tạo chương trình quản lý**:
   - Sử dụng static variable để đếm tổng số
   - Sử dụng instance variables để lưu thông tin riêng
   - Sử dụng local variables để xử lý logic

## Tài liệu tham khảo

- [Oracle Java Tutorial - Variables](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html)
- [Java Variable Scope](https://www.javatpoint.com/variable-scope-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
