# Bài 7: Wrapper Classes trong Java

> **Mục tiêu**: Hiểu được Wrapper classes là gì, cách chuyển đổi giữa primitive types và wrapper classes, và khi nào nên sử dụng wrapper classes.

## I. Giới thiệu về Wrapper Classes

### Wrapper Class là gì?

**Wrapper Classes** (Lớp bao bọc) là các lớp trong Java được sử dụng để **bọc gói** (wrap) các kiểu dữ liệu nguyên thủy (primitive types) thành các đối tượng (objects).

### Tại sao cần Wrapper Classes?

Trong Java, có **2 loại kiểu dữ liệu**:
1. **Primitive Types** (Kiểu nguyên thủy): `int`, `double`, `boolean`, v.v.
2. **Reference Types** (Kiểu tham chiếu): `String`, `Integer`, `Double`, v.v. (objects)

**Vấn đề**:
- Primitive types **không có phương thức** - chỉ lưu trữ giá trị
- Collections (như ArrayList) chỉ chấp nhận **objects**, không chấp nhận primitives
- Một số API chỉ làm việc với objects

**Giải pháp**: Wrapper Classes!

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **món quà**:
- **Primitive type** = Món quà (chỉ có giá trị)
- **Wrapper class** = Hộp đựng quà + món quà bên trong

Hộp đựng quà (wrapper) cho phép bạn:
- Thêm thông tin (nhãn, mô tả) = Phương thức của wrapper class
- Đặt vào tủ trưng bày (collections) = Collections chỉ nhận objects
- Xử lý như một đối tượng = Có thể null, có phương thức

## II. Bảng tương ứng giữa Primitive và Wrapper

Java cung cấp **8 Wrapper Classes** tương ứng với **8 Primitive Types**:

| Primitive Type | Wrapper Class | Mô tả |
|----------------|---------------|-------|
| `boolean` | `Boolean` | Lớp bao bọc cho boolean |
| `byte` | `Byte` | Lớp bao bọc cho byte |
| `short` | `Short` | Lớp bao bọc cho short |
| `int` | `Integer` | Lớp bao bọc cho int |
| `long` | `Long` | Lớp bao bọc cho long |
| `float` | `Float` | Lớp bao bọc cho float |
| `double` | `Double` | Lớp bao bọc cho double |
| `char` | `Character` | Lớp bao bọc cho char |

> **Lưu ý**: Tên wrapper class bắt đầu bằng chữ hoa (trừ `Integer` và `Character` có tên khác với primitive).

## III. Boxing và Unboxing

### Boxing (Đóng gói)

**Boxing** là quá trình **chuyển đổi** từ primitive type sang wrapper class object.

**Cách 1: Manual Boxing (Ép kiểu thủ công)**
```java
public class BoxingExample {
    public static void main(String[] args) {
        int primitive = 100;
        
        // Manual boxing - Chuyển đổi thủ công
        Integer wrapper = Integer.valueOf(primitive);  // ✅ Cách khuyến nghị
        // Hoặc
        Integer wrapper2 = new Integer(primitive);     // ⚠️ Deprecated từ Java 9+
        
        System.out.println("Primitive: " + primitive);   // 100
        System.out.println("Wrapper: " + wrapper);       // 100
    }
}
```

**Cách 2: Auto-Boxing (Tự động đóng gói - Java 5+)**
```java
public class AutoBoxingExample {
    public static void main(String[] args) {
        int primitive = 100;
        
        // Auto-boxing - Tự động chuyển đổi
        Integer wrapper = primitive;  // ✅ Java tự động chuyển đổi
        
        System.out.println("Wrapper: " + wrapper);  // 100
    }
}
```

**Giải thích**: 
- Từ Java 5+, Java **tự động chuyển đổi** primitive sang wrapper khi cần
- Trình biên dịch tự động chèn code `Integer.valueOf(primitive)`

### Unboxing (Mở gói)

**Unboxing** là quá trình **chuyển đổi** từ wrapper class object về primitive type.

**Cách 1: Manual Unboxing (Ép kiểu thủ công)**
```java
public class UnboxingExample {
    public static void main(String[] args) {
        Integer wrapper = Integer.valueOf(100);
        
        // Manual unboxing - Chuyển đổi thủ công
        int primitive = wrapper.intValue();  // ✅ Chuyển Integer → int
        
        System.out.println("Primitive: " + primitive);  // 100
    }
}
```

**Cách 2: Auto-Unboxing (Tự động mở gói - Java 5+)**
```java
public class AutoUnboxingExample {
    public static void main(String[] args) {
        Integer wrapper = Integer.valueOf(100);
        
        // Auto-unboxing - Tự động chuyển đổi
        int primitive = wrapper;  // ✅ Java tự động chuyển đổi
        
        System.out.println("Primitive: " + primitive);  // 100
    }
}
```

### Ví dụ hoàn chỉnh về Boxing và Unboxing

```java
public class BoxingUnboxingDemo {
    public static void main(String[] args) {
        // Primitive → Wrapper (Boxing)
        int primitiveInt = 42;
        Integer wrapperInt = primitiveInt;  // Auto-boxing
        
        // Wrapper → Primitive (Unboxing)
        Integer wrapperInteger = Integer.valueOf(100);
        int intValue = wrapperInteger;  // Auto-unboxing
        
        // Sử dụng trong toán tử
        Integer a = 10;  // Auto-boxing: int → Integer
        Integer b = 20;  // Auto-boxing: int → Integer
        Integer sum = a + b;  // Auto-unboxing → tính toán → Auto-boxing
        
        System.out.println("Sum: " + sum);  // 30
    }
}
```

## IV. Chuyển đổi giữa String và Primitive Types

### 1. String → Primitive (Parse)

Chuyển đổi từ String sang primitive type:

```java
public class StringToPrimitive {
    public static void main(String[] args) {
        // String → int
        String strInt = "123";
        int num = Integer.parseInt(strInt);  // ✅ Cách khuyến nghị
        System.out.println("Số nguyên: " + num);  // 123
        
        // String → double
        String strDouble = "3.14";
        double pi = Double.parseDouble(strDouble);
        System.out.println("Số thực: " + pi);  // 3.14
        
        // String → boolean
        String strBoolean = "true";
        boolean flag = Boolean.parseBoolean(strBoolean);
        System.out.println("Boolean: " + flag);  // true
        
        // String → long
        String strLong = "1000000000000";
        long bigNum = Long.parseLong(strLong);
        System.out.println("Long: " + bigNum);
    }
}
```

**Lưu ý**: Nếu String không đúng định dạng, sẽ ném `NumberFormatException`:

```java
public class ParseError {
    public static void main(String[] args) {
        String invalid = "abc";
        // int num = Integer.parseInt(invalid);  // ❌ LỖI: NumberFormatException
        
        // Xử lý lỗi
        try {
            int num = Integer.parseInt(invalid);
            System.out.println("Số: " + num);
        } catch (NumberFormatException e) {
            System.out.println("Không thể chuyển đổi '" + invalid + "' thành số!");
        }
    }
}
```

### 2. Primitive → String (ToString)

Chuyển đổi từ primitive type sang String:

**Cách 1: Sử dụng `toString()` method**
```java
public class PrimitiveToString {
    public static void main(String[] args) {
        int num = 123;
        String str1 = Integer.toString(num);  // ✅ Cách 1
        System.out.println("Chuỗi: " + str1);  // "123"
        
        double pi = 3.14;
        String str2 = Double.toString(pi);     // ✅ Cách 1
        System.out.println("Chuỗi: " + str2);  // "3.14"
    }
}
```

**Cách 2: Sử dụng `String.valueOf()`**
```java
public class StringValueOf {
    public static void main(String[] args) {
        int num = 123;
        String str1 = String.valueOf(num);  // ✅ Cách 2
        System.out.println("Chuỗi: " + str1);  // "123"
        
        double pi = 3.14;
        String str2 = String.valueOf(pi);
        System.out.println("Chuỗi: " + str2);  // "3.14"
        
        boolean flag = true;
        String str3 = String.valueOf(flag);
        System.out.println("Chuỗi: " + str3);  // "true"
    }
}
```

**Cách 3: Nối chuỗi (tự động chuyển đổi)**
```java
public class StringConcatenation {
    public static void main(String[] args) {
        int num = 123;
        String str = "" + num;  // ✅ Cách 3 (tự động chuyển đổi)
        System.out.println("Chuỗi: " + str);  // "123"
        
        // Hoặc
        String str2 = "Số: " + num;  // Tự động chuyển đổi int → String
        System.out.println(str2);  // "Số: 123"
    }
}
```

> **Lưu ý**: Cách 1 và 2 rõ ràng hơn, Cách 3 dễ gây nhầm lẫn.

## V. Các phương thức hữu ích của Wrapper Classes

### 1. Integer Class

```java
public class IntegerMethods {
    public static void main(String[] args) {
        // Giá trị min/max
        System.out.println("Max int: " + Integer.MAX_VALUE);   // 2147483647
        System.out.println("Min int: " + Integer.MIN_VALUE);   // -2147483648
        
        // So sánh
        int result = Integer.compare(10, 20);  // -1 (10 < 20)
        System.out.println("Compare: " + result);
        
        // Chuyển đổi cơ số
        String binary = Integer.toBinaryString(10);    // "1010" (nhị phân)
        String hex = Integer.toHexString(255);          // "ff" (thập lục phân)
        String octal = Integer.toOctalString(64);       // "100" (bát phân)
        
        System.out.println("Binary: " + binary);
        System.out.println("Hex: " + hex);
        System.out.println("Octal: " + octal);
        
        // Parse từ cơ số khác
        int fromBinary = Integer.parseInt("1010", 2);   // 10 (từ nhị phân)
        int fromHex = Integer.parseInt("FF", 16);       // 255 (từ hex)
        
        System.out.println("From binary: " + fromBinary);
        System.out.println("From hex: " + fromHex);
    }
}
```

### 2. Double Class

```java
public class DoubleMethods {
    public static void main(String[] args) {
        // Giá trị min/max
        System.out.println("Max double: " + Double.MAX_VALUE);
        System.out.println("Min double: " + Double.MIN_VALUE);
        
        // Kiểm tra đặc biệt
        System.out.println("Is NaN: " + Double.isNaN(0.0 / 0.0));        // true
        System.out.println("Is Infinite: " + Double.isInfinite(1.0 / 0.0)); // true
        
        // So sánh
        int result = Double.compare(10.5, 20.5);  // -1
        System.out.println("Compare: " + result);
    }
}
```

### 3. Character Class

```java
public class CharacterMethods {
    public static void main(String[] args) {
        char ch = 'A';
        
        // Kiểm tra loại ký tự
        System.out.println("Is letter: " + Character.isLetter(ch));      // true
        System.out.println("Is digit: " + Character.isDigit('5'));       // true
        System.out.println("Is whitespace: " + Character.isWhitespace(' ')); // true
        System.out.println("Is uppercase: " + Character.isUpperCase(ch));     // true
        System.out.println("Is lowercase: " + Character.isLowerCase('a'));    // true
        
        // Chuyển đổi
        System.out.println("To uppercase: " + Character.toUpperCase('a'));    // 'A'
        System.out.println("To lowercase: " + Character.toLowerCase('A'));    // 'a'
    }
}
```

### 4. Boolean Class

```java
public class BooleanMethods {
    public static void main(String[] args) {
        // Parse
        Boolean b1 = Boolean.parseBoolean("true");   // true
        Boolean b2 = Boolean.parseBoolean("false");  // false
        Boolean b3 = Boolean.parseBoolean("TRUE");   // true (không phân biệt hoa thường)
        
        // Logical operations
        System.out.println("Logical AND: " + Boolean.logicalAnd(true, false));  // false
        System.out.println("Logical OR: " + Boolean.logicalOr(true, false));    // true
        System.out.println("Logical XOR: " + Boolean.logicalXor(true, false));  // true
    }
}
```

## VI. So sánh Wrapper Objects

### 1. Sử dụng `==` (So sánh reference)

Toán tử `==` so sánh **reference** (địa chỉ bộ nhớ), không phải giá trị:

```java
public class WrapperComparison {
    public static void main(String[] args) {
        Integer a = new Integer(100);
        Integer b = new Integer(100);
        
        System.out.println(a == b);      // ❌ false (khác object)
        System.out.println(a.equals(b)); // ✅ true (cùng giá trị)
    }
}
```

### 2. Sử dụng `equals()` (So sánh giá trị)

Phương thức `equals()` so sánh **giá trị**:

```java
public class WrapperEquals {
    public static void main(String[] args) {
        Integer a = 100;
        Integer b = 100;
        
        System.out.println(a.equals(b));  // ✅ true (cùng giá trị)
    }
}
```

### 3. Integer Caching (Java 5+)

Java cache các giá trị Integer trong khoảng **-128 đến 127**:

```java
public class IntegerCaching {
    public static void main(String[] args) {
        Integer a = 100;   // Trong khoảng cache [-128, 127]
        Integer b = 100;
        System.out.println(a == b);  // ✅ true (cùng object trong cache)
        
        Integer c = 200;   // Ngoài khoảng cache
        Integer d = 200;
        System.out.println(c == d);  // ❌ false (khác object)
        System.out.println(c.equals(d));  // ✅ true (cùng giá trị)
    }
}
```

**Giải thích**:
- Giá trị từ -128 đến 127 được cache trong bộ nhớ
- `Integer.valueOf(100)` sẽ trả về cùng object
- Giá trị ngoài khoảng này tạo object mới mỗi lần

> **Lưu ý**: Luôn sử dụng `equals()` để so sánh wrapper objects, không dùng `==`!

### Ví dụ chi tiết về Integer Caching

```java
public class IntegerCachingDetail {
    public static void main(String[] args) {
        // Test các giá trị trong cache
        for (int i = -130; i <= 130; i++) {
            Integer a = Integer.valueOf(i);
            Integer b = Integer.valueOf(i);
            
            boolean sameReference = (a == b);
            System.out.println(i + " --> " + sameReference);
            
            if (i == -129 || i == 128) {
                System.out.println("  (Ngoài cache, sẽ là false)");
            }
        }
    }
}
```

**Kết quả**:
```
-130 --> false
-129 --> false
-128 --> true      ← Bắt đầu cache
...
127 --> true       ← Kết thúc cache
128 --> false
129 --> false
130 --> false
```

## VII. NullPointerException khi Unboxing

### Vấn đề

Khi unboxing một wrapper object là `null`, sẽ ném `NullPointerException`:

```java
public class NPEOnUnboxing {
    public static void main(String[] args) {
        Integer wrapper = null;
        
        // ❌ LỖI: NullPointerException
        // int primitive = wrapper;  // Ném NPE khi unboxing
        
        // Cách xử lý an toàn
        if (wrapper != null) {
            int primitive = wrapper;  // ✅ An toàn
            System.out.println("Giá trị: " + primitive);
        } else {
            System.out.println("Wrapper là null!");
        }
    }
}
```

### Ví dụ thực tế

```java
public class SafeUnboxing {
    public static int safeUnbox(Integer wrapper, int defaultValue) {
        return (wrapper != null) ? wrapper : defaultValue;
    }
    
    public static void main(String[] args) {
        Integer value1 = 100;
        Integer value2 = null;
        
        int result1 = safeUnbox(value1, 0);  // 100
        int result2 = safeUnbox(value2, 0);  // 0 (giá trị mặc định)
        
        System.out.println("Result 1: " + result1);
        System.out.println("Result 2: " + result2);
    }
}
```

## VIII. Khi nào sử dụng Wrapper Classes?

### 1. Với Collections (ArrayList, HashMap, v.v.)

Collections chỉ chấp nhận objects, không chấp nhận primitives:

```java
import java.util.ArrayList;
import java.util.List;

public class CollectionsWithWrappers {
    public static void main(String[] args) {
        // ❌ KHÔNG THỂ: List<int> numbers = new ArrayList<>();  // Lỗi!
        
        // ✅ PHẢI DÙNG: Wrapper class
        List<Integer> numbers = new ArrayList<>();
        numbers.add(10);      // Auto-boxing: int → Integer
        numbers.add(20);
        numbers.add(30);
        
        // Auto-unboxing khi lấy ra
        int first = numbers.get(0);  // Auto-unboxing: Integer → int
        System.out.println("First: " + first);  // 10
    }
}
```

### 2. Khi cần giá trị null

Primitives không thể là `null`, nhưng wrappers có thể:

```java
public class NullValue {
    public static void main(String[] args) {
        // ❌ KHÔNG THỂ: int value = null;  // Lỗi!
        
        // ✅ CÓ THỂ: Wrapper có thể null
        Integer value = null;  // Đại diện cho "chưa có giá trị"
        
        if (value == null) {
            System.out.println("Chưa có giá trị");
        }
    }
}
```

**Ví dụ thực tế**: Điểm số chưa thi:
```java
public class StudentScore {
    private Integer score;  // null = chưa thi, Integer = đã thi
    
    public boolean hasTakenExam() {
        return score != null;
    }
    
    public void setScore(int score) {
        this.score = score;
    }
}
```

### 3. Sử dụng với Generics (sẽ học ở bài nâng cao)

```java
// Generic methods chỉ làm việc với objects
public static <T> T process(T value) {
    // ...
}

// Không thể dùng: process(10)  // int
// Phải dùng: process(Integer.valueOf(10))  // Integer
```

### 4. API chỉ chấp nhận Objects

Một số API chỉ làm việc với objects:

```java
import java.util.Collections;
import java.util.List;

public class APIRequiresObjects {
    public static void main(String[] args) {
        List<Integer> numbers = List.of(3, 1, 4, 1, 5, 9);
        
        Integer max = Collections.max(numbers);  // Cần objects
        Integer min = Collections.min(numbers);
        
        System.out.println("Max: " + max);  // 9
        System.out.println("Min: " + min);  // 1
    }
}
```

## IX. So sánh Primitive và Wrapper

| Đặc điểm | Primitive Types | Wrapper Classes |
|----------|----------------|-----------------|
| **Tên** | Chữ thường (int, double) | Chữ hoa (Integer, Double) |
| **Giá trị null** | ❌ Không thể | ✅ Có thể |
| **Phương thức** | ❌ Không có | ✅ Có nhiều phương thức |
| **Collections** | ❌ Không thể dùng | ✅ Có thể dùng |
| **Hiệu năng** | ⚡ Nhanh hơn | 🐌 Chậm hơn |
| **Bộ nhớ** | 💾 Ít hơn | 💾 Nhiều hơn |

### Khi nào dùng Primitive, khi nào dùng Wrapper?

**Dùng Primitive khi**:
- ✅ Tính toán số học (nhanh hơn)
- ✅ Không cần null
- ✅ Không cần phương thức

**Dùng Wrapper khi**:
- ✅ Cần lưu trong Collections
- ✅ Cần giá trị null
- ✅ Cần các phương thức tiện ích
- ✅ Làm việc với Generics

**Ví dụ**:
```java
public class ChooseType {
    // Dùng primitive - tính toán nhanh
    public int calculateSum(int a, int b) {
        return a + b;  // Nhanh
    }
    
    // Dùng wrapper - có thể null
    public Integer getScore(String studentId) {
        // Nếu chưa thi → return null
        // Nếu đã thi → return điểm
        return null;  // Đại diện cho "chưa thi"
    }
    
    // Collections - phải dùng wrapper
    private List<Integer> scores = new ArrayList<>();  // ✅ Integer
}
```

## X. Ví dụ thực tế

### Ví dụ 1: Chuyển đổi kiểu trong Form

```java
import java.util.Scanner;

public class FormConversion {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Nhập tuổi (có thể để trống): ");
        String ageInput = scanner.nextLine();
        
        Integer age = null;  // Wrapper - có thể null
        
        if (!ageInput.isEmpty()) {
            age = Integer.parseInt(ageInput);  // String → Integer
        }
        
        if (age != null) {
            System.out.println("Tuổi: " + age);
        } else {
            System.out.println("Chưa nhập tuổi");
        }
        
        scanner.close();
    }
}
```

### Ví dụ 2: Validation với Character class

```java
public class PasswordValidator {
    public static boolean isValidPassword(String password) {
        if (password == null || password.length() < 8) {
            return false;
        }
        
        boolean hasUpper = false;
        boolean hasLower = false;
        boolean hasDigit = false;
        
        for (char ch : password.toCharArray()) {
            if (Character.isUpperCase(ch)) {
                hasUpper = true;
            } else if (Character.isLowerCase(ch)) {
                hasLower = true;
            } else if (Character.isDigit(ch)) {
                hasDigit = true;
            }
        }
        
        return hasUpper && hasLower && hasDigit;
    }
    
    public static void main(String[] args) {
        System.out.println(isValidPassword("Password123"));  // true
        System.out.println(isValidPassword("password"));     // false
        System.out.println(isValidPassword("PASSWORD"));     // false
    }
}
```

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu Wrapper Classes là gì và tại sao cần chúng
- ✅ Nắm được 8 wrapper classes tương ứng với 8 primitive types
- ✅ Hiểu Boxing và Unboxing (manual và auto)
- ✅ Biết cách chuyển đổi giữa String và Primitive
- ✅ Sử dụng các phương thức hữu ích của wrapper classes
- ✅ So sánh đúng cách wrapper objects
- ✅ Hiểu Integer Caching và xử lý NullPointerException
- ✅ Biết khi nào nên dùng primitive, khi nào dùng wrapper

## Bài tập thực hành

1. **Tạo chương trình chuyển đổi**:
   - Nhập một số nguyên từ String
   - Chuyển sang các cơ số khác (nhị phân, thập lục phân)
   - Hiển thị kết quả

2. **Tạo chương trình validation**:
   - Kiểm tra chuỗi nhập vào có phải là số không
   - Sử dụng try-catch để xử lý lỗi

3. **Tạo chương trình xử lý điểm**:
   - Sử dụng `Integer` để lưu điểm (có thể null nếu chưa thi)
   - Kiểm tra và hiển thị trạng thái

## Tài liệu tham khảo

- [Oracle Java Tutorial - Autoboxing](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html)
- [Java Wrapper Classes](https://www.javatpoint.com/wrapper-class-in-java)
- [Integer Caching in Java](https://www.baeldung.com/java-integer-cache)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
