# Bài 4: Xuất dữ liệu trong Java (Java Output)

> **Mục tiêu**: Hiểu cách hiển thị dữ liệu ra màn hình console trong Java, sử dụng `print()`, `println()`, và `printf()` một cách hiệu quả.

## I. Giới thiệu về xuất dữ liệu trong Java

### System.out là gì?

Trong Java, để hiển thị dữ liệu ra màn hình console, chúng ta sử dụng:
- `System` - Một lớp hệ thống của Java
- `out` - Một đối tượng `PrintStream` được khai báo là `public static final` trong lớp `System`
- `in` - Một đối tượng `InputStream` để nhận dữ liệu đầu vào (sẽ học ở bài Input)

**Cú pháp**:
```java
System.out.print();      // In ra không xuống dòng
System.out.println();    // In ra và xuống dòng
System.out.printf();     // In ra với định dạng (format)
```

> **Lưu ý**: Đừng lo nếu bạn chưa hiểu về `class`, `public`, `static` - chúng ta sẽ học chi tiết ở các bài sau. Bây giờ chỉ cần nhớ cách sử dụng là đủ!

### Ví dụ cơ bản

```java
public class OutputExample {
    public static void main(String[] args) {
        System.out.println("Xin chào Java!");
        System.out.println("Tôi đang học lập trình.");
    }
}
```

**Kết quả**:
```
Xin chào Java!
Tôi đang học lập trình.
```

## II. Sự khác biệt giữa print(), println() và printf()

### 1. print() - In ra không xuống dòng

**`print()`** in ra chuỗi nhưng **không tự động xuống dòng** sau khi in.

```java
public class PrintExample {
    public static void main(String[] args) {
        System.out.print("Dòng 1 ");
        System.out.print("Dòng 2 ");
        System.out.print("Dòng 3");
    }
}
```

**Kết quả**:
```
Dòng 1 Dòng 2 Dòng 3
```

Tất cả nội dung được in trên cùng một dòng.

### 2. println() - In ra và xuống dòng (khuyến nghị sử dụng)

**`println()`** (print line) in ra chuỗi và **tự động xuống dòng** sau khi in.

```java
public class PrintlnExample {
    public static void main(String[] args) {
        System.out.println("Dòng 1");
        System.out.println("Dòng 2");
        System.out.println("Dòng 3");
    }
}
```

**Kết quả**:
```
Dòng 1
Dòng 2
Dòng 3
```

Mỗi dòng được in trên một dòng riêng.

### 3. printf() - In ra với định dạng

**`printf()`** (print format) cho phép định dạng chuỗi trước khi in, tương tự như `printf` trong C/C++.

**Cú pháp**:
```java
System.out.printf("Format string", argument1, argument2, ...);
```

**Các ký tự định dạng phổ biến**:

| Ký tự | Mô tả | Ví dụ |
|-------|-------|-------|
| `%d` | Số nguyên (decimal) | `printf("%d", 10)` → `10` |
| `%f` | Số thực (floating point) | `printf("%f", 3.14)` → `3.140000` |
| `%s` | Chuỗi (String) | `printf("%s", "Hello")` → `Hello` |
| `%c` | Ký tự (Character) | `printf("%c", 'A')` → `A` |
| `%b` | Boolean | `printf("%b", true)` → `true` |
| `%n` | Xuống dòng mới | Tương tự `\n` |

**Ví dụ**:
```java
public class PrintfExample {
    public static void main(String[] args) {
        String name = "Nguyễn Văn A";
        int age = 20;
        double gpa = 8.5;
        
        System.out.printf("Tên: %s%n", name);
        System.out.printf("Tuổi: %d%n", age);
        System.out.printf("Điểm TB: %.2f%n", gpa);  // %.2f = 2 chữ số thập phân
        
        // In nhiều giá trị cùng lúc
        System.out.printf("Thông tin: %s - %d tuổi - Điểm TB: %.2f%n", 
                         name, age, gpa);
    }
}
```

**Kết quả**:
```
Tên: Nguyễn Văn A
Tuổi: 20
Điểm TB: 8.50
Thông tin: Nguyễn Văn A - 20 tuổi - Điểm TB: 8.50
```

### So sánh tóm tắt

```java
public class CompareOutput {
    public static void main(String[] args) {
        // print() - Không xuống dòng
        System.out.print("1. print ");
        System.out.print("2. print ");
        System.out.print("3. print");
        System.out.println();  // Xuống dòng
        
        // println() - Tự động xuống dòng
        System.out.println("1. println");
        System.out.println("2. println");
        System.out.println("3. println");
        
        // printf() - Định dạng
        int number = 100;
        System.out.printf("Số: %d%n", number);
        System.out.printf("Pi: %.2f%n", 3.14159);
    }
}
```

**Kết quả**:
```
1. print 2. print 3. print
1. println
2. println
3. println
Số: 100
Pi: 3.14
```

## III. In ra biến (Variables)

### In ra các kiểu dữ liệu

Bạn có thể in ra **bất kỳ kiểu dữ liệu nào** bằng cách truyền trực tiếp biến vào các phương thức:

```java
public class PrintVariables {
    public static void main(String[] args) {
        // Số nguyên
        int age = 20;
        System.out.println(age);  // 20
        
        // Số thực
        double price = 99.99;
        System.out.println(price);  // 99.99
        
        // Ký tự
        char grade = 'A';
        System.out.println(grade);  // A
        
        // Boolean
        boolean isActive = true;
        System.out.println(isActive);  // true
        
        // Chuỗi
        String name = "Java";
        System.out.println(name);  // Java
    }
}
```

**Lưu ý quan trọng**: Trong Java, không cần nhớ định dạng như C (`%d`, `%f`, v.v.) khi dùng `println()`. Java **tự động chuyển đổi** kiểu dữ liệu thành chuỗi để in ra.

### In ra nhiều giá trị cùng lúc

```java
public class PrintMultiple {
    public static void main(String[] args) {
        String name = "Nguyễn Văn A";
        int age = 20;
        double gpa = 8.5;
        
        // Cách 1: Sử dụng + (nối chuỗi)
        System.out.println("Tên: " + name + ", Tuổi: " + age + ", Điểm TB: " + gpa);
        
        // Cách 2: Sử dụng printf (định dạng đẹp hơn)
        System.out.printf("Tên: %s, Tuổi: %d, Điểm TB: %.2f%n", name, age, gpa);
    }
}
```

**Kết quả**:
```
Tên: Nguyễn Văn A, Tuổi: 20, Điểm TB: 8.5
Tên: Nguyễn Văn A, Tuổi: 20, Điểm TB: 8.50
```

## IV. Nối chuỗi (String Concatenation)

### Toán tử + (Plus Operator)

Trong Java, bạn có thể sử dụng toán tử `+` để **nối chuỗi**:

```java
public class StringConcatenation {
    public static void main(String[] args) {
        String firstName = "Nguyễn";
        String lastName = "Văn A";
        
        // Nối 2 chuỗi
        String fullName = firstName + " " + lastName;
        System.out.println(fullName);  // Nguyễn Văn A
        
        // Nối chuỗi với số
        int age = 20;
        System.out.println("Tuổi: " + age);  // Tuổi: 20
        
        // Nối nhiều chuỗi
        System.out.println("Xin chào, tôi là " + fullName + " và tôi " + age + " tuổi.");
    }
}
```

**Kết quả**:
```
Nguyễn Văn A
Tuổi: 20
Xin chào, tôi là Nguyễn Văn A và tôi 20 tuổi.
```

### Lưu ý về thứ tự thực hiện

```java
public class OrderOfOperations {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        
        System.out.println("Tổng: " + a + b);      // "Tổng: 1020" (nối chuỗi)
        System.out.println("Tổng: " + (a + b));    // "Tổng: 30" (tính toán trước)
        System.out.println(a + b + " là tổng");     // "30 là tổng" (tính toán trước)
    }
}
```

**Giải thích**:
- Khi gặp chuỗi trước, Java sẽ **nối chuỗi** với các giá trị sau
- Khi gặp số trước, Java sẽ **tính toán** trước, sau đó nối chuỗi

## V. Định dạng số với printf()

### Định dạng số thực (Floating Point)

```java
public class FormatNumbers {
    public static void main(String[] args) {
        double pi = 3.14159265359;
        
        // Mặc định (6 chữ số thập phân)
        System.out.printf("Pi: %f%n", pi);
        // Kết quả: Pi: 3.141593
        
        // 2 chữ số thập phân
        System.out.printf("Pi: %.2f%n", pi);
        // Kết quả: Pi: 3.14
        
        // 4 chữ số thập phân
        System.out.printf("Pi: %.4f%n", pi);
        // Kết quả: Pi: 3.1416
    }
}
```

### Định dạng số nguyên với số 0 đứng trước

```java
public class FormatIntegers {
    public static void main(String[] args) {
        int number = 42;
        
        // 5 chữ số, thêm số 0 đứng trước nếu cần
        System.out.printf("Số: %05d%n", number);
        // Kết quả: Số: 00042
        
        // 10 chữ số, căn phải
        System.out.printf("Số: %10d%n", number);
        // Kết quả: Số:         42
        
        // 10 chữ số, căn trái
        System.out.printf("Số: %-10d%n", number);
        // Kết quả: Số: 42        
    }
}
```

### Ví dụ thực tế: In bảng

```java
public class TableExample {
    public static void main(String[] args) {
        System.out.println("=== BẢNG ĐIỂM SINH VIÊN ===");
        System.out.printf("%-20s %-10s %-10s%n", "Tên", "Tuổi", "Điểm TB");
        System.out.println("----------------------------------------");
        System.out.printf("%-20s %-10d %-10.2f%n", "Nguyễn Văn A", 20, 8.5);
        System.out.printf("%-20s %-10d %-10.2f%n", "Trần Thị B", 21, 9.0);
        System.out.printf("%-20s %-10d %-10.2f%n", "Lê Văn C", 19, 7.8);
    }
}
```

**Kết quả**:
```
=== BẢNG ĐIỂM SINH VIÊN ===
Tên                  Tuổi       Điểm TB   
----------------------------------------
Nguyễn Văn A         20         8.50      
Trần Thị B           21         9.00      
Lê Văn C             19         7.80      
```

## VI. Text Blocks (Java 15+) - Cách mới để in chuỗi nhiều dòng

### Text Blocks là gì?

Từ **Java 15** trở đi, bạn có thể sử dụng **Text Blocks** để viết chuỗi nhiều dòng một cách dễ dàng hơn (không cần `\n`).

**Cú pháp**: Sử dụng `"""` (ba dấu nháy kép)

```java
public class TextBlockExample {
    public static void main(String[] args) {
        // Cách cũ (trước Java 15)
        String oldWay = "Dòng 1\nDòng 2\nDòng 3";
        System.out.println(oldWay);
        
        // Cách mới (Java 15+)
        String newWay = """
            Dòng 1
            Dòng 2
            Dòng 3
            """;
        System.out.println(newWay);
        
        // Text Block với format
        String formatted = """
            Tên: %s
            Tuổi: %d
            Điểm TB: %.2f
            """.formatted("Nguyễn Văn A", 20, 8.5);
        System.out.println(formatted);
    }
}
```

**Kết quả**:
```
Dòng 1
Dòng 2
Dòng 3
Dòng 1
Dòng 2
Dòng 3
Tên: Nguyễn Văn A
Tuổi: 20
Điểm TB: 8.50
```

### Ưu điểm của Text Blocks

1. **Dễ đọc**: Code dễ đọc hơn nhiều
2. **Không cần escape**: Không cần dùng `\n`, `\"`, v.v.
3. **Giữ nguyên format**: Giữ nguyên cách trình bày trong code

```java
public class TextBlockAdvantages {
    public static void main(String[] args) {
        // In JSON dễ dàng
        String json = """
            {
                "name": "Nguyễn Văn A",
                "age": 20,
                "gpa": 8.5
            }
            """;
        System.out.println(json);
    }
}
```

## VII. Ví dụ thực tế

### Ví dụ 1: Hiển thị thông tin sinh viên

```java
public class StudentInfo {
    public static void main(String[] args) {
        String name = "Nguyễn Văn A";
        int age = 20;
        double gpa = 8.5;
        char grade = 'A';
        
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Điểm TB: " + gpa);
        System.out.println("Xếp loại: " + grade);
    }
}
```

### Ví dụ 2: Tính toán và hiển thị

```java
public class Calculation {
    public static void main(String[] args) {
        int a = 10;
        int b = 5;
        
        System.out.println("a = " + a);
        System.out.println("b = " + b);
        System.out.println("Tổng: " + (a + b));
        System.out.println("Hiệu: " + (a - b));
        System.out.println("Tích: " + (a * b));
        System.out.println("Thương: " + ((double)a / b));  // Ép kiểu để có số thực
    }
}
```

### Ví dụ 3: In hình tam giác

```java
public class Triangle {
    public static void main(String[] args) {
        System.out.println("    *");
        System.out.println("   ***");
        System.out.println("  *****");
        System.out.println(" *******");
        System.out.println("*********");
    }
}
```

**Kết quả**:
```
    *
   ***
  *****
 *******
*********
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu cách sử dụng `print()`, `println()`, và `printf()`
- ✅ Biết cách in ra các kiểu dữ liệu khác nhau
- ✅ Nắm được cách nối chuỗi với toán tử `+`
- ✅ Biết cách định dạng số với `printf()`
- ✅ Hiểu về Text Blocks (Java 15+) để viết chuỗi nhiều dòng

## Bài tập thực hành

1. **In ra thông tin cá nhân của bạn**:
   - Tên, tuổi, địa chỉ, sở thích
   - Sử dụng cả `println()` và `printf()`

2. **Tạo một chương trình tính toán**:
   - Nhập 2 số, tính tổng, hiệu, tích, thương
   - Hiển thị kết quả dưới dạng bảng

3. **In ra một menu**:
   ```
   === MENU ===
   1. Phở bò
   2. Bún chả
   3. Bánh mì
   4. Cơm tấm
   ```
   - Sử dụng Text Blocks (nếu dùng Java 15+)

## Tài liệu tham khảo

- [Oracle Java Tutorial - PrintStream](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html)
- [Java Text Blocks (Java 15+)](https://docs.oracle.com/en/java/javase/15/text-blocks/index.html)
- [Formatter Class (for printf)](https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
