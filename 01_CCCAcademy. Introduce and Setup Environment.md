# Bài 1: Giới thiệu và Cài đặt môi trường

> **Dành cho người mới bắt đầu**: Bài học này sẽ giúp bạn hiểu Java là gì, tại sao nó quan trọng, và cách cài đặt môi trường để bắt đầu học lập trình Java.

## I. Giới thiệu về ngôn ngữ Java

### Java là gì?

**Java** là một ngôn ngữ lập trình phổ biến, được tạo ra bởi Sun Microsystems (hiện thuộc Oracle) vào năm 1995. Java được thiết kế với triết lý "Write Once, Run Anywhere" (Viết một lần, chạy mọi nơi), nghĩa là bạn chỉ cần viết code một lần, và nó có thể chạy trên bất kỳ thiết bị nào có cài đặt môi trường Java.

### Tại sao nên học Java?

1. **Dễ học**: Cú pháp Java gần giống với ngôn ngữ tự nhiên, rất dễ đọc và hiểu
2. **Phổ biến**: Java được sử dụng rộng rãi trong nhiều lĩnh vực:
   - Ứng dụng web (backend)
   - Ứng dụng di động (Android)
   - Ứng dụng doanh nghiệp
   - Hệ thống nhúng
3. **Cộng đồng lớn**: Có rất nhiều tài liệu, tutorial và người sẵn sàng giúp đỡ
4. **Nhiều cơ hội việc làm**: Java developers luôn được săn đón trên thị trường

### Lịch sử phát triển của Java

- **1991**: Nhóm do James Gosling dẫn đầu tại Sun Microsystems thiết kế một ngôn ngữ lập trình, có tên mã là _Green_, để sử dụng cho các thiết bị tiêu dùng như tivi thông minh
- **1996**: Java 1.0 được phát hành công khai
- **2005**: Java 5 ra đời với nhiều cải tiến lớn
- **2014**: Java 8 LTS (Long Term Support) - hỗ trợ đến 2022
- **2018**: Java 11 LTS - hỗ trợ đến 2023
- **2021**: Java 17 LTS - hỗ trợ đến 2026 (khuyến nghị sử dụng hiện tại)
- **2023**: Java 21 LTS - hỗ trợ đến 2028

> **Lưu ý**: Từ Java 9 trở đi, Oracle áp dụng chu kỳ phát hành 6 tháng một lần. Các phiên bản LTS (Long Term Support) được hỗ trợ lâu dài và được khuyến nghị sử dụng cho các dự án sản xuất.

### JDK, JRE và JVM - Hiểu đúng để tránh nhầm lẫn

Khi học Java, bạn sẽ nghe nhiều về JDK, JRE và JVM. Đây là ba thành phần khác nhau nhưng liên quan chặt chẽ với nhau:

#### JVM (Java Virtual Machine - Máy ảo Java)
- **Là gì?**: JVM là một chương trình chạy code Java
- **Nhiệm vụ**: 
  - Đọc code đã được biên dịch (bytecode) 
  - Chuyển đổi bytecode thành mã máy mà máy tính có thể hiểu
  - Chạy chương trình Java

**Ví dụ đơn giản**: Giống như một phiên dịch viên, JVM "dịch" code Java sang ngôn ngữ mà máy tính hiểu được.

#### JRE (Java Runtime Environment - Môi trường chạy Java)
- **Là gì?**: JRE là môi trường để chạy các ứng dụng Java
- **Bao gồm**:
  - JVM
  - Các thư viện cần thiết để chạy ứng dụng Java
  - Các công cụ hỗ trợ khác

**Khi nào dùng**: Khi bạn chỉ muốn chạy các ứng dụng Java mà người khác đã viết (không cần viết code)

#### JDK (Java Development Kit - Bộ công cụ phát triển Java)
- **Là gì?**: JDK là bộ công cụ đầy đủ để phát triển ứng dụng Java
- **Bao gồm**:
  - JRE (có JVM bên trong)
  - Trình biên dịch Java (javac) - chuyển code .java thành bytecode .class
  - Các công cụ phát triển khác (debugger, documentation generator, v.v.)

**Khi nào dùng**: Khi bạn muốn viết và chạy các ứng dụng Java của chính mình

**Mối quan hệ**:
```
JDK = JRE + Công cụ phát triển
JRE = JVM + Thư viện cần thiết
```

> **Ghi nhớ đơn giản**: 
> - **JVM**: Để chạy code
> - **JRE**: Để chạy ứng dụng (chứa JVM)
> - **JDK**: Để viết và chạy ứng dụng (chứa JRE)

### Quy trình biên dịch và chạy chương trình Java

Khi bạn viết một chương trình Java, quy trình diễn ra như sau:

1. **Viết code** (file `.java`)
   - Bạn viết code bằng ngôn ngữ Java
   - Ví dụ: `HelloWorld.java`

2. **Biên dịch** (Compile)
   - Trình biên dịch `javac` chuyển code Java thành bytecode
   - File `.class` được tạo ra
   - Ví dụ: `HelloWorld.class`

3. **Chạy** (Run)
   - JVM đọc file bytecode `.class`
   - JVM chuyển đổi bytecode thành mã máy
   - Chương trình chạy trên máy tính

```
Java Source Code (.java) 
    → [javac compiler] 
    → Bytecode (.class) 
    → [JVM] 
    → Machine Code 
    → [Computer] 
    → Program Runs
```

**Lợi ích của cách này**:
- Code Java chạy được trên mọi hệ điều hành (Windows, Mac, Linux)
- Chỉ cần có JVM cài đặt trên máy

## II. Cài đặt môi trường và phần mềm

### Bước 1: Cài đặt JDK

#### Cách 1: Tải từ Oracle (Khuyến nghị cho người mới)

1. **Truy cập website**: https://www.oracle.com/java/technologies/downloads/
2. **Chọn phiên bản**: Java 17 LTS hoặc Java 21 LTS (khuyến nghị)
3. **Chọn hệ điều hành**: Windows, macOS, hoặc Linux
4. **Tải file cài đặt**:
   - Windows: `.exe` (Installer)
   - macOS: `.dmg` hoặc `.pkg`
   - Linux: `.tar.gz` hoặc `.deb`/`.rpm`
5. **Chạy file cài đặt** và làm theo hướng dẫn

#### Cách 2: Sử dụng OpenJDK (Miễn phí, mã nguồn mở)

1. **Truy cập**: https://adoptium.net/ hoặc https://www.azul.com/downloads/
2. Chọn phiên bản và tải về
3. Cài đặt như cách 1

#### Kiểm tra cài đặt thành công

Mở Terminal (Mac/Linux) hoặc Command Prompt (Windows) và gõ:

```bash
java -version
```

Bạn sẽ thấy thông tin phiên bản Java, ví dụ:
```
java version "17.0.8" 2023-07-18 LTS
Java(TM) SE Runtime Environment (build 17.0.8+9-LTS-211)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.8+9-LTS-211, mixed mode, sharing)
```

Kiểm tra trình biên dịch:
```bash
javac -version
```

Kết quả sẽ hiển thị phiên bản của javac, ví dụ:
```
javac 17.0.8
```

> **Lưu ý**: Nếu thấy lỗi "command not found" hoặc "không nhận diện được lệnh", có thể bạn cần cài đặt lại hoặc thiết lập biến môi trường PATH. Hãy tham khảo hướng dẫn chi tiết trong tài liệu chính thức.

### Bước 2: Cài đặt IDE (Môi trường phát triển tích hợp)

IDE giúp bạn viết code dễ dàng hơn nhiều với các tính năng như:
- Tô màu cú pháp (syntax highlighting)
- Tự động hoàn thành code (code completion)
- Tìm lỗi trước khi chạy (error detection)
- Debug (tìm và sửa lỗi)
- Quản lý dự án

#### Lựa chọn IDE phổ biến:

1. **IntelliJ IDEA** (Khuyến nghị - miễn phí với phiên bản Community)
   - Website: https://www.jetbrains.com/idea/download/
   - Ưu điểm: Thông minh, giao diện đẹp, nhiều tính năng
   - Phù hợp: Người mới bắt đầu đến chuyên gia

2. **Eclipse** (Miễn phí hoàn toàn)
   - Website: https://www.eclipse.org/downloads/
   - Ưu điểm: Nhẹ, ổn định, nhiều plugin
   - Phù hợp: Người có kinh nghiệm

3. **VS Code** (Miễn phí, nhẹ)
   - Website: https://code.visualstudio.com/
   - Cần cài thêm: Extension Pack for Java
   - Ưu điểm: Nhẹ, nhanh, nhiều extension
   - Phù hợp: Người thích editor đơn giản

#### Hướng dẫn cài đặt IntelliJ IDEA Community Edition:

1. Tải IntelliJ IDEA Community Edition từ website
2. Chạy file cài đặt
3. Làm theo hướng dẫn (chọn các tùy chọn mặc định là được)
4. Khởi động IntelliJ IDEA
5. Tạo project mới:
   - File → New → Project
   - Chọn Java
   - Chọn JDK bạn đã cài đặt
   - Click Next và Finish

### Bước 3: Tạo chương trình Java đầu tiên

Sau khi cài đặt xong, hãy tạo một chương trình đơn giản để kiểm tra:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World! Chào mừng đến với Java!");
    }
}
```

**Giải thích từng dòng**:

1. `public class HelloWorld`:
   - `public`: Từ khóa cho phép class này được truy cập từ bất kỳ đâu
   - `class`: Từ khóa để khai báo một lớp (class) trong Java
   - `HelloWorld`: Tên của lớp (phải trùng với tên file, viết hoa chữ cái đầu mỗi từ)

2. `public static void main(String[] args)`:
   - Đây là phương thức `main` - điểm bắt đầu của mọi chương trình Java
   - `public`: Có thể truy cập từ bất kỳ đâu
   - `static`: Phương thức thuộc về lớp, không cần tạo đối tượng để gọi
   - `void`: Phương thức không trả về giá trị
   - `main`: Tên phương thức (bắt buộc phải là "main")
   - `String[] args`: Tham số nhận các đối số từ dòng lệnh

3. `System.out.println(...)`:
   - `System`: Lớp hệ thống
   - `out`: Đối tượng đại diện cho đầu ra chuẩn (màn hình console)
   - `println`: Phương thức in ra màn hình và xuống dòng

**Cách chạy trong IntelliJ IDEA**:
1. Lưu file với tên `HelloWorld.java`
2. Click chuột phải vào file hoặc vào phương thức `main`
3. Chọn "Run 'HelloWorld.main()'"
4. Xem kết quả trong cửa sổ Run ở dưới

**Kết quả mong đợi**:
```
Hello, World! Chào mừng đến với Java!
```

### Bước 4: Cấu hình biến môi trường (Nếu cần)

Thông thường, sau khi cài đặt JDK, bạn không cần cấu hình gì thêm. Tuy nhiên, nếu gặp lỗi, bạn có thể cần thiết lập biến môi trường `JAVA_HOME` và thêm vào `PATH`.

#### Windows:
1. Mở "Environment Variables"
2. Tạo biến mới `JAVA_HOME` trỏ đến thư mục JDK (ví dụ: `C:\Program Files\Java\jdk-17`)
3. Thêm `%JAVA_HOME%\bin` vào `PATH`

#### macOS/Linux:
Thêm vào file `~/.bash_profile` hoặc `~/.zshrc`:
```bash
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```

## Tổng kết

Sau bài học này, bạn đã:
- ✅ Hiểu Java là gì và tại sao nó quan trọng
- ✅ Hiểu sự khác biệt giữa JDK, JRE và JVM
- ✅ Biết cách cài đặt JDK và IDE
- ✅ Tạo và chạy được chương trình Java đầu tiên

## Bài tập thực hành

1. Cài đặt JDK phiên bản 17 hoặc 21
2. Cài đặt IntelliJ IDEA Community Edition
3. Tạo và chạy chương trình HelloWorld
4. Thử thay đổi nội dung in ra màn hình
5. Viết một chương trình in ra tên và tuổi của bạn

## Tài liệu tham khảo

- [Java Documentation](https://docs.oracle.com/javase/)
- [IntelliJ IDEA Documentation](https://www.jetbrains.com/help/idea/)
- [Java Tutorial by Oracle](https://docs.oracle.com/javase/tutorial/)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
