# Bài 26: Lambda Expressions - Tổng quan

> **Mục tiêu**: Hiểu được Lambda Expressions là gì, cú pháp cơ bản, Functional Interfaces, và cách sử dụng Lambda trong Java 8+.

## I. Giới thiệu về Lambda Expressions

### Lambda Expressions là gì?

**Lambda Expressions** (Biểu thức Lambda) là một tính năng mới quan trọng trong **Java 8**. Lambda expressions giống như **anonymous methods** (phương thức vô danh) được biểu diễn dưới dạng biểu thức.

### Tại sao cần Lambda?

**Vấn đề trước Java 8**:
- Code dài dòng khi sử dụng **anonymous inner classes**
- Khó đọc và khó hiểu
- Nhiều boilerplate code (code lặp lại không cần thiết)

**Giải pháp: Lambda Expressions**:
- ✅ **Ngắn gọn hơn**: Code ngắn gọn và dễ đọc
- ✅ **Dễ hiểu hơn**: Tập trung vào logic, không phải cú pháp
- ✅ **Functional programming**: Hỗ trợ lập trình hàm

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **máy tính**:

- **Anonymous Inner Class** = Viết một bản hướng dẫn dài dòng để máy tính thực hiện
- **Lambda Expression** = Nói ngắn gọn "Cộng hai số này lại"

**Trong Java**:
- **Anonymous Inner Class**: Rất dài dòng
- **Lambda**: Ngắn gọn và rõ ràng

### Ví dụ so sánh

**Trước Java 8 (Anonymous Inner Class)**:
```java
// Code dài dòng
Collections.sort(students, new Comparator<Student>() {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName());
    }
});
```

**Sau Java 8 (Lambda)**:
```java
// Code ngắn gọn
students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
```

**Rõ ràng ngắn gọn và dễ đọc hơn nhiều!**

## II. Cú pháp Lambda Expressions

### Cấu trúc cơ bản

```
(parameters) -> expression
(parameters) -> { statements; }
```

**Thành phần**:
- **Parameters**: Tham số (có thể không có, 1, hoặc nhiều)
- **Arrow token**: `->` (mũi tên)
- **Body**: Biểu thức hoặc khối code

### Các dạng Lambda Expressions

**1. Không tham số**:
```java
() -> System.out.println("Hello World");
() -> 42;  // Return 42
```

**2. Một tham số (không cần dấu ngoặc đơn)**:
```java
x -> x + 1;
x -> x * 2;
s -> s.length();
```

**3. Một tham số (có kiểu dữ liệu)**:
```java
(int x) -> x + 1;
(String s) -> s.toUpperCase();
```

**4. Nhiều tham số**:
```java
(x, y) -> x + y;
(int a, int b) -> a * b;
(String s1, String s2) -> s1.concat(s2);
```

**5. Body có nhiều câu lệnh**:
```java
(x, y) -> {
    int sum = x + y;
    return sum * 2;
}
```

### Ví dụ minh họa

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;

public class LambdaSyntax {
    public static void main(String[] args) {
        // 1. Không tham số
        Runnable runnable = () -> System.out.println("Hello Lambda!");
        runnable.run();
        
        // 2. Một tham số
        Function<Integer, Integer> doubleValue = x -> x * 2;
        System.out.println(doubleValue.apply(5));  // 10
        
        // 3. Nhiều tham số
        java.util.function.BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
        System.out.println(add.apply(10, 20));  // 30
        
        // 4. Body có nhiều câu lệnh
        Function<Integer, Integer> calculate = x -> {
            int result = x * 2;
            result += 10;
            return result;
        };
        System.out.println(calculate.apply(5));  // 20
        
        // 5. Với List
        List<String> names = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));
        names.forEach(name -> System.out.println("Hello, " + name));
    }
}
```

## III. Functional Interfaces

### Functional Interface là gì?

**Functional Interface** là một interface chỉ có **duy nhất một phương thức trừu tượng** (abstract method). Java 8 cung cấp annotation `@FunctionalInterface` để đánh dấu.

### Đặc điểm

- ✅ Chỉ có **một abstract method**
- ✅ Có thể có **default methods** (Java 8+)
- ✅ Có thể có **static methods** (Java 8+)
- ✅ Annotation `@FunctionalInterface` là **tùy chọn** (nhưng khuyến nghị)

### Ví dụ Functional Interfaces

**1. Runnable** (Java cũ):
```java
@FunctionalInterface
public interface Runnable {
    void run();
}

// Sử dụng với Lambda
Runnable task = () -> System.out.println("Task executed!");
task.run();
```

**2. Comparator**:
```java
@FunctionalInterface
public interface Comparator<T> {
    int compare(T o1, T o2);
    
    // Có thể có default methods và static methods
}

// Sử dụng với Lambda
Comparator<String> comparator = (s1, s2) -> s1.compareTo(s2);
```

### Tạo Functional Interface riêng

```java
@FunctionalInterface
public interface Calculator {
    // Chỉ có một abstract method
    double calculate(double a, double b);
    
    // ✅ OK: Có thể có default methods
    default void displayResult(double result) {
        System.out.println("Kết quả: " + result);
    }
    
    // ✅ OK: Có thể có static methods
    static Calculator create() {
        return (a, b) -> a + b;
    }
}

// Sử dụng
public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        // Lambda expression
        Calculator add = (a, b) -> a + b;
        Calculator multiply = (a, b) -> a * b;
        Calculator divide = (a, b) -> b != 0 ? a / b : 0;
        
        System.out.println("10 + 5 = " + add.calculate(10, 5));         // 15
        System.out.println("10 * 5 = " + multiply.calculate(10, 5));    // 50
        System.out.println("10 / 5 = " + divide.calculate(10, 5));      // 2.0
        
        // Sử dụng default method
        add.displayResult(add.calculate(10, 5));  // Kết quả: 15.0
        
        // Sử dụng static method
        Calculator calc = Calculator.create();
        System.out.println("Static: " + calc.calculate(20, 30));  // 50
    }
}
```

## IV. Các Functional Interfaces phổ biến trong Java

Java cung cấp các **predefined functional interfaces** trong package `java.util.function`:

### 1. Function<T, R>

**Function** nhận một giá trị kiểu `T` và trả về một giá trị kiểu `R`.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

**Ví dụ**:
```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Function: String → Integer (độ dài chuỗi)
        Function<String, Integer> length = s -> s.length();
        System.out.println(length.apply("Hello"));  // 5
        
        // Function: Integer → Integer (nhân đôi)
        Function<Integer, Integer> doubleValue = x -> x * 2;
        System.out.println(doubleValue.apply(10));  // 20
        
        // Function: Integer → String
        Function<Integer, String> toString = x -> "Number: " + x;
        System.out.println(toString.apply(42));  // "Number: 42"
        
        // Function chain - andThen()
        Function<Integer, Integer> multiply = x -> x * 2;
        Function<Integer, Integer> add = x -> x + 10;
        Function<Integer, Integer> chain = multiply.andThen(add);
        System.out.println(chain.apply(5));  // (5 * 2) + 10 = 20
    }
}
```

### 2. Predicate<T>

**Predicate** nhận một giá trị kiểu `T` và trả về `boolean`.

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```

**Ví dụ**:
```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        // Predicate: Kiểm tra số dương
        Predicate<Integer> isPositive = x -> x > 0;
        System.out.println(isPositive.test(10));   // true
        System.out.println(isPositive.test(-5));   // false
        
        // Predicate: Kiểm tra chuỗi rỗng
        Predicate<String> isEmpty = s -> s == null || s.isEmpty();
        System.out.println(isEmpty.test(""));      // true
        System.out.println(isEmpty.test("Hello")); // false
        
        // Sử dụng với List (filter)
        List<Integer> numbers = new ArrayList<>(List.of(-2, -1, 0, 1, 2, 3, 4, 5));
        
        // Lọc số dương
        numbers.removeIf(x -> x <= 0);  // removeIf() nhận Predicate
        System.out.println("Số dương: " + numbers);  // [1, 2, 3, 4, 5]
        
        // Lọc số chẵn
        List<Integer> evens = new ArrayList<>(List.of(1, 2, 3, 4, 5, 6));
        evens.removeIf(x -> x % 2 != 0);
        System.out.println("Số chẵn: " + evens);  // [2, 4, 6]
    }
}
```

**Predicate methods**:
```java
Predicate<Integer> isPositive = x -> x > 0;
Predicate<Integer> isEven = x -> x % 2 == 0;

// and() - Kết hợp 2 predicates (AND logic)
Predicate<Integer> isPositiveAndEven = isPositive.and(isEven);
System.out.println(isPositiveAndEven.test(4));   // true
System.out.println(isPositiveAndEven.test(3));   // false

// or() - Kết hợp 2 predicates (OR logic)
Predicate<Integer> isPositiveOrEven = isPositive.or(isEven);
System.out.println(isPositiveOrEven.test(-2));   // true (even)
System.out.println(isPositiveOrEven.test(3));    // true (positive)

// negate() - Phủ định
Predicate<Integer> isNotPositive = isPositive.negate();
System.out.println(isNotPositive.test(-5));      // true
```

### 3. Consumer<T>

**Consumer** nhận một giá trị kiểu `T` và không trả về gì (void).

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

**Ví dụ**:
```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        // Consumer: In ra màn hình
        Consumer<String> printer = s -> System.out.println(s);
        printer.accept("Hello World!");  // Hello World!
        
        // Consumer: Thêm vào danh sách
        List<String> list = new ArrayList<>();
        Consumer<String> addToList = s -> list.add(s);
        addToList.accept("Apple");
        addToList.accept("Banana");
        System.out.println("List: " + list);  // [Apple, Banana]
        
        // Sử dụng với forEach()
        List<Integer> numbers = new ArrayList<>(List.of(1, 2, 3, 4, 5));
        numbers.forEach(num -> System.out.println("Number: " + num));
        // Number: 1
        // Number: 2
        // Number: 3
        // Number: 4
        // Number: 5
        
        // Method reference
        numbers.forEach(System.out::println);  // 1, 2, 3, 4, 5
        
        // Consumer chain - andThen()
        Consumer<String> print = s -> System.out.print(s);
        Consumer<String> println = s -> System.out.println("!");
        Consumer<String> chain = print.andThen(println);
        chain.accept("Hello");  // Hello!
    }
}
```

### 4. Supplier<T>

**Supplier** không nhận tham số và trả về một giá trị kiểu `T`.

```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
```

**Ví dụ**:
```java
import java.util.function.Supplier;
import java.util.Random;

public class SupplierExample {
    public static void main(String[] args) {
        // Supplier: Trả về giá trị cố định
        Supplier<String> hello = () -> "Hello World!";
        System.out.println(hello.get());  // Hello World!
        
        // Supplier: Trả về số ngẫu nhiên
        Supplier<Integer> randomInt = () -> new Random().nextInt(100);
        System.out.println(randomInt.get());  // Số ngẫu nhiên từ 0-99
        
        // Supplier: Trả về đối tượng mới
        Supplier<Student> studentSupplier = () -> new Student("New Student", 20, 8.0);
        Student student = studentSupplier.get();
        System.out.println(student);  // Student mới được tạo
        
        // Supplier với logic phức tạp
        Supplier<String> timestamp = () -> {
            long time = System.currentTimeMillis();
            return "Timestamp: " + time;
        };
        System.out.println(timestamp.get());  // Timestamp: 1234567890
    }
}
```

## V. Method References (Java 8+)

### Method Reference là gì?

**Method Reference** là cú pháp ngắn gọn để tham chiếu đến một phương thức mà không gọi nó. Nó là một dạng đặc biệt của Lambda expression.

### Các loại Method Reference

**1. Static Method Reference** - `ClassName::staticMethod`:
```java
// Lambda
Function<String, Integer> length1 = s -> s.length();

// Method Reference
Function<String, Integer> length2 = String::length;
```

**2. Instance Method Reference** - `object::instanceMethod`:
```java
// Lambda
Consumer<String> printer1 = s -> System.out.println(s);

// Method Reference
Consumer<String> printer2 = System.out::println;
```

**3. Instance Method of Arbitrary Object** - `ClassName::instanceMethod`:
```java
// Lambda
Function<String, String> upper1 = s -> s.toUpperCase();

// Method Reference
Function<String, String> upper2 = String::toUpperCase;
```

**4. Constructor Reference** - `ClassName::new`:
```java
// Lambda
Supplier<String> supplier1 = () -> new String();

// Constructor Reference
Supplier<String> supplier2 = String::new;
```

### Ví dụ tổng hợp

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));
        
        // 1. Static Method Reference
        // Lambda: s -> Integer.parseInt(s)
        Function<String, Integer> parseInt1 = s -> Integer.parseInt(s);
        // Method Reference:
        Function<String, Integer> parseInt2 = Integer::parseInt;
        
        // 2. Instance Method Reference
        // Lambda: s -> System.out.println(s)
        Consumer<String> printer1 = s -> System.out.println(s);
        // Method Reference:
        names.forEach(System.out::println);
        
        // 3. Instance Method of Arbitrary Object
        // Lambda: s -> s.toUpperCase()
        Function<String, String> upper1 = s -> s.toUpperCase();
        // Method Reference:
        Function<String, String> upper2 = String::toUpperCase;
        names.forEach(s -> System.out.println(String::toUpperCase));
        
        // 4. Constructor Reference
        // Lambda: () -> new ArrayList<>()
        Supplier<List<String>> listSupplier1 = () -> new ArrayList<>();
        // Constructor Reference:
        Supplier<List<String>> listSupplier2 = ArrayList::new;
        
        // Ví dụ thực tế
        names.forEach(System.out::println);  // In mỗi phần tử
        names.removeIf(String::isEmpty);     // Xóa chuỗi rỗng
        names.replaceAll(String::toUpperCase);  // Chuyển thành chữ hoa
    }
}
```

## VI. Ví dụ thực tế với Lambda

### Ví dụ 1: Sắp xếp danh sách

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class LambdaSorting {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        // Sắp xếp theo tên (Lambda)
        students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
        
        // Sắp xếp theo GPA (Method Reference)
        students.sort(Comparator.comparing(Student::getGpa));
        
        // Sắp xếp theo nhiều tiêu chí
        students.sort(Comparator.comparing(Student::getName)
                              .thenComparing(Student::getAge)
                              .thenComparing(Student::getGpa));
        
        students.forEach(System.out::println);
    }
}
```

### Ví dụ 2: Lọc danh sách

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class LambdaFiltering {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.5));
        
        // Lọc sinh viên có GPA >= 8.0
        students.removeIf(s -> s.getGpa() < 8.0);
        
        // Hoặc tạo danh sách mới
        List<Student> topStudents = new ArrayList<>();
        for (Student s : students) {
            if (s.getGpa() >= 8.5) {
                topStudents.add(s);
            }
        }
        
        // Với Stream API (sẽ học ở bài nâng cao)
        // List<Student> topStudents = students.stream()
        //                                    .filter(s -> s.getGpa() >= 8.5)
        //                                    .collect(Collectors.toList());
        
        topStudents.forEach(System.out::println);
    }
}
```

### Ví dụ 3: Xử lý từng phần tử

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;

public class LambdaForEach {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>(List.of("Alice", "Bob", "Charlie"));
        
        // Lambda - In ra màn hình
        names.forEach(name -> System.out.println("Hello, " + name));
        
        // Method Reference
        names.forEach(System.out::println);
        
        // Lambda phức tạp
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        
        students.forEach(s -> {
            System.out.println("=== THÔNG TIN SINH VIÊN ===");
            System.out.println("Tên: " + s.getName());
            System.out.println("Tuổi: " + s.getAge());
            System.out.println("GPA: " + s.getGpa());
            System.out.println();
        });
    }
}
```

## VII. Lưu ý quan trọng

### 1. Type Inference (Suy luận kiểu)

Lambda tự động suy luận kiểu từ context:

```java
// Không cần chỉ định kiểu - Tự suy luận
List<String> names = new ArrayList<>();
names.sort((s1, s2) -> s1.compareTo(s2));  // Tự suy luận String

// Có thể chỉ định kiểu tường minh
names.sort((String s1, String s2) -> s1.compareTo(s2));
```

### 2. Variable Capture

Lambda có thể truy cập **final** hoặc **effectively final** variables từ scope ngoài:

```java
final int multiplier = 10;  // final
int factor = 5;              // effectively final (không thay đổi sau khi khai báo)

Function<Integer, Integer> multiply = x -> x * multiplier * factor;
System.out.println(multiply.apply(2));  // 100

// ❌ LỖI: Không thể thay đổi biến được capture
// factor = 10;  // Lỗi! factor phải là effectively final
```

### 3. `this` trong Lambda

Trong Lambda, `this` tham chiếu đến **enclosing class**, không phải Lambda:

```java
public class LambdaThis {
    private String name = "Outer";
    
    public void method() {
        Runnable r = () -> {
            // this tham chiếu đến LambdaThis, không phải Runnable
            System.out.println(this.name);  // "Outer"
        };
        r.run();
    }
}
```

## VIII. Best Practices

### 1. Khi nào dùng Lambda, khi nào dùng Method Reference?

**Dùng Lambda khi**:
- Logic **phức tạp** (nhiều dòng)
- Cần **thay đổi** logic thường xuyên
- Logic **không tái sử dụng** được

**Dùng Method Reference khi**:
- Logic **đơn giản** (chỉ gọi method)
- Method **đã tồn tại**
- Code **rõ ràng hơn**

**Ví dụ**:
```java
// ✅ TỐT: Method Reference (đơn giản)
names.forEach(System.out::println);

// ✅ TỐT: Lambda (logic phức tạp)
students.forEach(s -> {
    if (s.getGpa() >= 8.0) {
        System.out.println("Top student: " + s.getName());
    }
});
```

### 2. Đặt tên biến Lambda

```java
// ✅ TỐT: Tên có ý nghĩa
students.sort((student1, student2) -> 
    student1.getName().compareTo(student2.getName()));

// ❌ KHÔNG TỐT: Tên ngắn, không rõ nghĩa
students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu Lambda Expressions là gì và tại sao nó quan trọng
- ✅ Nắm được cú pháp cơ bản của Lambda
- ✅ Hiểu Functional Interfaces và cách tạo chúng
- ✅ Sử dụng các predefined functional interfaces (Function, Predicate, Consumer, Supplier)
- ✅ Sử dụng Method References
- ✅ Áp dụng Lambda vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo các Lambda expressions**:
   - Function tính bình phương
   - Predicate kiểm tra số chẵn
   - Consumer in ra màn hình
   - Supplier tạo đối tượng

2. **Sử dụng Lambda với List**:
   - Sắp xếp danh sách
   - Lọc danh sách
   - Xử lý từng phần tử

3. **Tạo Functional Interface riêng**:
   - Interface Calculator với Lambda
   - Interface Validator với Predicate

## Tài liệu tham khảo

- [Oracle Java Tutorial - Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)
- [Java Lambda Expressions](https://www.javatpoint.com/java-lambda-expressions)
- [Functional Interfaces in Java](https://www.baeldung.com/java-8-functional-interfaces)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
