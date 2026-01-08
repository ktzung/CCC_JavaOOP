# Bài 13: Biểu thức chính quy (Regex) trong Java

> **Mục tiêu**: Hiểu được Regex là gì, các ký tự đặc biệt, cách sử dụng regex để kiểm tra và xử lý chuỗi, và áp dụng vào các ví dụ thực tế.

## I. Giới thiệu về Regex

### Regex là gì?

**Regex (Regular Expression)** hay **Biểu thức chính quy** là một dãy ký tự đặc biệt định nghĩa một **khuôn mẫu (pattern)** để tìm kiếm, kiểm tra, hoặc xử lý chuỗi.

### Tại sao cần Regex?

Regex được sử dụng rộng rãi để:
- ✅ **Kiểm tra tính hợp lệ**: Email, số điện thoại, mật khẩu, v.v.
- ✅ **Tìm kiếm**: Tìm chuỗi con theo pattern
- ✅ **Thay thế**: Thay thế chuỗi theo pattern
- ✅ **Tách chuỗi**: Tách chuỗi thành các phần nhỏ hơn
- ✅ **Validation**: Xác thực dữ liệu đầu vào

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **khuôn mẫu**:
- **Pattern**: Khuôn mẫu (ví dụ: "Email phải có @ và .com")
- **String**: Chuỗi cần kiểm tra (ví dụ: "user@example.com")
- **Match**: Khớp với khuôn mẫu hay không? (✅ Có)

**Ví dụ**:
- Pattern: Email phải có `@` và `.com`
- String: `"user@example.com"` → ✅ Khớp
- String: `"invalid.email"` → ❌ Không khớp

## II. Cú pháp Regex cơ bản

### Các ký tự đặc biệt thường dùng

| Ký tự | Mô tả | Ví dụ | Khớp với |
|-------|-------|-------|----------|
| `.` | Bất kỳ ký tự nào | `"a.b"` | `"aab"`, `"acb"`, `"a1b"` |
| `^` | Bắt đầu chuỗi | `"^Hello"` | `"Hello World"` (bắt đầu bằng Hello) |
| `$` | Kết thúc chuỗi | `"World$"` | `"Hello World"` (kết thúc bằng World) |
| `*` | 0 hoặc nhiều lần | `"a*"` | `""`, `"a"`, `"aa"`, `"aaa"` |
| `+` | 1 hoặc nhiều lần | `"a+"` | `"a"`, `"aa"`, `"aaa"` |
| `?` | 0 hoặc 1 lần | `"a?"` | `""`, `"a"` |
| `\d` | Chữ số (0-9) | `"\\d"` | `"0"`, `"1"`, `"9"` |
| `\D` | Không phải chữ số | `"\\D"` | `"a"`, `" "`, `"@"` |
| `\w` | Chữ cái, chữ số, gạch dưới | `"\\w"` | `"a"`, `"1"`, `"_"` |
| `\W` | Không phải \w | `"\\W"` | `" "`, `"@"`, `"!"` |
| `\s` | Khoảng trắng | `"\\s"` | `" "`, `"\t"`, `"\n"` |
| `\S` | Không phải khoảng trắng | `"\\S"` | `"a"`, `"1"`, `"@"` |
| `[]` | Một trong các ký tự | `"[abc]"` | `"a"`, `"b"`, `"c"` |
| `[^]` | Không phải một trong các ký tự | `"[^abc]"` | `"d"`, `"1"`, `"@"` |
| `[a-z]` | Ký tự từ a đến z | `"[a-z]"` | `"a"`, `"b"`, `"z"` |
| `[A-Z]` | Ký tự từ A đến Z | `"[A-Z]"` | `"A"`, `"B"`, `"Z"` |
| `[0-9]` | Số từ 0 đến 9 | `"[0-9]"` | `"0"`, `"1"`, `"9"` |
| `{n}` | Đúng n lần | `"a{3}"` | `"aaa"` |
| `{n,}` | n lần trở lên | `"a{2,}"` | `"aa"`, `"aaa"`, `"aaaa"` |
| `{n,m}` | Từ n đến m lần | `"a{2,4}"` | `"aa"`, `"aaa"`, `"aaaa"` |
| `\|` | HOẶC (OR) | `"a\|b"` | `"a"` hoặc `"b"` |
| `()` | Nhóm | `"(ab)+"` | `"ab"`, `"abab"`, `"ababab"` |

> **Lưu ý quan trọng**: Trong Java, phải escape các ký tự đặc biệt với `\\` (hai dấu backslash) vì `\` là escape character trong String.

## III. Sử dụng Regex trong Java

### 1. String.matches() - Kiểm tra khớp toàn bộ chuỗi

Phương thức `matches()` kiểm tra xem **toàn bộ chuỗi** có khớp với pattern hay không.

```java
public class StringMatches {
    public static void main(String[] args) {
        String str = "Hello123";
        
        // Kiểm tra có chứa chữ số không?
        boolean hasDigit = str.matches(".*\\d.*");  // true
        System.out.println("Có chữ số: " + hasDigit);
        
        // Kiểm tra chỉ chứa chữ cái và số
        boolean alphanumeric = str.matches("[a-zA-Z0-9]+");  // true
        System.out.println("Chỉ chữ và số: " + alphanumeric);
        
        // Kiểm tra có khoảng trắng không?
        boolean hasSpace = str.matches(".*\\s.*");  // false
        System.out.println("Có khoảng trắng: " + hasSpace);
    }
}
```

**Lưu ý**: `matches()` yêu cầu **toàn bộ chuỗi** khớp với pattern. Nếu chỉ muốn tìm pattern trong chuỗi, dùng `Pattern` và `Matcher` (sẽ học ở phần sau).

### 2. String.replaceAll() - Thay thế tất cả

Phương thức `replaceAll()` thay thế **tất cả** các phần khớp với pattern.

```java
public class StringReplaceAll {
    public static void main(String[] args) {
        String str = "Hello World 123";
        
        // Xóa tất cả chữ số
        String noDigits = str.replaceAll("\\d", "");
        System.out.println("Không có số: " + noDigits);  // "Hello World  "
        
        // Xóa tất cả khoảng trắng
        String noSpaces = str.replaceAll("\\s", "");
        System.out.println("Không có khoảng trắng: " + noSpaces);  // "HelloWorld123"
        
        // Thay thế nhiều khoảng trắng bằng một khoảng trắng
        String str2 = "Hello    World";
        String singleSpace = str2.replaceAll("\\s+", " ");
        System.out.println("Một khoảng trắng: " + singleSpace);  // "Hello World"
        
        // Xóa tất cả chữ cái
        String noLetters = str.replaceAll("[a-zA-Z]", "");
        System.out.println("Không có chữ: " + noLetters);  // "  123"
    }
}
```

### 3. String.replaceFirst() - Thay thế lần đầu tiên

Phương thức `replaceFirst()` chỉ thay thế **lần xuất hiện đầu tiên** khớp với pattern.

```java
public class StringReplaceFirst {
    public static void main(String[] args) {
        String str = "Hello World Hello";
        
        // Thay thế lần đầu tiên
        String replaced = str.replaceFirst("Hello", "Hi");
        System.out.println("Sau replaceFirst: " + replaced);  // "Hi World Hello"
        
        // replaceAll thay thế tất cả
        String replacedAll = str.replaceAll("Hello", "Hi");
        System.out.println("Sau replaceAll: " + replacedAll);  // "Hi World Hi"
    }
}
```

### 4. String.split() - Tách chuỗi

Phương thức `split()` tách chuỗi thành mảng các chuỗi con dựa trên pattern.

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
        
        // Tách bằng khoảng trắng (một hoặc nhiều)
        String sentence = "Hello   World    Java";
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
        
        // Tách số
        String numbers = "1-2-3-4-5";
        String[] nums = numbers.split("-");
        for (String num : nums) {
            System.out.print(num + " ");  // 1 2 3 4 5
        }
    }
}
```

## IV. Pattern và Matcher Classes

### Pattern và Matcher là gì?

**Pattern** và **Matcher** là các lớp trong `java.util.regex` cung cấp khả năng xử lý regex **mạnh mẽ hơn** so với các phương thức của String.

### Cách sử dụng Pattern và Matcher

**1. Compile Pattern**:
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

Pattern pattern = Pattern.compile("\\d+");  // Pattern: một hoặc nhiều chữ số
```

**2. Tạo Matcher**:
```java
Matcher matcher = pattern.matcher("Hello 123 World");
```

**3. Sử dụng Matcher**:
```java
public class PatternMatcher {
    public static void main(String[] args) {
        String text = "Hello 123 World 456 Java";
        Pattern pattern = Pattern.compile("\\d+");  // Một hoặc nhiều chữ số
        Matcher matcher = pattern.matcher(text);
        
        // find() - Tìm lần tiếp theo khớp với pattern
        while (matcher.find()) {
            System.out.println("Tìm thấy: " + matcher.group());  // 123, 456
            System.out.println("Vị trí: " + matcher.start() + " - " + matcher.end());
        }
        
        // matches() - Kiểm tra toàn bộ chuỗi
        Pattern exactPattern = Pattern.compile("\\d+");
        Matcher exactMatcher = exactPattern.matcher("123");
        boolean matches = exactMatcher.matches();  // true
        System.out.println("Toàn bộ chuỗi khớp: " + matches);
        
        // lookingAt() - Kiểm tra từ đầu chuỗi
        Pattern startPattern = Pattern.compile("Hello");
        Matcher startMatcher = startPattern.matcher(text);
        boolean lookingAt = startMatcher.lookingAt();  // true
        System.out.println("Bắt đầu khớp: " + lookingAt);
    }
}
```

### Các phương thức phổ biến của Matcher

| Phương thức | Mô tả | Ví dụ |
|-------------|-------|-------|
| `find()` | Tìm lần tiếp theo khớp | `while (matcher.find())` |
| `matches()` | Kiểm tra toàn bộ chuỗi khớp | `matcher.matches()` |
| `lookingAt()` | Kiểm tra từ đầu chuỗi khớp | `matcher.lookingAt()` |
| `group()` | Lấy chuỗi khớp | `matcher.group()` |
| `start()` | Vị trí bắt đầu khớp | `matcher.start()` |
| `end()` | Vị trí kết thúc khớp | `matcher.end()` |
| `replaceAll()` | Thay thế tất cả | `matcher.replaceAll("new")` |
| `replaceFirst()` | Thay thế lần đầu | `matcher.replaceFirst("new")` |

### Ví dụ: Tìm và trích xuất số

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class ExtractNumbers {
    public static void main(String[] args) {
        String text = "Giá sản phẩm: 100000 VNĐ, Giảm giá 20%, Tổng: 80000 VNĐ";
        Pattern pattern = Pattern.compile("\\d+");  // Tìm số
        Matcher matcher = pattern.matcher(text);
        
        System.out.println("Các số tìm thấy:");
        while (matcher.find()) {
            String number = matcher.group();
            int start = matcher.start();
            int end = matcher.end();
            System.out.println("Số: " + number + " (vị trí " + start + "-" + end + ")");
        }
    }
}
```

**Kết quả**:
```
Các số tìm thấy:
Số: 100000 (vị trí 14-20)
Số: 20 (vị trí 32-34)
Số: 80000 (vị trí 43-48)
```

## V. Các Pattern Regex thường dùng

### 1. Email Pattern

```java
public class EmailPattern {
    // Pattern cơ bản cho email
    private static final String EMAIL_PATTERN = 
        "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$";
    
    public static boolean isValidEmail(String email) {
        if (email == null || email.isEmpty()) {
            return false;
        }
        return email.matches(EMAIL_PATTERN);
    }
    
    public static void main(String[] args) {
        System.out.println(isValidEmail("user@example.com"));     // true
        System.out.println(isValidEmail("test.email@domain.co.uk")); // true
        System.out.println(isValidEmail("invalid.email"));        // false
        System.out.println(isValidEmail("@example.com"));         // false
        System.out.println(isValidEmail("user@"));                // false
    }
}
```

**Giải thích Pattern**:
- `^` - Bắt đầu chuỗi
- `[\\w-\\.]+` - Một hoặc nhiều: chữ cái, số, gạch dưới, gạch ngang, dấu chấm
- `@` - Ký tự @ (bắt buộc)
- `([\\w-]+\\.)+` - Một hoặc nhiều nhóm: chữ cái/số/gạch ngang + dấu chấm
- `[\\w-]{2,4}` - 2-4 ký tự: chữ cái, số, gạch ngang (domain extension)
- `$` - Kết thúc chuỗi

### 2. Số điện thoại Pattern (Việt Nam)

```java
public class PhonePattern {
    // Pattern cho số điện thoại Việt Nam (10 số, bắt đầu bằng 0)
    private static final String PHONE_PATTERN = "^0[3-9]\\d{8}$";
    
    public static boolean isValidPhone(String phone) {
        if (phone == null || phone.isEmpty()) {
            return false;
        }
        return phone.matches(PHONE_PATTERN);
    }
    
    public static void main(String[] args) {
        System.out.println(isValidPhone("0912345678"));   // true
        System.out.println(isValidPhone("0987654321"));   // true
        System.out.println(isValidPhone("0123456789"));   // false (bắt đầu bằng 01)
        System.out.println(isValidPhone("1234567890"));   // false (không bắt đầu bằng 0)
        System.out.println(isValidPhone("091234567"));    // false (chỉ có 9 số)
    }
}
```

**Giải thích Pattern**:
- `^0` - Bắt đầu bằng 0
- `[3-9]` - Chữ số thứ 2: 3, 4, 5, 6, 7, 8, hoặc 9
- `\\d{8}` - 8 chữ số tiếp theo
- `$` - Kết thúc chuỗi

### 3. Mật khẩu mạnh Pattern

```java
public class PasswordPattern {
    // Pattern mật khẩu mạnh:
    // - Ít nhất 8 ký tự
    // - Có ít nhất 1 chữ hoa
    // - Có ít nhất 1 chữ thường
    // - Có ít nhất 1 chữ số
    // - Có ít nhất 1 ký tự đặc biệt (@#$%!)
    private static final String STRONG_PASSWORD_PATTERN = 
        "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@#$%!]).{8,}$";
    
    public static boolean isStrongPassword(String password) {
        if (password == null || password.isEmpty()) {
            return false;
        }
        return password.matches(STRONG_PASSWORD_PATTERN);
    }
    
    public static void main(String[] args) {
        System.out.println(isStrongPassword("Password123!"));   // true
        System.out.println(isStrongPassword("password123"));    // false (thiếu chữ hoa, ký tự đặc biệt)
        System.out.println(isStrongPassword("PASSWORD123!"));   // false (thiếu chữ thường)
        System.out.println(isStrongPassword("Password!"));      // false (thiếu số)
        System.out.println(isStrongPassword("Pass123"));        // false (chỉ có 7 ký tự)
    }
}
```

**Giải thích Pattern**:
- `^` - Bắt đầu chuỗi
- `(?=.*[a-z])` - Lookahead: Phải có ít nhất 1 chữ thường
- `(?=.*[A-Z])` - Lookahead: Phải có ít nhất 1 chữ hoa
- `(?=.*\\d)` - Lookahead: Phải có ít nhất 1 chữ số
- `(?=.*[@#$%!])` - Lookahead: Phải có ít nhất 1 ký tự đặc biệt
- `.{8,}` - Ít nhất 8 ký tự bất kỳ
- `$` - Kết thúc chuỗi

### 4. Ngày tháng Pattern (DD/MM/YYYY)

```java
public class DatePattern {
    // Pattern cho ngày tháng DD/MM/YYYY
    private static final String DATE_PATTERN = 
        "^(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[0-2])/\\d{4}$";
    
    public static boolean isValidDate(String date) {
        if (date == null || date.isEmpty()) {
            return false;
        }
        return date.matches(DATE_PATTERN);
    }
    
    public static void main(String[] args) {
        System.out.println(isValidDate("01/01/2023"));   // true
        System.out.println(isValidDate("31/12/2023"));   // true
        System.out.println(isValidDate("32/01/2023"));   // false (ngày không hợp lệ)
        System.out.println(isValidDate("01/13/2023"));   // false (tháng không hợp lệ)
        System.out.println(isValidDate("1/1/2023"));     // false (thiếu số 0 đầu)
    }
}
```

**Giải thích Pattern**:
- `^(0[1-9]|[12][0-9]|3[01])` - Ngày: 01-09 hoặc 10-29 hoặc 30-31
- `/` - Dấu phân cách
- `(0[1-9]|1[0-2])` - Tháng: 01-09 hoặc 10-12
- `/` - Dấu phân cách
- `\\d{4}` - 4 chữ số (năm)
- `$` - Kết thúc chuỗi

## VI. Ví dụ thực tế

### Ví dụ 1: Validation Form đăng ký

```java
import java.util.Scanner;

public class RegistrationValidator {
    // Patterns
    private static final String EMAIL_PATTERN = 
        "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$";
    
    private static final String PHONE_PATTERN = "^0[3-9]\\d{8}$";
    
    private static final String PASSWORD_PATTERN = 
        "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@#$%!]).{8,}$";
    
    // Validation methods
    public static boolean isValidEmail(String email) {
        return email != null && email.matches(EMAIL_PATTERN);
    }
    
    public static boolean isValidPhone(String phone) {
        return phone != null && phone.matches(PHONE_PATTERN);
    }
    
    public static boolean isStrongPassword(String password) {
        return password != null && password.matches(PASSWORD_PATTERN);
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("=== ĐĂNG KÝ TÀI KHOẢN ===\n");
        
        // Nhập email
        String email;
        do {
            System.out.print("Nhập email: ");
            email = scanner.nextLine();
            if (!isValidEmail(email)) {
                System.out.println("❌ Email không hợp lệ! Vui lòng nhập lại.");
            }
        } while (!isValidEmail(email));
        System.out.println("✅ Email hợp lệ!\n");
        
        // Nhập số điện thoại
        String phone;
        do {
            System.out.print("Nhập số điện thoại: ");
            phone = scanner.nextLine();
            if (!isValidPhone(phone)) {
                System.out.println("❌ Số điện thoại không hợp lệ! (10 số, bắt đầu bằng 0)");
            }
        } while (!isValidPhone(phone));
        System.out.println("✅ Số điện thoại hợp lệ!\n");
        
        // Nhập mật khẩu
        String password;
        do {
            System.out.print("Nhập mật khẩu (ít nhất 8 ký tự, có chữ hoa, thường, số, ký tự đặc biệt): ");
            password = scanner.nextLine();
            if (!isStrongPassword(password)) {
                System.out.println("❌ Mật khẩu không đủ mạnh!");
            }
        } while (!isStrongPassword(password));
        System.out.println("✅ Mật khẩu hợp lệ!\n");
        
        System.out.println("=== ĐĂNG KÝ THÀNH CÔNG ===");
        System.out.println("Email: " + email);
        System.out.println("SĐT: " + phone);
        System.out.println("Mật khẩu: ********");
        
        scanner.close();
    }
}
```

### Ví dụ 2: Xử lý và làm sạch dữ liệu

```java
public class DataCleaning {
    public static String cleanPhoneNumber(String phone) {
        if (phone == null) {
            return null;
        }
        
        // Xóa tất cả ký tự không phải số
        String cleaned = phone.replaceAll("[^\\d]", "");
        
        // Thêm số 0 đầu nếu thiếu (cho số Việt Nam)
        if (!cleaned.isEmpty() && !cleaned.startsWith("0")) {
            cleaned = "0" + cleaned;
        }
        
        return cleaned;
    }
    
    public static String cleanEmail(String email) {
        if (email == null) {
            return null;
        }
        
        // Xóa khoảng trắng đầu/cuối và chuyển thành chữ thường
        return email.trim().toLowerCase();
    }
    
    public static String extractNumbers(String text) {
        if (text == null) {
            return null;
        }
        
        // Trích xuất tất cả số
        StringBuilder numbers = new StringBuilder();
        java.util.regex.Pattern pattern = java.util.regex.Pattern.compile("\\d+");
        java.util.regex.Matcher matcher = pattern.matcher(text);
        
        while (matcher.find()) {
            if (numbers.length() > 0) {
                numbers.append(" ");
            }
            numbers.append(matcher.group());
        }
        
        return numbers.toString();
    }
    
    public static void main(String[] args) {
        // Làm sạch số điện thoại
        String phone1 = "091 234 5678";
        String phone2 = "+84-91-234-5678";
        System.out.println("Phone 1 cleaned: " + cleanPhoneNumber(phone1));  // 0912345678
        System.out.println("Phone 2 cleaned: " + cleanPhoneNumber(phone2));  // 0912345678
        
        // Làm sạch email
        String email = "  USER@EXAMPLE.COM  ";
        System.out.println("Email cleaned: " + cleanEmail(email));  // user@example.com
        
        // Trích xuất số
        String text = "Giá: 100000 VNĐ, Giảm 20%, Tổng: 80000 VNĐ";
        System.out.println("Numbers: " + extractNumbers(text));  // 100000 20 80000
    }
}
```

### Ví dụ 3: Tìm và đếm từ

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class WordCounter {
    public static int countWords(String text) {
        if (text == null || text.trim().isEmpty()) {
            return 0;
        }
        
        // Tách bằng khoảng trắng (một hoặc nhiều)
        String[] words = text.trim().split("\\s+");
        return words.length;
    }
    
    public static int countOccurrences(String text, String word) {
        if (text == null || word == null) {
            return 0;
        }
        
        // Pattern với word boundaries
        Pattern pattern = Pattern.compile("\\b" + Pattern.quote(word) + "\\b", Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(text);
        
        int count = 0;
        while (matcher.find()) {
            count++;
        }
        
        return count;
    }
    
    public static void main(String[] args) {
        String text = "Hello world, hello Java, Hello programming";
        
        System.out.println("Số từ: " + countWords(text));  // 6
        System.out.println("Số lần xuất hiện 'hello': " + countOccurrences(text, "hello"));  // 3
    }
}
```

## VII. Lưu ý quan trọng

### 1. Escape ký tự đặc biệt trong Java

Trong Java String, phải escape các ký tự đặc biệt:

```java
// ❌ SAI
String pattern = "\d";  // Lỗi! \d không hợp lệ trong String

// ✅ ĐÚNG
String pattern = "\\d";  // Đúng! \\ = một dấu \
```

### 2. Pattern.quote() - Escape toàn bộ chuỗi

Khi muốn tìm kiếm chuỗi literal (không phải pattern), dùng `Pattern.quote()`:

```java
import java.util.regex.Pattern;

public class PatternQuote {
    public static void main(String[] args) {
        String text = "Price is $100.00";
        String search = "$100.00";  // Có ký tự đặc biệt: $ và .
        
        // ❌ SAI: Không escape
        // boolean found = text.matches(".*" + search + ".*");  // Lỗi!
        
        // ✅ ĐÚNG: Dùng Pattern.quote()
        boolean found = text.matches(".*" + Pattern.quote(search) + ".*");
        System.out.println("Tìm thấy: " + found);  // true
    }
}
```

### 3. Hiệu năng - Compile Pattern một lần

Nếu dùng Pattern nhiều lần, nên compile một lần:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class PatternPerformance {
    // ✅ TỐT: Compile một lần
    private static final Pattern EMAIL_PATTERN = Pattern.compile("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$");
    
    public static boolean isValidEmail(String email) {
        if (email == null) {
            return false;
        }
        Matcher matcher = EMAIL_PATTERN.matcher(email);
        return matcher.matches();
    }
    
    public static void main(String[] args) {
        String[] emails = {"user1@example.com", "user2@test.com", "invalid.email"};
        
        for (String email : emails) {
            System.out.println(email + ": " + isValidEmail(email));
        }
    }
}
```

## VIII. Tổng kết các Pattern thường dùng

### Các Pattern Regex phổ biến

| Mục đích | Pattern | Ví dụ |
|----------|---------|-------|
| **Email** | `^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$` | `user@example.com` |
| **Số điện thoại VN** | `^0[3-9]\\d{8}$` | `0912345678` |
| **Mật khẩu mạnh** | `^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@#$%!]).{8,}$` | `Password123!` |
| **Chỉ chữ số** | `^\\d+$` | `123` |
| **Chỉ chữ cái** | `^[a-zA-Z]+$` | `Hello` |
| **Chữ và số** | `^[a-zA-Z0-9]+$` | `Hello123` |
| **URL** | `^https?://([\\w-]+\\.)+[\\w-]+(/[\\w-./?%&=]*)?$` | `https://example.com` |
| **Ngày DD/MM/YYYY** | `^(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[0-2])/\\d{4}$` | `01/01/2023` |
| **Thời gian HH:MM** | `^([01][0-9]|2[0-3]):[0-5][0-9]$` | `14:30` |
| **Zip code (5 số)** | `^\\d{5}$` | `12345` |

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu Regex là gì và tại sao nó quan trọng
- ✅ Nắm được các ký tự đặc biệt và pattern cơ bản
- ✅ Sử dụng `String.matches()`, `replaceAll()`, `split()`
- ✅ Sử dụng `Pattern` và `Matcher` để xử lý regex nâng cao
- ✅ Áp dụng regex vào validation (email, phone, password)
- ✅ Xử lý và làm sạch dữ liệu với regex
- ✅ Nắm được các pattern thường dùng và best practices

## Bài tập thực hành

1. **Tạo chương trình validation**:
   - Kiểm tra email hợp lệ
   - Kiểm tra số điện thoại Việt Nam
   - Kiểm tra mật khẩu mạnh

2. **Tạo chương trình xử lý văn bản**:
   - Đếm số từ trong văn bản
   - Tìm và thay thế từ
   - Trích xuất số từ văn bản

3. **Tạo chương trình làm sạch dữ liệu**:
   - Xóa khoảng trắng thừa
   - Chuẩn hóa email
   - Chuẩn hóa số điện thoại

## Tài liệu tham khảo

- [Oracle Java Tutorial - Regular Expressions](https://docs.oracle.com/javase/tutorial/essential/regex/index.html)
- [Java Regex Documentation](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)
- [Regex Test Tool](https://regex101.com/) - Tool để test regex online

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
