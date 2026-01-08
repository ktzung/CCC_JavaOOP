# Bài 11: Nhập dữ liệu trong Java (Java Input)

> **Mục tiêu**: Hiểu cách nhập dữ liệu từ bàn phím trong Java, sử dụng lớp `Scanner` để đọc các kiểu dữ liệu khác nhau, và xử lý các lỗi thường gặp.

## I. Giới thiệu về nhập dữ liệu

### Tại sao cần nhập dữ liệu?

Trong các bài trước, chúng ta đã học cách **xuất dữ liệu** (hiển thị kết quả ra màn hình). Bây giờ chúng ta cần học cách **nhập dữ liệu** (lấy dữ liệu từ người dùng) để tạo ra các chương trình **tương tác**.

**Ví dụ đơn giản**:
- Chương trình tính tổng 2 số: Cần người dùng nhập 2 số
- Chương trình đăng nhập: Cần người dùng nhập tên và mật khẩu
- Form đăng ký: Cần người dùng nhập thông tin

### Scanner Class - Công cụ chính để nhập dữ liệu

**Scanner** là một lớp trong Java được sử dụng để đọc dữ liệu từ nhiều nguồn khác nhau:
- **Bàn phím** (System.in) - Phổ biến nhất
- **File** - Đọc từ file
- **Chuỗi** (String) - Đọc từ chuỗi ký tự

**Vị trí**: Lớp `Scanner` nằm trong package `java.util`

## II. Cách sử dụng Scanner

### 1. Import Scanner

Trước khi sử dụng `Scanner`, bạn cần **import** nó:

```java
import java.util.Scanner;  // Import Scanner class
```

### 2. Tạo đối tượng Scanner

Để nhập dữ liệu từ **bàn phím**, bạn tạo đối tượng Scanner như sau:

```java
Scanner scanner = new Scanner(System.in);
```

**Giải thích**:
- `Scanner` - Tên lớp
- `scanner` - Tên đối tượng (bạn có thể đặt tên khác)
- `new Scanner(System.in)` - Tạo đối tượng Scanner để đọc từ bàn phím
  - `System.in` - Đại diện cho đầu vào chuẩn (standard input) - bàn phím

### 3. Đọc dữ liệu

Sau khi tạo đối tượng Scanner, bạn có thể sử dụng các phương thức để đọc các kiểu dữ liệu khác nhau:

```java
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập tên của bạn: ");
        String name = scanner.nextLine();  // Đọc chuỗi
        
        System.out.print("Nhập tuổi: ");
        int age = scanner.nextInt();  // Đọc số nguyên
        
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        
        scanner.close();  // Đóng Scanner khi không dùng nữa
    }
}
```

**Lưu ý quan trọng**: Sau khi sử dụng xong, nên **đóng Scanner** bằng `scanner.close()` để giải phóng tài nguyên.

## III. Các phương thức phổ biến của Scanner

### Bảng tóm tắt các phương thức

| Phương thức | Kiểu trả về | Mô tả | Ví dụ |
|-------------|-------------|-------|-------|
| `nextByte()` | `byte` | Đọc một giá trị byte | `byte b = scanner.nextByte();` |
| `nextShort()` | `short` | Đọc một giá trị short | `short s = scanner.nextShort();` |
| `nextInt()` | `int` | Đọc một giá trị int | `int i = scanner.nextInt();` |
| `nextLong()` | `long` | Đọc một giá trị long | `long l = scanner.nextLong();` |
| `nextFloat()` | `float` | Đọc một giá trị float | `float f = scanner.nextFloat();` |
| `nextDouble()` | `double` | Đọc một giá trị double | `double d = scanner.nextDouble();` |
| `nextBoolean()` | `boolean` | Đọc một giá trị boolean | `boolean b = scanner.nextBoolean();` |
| `next()` | `String` | Đọc một từ (trước khoảng trắng) | `String s = scanner.next();` |
| `nextLine()` | `String` | Đọc một dòng (cả chuỗi) | `String s = scanner.nextLine();` |

### Chi tiết từng phương thức

#### 1. Đọc số nguyên

```java
import java.util.Scanner;

public class IntegerInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập một số nguyên: ");
        int number = scanner.nextInt();
        
        System.out.println("Số bạn vừa nhập: " + number);
        
        scanner.close();
    }
}
```

**Lưu ý**: 
- `nextInt()` chỉ đọc số nguyên, không đọc phần thập phân
- Nếu nhập sai định dạng (ví dụ: nhập chữ), sẽ bị lỗi `InputMismatchException`

#### 2. Đọc số thực

```java
import java.util.Scanner;

public class DoubleInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập một số thực: ");
        double number = scanner.nextDouble();
        
        System.out.println("Số bạn vừa nhập: " + number);
        
        scanner.close();
    }
}
```

**Ví dụ input/output**:
```
Nhập một số thực: 3.14159
Số bạn vừa nhập: 3.14159
```

#### 3. Đọc Boolean

```java
import java.util.Scanner;

public class BooleanInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập true hoặc false: ");
        boolean value = scanner.nextBoolean();
        
        System.out.println("Giá trị: " + value);
        
        scanner.close();
    }
}
```

**Lưu ý**: Chỉ nhận `true` hoặc `false` (chữ thường)

## IV. Đọc chuỗi - next() vs nextLine()

### Sự khác biệt quan trọng

Đây là một điểm **quan trọng** và thường gây nhầm lẫn:

| Phương thức | Hành vi | Ví dụ input | Kết quả |
|-------------|---------|-------------|---------|
| `next()` | Đọc **một từ** (trước khoảng trắng) | `"Hello World"` | `"Hello"` |
| `nextLine()` | Đọc **cả dòng** (toàn bộ chuỗi) | `"Hello World"` | `"Hello World"` |

### Ví dụ minh họa

```java
import java.util.Scanner;

public class StringInputComparison {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Test next()
        System.out.print("Nhập chuỗi (sử dụng next()): ");
        String str1 = scanner.next();
        System.out.println("Kết quả: '" + str1 + "'");
        System.out.println("Độ dài: " + str1.length());
        
        // Xóa dòng còn lại trong buffer
        scanner.nextLine();
        
        // Test nextLine()
        System.out.print("\nNhập chuỗi (sử dụng nextLine()): ");
        String str2 = scanner.nextLine();
        System.out.println("Kết quả: '" + str2 + "'");
        System.out.println("Độ dài: " + str2.length());
        
        scanner.close();
    }
}
```

**Input**:
```
Nhập chuỗi (sử dụng next()): Hello World
Nhập chuỗi (sử dụng nextLine()): Hello World
```

**Output**:
```
Kết quả: 'Hello'
Độ dài: 5

Kết quả: 'Hello World'
Độ dài: 11
```

### Khi nào dùng next() và nextLine()?

**Sử dụng `next()` khi**:
- Chỉ cần đọc một từ
- Ví dụ: Đọc tên người dùng (không có khoảng trắng)

**Sử dụng `nextLine()` khi**:
- Cần đọc cả dòng (có khoảng trắng)
- Ví dụ: Đọc địa chỉ, mô tả, tên đầy đủ

**Ví dụ thực tế**:
```java
import java.util.Scanner;

public class UserInfo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập username (không có khoảng trắng): ");
        String username = scanner.next();  // Sử dụng next()
        
        // Xóa dòng còn lại
        scanner.nextLine();
        
        System.out.print("Nhập địa chỉ đầy đủ: ");
        String address = scanner.nextLine();  // Sử dụng nextLine()
        
        System.out.println("\nUsername: " + username);
        System.out.println("Địa chỉ: " + address);
        
        scanner.close();
    }
}
```

## V. Vấn đề thường gặp: Mixing nextInt() và nextLine()

### Vấn đề

Khi sử dụng `nextInt()`, `nextDouble()`, v.v. rồi sau đó dùng `nextLine()`, có thể gặp vấn đề:

```java
import java.util.Scanner;

public class MixingProblem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập tuổi: ");
        int age = scanner.nextInt();  // Nhập 20 và nhấn Enter
        
        System.out.print("Nhập tên: ");
        String name = scanner.nextLine();  // ❌ Sẽ đọc luôn ký tự Enter!
        
        System.out.println("Tuổi: " + age);
        System.out.println("Tên: '" + name + "'");  // Tên sẽ rỗng!
        
        scanner.close();
    }
}
```

**Giải thích**:
- Khi nhập số và nhấn Enter, `nextInt()` đọc số nhưng **bỏ qua Enter**
- Enter (`\n`) vẫn còn trong buffer
- `nextLine()` đọc luôn Enter đó → chuỗi rỗng

### Giải pháp

**Cách 1: Thêm một nextLine() để xóa buffer**
```java
import java.util.Scanner;

public class FixMixingProblem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập tuổi: ");
        int age = scanner.nextInt();
        
        scanner.nextLine();  // ✅ Xóa Enter trong buffer
        
        System.out.print("Nhập tên: ");
        String name = scanner.nextLine();  // Bây giờ sẽ đọc đúng
        
        System.out.println("Tuổi: " + age);
        System.out.println("Tên: " + name);
        
        scanner.close();
    }
}
```

**Cách 2: Luôn dùng nextLine() rồi chuyển đổi kiểu**
```java
import java.util.Scanner;

public class FixMixingProblem2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập tuổi: ");
        int age = Integer.parseInt(scanner.nextLine());  // Đọc chuỗi rồi chuyển
        
        System.out.print("Nhập tên: ");
        String name = scanner.nextLine();
        
        System.out.println("Tuổi: " + age);
        System.out.println("Tên: " + name);
        
        scanner.close();
    }
}
```

**Cách 2 khuyến nghị hơn** vì tránh được vấn đề mixing và dễ xử lý lỗi hơn.

## VI. Kiểm tra dữ liệu nhập vào

### Sử dụng hasNext...() để kiểm tra

Scanner cung cấp các phương thức để **kiểm tra** xem có dữ liệu đúng kiểu hay không:

| Phương thức | Kiểm tra | Ví dụ |
|-------------|----------|-------|
| `hasNextInt()` | Có số nguyên không? | `if (scanner.hasNextInt())` |
| `hasNextDouble()` | Có số thực không? | `if (scanner.hasNextDouble())` |
| `hasNextBoolean()` | Có boolean không? | `if (scanner.hasNextBoolean())` |
| `hasNextLine()` | Có dòng tiếp theo không? | `if (scanner.hasNextLine())` |
| `hasNext()` | Có từ tiếp theo không? | `if (scanner.hasNext())` |

**Ví dụ**:
```java
import java.util.Scanner;

public class CheckInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập một số nguyên: ");
        
        if (scanner.hasNextInt()) {
            int number = scanner.nextInt();
            System.out.println("Số bạn nhập: " + number);
        } else {
            String invalid = scanner.next();
            System.out.println("'" + invalid + "' không phải là số nguyên!");
        }
        
        scanner.close();
    }
}
```

### Ví dụ xử lý nhập lặp lại cho đến khi đúng

```java
import java.util.Scanner;

public class ValidInputLoop {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int age = -1;
        
        // Lặp lại cho đến khi nhập đúng
        while (age < 0) {
            System.out.print("Nhập tuổi (>= 0): ");
            
            if (scanner.hasNextInt()) {
                age = scanner.nextInt();
                
                if (age < 0) {
                    System.out.println("Tuổi phải >= 0. Vui lòng nhập lại!");
                }
            } else {
                String invalid = scanner.next();
                System.out.println("'" + invalid + "' không phải là số nguyên. Vui lòng nhập lại!");
            }
        }
        
        System.out.println("Bạn đã nhập tuổi: " + age);
        scanner.close();
    }
}
```

## VII. Ví dụ thực tế

### Ví dụ 1: Chương trình tính tổng 2 số

```java
import java.util.Scanner;

public class SumTwoNumbers {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== TÍNH TỔNG HAI SỐ ===");
        
        System.out.print("Nhập số thứ nhất: ");
        double num1 = scanner.nextDouble();
        
        System.out.print("Nhập số thứ hai: ");
        double num2 = scanner.nextDouble();
        
        double sum = num1 + num2;
        
        System.out.println("\nKết quả:");
        System.out.printf("%.2f + %.2f = %.2f%n", num1, num2, sum);
        
        scanner.close();
    }
}
```

### Ví dụ 2: Form đăng ký sinh viên

```java
import java.util.Scanner;

public class StudentRegistration {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== ĐĂNG KÝ SINH VIÊN ===\n");
        
        // Nhập thông tin
        System.out.print("Nhập mã sinh viên: ");
        String studentId = scanner.nextLine();
        
        System.out.print("Nhập họ tên: ");
        String fullName = scanner.nextLine();
        
        System.out.print("Nhập tuổi: ");
        int age = Integer.parseInt(scanner.nextLine());
        
        System.out.print("Nhập điểm trung bình: ");
        double gpa = Double.parseDouble(scanner.nextLine());
        
        System.out.print("Nhập email: ");
        String email = scanner.nextLine();
        
        // Hiển thị thông tin
        System.out.println("\n=== THÔNG TIN ĐÃ ĐĂNG KÝ ===");
        System.out.println("Mã SV: " + studentId);
        System.out.println("Họ tên: " + fullName);
        System.out.println("Tuổi: " + age);
        System.out.println("Điểm TB: " + gpa);
        System.out.println("Email: " + email);
        
        scanner.close();
    }
}
```

### Ví dụ 3: Menu tương tác

```java
import java.util.Scanner;

public class MenuExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;
        
        while (running) {
            System.out.println("\n=== MENU ===");
            System.out.println("1. Xem thông tin");
            System.out.println("2. Cập nhật thông tin");
            System.out.println("3. Xóa thông tin");
            System.out.println("0. Thoát");
            System.out.print("Chọn: ");
            
            int choice = Integer.parseInt(scanner.nextLine());
            
            switch (choice) {
                case 1:
                    System.out.println("Đã chọn: Xem thông tin");
                    break;
                case 2:
                    System.out.println("Đã chọn: Cập nhật thông tin");
                    break;
                case 3:
                    System.out.println("Đã chọn: Xóa thông tin");
                    break;
                case 0:
                    System.out.println("Tạm biệt!");
                    running = false;
                    break;
                default:
                    System.out.println("Lựa chọn không hợp lệ!");
            }
        }
        
        scanner.close();
    }
}
```

## VIII. Best Practices

### 1. Luôn đóng Scanner

```java
Scanner scanner = new Scanner(System.in);
// ... sử dụng scanner ...
scanner.close();  // ✅ Đóng sau khi dùng xong
```

### 2. Sử dụng try-with-resources (Java 7+)

Tự động đóng Scanner khi không còn dùng:

```java
import java.util.Scanner;

public class TryWithResources {
    public static void main(String[] args) {
        // ✅ Tự động đóng Scanner khi kết thúc block
        try (Scanner scanner = new Scanner(System.in)) {
            System.out.print("Nhập tên: ");
            String name = scanner.nextLine();
            System.out.println("Tên: " + name);
        }  // Scanner tự động đóng ở đây
    }
}
```

### 3. Xử lý lỗi nhập không hợp lệ

```java
import java.util.Scanner;

public class ErrorHandling {
    public static int readInt(Scanner scanner, String prompt) {
        while (true) {
            System.out.print(prompt);
            if (scanner.hasNextInt()) {
                return scanner.nextInt();
            } else {
                String invalid = scanner.next();
                System.out.println("'" + invalid + "' không phải số nguyên. Vui lòng nhập lại!");
            }
        }
    }
    
    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(System.in)) {
            int age = readInt(scanner, "Nhập tuổi: ");
            System.out.println("Tuổi: " + age);
        }
    }
}
```

## IX. So sánh các cách nhập dữ liệu

| Cách | Ưu điểm | Nhược điểm | Khi nào dùng |
|------|---------|------------|--------------|
| `nextInt()` | Nhanh, tiện lợi | Có vấn đề với nextLine() | Khi chắc chắn input là số |
| `nextLine()` + `parseInt()` | Tránh vấn đề mixing | Phải xử lý lỗi parse | **Khuyến nghị** cho mọi trường hợp |
| `hasNextInt()` | An toàn | Code dài hơn | Khi cần kiểm tra trước |

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu cách nhập dữ liệu từ bàn phím bằng Scanner
- ✅ Nắm được các phương thức đọc các kiểu dữ liệu khác nhau
- ✅ Phân biệt được `next()` và `nextLine()`
- ✅ Biết cách xử lý vấn đề mixing nextInt() và nextLine()
- ✅ Biết cách kiểm tra và xử lý lỗi nhập không hợp lệ
- ✅ Áp dụng vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo chương trình tính chu vi và diện tích hình chữ nhật**:
   - Nhập chiều dài và chiều rộng
   - Tính và hiển thị chu vi, diện tích

2. **Tạo form đăng nhập**:
   - Nhập username và password
   - Kiểm tra và hiển thị kết quả

3. **Tạo chương trình quản lý sinh viên**:
   - Nhập thông tin: mã SV, tên, tuổi, điểm TB
   - Hiển thị thông tin dưới dạng bảng
   - Xử lý lỗi nhập không hợp lệ

## Tài liệu tham khảo

- [Oracle Java Tutorial - Scanner](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html)
- [Java Scanner Class](https://www.javatpoint.com/scanner-class-in-java)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
