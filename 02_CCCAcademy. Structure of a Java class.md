# Bài 2: Cấu trúc của một lớp Java

> **Mục tiêu**: Hiểu được cấu trúc cơ bản của một lớp Java, cách viết chương trình Java đơn giản, và các quy tắc đặt tên trong Java.

## I. Ôn tập kiến thức

Trước khi bắt đầu với Java, nếu bạn đã học qua ngôn ngữ lập trình C hoặc các ngôn ngữ lập trình cấu trúc khác, bạn sẽ thấy nhiều khái niệm tương tự:

### Các kiến thức tương tự giữa C và Java:

- **Câu lệnh rẽ nhánh**:
  - `if - else`: Kiểm tra điều kiện và thực hiện khối code tương ứng
  - `switch - case`: Chọn một trong nhiều lựa chọn dựa trên giá trị

- **Vòng lặp**:
  - `for`: Lặp với số lần xác định
  - `while`: Lặp khi điều kiện còn đúng
  - `do-while`: Lặp ít nhất một lần rồi kiểm tra điều kiện
  - `break`: Thoát khỏi vòng lặp
  - `continue`: Bỏ qua lần lặp hiện tại, tiếp tục lần lặp tiếp theo

- **Toán tử**:
  - **Toán tử toán học** (Arithmetic Operators): `+`, `-`, `*`, `/`, `%`
  - **Toán tử tăng/giảm** (Increment/Decrement): `++`, `--`
  - **Toán tử gán** (Assignment): `=`, `+=`, `-=`, `*=`, `/=`
  - **Toán tử quan hệ** (Relational): `==`, `!=`, `<`, `>`, `<=`, `>=`
  - **Toán tử logic** (Logical): `&&` (và), `||` (hoặc), `!` (phủ định)

- **Chuyển đổi kiểu** (Type Conversion):
  - **Chuyển đổi ngầm định** (Implicit): Tự động chuyển đổi (ví dụ: int → long)
  - **Chuyển đổi tường minh** (Explicit): Ép kiểu bằng cách khai báo rõ ràng (ví dụ: `(int) doubleValue`)

- **Hàm/Phương thức** (Functions/Methods):
  - Trong C gọi là "function", trong Java gọi là "method"
  - Cả hai đều là khối code có tên, có thể nhận tham số và trả về giá trị

> **Lưu ý**: Java không có hàm độc lập như C. Tất cả các hàm trong Java đều phải nằm trong một lớp (class).

## II. Chương trình Java đầu tiên

### Cấu trúc cơ bản của một lớp Java

Một lớp Java đơn giản có cấu trúc như sau:

```java
public class TenClass {
    // Các trường (Fields) - biến của lớp
    int soTuoi;
    String ten;
    
    // Phương thức main - điểm bắt đầu của chương trình
    public static void main(String[] args) {
        // Code của bạn ở đây
        System.out.println("Xin chào Java!");
    }
    
    // Các phương thức khác
    public void hienThiThongTin() {
        System.out.println("Tên: " + ten);
        System.out.println("Tuổi: " + soTuoi);
    }
}
```

### Giải thích từng phần:

#### 1. Khai báo lớp (Class Declaration)

```java
public class TenClass {
```

- `public`: Từ khóa chỉ định phạm vi truy cập. `public` nghĩa là lớp này có thể được truy cập từ bất kỳ đâu
- `class`: Từ khóa để khai báo một lớp
- `TenClass`: Tên của lớp
  - Phải bắt đầu bằng chữ cái hoặc dấu gạch dưới
  - Theo quy ước: Viết hoa chữ cái đầu mỗi từ (PascalCase)
  - Tên lớp phải trùng với tên file (ví dụ: `TenClass.java`)
- `{`: Mở khối code của lớp

#### 2. Trường (Fields) - Thuộc tính của lớp

```java
int soTuoi;
String ten;
```

- Trường là các biến lưu trữ dữ liệu của lớp
- `int`: Kiểu dữ liệu số nguyên
- `String`: Kiểu dữ liệu chuỗi ký tự
- `soTuoi`, `ten`: Tên của trường (theo quy ước: camelCase - viết thường chữ đầu, viết hoa chữ đầu các từ tiếp theo)

#### 3. Phương thức main (Main Method)

```java
public static void main(String[] args) {
    // Code của bạn
}
```

Đây là phương thức **đặc biệt** trong Java:
- **Bắt buộc**: Mọi chương trình Java chạy được đều phải có phương thức `main`
- **Điểm bắt đầu**: JVM sẽ tìm và chạy phương thức `main` đầu tiên
- **Cú pháp cố định**: Phải khai báo chính xác như trên

**Giải thích chi tiết**:
- `public`: Có thể truy cập từ bất kỳ đâu
- `static`: Thuộc về lớp, không cần tạo đối tượng để gọi
- `void`: Không trả về giá trị
- `main`: Tên phương thức (bắt buộc)
- `String[] args`: Tham số nhận mảng chuỗi ký tự từ dòng lệnh (command line arguments)

#### 4. Các phương thức khác (Other Methods)

```java
public void hienThiThongTin() {
    // Code của phương thức
}
```

- Phương thức là các hành động mà lớp có thể thực hiện
- Có thể có nhiều phương thức trong một lớp
- Mỗi phương thức có tên và chức năng riêng

### Ví dụ hoàn chỉnh: Chương trình đơn giản

```java
public class HelloWorld {
    // Phương thức main - điểm bắt đầu
    public static void main(String[] args) {
        // In ra màn hình
        System.out.println("Xin chào, đây là chương trình Java đầu tiên!");
        System.out.println("Tôi đang học lập trình Java.");
        
        // Khai báo biến
        String ten = "Nguyễn Văn A";
        int tuoi = 20;
        
        // In ra thông tin
        System.out.println("Tên: " + ten);
        System.out.println("Tuổi: " + tuoi);
    }
}
```

**Kết quả khi chạy**:
```
Xin chào, đây là chương trình Java đầu tiên!
Tôi đang học lập trình Java.
Tên: Nguyễn Văn A
Tuổi: 20
```

## III. Quy tắc đặt tên trong Java (Naming Conventions)

Java có các quy tắc đặt tên cụ thể để code dễ đọc và nhất quán:

### 1. Tên lớp (Class Names)

- **Quy tắc**: Viết hoa chữ cái đầu mỗi từ (PascalCase)
- **Ví dụ**: 
  - ✅ Đúng: `Student`, `Car`, `BankAccount`, `HelloWorld`
  - ❌ Sai: `student`, `car`, `bankAccount`, `HELLOWORLD`

### 2. Tên phương thức (Method Names)

- **Quy tắc**: Viết thường chữ đầu, viết hoa chữ đầu các từ tiếp theo (camelCase)
- Thường là động từ hoặc cụm động từ
- **Ví dụ**:
  - ✅ Đúng: `getName()`, `setAge()`, `calculateTotal()`, `hienThiThongTin()`
  - ❌ Sai: `GetName()`, `SET_AGE()`, `calculate_total()`

### 3. Tên biến và trường (Variable and Field Names)

- **Quy tắc**: camelCase (giống phương thức)
- Nên đặt tên có ý nghĩa, mô tả rõ ràng
- **Ví dụ**:
  - ✅ Đúng: `age`, `studentName`, `totalAmount`, `soLuong`
  - ❌ Sai: `Age`, `STUDENT_NAME`, `total_amount`, `x`, `temp`

### 4. Hằng số (Constants)

- **Quy tắc**: Tất cả chữ hoa, các từ cách nhau bằng dấu gạch dưới (UPPER_SNAKE_CASE)
- **Ví dụ**:
  - ✅ Đúng: `MAX_SIZE`, `PI`, `DEFAULT_TIMEOUT`, `SO_HOC_SINH_TOI_DA`
  - ❌ Sai: `maxSize`, `MaxSize`, `pi`

### 5. Gói (Package Names)

- **Quy tắc**: Tất cả chữ thường, các từ cách nhau bằng dấu chấm
- Thường là tên miền đảo ngược
- **Ví dụ**:
  - ✅ Đúng: `com.cccacademy.student`, `java.util`, `org.example`

### 6. Tên file

- **Quy tắc**: Phải trùng với tên lớp chính, có phần mở rộng `.java`
- **Ví dụ**: 
  - Lớp `HelloWorld` → File `HelloWorld.java`
  - Lớp `Student` → File `Student.java`

## IV. Cấu trúc file Java

### Một file Java hoàn chỉnh

```java
// Package declaration (khai báo gói) - tùy chọn
package com.cccacademy.baihoc;

// Import statements (khai báo import) - tùy chọn
import java.util.Scanner;
import java.util.Date;

// Class declaration (khai báo lớp) - bắt buộc
public class TenLop {
    
    // Class variables/Fields (Biến lớp) - tùy chọn
    private String ten;
    private int tuoi;
    
    // Constructor (Hàm khởi tạo) - tùy chọn
    public TenLop(String ten, int tuoi) {
        this.ten = ten;
        this.tuoi = tuoi;
    }
    
    // Main method (Phương thức main) - bắt buộc nếu muốn chạy chương trình
    public static void main(String[] args) {
        // Code của chương trình
    }
    
    // Other methods (Các phương thức khác) - tùy chọn
    public void hienThi() {
        System.out.println("Tên: " + ten);
        System.out.println("Tuổi: " + tuoi);
    }
}
```

### Giải thích thứ tự:

1. **Package declaration** (nếu có): Khai báo gói mà lớp thuộc về
2. **Import statements** (nếu có): Import các lớp từ thư viện khác
3. **Class declaration**: Khai báo lớp chính
4. **Fields**: Các biến của lớp
5. **Constructors**: Hàm khởi tạo (sẽ học ở bài sau)
6. **Methods**: Các phương thức, bao gồm `main`

## V. Ví dụ thực tế: Lớp Sinh viên

```java
public class Student {
    // Các trường (thuộc tính)
    String ten;
    int tuoi;
    double diemTrungBinh;
    
    // Phương thức main
    public static void main(String[] args) {
        // Tạo đối tượng Student
        Student sv1 = new Student();
        
        // Gán giá trị cho các trường
        sv1.ten = "Nguyễn Văn A";
        sv1.tuoi = 20;
        sv1.diemTrungBinh = 8.5;
        
        // Gọi phương thức hiển thị
        sv1.hienThiThongTin();
    }
    
    // Phương thức hiển thị thông tin
    public void hienThiThongTin() {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + ten);
        System.out.println("Tuổi: " + tuoi);
        System.out.println("Điểm TB: " + diemTrungBinh);
    }
}
```

**Kết quả**:
```
=== THÔNG TIN SINH VIÊN ===
Tên: Nguyễn Văn A
Tuổi: 20
Điểm TB: 8.5
```

## VI. Các lỗi thường gặp

### 1. Tên lớp không trùng với tên file

```java
// File: HelloWorld.java
public class Hello {  // ❌ SAI! Tên lớp khác tên file
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

**Sửa**: Đổi tên lớp thành `HelloWorld` hoặc đổi tên file thành `Hello.java`

### 2. Thiếu phương thức main

```java
public class Test {
    // ❌ SAI! Không có phương thức main
    public void xinChao() {
        System.out.println("Xin chào");
    }
}
```

**Sửa**: Thêm phương thức `main` hoặc gọi `xinChao()` từ phương thức khác

### 3. Viết hoa/sai chữ cái trong phương thức main

```java
public class Test {
    public static void Main(String[] args) {  // ❌ SAI! Main phải là main (chữ thường)
        System.out.println("Hello");
    }
}
```

**Sửa**: Đổi `Main` thành `main` (chữ thường)

### 4. Thiếu dấu ngoặc nhọn

```java
public class Test  // ❌ SAI! Thiếu dấu {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

**Sửa**: Thêm dấu `{` sau `Test`

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu cấu trúc cơ bản của một lớp Java
- ✅ Biết cách viết phương thức `main` - điểm bắt đầu của chương trình
- ✅ Nắm được quy tắc đặt tên trong Java
- ✅ Biết cấu trúc của một file Java hoàn chỉnh
- ✅ Tránh được các lỗi thường gặp

## Bài tập thực hành

1. **Viết chương trình in ra màn hình thông tin cá nhân của bạn**:
   - Tên
   - Tuổi
   - Nơi ở
   - Sở thích

2. **Tạo lớp `Car` (Ô tô) với**:
   - Các trường: `tenXe`, `mauSac`, `giaTien`
   - Phương thức `main` để tạo và hiển thị thông tin một chiếc xe

3. **Tạo lớp `Rectangle` (Hình chữ nhật) với**:
   - Các trường: `chieuDai`, `chieuRong`
   - Phương thức `main` để tính và in ra diện tích hình chữ nhật

4. **Kiểm tra các quy tắc đặt tên**:
   - Tạo các biến với tên đúng quy tắc
   - Tạo các biến với tên sai quy tắc (xem IDE báo lỗi gì)

## Tài liệu tham khảo

- [Oracle Java Naming Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html)
- [Java Documentation - Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/classes.html)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
