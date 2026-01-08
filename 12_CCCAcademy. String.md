# Bài 12: Xử lý chuỗi (String) trong Java

> **Mục tiêu**: Hiểu được String trong Java, các phương thức xử lý chuỗi phổ biến, sự khác biệt giữa String và StringBuilder, và cách sử dụng hiệu quả.

## I. Giới thiệu về String

### String là gì?

**String** trong Java là một lớp được sử dụng để **lưu trữ** và **xử lý** chuỗi ký tự (text). String là một trong những lớp được sử dụng nhiều nhất trong Java.

### Đặc điểm của String

1. **Immutable** (Bất biến): Không thể thay đổi sau khi tạo
2. **Reference Type**: String là một đối tượng, không phải primitive type
3. **String Pool**: String được lưu trữ trong pool để tối ưu bộ nhớ
4. **Unicode Support**: Hỗ trợ đầy đủ Unicode (tiếng Việt, Trung, v.v.)

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **tấm bảng gỗ**:
- **String** = Tấm bảng đã khắc chữ (không thể sửa, muốn thay đổi phải làm tấm bảng mới)
- **StringBuilder** = Tấm bảng có thể ghi/xóa (có thể thay đổi)

## II. Cách tạo String trong Java

### Có 3 cách tạo String:

**1. String Literal** (Hằng số chuỗi) - Phổ biến nhất
```java
String str1 = "Hello World";
String str2 = "Xin chào Java!";
```

**2. Sử dụng Constructor**
```java
String str1 = new String("Hello World");
String str2 = new String(new char[]{'H', 'e', 'l', 'l', 'o'});
```

**3. Text Blocks** (Java 15+) - Chuỗi nhiều dòng
```java
String textBlock = """
    Đây là một đoạn văn bản
    có thể viết trên nhiều dòng
    mà không cần dùng \\n
    """;
```

### Ví dụ

```java
public class StringCreation {
    public static void main(String[] args) {
        // Cách 1: String Literal
        String str1 = "Hello";
        String str2 = "World";
        
        // Cách 2: Constructor
        String str3 = new String("Hello");
        String str4 = new String(new char[]{'J', 'a', 'v', 'a'});
        
        // Cách 3: Text Blocks (Java 15+)
        String multiLine = """
            Dòng 1
            Dòng 2
            Dòng 3
            """;
        
        System.out.println(str1);       // Hello
        System.out.println(str2);       // World
        System.out.println(str4);       // Java
        System.out.println(multiLine);
    }
}
```

## III. String Pool (Bể chứa chuỗi)

### String Pool là gì?

**String Pool** là một vùng đặc biệt trong bộ nhớ (heap) để lưu trữ các chuỗi literal. Cùng một chuỗi literal chỉ được lưu **một lần** trong pool.

### So sánh String Literal và Constructor

**String Literal** - Lưu trong String Pool:
```java
String s1 = "Hello";
String s2 = "Hello";  // Cùng object trong pool

System.out.println(s1 == s2);        // ✅ true (cùng object)
System.out.println(s1.equals(s2));   // ✅ true (cùng giá trị)
```

**Constructor** - Lưu trong heap (object mới):
```java
String s1 = new String("Hello");
String s2 = new String("Hello");  // Khác object

System.out.println(s1 == s2);        // ❌ false (khác object)
System.out.println(s1.equals(s2));   // ✅ true (cùng giá trị)
```

### Ví dụ minh họa

```java
public class StringPool {
    public static void main(String[] args) {
        // String Literal - Trong pool
        String s1 = "Hello";
        String s2 = "Hello";
        
        // Constructor - Trong heap
        String s3 = new String("Hello");
        String s4 = new String("Hello");
        
        // So sánh reference (==)
        System.out.println("s1 == s2: " + (s1 == s2));        // true (cùng pool)
        System.out.println("s3 == s4: " + (s3 == s4));        // false (khác object)
        System.out.println("s1 == s3: " + (s1 == s3));        // false (pool vs heap)
        
        // So sánh giá trị (equals)
        System.out.println("s1.equals(s2): " + s1.equals(s2));  // true
        System.out.println("s3.equals(s4): " + s3.equals(s4));  // true
        System.out.println("s1.equals(s3): " + s1.equals(s3));  // true
        
        // ⚠️ QUAN TRỌNG: Luôn dùng equals() để so sánh String, không dùng ==!
    }
}
```

**Kết quả**:
```
s1 == s2: true
s3 == s4: false
s1 == s3: false
s1.equals(s2): true
s3.equals(s4): true
s1.equals(s3): true
```

> **Lưu ý quan trọng**: **Luôn dùng `equals()` để so sánh String, không dùng `==`!**

## IV. Các phương thức phổ biến của String

### Bảng tóm tắt các phương thức thường dùng

| Phương thức | Kiểu trả về | Mô tả | Ví dụ |
|-------------|-------------|-------|-------|
| `length()` | `int` | Độ dài chuỗi | `"Hello".length()` → `5` |
| `charAt(int)` | `char` | Ký tự tại vị trí | `"Hello".charAt(0)` → `'H'` |
| `substring(int)` | `String` | Chuỗi con từ vị trí | `"Hello".substring(2)` → `"llo"` |
| `substring(int, int)` | `String` | Chuỗi con từ ... đến | `"Hello".substring(1, 4)` → `"ell"` |
| `indexOf(String)` | `int` | Vị trí xuất hiện đầu tiên | `"Hello".indexOf("l")` → `2` |
| `lastIndexOf(String)` | `int` | Vị trí xuất hiện cuối cùng | `"Hello".lastIndexOf("l")` → `3` |
| `contains(String)` | `boolean` | Có chứa chuỗi không? | `"Hello".contains("ell")` → `true` |
| `startsWith(String)` | `boolean` | Bắt đầu bằng chuỗi? | `"Hello".startsWith("He")` → `true` |
| `endsWith(String)` | `boolean` | Kết thúc bằng chuỗi? | `"Hello".endsWith("lo")` → `true` |
| `equals(String)` | `boolean` | So sánh giá trị | `"Hello".equals("Hello")` → `true` |
| `equalsIgnoreCase(String)` | `boolean` | So sánh không phân biệt hoa thường | `"Hello".equalsIgnoreCase("HELLO")` → `true` |
| `compareTo(String)` | `int` | So sánh từ vựng | `"a".compareTo("b")` → `-1` |
| `toUpperCase()` | `String` | Chuyển thành chữ hoa | `"Hello".toUpperCase()` → `"HELLO"` |
| `toLowerCase()` | `String` | Chuyển thành chữ thường | `"Hello".toLowerCase()` → `"hello"` |
| `trim()` | `String` | Xóa khoảng trắng đầu/cuối | `" Hello ".trim()` → `"Hello"` |
| `replace(String, String)` | `String` | Thay thế chuỗi | `"Hello".replace("l", "L")` → `"HeLLo"` |
| `split(String)` | `String[]` | Tách chuỗi thành mảng | `"a,b,c".split(",")` → `["a","b","c"]` |
| `concat(String)` | `String` | Nối chuỗi | `"Hello".concat(" World")` → `"Hello World"` |
| `isEmpty()` | `boolean` | Rỗng không? | `"".isEmpty()` → `true` |
| `isBlank()` | `boolean` | Rỗng hoặc chỉ có khoảng trắng? (Java 11+) | `"  ".isBlank()` → `true` |

### Chi tiết các phương thức quan trọng

#### 1. length() - Độ dài chuỗi

```java
public class StringLength {
    public static void main(String[] args) {
        String str = "Hello World";
        int length = str.length();
        System.out.println("Độ dài: " + length);  // 11
        
        String empty = "";
        System.out.println("Độ dài rỗng: " + empty.length());  // 0
    }
}
```

#### 2. charAt() - Lấy ký tự tại vị trí

```java
public class StringCharAt {
    public static void main(String[] args) {
        String str = "Hello";
        
        char first = str.charAt(0);   // 'H' (vị trí đầu tiên = 0)
        char last = str.charAt(4);    // 'o' (vị trí cuối cùng = length - 1)
        
        System.out.println("Ký tự đầu: " + first);  // H
        System.out.println("Ký tự cuối: " + last);  // o
        
        // ❌ LỖI: Vượt quá độ dài
        // char error = str.charAt(10);  // StringIndexOutOfBoundsException
    }
}
```

#### 3. substring() - Lấy chuỗi con

```java
public class StringSubstring {
    public static void main(String[] args) {
        String str = "Hello World";
        
        // substring(beginIndex) - Từ vị trí đến cuối
        String sub1 = str.substring(6);      // "World"
        System.out.println("Từ vị trí 6: " + sub1);
        
        // substring(beginIndex, endIndex) - Từ vị trí ... đến vị trí (không bao gồm endIndex)
        String sub2 = str.substring(0, 5);   // "Hello" (từ 0 đến 4)
        String sub3 = str.substring(6, 11);  // "World" (từ 6 đến 10)
        
        System.out.println("Từ 0-5: " + sub2);   // Hello
        System.out.println("Từ 6-11: " + sub3);  // World
        
        // Lấy tên (bỏ họ)
        String fullName = "Nguyễn Văn A";
        String lastName = fullName.substring(fullName.lastIndexOf(" ") + 1);
        System.out.println("Tên: " + lastName);  // A
    }
}
```

#### 4. indexOf() và lastIndexOf() - Tìm vị trí

```java
public class StringIndexOf {
    public static void main(String[] args) {
        String str = "Hello World Hello";
        
        // indexOf() - Vị trí xuất hiện đầu tiên
        int first = str.indexOf("Hello");   // 0
        int firstL = str.indexOf('l');      // 2 (ký tự 'l' đầu tiên)
        
        // lastIndexOf() - Vị trí xuất hiện cuối cùng
        int last = str.lastIndexOf("Hello"); // 12
        int lastL = str.lastIndexOf('l');    // 14
        
        System.out.println("First 'Hello': " + first);  // 0
        System.out.println("Last 'Hello': " + last);    // 12
        System.out.println("First 'l': " + firstL);     // 2
        System.out.println("Last 'l': " + lastL);       // 14
        
        // Không tìm thấy → -1
        int notFound = str.indexOf("Java");
        System.out.println("Not found: " + notFound);  // -1
    }
}
```

#### 5. contains() - Kiểm tra chứa chuỗi

```java
public class StringContains {
    public static void main(String[] args) {
        String str = "Hello World";
        
        boolean hasHello = str.contains("Hello");    // true
        boolean hasWorld = str.contains("World");    // true
        boolean hasJava = str.contains("Java");      // false
        
        System.out.println("Có 'Hello': " + hasHello);  // true
        System.out.println("Có 'World': " + hasWorld);  // true
        System.out.println("Có 'Java': " + hasJava);    // false
    }
}
```

#### 6. startsWith() và endsWith() - Kiểm tra đầu/cuối

```java
public class StringStartsEnds {
    public static void main(String[] args) {
        String str = "Hello World";
        
        boolean starts = str.startsWith("Hello");   // true
        boolean ends = str.endsWith("World");       // true
        
        System.out.println("Bắt đầu bằng 'Hello': " + starts);  // true
        System.out.println("Kết thúc bằng 'World': " + ends);   // true
        
        // Kiểm tra file extension
        String filename = "document.pdf";
        boolean isPdf = filename.endsWith(".pdf");  // true
        System.out.println("Là file PDF: " + isPdf);
    }
}
```

#### 7. equals() và equalsIgnoreCase() - So sánh chuỗi

```java
public class StringEquals {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = "HELLO";
        String str4 = "World";
        
        // equals() - So sánh phân biệt hoa thường
        System.out.println("str1.equals(str2): " + str1.equals(str2));       // true
        System.out.println("str1.equals(str3): " + str1.equals(str3));       // false
        System.out.println("str1.equals(str4): " + str1.equals(str4));       // false
        
        // equalsIgnoreCase() - So sánh không phân biệt hoa thường
        System.out.println("str1.equalsIgnoreCase(str3): " + str1.equalsIgnoreCase(str3)); // true
        
        // ⚠️ QUAN TRỌNG: Luôn dùng equals(), không dùng ==!
        String s1 = new String("Hello");
        String s2 = new String("Hello");
        System.out.println("s1 == s2: " + (s1 == s2));         // false (khác object)
        System.out.println("s1.equals(s2): " + s1.equals(s2)); // true (cùng giá trị)
    }
}
```

#### 8. toUpperCase() và toLowerCase() - Chuyển đổi chữ hoa/thường

```java
public class StringCase {
    public static void main(String[] args) {
        String str = "Hello World";
        
        String upper = str.toUpperCase();  // "HELLO WORLD"
        String lower = str.toLowerCase();  // "hello world"
        
        System.out.println("Uppercase: " + upper);
        System.out.println("Lowercase: " + lower);
        
        // So sánh không phân biệt hoa thường
        String input = "HELLO";
        if (input.equalsIgnoreCase("hello")) {
            System.out.println("Khớp!");
        }
    }
}
```

#### 9. trim() - Xóa khoảng trắng đầu/cuối

```java
public class StringTrim {
    public static void main(String[] args) {
        String str = "  Hello World  ";
        
        String trimmed = str.trim();  // "Hello World"
        
        System.out.println("Gốc: '" + str + "'");        // '  Hello World  '
        System.out.println("Trim: '" + trimmed + "'");   // 'Hello World'
        
        // Java 11+: strip() - Xóa khoảng trắng Unicode
        String unicodeWhitespace = "  Hello  ";
        String stripped = unicodeWhitespace.strip();  // Java 11+
        System.out.println("Strip: '" + stripped + "'");
    }
}
```

#### 10. replace() - Thay thế chuỗi

```java
public class StringReplace {
    public static void main(String[] args) {
        String str = "Hello World";
        
        // replace() - Thay thế tất cả
        String replaced = str.replace("World", "Java");   // "Hello Java"
        String replacedChar = str.replace('l', 'L');      // "HeLLo WorLd"
        
        System.out.println("Replaced: " + replaced);      // Hello Java
        System.out.println("Replaced char: " + replacedChar);  // HeLLo WorLd
        
        // replaceFirst() - Thay thế lần đầu tiên
        String first = str.replaceFirst("l", "L");       // "HeLlo World"
        
        // replaceAll() - Thay thế tất cả (dùng regex)
        String all = str.replaceAll("l+", "L");          // "HeLo WorLd" (regex)
        
        System.out.println("Replace first: " + first);
        System.out.println("Replace all: " + all);
    }
}
```

#### 11. split() - Tách chuỗi thành mảng

```java
public class StringSplit {
    public static void main(String[] args) {
        String str = "apple,banana,orange";
        
        // Tách bằng dấu phẩy
        String[] fruits = str.split(",");
        
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        // apple
        // banana
        // orange
        
        // Tách bằng khoảng trắng
        String sentence = "Hello World Java";
        String[] words = sentence.split("\\s+");  // \\s+ = một hoặc nhiều khoảng trắng
        
        for (String word : words) {
            System.out.println(word);
        }
        // Hello
        // World
        // Java
        
        // Tách email
        String email = "user@example.com";
        String[] parts = email.split("@");
        System.out.println("Username: " + parts[0]);  // user
        System.out.println("Domain: " + parts[1]);    // example.com
    }
}
```

#### 12. compareTo() - So sánh từ vựng

```java
public class StringCompareTo {
    public static void main(String[] args) {
        String str1 = "apple";
        String str2 = "banana";
        String str3 = "apple";
        
        // compareTo() - So sánh từ vựng (lexicographically)
        int result1 = str1.compareTo(str2);  // < 0 (apple < banana)
        int result2 = str1.compareTo(str3);  // 0 (apple == apple)
        int result3 = str2.compareTo(str1);  // > 0 (banana > apple)
        
        System.out.println("apple vs banana: " + result1);  // < 0
        System.out.println("apple vs apple: " + result2);   // 0
        System.out.println("banana vs apple: " + result3);  // > 0
        
        // Quy tắc:
        // < 0: Chuỗi này nhỏ hơn chuỗi kia
        // = 0: Hai chuỗi bằng nhau
        // > 0: Chuỗi này lớn hơn chuỗi kia
        
        // compareToIgnoreCase() - Không phân biệt hoa thường
        int result4 = "Apple".compareToIgnoreCase("apple");  // 0
        System.out.println("Compare ignore case: " + result4);
    }
}
```

## V. Nối chuỗi (String Concatenation)

### Toán tử + (Plus Operator)

Trong Java, bạn có thể sử dụng toán tử `+` để **nối chuỗi**:

```java
public class StringConcatenation {
    public static void main(String[] args) {
        // Nối chuỗi với chuỗi
        String str1 = "Hello" + " " + "World";
        System.out.println(str1);  // Hello World
        
        // Nối chuỗi với số (tự động chuyển đổi)
        int age = 20;
        String message = "Tuổi: " + age;  // Tự động chuyển int → String
        System.out.println(message);  // Tuổi: 20
        
        // Nối nhiều giá trị
        String name = "Nguyễn Văn A";
        int score = 85;
        double gpa = 8.5;
        String info = "Tên: " + name + ", Điểm: " + score + ", GPA: " + gpa;
        System.out.println(info);
    }
}
```

### concat() Method

```java
public class StringConcat {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "World";
        
        // concat() - Nối chuỗi
        String result = str1.concat(" ").concat(str2);
        System.out.println(result);  // Hello World
        
        // Tương đương với
        String result2 = str1 + " " + str2;
        System.out.println(result2);  // Hello World
    }
}
```

### Vấn đề hiệu năng: Nối chuỗi trong vòng lặp

**❌ SAI - Rất chậm**:
```java
public class SlowConcatenation {
    public static void main(String[] args) {
        String result = "";
        
        // ❌ SAI: Mỗi lần nối tạo object mới (rất chậm!)
        for (int i = 0; i < 10000; i++) {
            result += "a";  // Tạo object mới mỗi lần!
        }
        
        System.out.println("Độ dài: " + result.length());
    }
}
```

**✅ ĐÚNG - Sử dụng StringBuilder** (sẽ học ở phần sau):
```java
public class FastConcatenation {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        
        // ✅ ĐÚNG: Chỉ thay đổi object hiện tại (nhanh!)
        for (int i = 0; i < 10000; i++) {
            sb.append("a");
        }
        
        String result = sb.toString();
        System.out.println("Độ dài: " + result.length());
    }
}
```

## VI. String Immutability (Tính bất biến)

### String là Immutable (Bất biến)

**Immutable** nghĩa là **không thể thay đổi** sau khi tạo. Mọi thao tác trên String đều **tạo object mới**.

### Ví dụ minh họa

```java
public class StringImmutability {
    public static void main(String[] args) {
        String str = "Hello";
        
        System.out.println("Gốc: " + str);        // Hello
        System.out.println("HashCode: " + str.hashCode());  // 69609650
        
        // Thay đổi String
        str = str + " World";  // Tạo object mới, không sửa object cũ!
        
        System.out.println("Sau khi nối: " + str);  // Hello World
        System.out.println("HashCode mới: " + str.hashCode());  // Khác hashCode!
    }
}
```

**Giải thích**:
- `str = "Hello"` → Object 1 trong bộ nhớ
- `str = str + " World"` → Tạo Object 2 mới với giá trị "Hello World"
- Object 1 vẫn tồn tại trong bộ nhớ (cho đến khi GC xóa)
- Object 2 được gán cho biến `str`

### Lợi ích của Immutability

1. **Thread-safe**: Không thể bị thay đổi → An toàn trong đa luồng
2. **Caching**: Có thể cache trong String Pool
3. **HashCode**: HashCode không đổi → Phù hợp cho HashMap, HashSet

### Nhược điểm

1. **Hiệu năng**: Mỗi thao tác tạo object mới → Chậm hơn
2. **Bộ nhớ**: Nhiều object tạm thời → Tốn bộ nhớ

**Giải pháp**: Sử dụng `StringBuilder` khi cần thay đổi chuỗi nhiều lần (sẽ học ở phần sau).

## VII. So sánh String

### 1. Toán tử == (So sánh reference)

```java
public class StringComparison {
    public static void main(String[] args) {
        // String Literal - Trong pool
        String s1 = "Hello";
        String s2 = "Hello";
        System.out.println("s1 == s2: " + (s1 == s2));  // true (cùng pool)
        
        // Constructor - Trong heap
        String s3 = new String("Hello");
        String s4 = new String("Hello");
        System.out.println("s3 == s4: " + (s3 == s4));  // false (khác object)
        
        // ⚠️ LƯU Ý: == so sánh reference, không phải giá trị!
    }
}
```

### 2. equals() - So sánh giá trị

```java
public class StringEquals {
    public static void main(String[] args) {
        String s1 = "Hello";
        String s2 = new String("Hello");
        String s3 = "HELLO";
        
        // equals() - So sánh giá trị (phân biệt hoa thường)
        System.out.println("s1.equals(s2): " + s1.equals(s2));       // true
        System.out.println("s1.equals(s3): " + s1.equals(s3));       // false
        
        // equalsIgnoreCase() - So sánh giá trị (không phân biệt hoa thường)
        System.out.println("s1.equalsIgnoreCase(s3): " + s1.equalsIgnoreCase(s3)); // true
        
        // ⚠️ QUAN TRỌNG: Luôn dùng equals() để so sánh String!
    }
}
```

### Quy tắc vàng

> **QUAN TRỌNG**: **Luôn dùng `equals()` để so sánh String, KHÔNG BAO GIỜ dùng `==`!**

## VIII. StringBuilder và StringBuffer

### Vấn đề với String Immutability

Khi cần thay đổi chuỗi nhiều lần (ví dụ: trong vòng lặp), String tạo nhiều object mới → **Rất chậm** và **tốn bộ nhớ**.

### Giải pháp: StringBuilder

**StringBuilder** (Java 5+) là lớp **mutable** (có thể thay đổi) để xử lý chuỗi hiệu quả hơn.

**Đặc điểm**:
- ✅ **Mutable**: Có thể thay đổi
- ✅ **Nhanh hơn**: Không tạo object mới mỗi lần
- ✅ **Hiệu quả**: Tiết kiệm bộ nhớ

### So sánh String và StringBuilder

```java
public class StringVsStringBuilder {
    public static void main(String[] args) {
        // String - Immutable (chậm)
        String str = "";
        for (int i = 0; i < 1000; i++) {
            str += "a";  // ❌ Tạo object mới mỗi lần (chậm!)
        }
        
        // StringBuilder - Mutable (nhanh)
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 1000; i++) {
            sb.append("a");  // ✅ Chỉ thay đổi object hiện tại (nhanh!)
        }
        String result = sb.toString();
        
        System.out.println("String length: " + str.length());
        System.out.println("StringBuilder length: " + result.length());
    }
}
```

### Các phương thức phổ biến của StringBuilder

```java
public class StringBuilderMethods {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        
        // append() - Thêm vào cuối
        sb.append("Hello");
        sb.append(" ");
        sb.append("World");
        System.out.println(sb.toString());  // Hello World
        
        // insert() - Chèn vào vị trí
        sb.insert(5, " Java");
        System.out.println(sb.toString());  // Hello Java World
        
        // delete() - Xóa
        sb.delete(5, 10);
        System.out.println(sb.toString());  // Hello World
        
        // reverse() - Đảo ngược
        sb.reverse();
        System.out.println(sb.toString());  // dlroW olleH
        
        // length(), capacity()
        System.out.println("Length: " + sb.length());
        System.out.println("Capacity: " + sb.capacity());
    }
}
```

### StringBuffer vs StringBuilder

| Đặc điểm | StringBuffer | StringBuilder |
|----------|--------------|---------------|
| **Thread-safe** | ✅ Synchronized (an toàn đa luồng) | ❌ Không synchronized |
| **Hiệu năng** | 🐌 Chậm hơn | ⚡ Nhanh hơn |
| **Khi nào dùng** | Đa luồng | Đơn luồng (khuyến nghị) |

**Khuyến nghị**: Dùng **StringBuilder** trong hầu hết trường hợp (đơn luồng, nhanh hơn).

## IX. Ví dụ thực tế

### Ví dụ 1: Validation email

```java
public class EmailValidator {
    public static boolean isValidEmail(String email) {
        if (email == null || email.isEmpty()) {
            return false;
        }
        
        // Kiểm tra có @
        if (!email.contains("@")) {
            return false;
        }
        
        // Kiểm tra có ít nhất 1 ký tự trước @
        int atIndex = email.indexOf("@");
        if (atIndex == 0) {
            return false;
        }
        
        // Kiểm tra có ít nhất 1 ký tự sau @
        if (atIndex == email.length() - 1) {
            return false;
        }
        
        // Kiểm tra có dấu chấm sau @
        String domain = email.substring(atIndex + 1);
        if (!domain.contains(".")) {
            return false;
        }
        
        return true;
    }
    
    public static void main(String[] args) {
        System.out.println(isValidEmail("user@example.com"));    // true
        System.out.println(isValidEmail("invalid.email"));       // false
        System.out.println(isValidEmail("@example.com"));        // false
        System.out.println(isValidEmail("user@"));               // false
    }
}
```

### Ví dụ 2: Xử lý tên

```java
public class NameProcessor {
    public static String capitalizeName(String name) {
        if (name == null || name.trim().isEmpty()) {
            return name;
        }
        
        String trimmed = name.trim();
        String[] parts = trimmed.split("\\s+");  // Tách theo khoảng trắng
        
        StringBuilder result = new StringBuilder();
        for (int i = 0; i < parts.length; i++) {
            if (i > 0) {
                result.append(" ");
            }
            String part = parts[i];
            if (!part.isEmpty()) {
                result.append(Character.toUpperCase(part.charAt(0)));
                if (part.length() > 1) {
                    result.append(part.substring(1).toLowerCase());
                }
            }
        }
        
        return result.toString();
    }
    
    public static void main(String[] args) {
        System.out.println(capitalizeName("  nguyễn văn a  "));  // Nguyễn Văn A
        System.out.println(capitalizeName("JOHN DOE"));           // John Doe
        System.out.println(capitalizeName("hello world"));        // Hello World
    }
}
```

### Ví dụ 3: Đảo ngược chuỗi

```java
public class StringReverse {
    // Cách 1: Sử dụng StringBuilder
    public static String reverseWithStringBuilder(String str) {
        if (str == null) {
            return null;
        }
        return new StringBuilder(str).reverse().toString();
    }
    
    // Cách 2: Thủ công (học thuật toán)
    public static String reverseManual(String str) {
        if (str == null || str.isEmpty()) {
            return str;
        }
        
        StringBuilder sb = new StringBuilder();
        for (int i = str.length() - 1; i >= 0; i--) {
            sb.append(str.charAt(i));
        }
        return sb.toString();
    }
    
    public static void main(String[] args) {
        String str = "Hello";
        
        System.out.println("Gốc: " + str);
        System.out.println("Reverse (SB): " + reverseWithStringBuilder(str));  // olleH
        System.out.println("Reverse (Manual): " + reverseManual(str));         // olleH
    }
}
```

## X. Text Blocks (Java 15+) - Cách mới viết chuỗi nhiều dòng

### Text Blocks là gì?

**Text Blocks** (Java 15+) cho phép viết chuỗi nhiều dòng một cách dễ dàng hơn.

### Cú pháp

Sử dụng `"""` (ba dấu nháy kép):

```java
public class TextBlocks {
    public static void main(String[] args) {
        // Cách cũ (trước Java 15)
        String oldWay = "Dòng 1\n" +
                       "Dòng 2\n" +
                       "Dòng 3";
        
        // Cách mới (Java 15+)
        String newWay = """
            Dòng 1
            Dòng 2
            Dòng 3
            """;
        
        System.out.println("Cách cũ:");
        System.out.println(oldWay);
        
        System.out.println("\nCách mới:");
        System.out.println(newWay);
        
        // Text Block với format
        String name = "Nguyễn Văn A";
        int age = 20;
        String formatted = """
            Tên: %s
            Tuổi: %d
            """.formatted(name, age);
        
        System.out.println("\nFormatted:");
        System.out.println(formatted);
    }
}
```

**Kết quả**:
```
Cách cũ:
Dòng 1
Dòng 2
Dòng 3

Cách mới:
Dòng 1
Dòng 2
Dòng 3

Formatted:
Tên: Nguyễn Văn A
Tuổi: 20
```

### Ưu điểm của Text Blocks

1. **Dễ đọc**: Code dễ đọc hơn nhiều
2. **Không cần escape**: Không cần dùng `\n`, `\"`, v.v.
3. **Giữ nguyên format**: Giữ nguyên cách trình bày trong code
4. **Hỗ trợ format**: Có thể dùng `.formatted()` để format

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu String là gì và đặc điểm của nó
- ✅ Nắm được 3 cách tạo String
- ✅ Hiểu String Pool và sự khác biệt giữa literal và constructor
- ✅ Sử dụng các phương thức phổ biến của String
- ✅ Hiểu tính immutability của String
- ✅ So sánh String đúng cách (dùng equals, không dùng ==)
- ✅ Biết khi nào dùng StringBuilder thay vì String
- ✅ Sử dụng Text Blocks (Java 15+) để viết chuỗi nhiều dòng

## Bài tập thực hành

1. **Tạo chương trình xử lý chuỗi**:
   - Nhập một chuỗi từ bàn phím
   - Đếm số từ, số ký tự
   - Đảo ngược chuỗi
   - Kiểm tra đối xứng (palindrome)

2. **Tạo chương trình validation**:
   - Kiểm tra email hợp lệ
   - Kiểm tra số điện thoại
   - Kiểm tra mật khẩu mạnh

3. **Tạo chương trình xử lý tên**:
   - Chuẩn hóa tên (viết hoa chữ đầu)
   - Tách họ, tên đệm, tên
   - So sánh tên

## Tài liệu tham khảo

- [Oracle Java Tutorial - Strings](https://docs.oracle.com/javase/tutorial/java/data/strings.html)
- [Java String Documentation](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)
- [Java Text Blocks (Java 15+)](https://docs.oracle.com/en/java/javase/15/text-blocks/index.html)
- [StringBuilder vs StringBuffer](https://www.baeldung.com/java-string-builder-string-buffer)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
