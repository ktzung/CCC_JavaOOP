# Bài 8: Từ khóa `static` trong Java

> **Mục tiêu**: Hiểu được từ khóa `static` là gì, cách sử dụng static cho variables, methods, blocks, và khi nào nên sử dụng static.

## I. Giới thiệu về từ khóa `static`

### `static` là gì?

Từ khóa **`static`** trong Java được sử dụng để đánh dấu một thành phần (variable, method, block, class) **thuộc về lớp** (class) thay vì **thuộc về đối tượng** (instance) của lớp đó.

### Đặc điểm của `static`

**`static` có nghĩa là**:
- Thành phần đó **thuộc về lớp**, không thuộc về bất kỳ đối tượng cụ thể nào
- Có thể truy cập **trực tiếp qua tên lớp**, không cần tạo đối tượng
- **Chỉ có một bản sao** cho tất cả các đối tượng (chia sẻ chung)

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một lớp học:

- **Non-static** (Instance): 
  - Tên học sinh, tuổi của học sinh → Mỗi học sinh có tên, tuổi riêng
  
- **Static** (Class):
  - Tên trường, địa chỉ trường → Tất cả học sinh cùng học một trường
  - Số lượng học sinh trong lớp → Giá trị chung cho cả lớp

**Tương tự trong Java**:
- **Instance variables/methods**: Thuộc về từng đối tượng riêng lẻ
- **Static variables/methods**: Thuộc về lớp, dùng chung cho tất cả đối tượng

## II. Static Variables (Biến tĩnh)

### Biến static là gì?

**Static variable** (Biến tĩnh) là biến được khai báo với từ khóa `static`, thuộc về **lớp** chứ không thuộc về bất kỳ đối tượng nào.

### Đặc điểm của Static Variables

1. **Chỉ có một bản sao**: Dù tạo bao nhiêu đối tượng, chỉ có **một biến static** duy nhất
2. **Chia sẻ chung**: Tất cả đối tượng cùng chia sẻ một biến static
3. **Tồn tại trong suốt chương trình**: Được tạo khi lớp được nạp, tồn tại đến khi chương trình kết thúc
4. **Giá trị mặc định**: Có giá trị mặc định (0, null, false) tương tự instance variables

### Ví dụ minh họa

```java
public class Counter {
    // Static variable - Dùng chung cho tất cả đối tượng
    private static int count = 0;  // Đếm số đối tượng đã được tạo
    
    // Instance variable - Riêng cho mỗi đối tượng
    private String name;
    
    public Counter(String name) {
        this.name = name;
        count++;  // Tăng biến static mỗi khi tạo đối tượng
    }
    
    // Static method để lấy giá trị static variable
    public static int getCount() {
        return count;
    }
    
    public String getName() {
        return name;
    }
    
    public static void main(String[] args) {
        System.out.println("Ban đầu: " + Counter.getCount());  // 0
        
        Counter c1 = new Counter("Counter 1");
        System.out.println("Sau khi tạo c1: " + Counter.getCount());  // 1
        
        Counter c2 = new Counter("Counter 2");
        System.out.println("Sau khi tạo c2: " + Counter.getCount());  // 2
        
        Counter c3 = new Counter("Counter 3");
        System.out.println("Sau khi tạo c3: " + Counter.getCount());  // 3
        
        // Tất cả đối tượng đều thấy cùng giá trị
        System.out.println("Từ c1: " + c1.getCount());  // 3
        System.out.println("Từ c2: " + c2.getCount());  // 3
        System.out.println("Từ c3: " + c3.getCount());  // 3
    }
}
```

**Kết quả**:
```
Ban đầu: 0
Sau khi tạo c1: 1
Sau khi tạo c2: 2
Sau khi tạo c3: 3
Từ c1: 3
Từ c2: 3
Từ c3: 3
```

**Giải thích**:
- Biến `count` là **static** → Chỉ có **một bản sao** duy nhất
- Mỗi khi tạo đối tượng mới, `count` tăng lên
- Tất cả đối tượng đều thấy cùng giá trị `count = 3`

### So sánh Static và Non-Static Variables

```java
public class CompareStatic {
    // Instance variable - Mỗi đối tượng có một bản sao riêng
    private int instanceVar = 0;
    
    // Static variable - Tất cả đối tượng chia sẻ một bản sao
    private static int staticVar = 0;
    
    public void increment() {
        instanceVar++;   // Tăng biến riêng của đối tượng này
        staticVar++;     // Tăng biến chung của lớp
    }
    
    public void display() {
        System.out.println("Instance: " + instanceVar + ", Static: " + staticVar);
    }
    
    public static void main(String[] args) {
        CompareStatic obj1 = new CompareStatic();
        CompareStatic obj2 = new CompareStatic();
        CompareStatic obj3 = new CompareStatic();
        
        obj1.increment();
        obj1.increment();
        obj1.display();  // Instance: 2, Static: 2
        
        obj2.increment();
        obj2.display();  // Instance: 1, Static: 3
        
        obj3.increment();
        obj3.increment();
        obj3.increment();
        obj3.display();  // Instance: 3, Static: 6
        
        // Tất cả đối tượng thấy cùng giá trị staticVar
        obj1.display();  // Instance: 2, Static: 6
        obj2.display();  // Instance: 1, Static: 6
    }
}
```

## III. Static Methods (Phương thức tĩnh)

### Phương thức static là gì?

**Static method** (Phương thức tĩnh) là phương thức được khai báo với từ khóa `static`, thuộc về **lớp** chứ không thuộc về đối tượng.

### Đặc điểm của Static Methods

1. **Thuộc về lớp**: Không cần tạo đối tượng để gọi
2. **Truy cập trực tiếp**: Gọi qua tên lớp: `ClassName.methodName()`
3. **Không thể truy cập instance members**: Không thể truy cập non-static variables/methods trực tiếp
4. **Không thể dùng `this` và `super`**: Vì không có instance

### Cách gọi Static Methods

**Cách 1: Qua tên lớp** (Khuyến nghị)
```java
public class MathUtils {
    public static int add(int a, int b) {
        return a + b;
    }
    
    public static double calculateCircleArea(double radius) {
        return Math.PI * radius * radius;
    }
}

public class Test {
    public static void main(String[] args) {
        // Gọi qua tên lớp - ✅ Khuyến nghị
        int sum = MathUtils.add(10, 20);
        double area = MathUtils.calculateCircleArea(5.0);
        
        System.out.println("Sum: " + sum);    // 30
        System.out.println("Area: " + area);  // 78.539...
    }
}
```

**Cách 2: Qua đối tượng** (Không khuyến nghị)
```java
public class Test {
    public static void main(String[] args) {
        MathUtils utils = new MathUtils();
        
        // ⚠️ Có thể nhưng không khuyến nghị
        int sum = utils.add(10, 20);
        
        // ✅ Nên dùng cách này
        int sum2 = MathUtils.add(10, 20);
    }
}
```

### Hạn chế của Static Methods

**Static methods KHÔNG THỂ**:
1. ❌ Truy cập non-static variables/methods trực tiếp
2. ❌ Sử dụng `this` và `super`
3. ❌ Override (sẽ học ở bài Polymorphism)

**Ví dụ lỗi**:
```java
public class ErrorExample {
    private int instanceVar = 10;  // Non-static variable
    
    // ❌ LỖI: Static method không thể truy cập instance variable
    public static void staticMethod() {
        // System.out.println(instanceVar);  // Lỗi!
    }
    
    // ✅ OK: Instance method có thể truy cập
    public void instanceMethod() {
        System.out.println(instanceVar);  // OK
    }
}
```

**Cách sửa**:
```java
public class CorrectExample {
    private int instanceVar = 10;
    
    public static void staticMethod() {
        // Cách 1: Truyền đối tượng vào
        CorrectExample obj = new CorrectExample();
        System.out.println(obj.instanceVar);  // ✅ OK
        
        // Cách 2: Truyền giá trị vào như tham số
        // (tùy trường hợp)
    }
}
```

### Khi nào sử dụng Static Methods?

**Sử dụng static methods khi**:
- ✅ Phương thức không phụ thuộc vào trạng thái đối tượng (không cần instance variables)
- ✅ Phương thức tiện ích (utility methods) - như các phương thức trong lớp `Math`
- ✅ Phương thức chỉ xử lý tham số, không cần dữ liệu từ đối tượng

**Ví dụ**:
```java
public class MathUtils {
    // ✅ Tốt - Không cần dữ liệu từ đối tượng
    public static int max(int a, int b) {
        return a > b ? a : b;
    }
    
    public static double calculateArea(double width, double height) {
        return width * height;
    }
    
    // ❌ Không tốt - Cần dữ liệu từ đối tượng
    // public static void displayInfo() {
    //     System.out.println(name);  // Không có name ở đây!
    // }
}
```

### Ví dụ: Lớp Math trong Java

Lớp `Math` là ví dụ điển hình về static methods:

```java
public class MathExamples {
    public static void main(String[] args) {
        // Tất cả đều là static methods
        double max = Math.max(10.5, 20.3);        // 20.3
        double min = Math.min(10.5, 20.3);        // 10.5
        double pow = Math.pow(2, 3);              // 8.0
        double sqrt = Math.sqrt(16);              // 4.0
        double abs = Math.abs(-10);               // 10
        double round = Math.round(3.7);           // 4.0
        
        // Static constants
        double pi = Math.PI;                      // 3.14159...
        double e = Math.E;                        // 2.71828...
        
        System.out.println("Max: " + max);
        System.out.println("Min: " + min);
        System.out.println("Pi: " + pi);
    }
}
```

## IV. Static Blocks (Khối tĩnh)

### Static Block là gì?

**Static block** (Khối tĩnh) là khối code được đánh dấu bằng `static`, được thực thi **một lần duy nhất** khi lớp được nạp vào bộ nhớ, **trước** khi phương thức `main()` được gọi.

### Đặc điểm của Static Blocks

1. **Chạy một lần duy nhất**: Chỉ chạy khi lớp được nạp
2. **Chạy trước main()**: Được thực thi trước phương thức `main()`
3. **Có thể có nhiều static blocks**: Nếu có nhiều static blocks, chúng chạy theo thứ tự
4. **Dùng để khởi tạo**: Thường dùng để khởi tạo static variables

### Ví dụ

```java
public class StaticBlockExample {
    // Static variable
    private static String message;
    private static int number;
    
    // Static block 1
    static {
        System.out.println("Static block 1 được thực thi");
        message = "Xin chào từ static block!";
    }
    
    // Static block 2
    static {
        System.out.println("Static block 2 được thực thi");
        number = 100;
    }
    
    // Constructor
    public StaticBlockExample() {
        System.out.println("Constructor được gọi");
    }
    
    public static void main(String[] args) {
        System.out.println("Main method được thực thi");
        System.out.println("Message: " + message);
        System.out.println("Number: " + number);
        
        // Tạo đối tượng
        StaticBlockExample obj = new StaticBlockExample();
    }
}
```

**Kết quả**:
```
Static block 1 được thực thi
Static block 2 được thực thi
Main method được thực thi
Message: Xin chào từ static block!
Number: 100
Constructor được gọi
```

**Thứ tự thực thi**:
1. Static blocks (theo thứ tự)
2. Main method
3. Constructor (khi tạo đối tượng)

### Sử dụng Static Block để khởi tạo phức tạp

```java
import java.util.ArrayList;
import java.util.List;

public class StaticInitialization {
    // Static variable cần khởi tạo phức tạp
    private static List<String> validCodes;
    
    // Static block để khởi tạo
    static {
        validCodes = new ArrayList<>();
        validCodes.add("VIP");
        validCodes.add("GOLD");
        validCodes.add("SILVER");
        validCodes.add("STANDARD");
        System.out.println("Đã khởi tạo " + validCodes.size() + " mã hợp lệ");
    }
    
    public static boolean isValidCode(String code) {
        return validCodes.contains(code);
    }
    
    public static void main(String[] args) {
        System.out.println("VIP hợp lệ? " + isValidCode("VIP"));        // true
        System.out.println("INVALID hợp lệ? " + isValidCode("INVALID")); // false
    }
}
```

## V. Static Nested Classes (Lớp lồng nhau tĩnh)

### Static Nested Class là gì?

**Static nested class** là một lớp được khai báo bên trong một lớp khác với từ khóa `static`.

### Đặc điểm

- Có thể truy cập **chỉ static members** của lớp ngoài
- Có thể tạo đối tượng mà **không cần** đối tượng của lớp ngoài

### Ví dụ

```java
public class OuterClass {
    private static String staticField = "Static field";
    private String instanceField = "Instance field";
    
    // Static nested class
    public static class NestedClass {
        public void display() {
            // ✅ Có thể truy cập static field
            System.out.println("Static: " + staticField);
            
            // ❌ KHÔNG THỂ truy cập instance field
            // System.out.println("Instance: " + instanceField);  // Lỗi!
        }
    }
    
    // Instance method
    public void instanceMethod() {
        // ✅ Có thể tạo đối tượng nested class
        NestedClass nested = new NestedClass();
        nested.display();
    }
    
    public static void main(String[] args) {
        // ✅ Tạo đối tượng nested class mà không cần OuterClass
        OuterClass.NestedClass nested = new OuterClass.NestedClass();
        nested.display();
        
        // Hoặc
        NestedClass nested2 = new NestedClass();
        nested2.display();
    }
}
```

> **Lưu ý**: Static nested classes sẽ được học chi tiết hơn ở các bài nâng cao.

## VI. Static Import (Java 5+)

### Static Import là gì?

**Static import** cho phép import các thành viên static (static members) của một lớp để sử dụng trực tiếp mà không cần tên lớp.

### Cú pháp

```java
import static package.ClassName.staticMember;
import static package.ClassName.*;  // Import tất cả static members
```

### Ví dụ

**Không dùng static import**:
```java
import java.lang.Math;

public class WithoutStaticImport {
    public static void main(String[] args) {
        double max = Math.max(10, 20);
        double pow = Math.pow(2, 3);
        double pi = Math.PI;
        
        System.out.println("Max: " + max);
        System.out.println("Pow: " + pow);
        System.out.println("Pi: " + pi);
    }
}
```

**Dùng static import**:
```java
import static java.lang.Math.*;
import static java.lang.System.out;

public class WithStaticImport {
    public static void main(String[] args) {
        // Không cần Math. nữa
        double max = max(10, 20);      // Thay vì Math.max()
        double pow = pow(2, 3);         // Thay vì Math.pow()
        double pi = PI;                 // Thay vì Math.PI
        
        // Không cần System. nữa
        out.println("Max: " + max);     // Thay vì System.out.println()
        out.println("Pow: " + pow);
        out.println("Pi: " + pi);
    }
}
```

**Lưu ý**:
- ⚠️ Có thể gây nhầm lẫn nếu có nhiều phương thức cùng tên
- ✅ Chỉ nên dùng khi rõ ràng và không gây nhầm lẫn

**Ví dụ có thể gây nhầm lẫn**:
```java
import static java.lang.Math.*;
import static java.lang.Integer.*;

public class Confusing {
    public static void main(String[] args) {
        // ❌ Nhầm lẫn: max() từ Math hay Integer?
        // int result = max(10, 20);  // Lỗi ambiguous!
        
        // ✅ Phải chỉ rõ
        double result1 = Math.max(10.0, 20.0);
        int result2 = Integer.max(10, 20);
    }
}
```

## VII. So sánh Static và Non-Static

### Bảng so sánh

| Đặc điểm | Static | Non-Static (Instance) |
|----------|--------|----------------------|
| **Thuộc về** | Class | Object |
| **Số lượng** | 1 bản sao cho cả lớp | 1 bản sao cho mỗi đối tượng |
| **Truy cập** | Qua tên lớp | Qua đối tượng |
| **Tồn tại** | Khi lớp được nạp | Khi đối tượng được tạo |
| **Có thể truy cập static?** | ✅ Có | ✅ Có |
| **Có thể truy cập non-static?** | ❌ Không (trừ khi có đối tượng) | ✅ Có |
| **Có thể dùng `this`?** | ❌ Không | ✅ Có |
| **Có thể dùng `super`?** | ❌ Không | ✅ Có |

### Ví dụ tổng hợp

```java
public class StaticVsInstance {
    // Static variable
    private static int staticCounter = 0;
    
    // Instance variable
    private int instanceCounter = 0;
    private String name;
    
    // Constructor
    public StaticVsInstance(String name) {
        this.name = name;
        staticCounter++;      // Tăng biến static chung
        instanceCounter++;    // Tăng biến instance riêng
    }
    
    // Static method
    public static int getStaticCounter() {
        return staticCounter;  // ✅ Có thể truy cập static variable
        
        // ❌ KHÔNG THỂ: return instanceCounter;  // Không có instance
        // ❌ KHÔNG THỂ: return this.name;        // Không có this
    }
    
    // Instance method
    public int getInstanceCounter() {
        return instanceCounter;  // ✅ Có thể truy cập instance variable
    }
    
    public static void staticDisplay() {
        // ✅ Có thể gọi static method
        System.out.println("Static counter: " + getStaticCounter());
        
        // ❌ KHÔNG THỂ: System.out.println(name);  // Không có instance
    }
    
    public void instanceDisplay() {
        // ✅ Có thể truy cập cả static và instance
        System.out.println("Name: " + name);
        System.out.println("Instance counter: " + instanceCounter);
        System.out.println("Static counter: " + staticCounter);  // ✅ OK
    }
    
    public static void main(String[] args) {
        // Gọi static method
        StaticVsInstance.staticDisplay();  // Static counter: 0
        
        // Tạo đối tượng
        StaticVsInstance obj1 = new StaticVsInstance("Object 1");
        StaticVsInstance obj2 = new StaticVsInstance("Object 2");
        
        // Kiểm tra
        System.out.println("Static counter: " + StaticVsInstance.getStaticCounter());  // 2 (chung)
        System.out.println("Obj1 instance counter: " + obj1.getInstanceCounter());      // 1 (riêng)
        System.out.println("Obj2 instance counter: " + obj2.getInstanceCounter());      // 1 (riêng)
        
        obj1.instanceDisplay();
        obj2.instanceDisplay();
    }
}
```

## VIII. Ví dụ thực tế

### Ví dụ 1: Quản lý số lượng sản phẩm

```java
public class Product {
    // Static variable - Đếm tổng số sản phẩm
    private static int totalProducts = 0;
    
    // Instance variables
    private int productId;
    private String name;
    private double price;
    
    // Constructor
    public Product(String name, double price) {
        this.productId = ++totalProducts;  // Tự động tạo ID
        this.name = name;
        this.price = price;
    }
    
    // Static method - Lấy tổng số sản phẩm
    public static int getTotalProducts() {
        return totalProducts;
    }
    
    // Instance methods
    public int getProductId() {
        return productId;
    }
    
    public String getName() {
        return name;
    }
    
    public double getPrice() {
        return price;
    }
    
    public void displayInfo() {
        System.out.println("ID: " + productId + ", Tên: " + name + ", Giá: " + price);
    }
    
    public static void main(String[] args) {
        System.out.println("Tổng số sản phẩm: " + Product.getTotalProducts());  // 0
        
        Product p1 = new Product("Laptop", 15000000);
        Product p2 = new Product("Mouse", 500000);
        Product p3 = new Product("Keyboard", 1000000);
        
        System.out.println("\nTổng số sản phẩm: " + Product.getTotalProducts());  // 3
        
        p1.displayInfo();
        p2.displayInfo();
        p3.displayInfo();
    }
}
```

**Kết quả**:
```
Tổng số sản phẩm: 0

Tổng số sản phẩm: 3
ID: 1, Tên: Laptop, Giá: 15000000.0
ID: 2, Tên: Mouse, Giá: 500000.0
ID: 3, Tên: Keyboard, Giá: 1000000.0
```

### Ví dụ 2: Lớp tiện ích (Utility Class)

```java
public class StringUtils {
    // Private constructor để ngăn tạo đối tượng
    private StringUtils() {
        throw new AssertionError("Cannot instantiate utility class");
    }
    
    // Static methods - Tiện ích
    public static boolean isEmpty(String str) {
        return str == null || str.trim().isEmpty();
    }
    
    public static boolean isEmail(String email) {
        return email != null && email.matches("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$");
    }
    
    public static String capitalize(String str) {
        if (isEmpty(str)) {
            return str;
        }
        return str.substring(0, 1).toUpperCase() + str.substring(1).toLowerCase();
    }
    
    public static String reverse(String str) {
        if (str == null) {
            return null;
        }
        return new StringBuilder(str).reverse().toString();
    }
    
    public static void main(String[] args) {
        System.out.println(isEmpty(""));           // true
        System.out.println(isEmpty("  "));         // true
        System.out.println(isEmpty("Hello"));      // false
        
        System.out.println(isEmail("test@example.com"));    // true
        System.out.println(isEmail("invalid.email"));       // false
        
        System.out.println(capitalize("hello"));   // Hello
        System.out.println(capitalize("WORLD"));   // World
        
        System.out.println(reverse("Java"));       // avaJ
    }
}
```

## IX. Lưu ý quan trọng

### 1. Static không thể override

```java
public class Parent {
    public static void display() {
        System.out.println("Parent");
    }
}

public class Child extends Parent {
    public static void display() {  // Không phải override, mà là hide
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent.display();           // Parent
        Child.display();            // Child
        
        Parent p = new Child();
        p.display();                // Parent (không phải Child!)
    }
}
```

> **Lưu ý**: Static methods không thể override, chỉ có thể **hide** (ẩn).

### 2. Static không thể abstract

```java
// ❌ SAI: Static method không thể abstract
public abstract class Example {
    // public static abstract void method();  // Lỗi!
}
```

### 3. Static trong Main method

Phương thức `main()` phải là `static` vì JVM gọi nó trước khi tạo bất kỳ đối tượng nào:

```java
public class MainMethod {
    // ✅ Phải là static
    public static void main(String[] args) {
        // Code của chương trình
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu từ khóa `static` là gì và tại sao nó quan trọng
- ✅ Phân biệt được static variables và instance variables
- ✅ Nắm được static methods và cách sử dụng
- ✅ Hiểu static blocks và khi nào dùng chúng
- ✅ Biết về static nested classes và static import
- ✅ Nắm được các hạn chế và lưu ý khi sử dụng static

## Bài tập thực hành

1. **Tạo lớp `Student` với static counter**:
   - Đếm tổng số sinh viên đã tạo
   - Mỗi sinh viên có ID tự động tăng
   - Static method để lấy tổng số sinh viên

2. **Tạo lớp tiện ích `ArrayUtils`**:
   - Static methods: `max()`, `min()`, `average()`, `sum()`
   - Tất cả đều static, không cần tạo đối tượng

3. **Tạo lớp `Config` với static blocks**:
   - Static variables: databaseUrl, apiKey
   - Static blocks để khởi tạo các giá trị này
   - Static methods để lấy các giá trị

## Tài liệu tham khảo

- [Oracle Java Tutorial - Static Members](https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html)
- [Java Static Keyword](https://www.javatpoint.com/static-keyword-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
