# Bài 3: Kiểu dữ liệu trong Java

> **Mục tiêu**: Hiểu rõ các kiểu dữ liệu trong Java, sự khác biệt giữa primitive types và reference types, và cách sử dụng chúng hiệu quả.

## I. Giới thiệu về kiểu dữ liệu

### Kiểu dữ liệu là gì?

**Kiểu dữ liệu (Data Type)** xác định loại giá trị mà một biến có thể lưu trữ và các thao tác có thể thực hiện trên giá trị đó.

Ví dụ đời thường:
- **Số nguyên**: 1, 2, 100 (không có phần thập phân)
- **Số thập phân**: 3.14, 2.5 (có phần thập phân)
- **Chữ cái**: 'A', 'B', 'a' (một ký tự)
- **Chuỗi**: "Hello", "Java" (nhiều ký tự)
- **Đúng/Sai**: true, false (logic)

### Phân loại kiểu dữ liệu trong Java

Java có **2 loại kiểu dữ liệu chính**:

1. **Primitive Types** (Kiểu nguyên thủy): Các kiểu dữ liệu cơ bản
2. **Reference Types** (Kiểu tham chiếu): Các kiểu dữ liệu đối tượng

## II. Primitive Types (Kiểu nguyên thủy)

### Tổng quan

Java có **8 kiểu dữ liệu nguyên thủy**:

| Kiểu dữ liệu | Kích thước (bits) | Giá trị nhỏ nhất | Giá trị lớn nhất | Ví dụ |
|--------------|-------------------|------------------|------------------|-------|
| `byte` | 8 | -128 (2^7) | 127 (2^7 - 1) | `byte b = 100;` |
| `short` | 16 | -32,768 (2^15) | 32,767 (2^15 - 1) | `short s = 30000;` |
| `int` | 32 | -2,147,483,648 (2^31) | 2,147,483,647 (2^31 - 1) | `int i = 1000000000;` |
| `long` | 64 | -2^63 | 2^63 - 1 | `long l = 1000000000000L;` |
| `float` | 32 | ~1.4E-45 | ~3.4E+38 | `float f = 1.456f;` |
| `double` | 64 | ~4.9E-324 | ~1.7E+308 | `double d = 1.456789012345678;` |
| `char` | 16 | '\u0000' (0) | '\uffff' (65,535) | `char c = 'A';` |
| `boolean` | 1 bit | `false` | `true` | `boolean b = true;` |

### Chi tiết từng kiểu

#### 1. Kiểu số nguyên

**`byte`** - Kích thước nhỏ nhất
```java
byte b1 = 100;
byte b2 = -50;
// byte b3 = 200; // ❌ LỖI! Vượt quá giới hạn (127)
```

**`short`** - Kích thước vừa
```java
short s1 = 30000;
short s2 = -15000;
```

**`int`** - Kiểu mặc định cho số nguyên (khuyến nghị sử dụng)
```java
int i1 = 1000000000;
int i2 = -500000000;
int i3 = 1_000_000_000; // Có thể dùng dấu gạch dưới để dễ đọc
```

**`long`** - Kích thước lớn nhất
```java
long l1 = 1000000000000L; // Phải có 'L' hoặc 'l' ở cuối
long l2 = 1_000_000_000_000L;
```

> **Lưu ý**: Từ Java 7 trở đi, bạn có thể sử dụng dấu gạch dưới (`_`) trong số để dễ đọc: `1_000_000`

#### 2. Kiểu số thực (số có dấu phẩy động)

**`float`** - Độ chính xác đơn
```java
float f1 = 3.14f;     // Phải có 'f' hoặc 'F' ở cuối
float f2 = 1.5F;
float f3 = 123.456f;
```

**`double`** - Độ chính xác kép (khuyến nghị sử dụng)
```java
double d1 = 3.141592653589793;
double d2 = 1.5; // Mặc định là double
double d3 = 123.456789012345678;
```

> **Lưu ý**: `double` chính xác hơn `float` và là kiểu mặc định cho số thực trong Java.

#### 3. Kiểu ký tự

**`char`** - Lưu trữ một ký tự Unicode (16-bit)
```java
char c1 = 'A';
char c2 = '中';      // Hỗ trợ Unicode (tiếng Việt, Trung, v.v.)
char c3 = '\u0041';  // Ký tự Unicode: 'A'
char c4 = '\n';      // Ký tự đặc biệt: xuống dòng
char c5 = '\t';      // Tab
char c6 = '\\';      // Dấu backslash
```

**Các ký tự đặc biệt (Escape sequences)**:
- `\n`: Xuống dòng (newline)
- `\t`: Tab
- `\\`: Dấu backslash
- `\'`: Dấu nháy đơn
- `\"`: Dấu nháy kép
- `\r`: Carriage return

#### 4. Kiểu logic

**`boolean`** - Chỉ có 2 giá trị: `true` hoặc `false`
```java
boolean b1 = true;
boolean b2 = false;
boolean isActive = true;
boolean hasPermission = false;
```

> **Lưu ý**: Trong Java, `boolean` không thể chuyển đổi sang số như trong C/C++ (0 = false, 1 = true).

### Giá trị mặc định

Khi khai báo biến **instance variable** (biến của lớp) mà không khởi tạo, Java sẽ gán giá trị mặc định:

| Kiểu dữ liệu | Giá trị mặc định |
|--------------|------------------|
| `byte`, `short`, `int`, `long` | `0` |
| `float`, `double` | `0.0` |
| `char` | `'\u0000'` (null character) |
| `boolean` | `false` |
| Reference types | `null` |

**Ví dụ**:
```java
public class DefaultValues {
    // Instance variables - có giá trị mặc định
    int age;           // 0
    double price;      // 0.0
    char grade;        // '\u0000'
    boolean isActive;  // false
    String name;       // null
    
    public static void main(String[] args) {
        DefaultValues obj = new DefaultValues();
        System.out.println("age: " + obj.age);        // 0
        System.out.println("price: " + obj.price);    // 0.0
        System.out.println("grade: " + obj.grade);    // (empty)
        System.out.println("isActive: " + obj.isActive); // false
        System.out.println("name: " + obj.name);      // null
    }
}
```

> **Lưu ý quan trọng**: **Local variables** (biến trong phương thức) **KHÔNG có** giá trị mặc định và **phải** được khởi tạo trước khi sử dụng!

```java
public void example() {
    int x;           // ❌ LỖI! Phải khởi tạo
    System.out.println(x); // Compiler error
    
    int y = 10;      // ✅ OK
    System.out.println(y); // 10
}
```

## III. Reference Types (Kiểu tham chiếu)

### Tổng quan

**Reference Types** (Kiểu tham chiếu) là các kiểu dữ liệu đối tượng, bao gồm:
- **Classes** (Lớp)
- **Interfaces** (Giao diện)
- **Arrays** (Mảng)

### Sự khác biệt giữa Primitive và Reference Types

#### Primitive Types - Lưu trữ giá trị trực tiếp

```java
int a = 10;
int b = a;  // Sao chép giá trị: b = 10
b = 20;     // Thay đổi b không ảnh hưởng đến a

System.out.println(a); // 10
System.out.println(b); // 20
```

**Trong bộ nhớ**:
```
Stack:
a → 10
b → 20
```

#### Reference Types - Lưu trữ địa chỉ (reference) đến đối tượng

```java
String str1 = "Hello";
String str2 = str1;  // Sao chép reference, cùng trỏ đến một đối tượng

// Với String thì hơi đặc biệt vì immutability
str2 = "World";  // Tạo đối tượng mới

System.out.println(str1); // "Hello"
System.out.println(str2); // "World"
```

**Với đối tượng bình thường**:
```java
class Point {
    int x, y;
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

Point p1 = new Point(10, 20);
Point p2 = p1;  // Sao chép reference, cùng trỏ đến một đối tượng

p2.x = 30;      // Thay đổi đối tượng mà cả p1 và p2 đang trỏ đến

System.out.println(p1.x); // 30 (cùng đối tượng!)
System.out.println(p2.x); // 30
```

**Trong bộ nhớ**:
```
Stack:              Heap:
p1 → [reference] →  Point {x=30, y=20}
p2 → [reference] ┘
```

### Ví dụ với Array (Mảng)

```java
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1;  // Sao chép reference

arr2[0] = 100;      // Thay đổi đối tượng mảng

System.out.println(arr1[0]); // 100 (cùng mảng!)
System.out.println(arr2[0]); // 100
```

## IV. Literals (Hằng số)

### Literal là gì?

**Literal** là giá trị được viết trực tiếp trong code, không cần tính toán.

### Các loại Literal

#### 1. Integer Literals (Hằng số nguyên)

**Decimal (Thập phân)** - Cơ số 10:
```java
int d = 123;        // 123
int d2 = -456;      // -456
int d3 = 1_000_000; // 1,000,000 (dễ đọc)
```

**Octal (Bát phân)** - Cơ số 8 (bắt đầu bằng 0):
```java
int o = 0175;       // 123 trong hệ thập phân (0*8^0 + 7*8^1 + 1*8^2)
```

**Hexadecimal (Thập lục phân)** - Cơ số 16 (bắt đầu bằng 0x hoặc 0X):
```java
int h = 0x7B;       // 123 trong hệ thập phân
int h2 = 0xFF;      // 255 trong hệ thập phân
```

**Binary (Nhị phân)** - Cơ số 2 (bắt đầu bằng 0b hoặc 0B, từ Java 7+):
```java
int b = 0b11011;    // 27 trong hệ thập phân
int b2 = 0b1010;    // 10 trong hệ thập phân
```

#### 2. Floating-Point Literals (Hằng số thực)

**Single Precision (float)**:
```java
float f1 = 4.0f;      // Phải có 'f' hoặc 'F'
float f2 = 4F;
float f3 = 3.14f;
```

**Double Precision (double)** - Mặc định:
```java
double d1 = 3.14;     // Mặc định là double
double d2 = 3.14d;    // Có thể có 'd' hoặc 'D'
double d3 = 1.5e2;    // 150.0 (scientific notation)
double d4 = 1.5E-2;   // 0.015
```

#### 3. Character Literals (Hằng số ký tự)

```java
char c1 = 'A';
char c2 = '中';
char c3 = '\u0041';   // Unicode: 'A'
char c4 = '\n';       // Newline
char c5 = '\t';       // Tab
```

#### 4. String Literals (Hằng số chuỗi)

```java
String s1 = "Hello World";
String s2 = "Tiếng Việt: Xin chào";
String s3 = "Line 1\nLine 2";  // Có xuống dòng
```

**Text Blocks** (Java 13+, khuyến nghị Java 15+):
```java
String textBlock = """
    Đây là một đoạn văn bản
    có thể viết trên nhiều dòng
    mà không cần dùng \\n
    """;
```

#### 5. Boolean Literals (Hằng số logic)

```java
boolean b1 = true;
boolean b2 = false;
// boolean b3 = TRUE;  // ❌ LỖI! Phải viết thường
// boolean b4 = 1;     // ❌ LỖI! Không phải số
```

#### 6. Null Literal

```java
String str = null;    // Chưa trỏ đến đối tượng nào
Object obj = null;
```

## V. Type Casting (Ép kiểu)

### Ép kiểu là gì?

**Type Casting** là chuyển đổi từ kiểu dữ liệu này sang kiểu dữ liệu khác.

### 1. Implicit Casting (Ép kiểu ngầm định)

**Tự động** khi chuyển từ kiểu nhỏ sang kiểu lớn hơn:

```
byte → short → int → long → float → double
           ↓
         char → int
```

**Ví dụ**:
```java
int a = 10;
long b = a;        // ✅ Tự động ép kiểu: int → long
double c = b;      // ✅ Tự động ép kiểu: long → double

float f = 3.14f;
double d = f;      // ✅ Tự động ép kiểu: float → double

char ch = 'A';
int i = ch;        // ✅ Tự động ép kiểu: char → int (65)
```

### 2. Explicit Casting (Ép kiểu tường minh)

**Cần khai báo rõ ràng** khi chuyển từ kiểu lớn sang kiểu nhỏ hơn (có thể mất dữ liệu):

```java
double d = 3.14159;
int i = (int) d;   // ✅ Ép kiểu tường minh: double → int (mất phần thập phân)
// i = 3

long l = 10000000000L;
int i2 = (int) l;  // ⚠️ Có thể mất dữ liệu nếu vượt quá giới hạn int

float f = 3.14f;
int i3 = (int) f;  // ✅ Ép kiểu: float → int (3)
```

**Ví dụ mất dữ liệu**:
```java
int largeInt = 1_000_000_000;
byte b = (byte) largeInt;  // ⚠️ Mất dữ liệu! Giá trị sẽ bị cắt bớt
System.out.println(b);     // Không phải 1,000,000,000

double pi = 3.14159;
int intPi = (int) pi;      // Mất phần thập phân
System.out.println(intPi); // 3 (không phải 3.14159)
```

## VI. Ví dụ thực tế

### Ví dụ 1: Tính diện tích hình tròn

```java
public class CircleArea {
    public static void main(String[] args) {
        // Sử dụng các kiểu dữ liệu phù hợp
        double radius = 5.5;      // Bán kính (số thực)
        double pi = 3.14159;      // Số pi
        double area;              // Diện tích
        
        area = pi * radius * radius;
        
        System.out.println("Bán kính: " + radius);
        System.out.println("Diện tích: " + area);
    }
}
```

### Ví dụ 2: Thông tin sinh viên

```java
public class Student {
    // Instance variables với kiểu dữ liệu phù hợp
    String name;           // Reference type
    int age;               // Primitive type
    double gpa;            // Primitive type
    boolean isActive;      // Primitive type
    char grade;            // Primitive type
    
    public Student(String name, int age, double gpa, boolean isActive, char grade) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
        this.isActive = isActive;
        this.grade = grade;
    }
    
    public void displayInfo() {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + name);           // String
        System.out.println("Tuổi: " + age);           // int
        System.out.println("Điểm TB: " + gpa);        // double
        System.out.println("Đang học: " + isActive);  // boolean
        System.out.println("Xếp loại: " + grade);     // char
    }
    
    public static void main(String[] args) {
        Student student = new Student(
            "Nguyễn Văn A",  // String
            20,              // int
            8.5,             // double
            true,            // boolean
            'A'              // char
        );
        student.displayInfo();
    }
}
```

## VII. Lưu ý quan trọng

### 1. Chọn kiểu dữ liệu phù hợp

- **Số nguyên**: Dùng `int` cho hầu hết trường hợp, `long` khi cần số rất lớn
- **Số thực**: Dùng `double` (chính xác hơn `float`)
- **Logic**: Dùng `boolean`
- **Ký tự**: Dùng `char` cho một ký tự, `String` cho chuỗi

### 2. Hiệu năng và bộ nhớ

- `byte` và `short` tiết kiệm bộ nhớ nhưng ít khi cần thiết
- `int` và `double` là các lựa chọn mặc định tốt
- `long` và `float` chỉ dùng khi thực sự cần

### 3. Overflow (Tràn số)

```java
int maxInt = Integer.MAX_VALUE;  // 2,147,483,647
int overflow = maxInt + 1;       // -2,147,483,648 (tràn số!)

System.out.println(overflow);    // Giá trị âm!
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu 8 kiểu dữ liệu nguyên thủy trong Java
- ✅ Nắm được sự khác biệt giữa primitive types và reference types
- ✅ Biết cách sử dụng literals (hằng số)
- ✅ Hiểu cách ép kiểu (type casting)
- ✅ Chọn kiểu dữ liệu phù hợp cho từng trường hợp

## Bài tập thực hành

1. **Tạo chương trình tính toán**:
   - Khai báo các biến với kiểu dữ liệu phù hợp
   - Tính diện tích hình chữ nhật (chiều dài × chiều rộng)
   - Tính chu vi hình tròn (2 × π × bán kính)

2. **Tạo lớp `Product`** với các kiểu dữ liệu:
   - `name` (String)
   - `price` (double)
   - `quantity` (int)
   - `isAvailable` (boolean)

3. **Thực hành ép kiểu**:
   - Ép kiểu từ `double` sang `int`
   - Ép kiểu từ `int` sang `byte` và quan sát kết quả

## Tài liệu tham khảo

- [Oracle Java Tutorial - Primitive Data Types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)
- [Java Text Blocks (Java 15+)](https://docs.oracle.com/en/java/javase/15/text-blocks/index.html)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
