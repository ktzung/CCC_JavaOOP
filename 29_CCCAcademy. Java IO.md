# Bài 29: Java I/O (Input/Output) - Đọc và ghi file

> **Mục tiêu**: Hiểu được Java I/O là gì, cách đọc và ghi file, sử dụng File, FileInputStream, FileOutputStream, và các lớp I/O phổ biến.

## I. Giới thiệu về Java I/O

### I/O là gì?

**I/O (Input/Output)** trong Java được sử dụng để xử lý **đầu vào** (input) và **đầu ra** (output). Java sử dụng khái niệm **stream** (dòng dữ liệu) để làm cho hoạt động I/O nhanh hơn.

### Stream là gì?

**Stream** (Dòng dữ liệu) là một dãy dữ liệu liên tục. Trong Java, stream bao gồm các **byte** hoặc **character**. Nó được gọi là stream vì giống như một dòng nước chảy liên tục.

### Các loại Stream

Java có **2 loại stream** chính:

1. **Byte Stream**: Xử lý dữ liệu dạng byte (8-bit)
   - `InputStream` / `OutputStream`
   - Dùng cho: File binary, images, audio, v.v.

2. **Character Stream**: Xử lý dữ liệu dạng character (16-bit Unicode)
   - `Reader` / `Writer`
   - Dùng cho: Text files

### Standard Streams

Java tự động tạo **3 streams** cho chúng ta:

- **`System.in`**: Input stream tiêu chuẩn (bàn phím)
- **`System.out`**: Output stream tiêu chuẩn (màn hình console)
- **`System.err`**: Error stream tiêu chuẩn (màn hình console - lỗi)

## II. File Class

### File Class là gì?

Lớp **`File`** trong package `java.io` đại diện cho một **file** hoặc **directory** (thư mục) trong hệ thống file.

### Đặc điểm

- ✅ Đại diện cho file/directory (có thể tồn tại hoặc không)
- ✅ **Không tạo file/directory** - Chỉ đại diện
- ✅ Cung cấp các phương thức để thao tác với file/directory

### Khai báo File

```java
import java.io.File;

// File trên hệ thống
File file1 = new File("/path/to/file.txt");  // Absolute path

// File trong thư mục hiện tại
File file2 = new File("file.txt");  // Relative path

// File trong thư mục con
File file3 = new File("data/file.txt");
```

### Các phương thức phổ biến của File

| Phương thức | Kiểu trả về | Mô tả |
|-------------|-------------|-------|
| `exists()` | `boolean` | File/directory có tồn tại không? |
| `isFile()` | `boolean` | Là file (không phải directory)? |
| `isDirectory()` | `boolean` | Là directory? |
| `getName()` | `String` | Tên file/directory |
| `getPath()` | `String` | Đường dẫn đầy đủ |
| `getParent()` | `String` | Thư mục cha |
| `length()` | `long` | Kích thước file (bytes) |
| `canRead()` | `boolean` | Có thể đọc không? |
| `canWrite()` | `boolean` | Có thể ghi không? |
| `canExecute()` | `boolean` | Có thể thực thi không? |
| `createNewFile()` | `boolean` | Tạo file mới |
| `delete()` | `boolean` | Xóa file/directory |
| `mkdir()` | `boolean` | Tạo directory |
| `mkdirs()` | `boolean` | Tạo directory và parent directories |

### Ví dụ sử dụng File

```java
import java.io.File;

public class FileExample {
    public static void main(String[] args) {
        // Tạo File object
        File file = new File("test.txt");
        
        // Kiểm tra tồn tại
        if (file.exists()) {
            System.out.println("File tồn tại!");
            System.out.println("Tên file: " + file.getName());
            System.out.println("Đường dẫn: " + file.getPath());
            System.out.println("Kích thước: " + file.length() + " bytes");
            System.out.println("Là file? " + file.isFile());
            System.out.println("Có thể đọc? " + file.canRead());
            System.out.println("Có thể ghi? " + file.canWrite());
        } else {
            System.out.println("File không tồn tại!");
        }
        
        // Tạo directory
        File dir = new File("data");
        if (!dir.exists()) {
            boolean created = dir.mkdir();
            System.out.println("Tạo directory: " + created);
        }
    }
}
```

### Tạo File và Directory

```java
import java.io.File;
import java.io.IOException;

public class CreateFileDirectory {
    public static void main(String[] args) {
        try {
            // Tạo file
            File file = new File("test.txt");
            if (file.createNewFile()) {
                System.out.println("✅ File đã được tạo: " + file.getName());
            } else {
                System.out.println("File đã tồn tại.");
            }
            
            // Tạo directory (một cấp)
            File dir1 = new File("data");
            if (dir1.mkdir()) {
                System.out.println("✅ Directory đã được tạo: " + dir1.getName());
            }
            
            // Tạo directory (nhiều cấp)
            File dir2 = new File("data/sub1/sub2");
            if (dir2.mkdirs()) {
                System.out.println("✅ Directory đã được tạo: " + dir2.getPath());
            }
            
        } catch (IOException e) {
            System.out.println("Lỗi: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Xóa File và Directory

```java
import java.io.File;

public class DeleteFileDirectory {
    public static void main(String[] args) {
        // Xóa file
        File file = new File("test.txt");
        if (file.delete()) {
            System.out.println("✅ File đã được xóa: " + file.getName());
        } else {
            System.out.println("Không thể xóa file.");
        }
        
        // Xóa directory (chỉ xóa được nếu rỗng)
        File dir = new File("data");
        if (dir.delete()) {
            System.out.println("✅ Directory đã được xóa: " + dir.getName());
        } else {
            System.out.println("Không thể xóa directory (có thể không rỗng).");
        }
    }
}
```

## III. Đọc và ghi File với Byte Stream

### FileInputStream - Đọc file (Byte Stream)

**FileInputStream** dùng để đọc dữ liệu từ file dạng **byte**.

```java
import java.io.FileInputStream;
import java.io.IOException;

public class ReadFileExample {
    public static void main(String[] args) {
        FileInputStream fis = null;
        
        try {
            fis = new FileInputStream("test.txt");
            
            // Đọc từng byte
            int data;
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);  // Chuyển byte thành char
            }
            
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        } finally {
            // Đóng stream
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

**Sử dụng try-with-resources (Java 7+)** - Tự động đóng:
```java
import java.io.FileInputStream;
import java.io.IOException;

public class ReadFileWithResources {
    public static void main(String[] args) {
        // ✅ Tự động đóng khi kết thúc try block
        try (FileInputStream fis = new FileInputStream("test.txt")) {
            int data;
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }  // FileInputStream tự động đóng ở đây
    }
}
```

**Đọc nhiều byte cùng lúc** (hiệu quả hơn):
```java
try (FileInputStream fis = new FileInputStream("test.txt")) {
    byte[] buffer = new byte[1024];  // Buffer 1KB
    int bytesRead;
    
    while ((bytesRead = fis.read(buffer)) != -1) {
        String content = new String(buffer, 0, bytesRead);
        System.out.print(content);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### FileOutputStream - Ghi file (Byte Stream)

**FileOutputStream** dùng để ghi dữ liệu vào file dạng **byte**.

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class WriteFileExample {
    public static void main(String[] args) {
        // ✅ Tự động đóng với try-with-resources
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            String content = "Hello World!\nXin chào Java!";
            
            // Ghi byte array
            fos.write(content.getBytes());
            
            System.out.println("✅ Đã ghi file thành công!");
            
        } catch (IOException e) {
            System.out.println("Lỗi ghi file: " + e.getMessage());
        }
    }
}
```

**Ghi từng byte**:
```java
try (FileOutputStream fos = new FileOutputStream("output.txt")) {
    String text = "Hello";
    for (char c : text.toCharArray()) {
        fos.write((byte) c);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

**Append mode** (thêm vào cuối file):
```java
// Tham số thứ 2 = true → Append mode
try (FileOutputStream fos = new FileOutputStream("output.txt", true)) {
    String newContent = "\nThêm dòng mới";
    fos.write(newContent.getBytes());
} catch (IOException e) {
    e.printStackTrace();
}
```

## IV. Đọc và ghi File với Character Stream

### FileReader - Đọc file (Character Stream)

**FileReader** dùng để đọc dữ liệu từ file dạng **character** (text files).

```java
import java.io.FileReader;
import java.io.IOException;

public class ReadTextFile {
    public static void main(String[] args) {
        try (FileReader reader = new FileReader("test.txt")) {
            int data;
            while ((data = reader.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }
    }
}
```

**Đọc với buffer** (hiệu quả hơn):
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadTextFileBuffered {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("test.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }
    }
}
```

### FileWriter - Ghi file (Character Stream)

**FileWriter** dùng để ghi dữ liệu vào file dạng **character** (text files).

```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteTextFile {
    public static void main(String[] args) {
        try (FileWriter writer = new FileWriter("output.txt")) {
            writer.write("Dòng 1\n");
            writer.write("Dòng 2\n");
            writer.write("Dòng 3\n");
            
            System.out.println("✅ Đã ghi file thành công!");
        } catch (IOException e) {
            System.out.println("Lỗi ghi file: " + e.getMessage());
        }
    }
}
```

**Append mode**:
```java
// Tham số thứ 2 = true → Append mode
try (FileWriter writer = new FileWriter("output.txt", true)) {
    writer.write("Thêm dòng mới\n");
} catch (IOException e) {
    e.printStackTrace();
}
```

**Sử dụng BufferedWriter** (hiệu quả hơn):
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class WriteTextFileBuffered {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
            writer.write("Dòng 1");
            writer.newLine();  // Xuống dòng mới
            writer.write("Dòng 2");
            writer.newLine();
            writer.write("Dòng 3");
            
            System.out.println("✅ Đã ghi file thành công!");
        } catch (IOException e) {
            System.out.println("Lỗi ghi file: " + e.getMessage());
        }
    }
}
```

## V. Ví dụ thực tế

### Ví dụ 1: Đọc và hiển thị nội dung file

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ReadFileContent {
    public static void readFile(String filePath) {
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            System.out.println("=== NỘI DUNG FILE ===");
            String line;
            int lineNumber = 1;
            
            while ((line = reader.readLine()) != null) {
                System.out.printf("%d: %s%n", lineNumber++, line);
            }
            
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        readFile("test.txt");
    }
}
```

### Ví dụ 2: Ghi danh sách sinh viên vào file

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class WriteStudentsToFile {
    public static void writeStudents(List<Student> students, String filePath) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            writer.write("=== DANH SÁCH SINH VIÊN ===\n");
            writer.write(String.format("%-10s %-20s %-10s %-10s%n",
                                      "ID", "Tên", "Tuổi", "GPA"));
            writer.write("----------------------------------------\n");
            
            for (Student student : students) {
                writer.write(String.format("%-10s %-20s %-10d %-10.2f%n",
                    student.getStudentId(),
                    student.getName(),
                    student.getAge(),
                    student.getGpa()));
            }
            
            System.out.println("✅ Đã ghi danh sách sinh viên vào file!");
            
        } catch (IOException e) {
            System.out.println("Lỗi ghi file: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn A", 20, 8.5));
        students.add(new Student("SV002", "Trần Thị B", 21, 9.0));
        students.add(new Student("SV003", "Lê Văn C", 19, 7.8));
        
        writeStudents(students, "students.txt");
    }
}
```

### Ví dụ 3: Copy file

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class CopyFile {
    public static void copyFile(String sourcePath, String destPath) {
        try (FileInputStream fis = new FileInputStream(sourcePath);
             FileOutputStream fos = new FileOutputStream(destPath)) {
            
            byte[] buffer = new byte[1024];
            int bytesRead;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                fos.write(buffer, 0, bytesRead);
            }
            
            System.out.println("✅ Đã copy file thành công!");
            
        } catch (IOException e) {
            System.out.println("Lỗi copy file: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        copyFile("source.txt", "destination.txt");
    }
}
```

### Ví dụ 4: Đếm số dòng trong file

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class CountLines {
    public static int countLines(String filePath) {
        int count = 0;
        
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            while (reader.readLine() != null) {
                count++;
            }
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
            return -1;
        }
        
        return count;
    }
    
    public static void main(String[] args) {
        int lines = countLines("test.txt");
        if (lines >= 0) {
            System.out.println("Số dòng trong file: " + lines);
        }
    }
}
```

## VI. So sánh Byte Stream và Character Stream

### Bảng so sánh

| Đặc điểm | Byte Stream | Character Stream |
|----------|------------|------------------|
| **Lớp cơ sở** | `InputStream` / `OutputStream` | `Reader` / `Writer` |
| **Đơn vị dữ liệu** | Byte (8-bit) | Character (16-bit Unicode) |
| **Dùng cho** | Binary files (images, audio, video) | Text files |
| **Ví dụ** | `FileInputStream`, `FileOutputStream` | `FileReader`, `FileWriter` |
| **Encoding** | Không xử lý encoding | Xử lý encoding (UTF-8, v.v.) |

### Khi nào dùng gì?

**Dùng Byte Stream khi**:
- ✅ Đọc/ghi **binary files** (images, PDF, audio, video)
- ✅ Không quan tâm đến encoding
- ✅ Cần hiệu năng cao

**Dùng Character Stream khi**:
- ✅ Đọc/ghi **text files**
- ✅ Cần xử lý encoding (tiếng Việt, v.v.)
- ✅ Dễ đọc và xử lý text

**Ví dụ**:
```java
// ✅ Byte Stream - Cho binary files
FileInputStream fis = new FileInputStream("image.jpg");
FileOutputStream fos = new FileOutputStream("copy.jpg");

// ✅ Character Stream - Cho text files
FileReader reader = new FileReader("text.txt");
FileWriter writer = new FileWriter("output.txt");
```

## VII. Xử lý lỗi (Exception Handling)

### IOException

Hầu hết các thao tác I/O có thể ném **IOException**, cần xử lý:

```java
import java.io.FileReader;
import java.io.IOException;

public class ExceptionHandling {
    public static void readFile(String filePath) {
        try (FileReader reader = new FileReader(filePath)) {
            // Đọc file
            int data;
            while ((data = reader.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
            e.printStackTrace();  // In stack trace để debug
        }
    }
    
    public static void main(String[] args) {
        readFile("nonexistent.txt");  // File không tồn tại → IOException
    }
}
```

### Try-with-resources (Java 7+)

**Try-with-resources** tự động đóng resources (FileInputStream, FileReader, v.v.) khi kết thúc try block:

```java
// ✅ TỐT: Try-with-resources (tự động đóng)
try (FileReader reader = new FileReader("test.txt")) {
    // Sử dụng reader
} catch (IOException e) {
    // Xử lý lỗi
}  // reader tự động đóng ở đây

// ❌ KHÔNG TỐT: Phải đóng thủ công
FileReader reader = null;
try {
    reader = new FileReader("test.txt");
    // Sử dụng reader
} catch (IOException e) {
    // Xử lý lỗi
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## VIII. Best Practices

### 1. Luôn sử dụng try-with-resources

```java
// ✅ TỐT: Tự động đóng
try (FileReader reader = new FileReader("file.txt")) {
    // Code
}

// ❌ KHÔNG TỐT: Phải đóng thủ công
FileReader reader = new FileReader("file.txt");
// ... code ...
reader.close();  // Có thể quên đóng!
```

### 2. Sử dụng Buffered Streams cho hiệu năng

```java
// ✅ TỐT: Buffered (nhanh hơn)
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    // Code
}

// ⚠️ CHẬM HƠN: Không buffered
try (FileReader reader = new FileReader("file.txt")) {
    // Code
}
```

### 3. Kiểm tra file tồn tại trước khi đọc

```java
File file = new File("test.txt");
if (file.exists() && file.isFile()) {
    try (FileReader reader = new FileReader(file)) {
        // Đọc file
    }
} else {
    System.out.println("File không tồn tại!");
}
```

### 4. Xử lý encoding cho text files

```java
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;

// Đọc file với encoding UTF-8
try (BufferedReader reader = new BufferedReader(
        new InputStreamReader(
            new FileInputStream("file.txt"),
            StandardCharsets.UTF_8))) {
    // Đọc file
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu Java I/O là gì và các loại stream
- ✅ Sử dụng File class để thao tác với file/directory
- ✅ Đọc file với FileInputStream và FileReader
- ✅ Ghi file với FileOutputStream và FileWriter
- ✅ Sử dụng Buffered streams để tăng hiệu năng
- ✅ Xử lý lỗi với try-with-resources
- ✅ Áp dụng vào các ví dụ thực tế

## Bài tập thực hành

1. **Tạo chương trình đọc file**:
   - Đọc và hiển thị nội dung file
   - Đếm số dòng, số từ
   - Tìm kiếm từ trong file

2. **Tạo chương trình ghi file**:
   - Ghi danh sách sinh viên vào file
   - Ghi log vào file
   - Append dữ liệu vào file

3. **Tạo chương trình copy file**:
   - Copy file text
   - Copy file binary (image)
   - Copy directory

## Tài liệu tham khảo

- [Oracle Java Tutorial - I/O Streams](https://docs.oracle.com/javase/tutorial/essential/io/streams.html)
- [Java File I/O](https://www.javatpoint.com/java-file-class)
- [Java FileInputStream](https://www.javatpoint.com/java-fileinputstream-class)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
