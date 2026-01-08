# Bài 24: ArrayList trong Java

> **Mục tiêu**: Hiểu được ArrayList là gì, cách sử dụng ArrayList, các phương thức phổ biến, và so sánh ArrayList với Array thông thường.

## I. Giới thiệu về ArrayList

### ArrayList là gì?

**ArrayList** là một lớp trong Java Collections Framework được sử dụng để lưu trữ danh sách các phần tử. ArrayList được triển khai như một **mảng động** (dynamic array) - có thể thay đổi kích thước tự động.

### Tại sao cần ArrayList?

**Vấn đề với Array thông thường**:
- ❌ Kích thước **cố định** - Không thể thay đổi sau khi tạo
- ❌ Phải biết trước số lượng phần tử
- ❌ Khó thêm/xóa phần tử

**Giải pháp: ArrayList**:
- ✅ Kích thước **động** - Tự động mở rộng khi cần
- ✅ Không cần biết trước số lượng phần tử
- ✅ Dễ dàng thêm/xóa phần tử
- ✅ Nhiều phương thức tiện ích

### Ví dụ đời thường dễ hiểu

Hãy tưởng tượng bạn có một **cái hộp**:

- **Array** = Hộp có kích thước cố định (ví dụ: chỉ chứa được 10 đồ vật)
- **ArrayList** = Hộp có thể mở rộng (ban đầu chứa 10, khi đầy tự động lớn lên để chứa thêm)

**Trong Java**:
- **Array**: `int[] numbers = new int[10];` → Chỉ chứa được 10 số
- **ArrayList**: `ArrayList<Integer> numbers = new ArrayList<>();` → Chứa được bao nhiêu số cũng được

## II. Đặc điểm của ArrayList

### Đặc điểm chính

- ✅ **Có thể chứa phần tử trùng lặp**: Cho phép các giá trị giống nhau
- ✅ **Giữ nguyên thứ tự**: Thứ tự thêm vào được giữ nguyên
- ✅ **Truy cập ngẫu nhiên**: Truy cập phần tử theo index (vị trí) rất nhanh
- ✅ **Kích thước động**: Tự động mở rộng khi cần (thường tăng 50% mỗi lần)
- ✅ **Không đồng bộ**: Không thread-safe (không an toàn đa luồng)

### Hiệu năng (Performance)

| Thao tác | Độ phức tạp | Mô tả |
|----------|-------------|-------|
| `get(index)` | **O(1)** | Truy cập phần tử theo index (rất nhanh) |
| `add(element)` | **O(1)** amortized | Thêm vào cuối (nhanh, đôi khi O(n) khi resize) |
| `add(index, element)` | **O(n)** | Chèn vào vị trí cụ thể (chậm - phải dịch chuyển) |
| `remove(index)` | **O(n)** | Xóa phần tử (chậm - phải dịch chuyển) |
| `contains(element)` | **O(n)** | Tìm kiếm (phải duyệt từ đầu) |

## III. Khai báo và khởi tạo ArrayList

### Import ArrayList

```java
import java.util.ArrayList;
import java.util.List;  // Interface (khuyến nghị)
```

### Các cách khai báo và khởi tạo

**1. Khai báo và khởi tạo trống**:
```java
// Cách 1: Sử dụng ArrayList cụ thể
ArrayList<String> list1 = new ArrayList<>();

// Cách 2: Sử dụng List interface (khuyến nghị - linh hoạt hơn)
List<String> list2 = new ArrayList<>();
```

**2. Khai báo với capacity ban đầu**:
```java
// Chỉ định capacity ban đầu (tối ưu bộ nhớ nếu biết trước)
List<Integer> numbers = new ArrayList<>(100);  // Capacity = 100
```

**3. Khởi tạo từ collection khác**:
```java
// Từ mảng
List<Integer> list1 = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));

// Từ List khác (Java 9+)
List<Integer> list2 = new ArrayList<>(List.of(10, 20, 30, 40, 50));

// Từ ArrayList khác
ArrayList<String> source = new ArrayList<>();
source.add("A");
source.add("B");
List<String> list3 = new ArrayList<>(source);
```

**4. Immutable List (Java 9+)**:
```java
// List immutable - Không thể thay đổi
List<Integer> immutableList = List.of(1, 2, 3, 4, 5);
// immutableList.add(6);  // ❌ LỖI: UnsupportedOperationException
```

### Ví dụ

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ArrayListInitialization {
    public static void main(String[] args) {
        // Cách 1: Trống
        List<String> list1 = new ArrayList<>();
        list1.add("Apple");
        list1.add("Banana");
        System.out.println("List 1: " + list1);
        
        // Cách 2: Với capacity
        List<Integer> list2 = new ArrayList<>(10);  // Capacity = 10
        for (int i = 1; i <= 5; i++) {
            list2.add(i);
        }
        System.out.println("List 2: " + list2);
        
        // Cách 3: Từ Arrays.asList()
        List<String> list3 = new ArrayList<>(Arrays.asList("Red", "Green", "Blue"));
        System.out.println("List 3: " + list3);
        
        // Cách 4: Từ List.of() (Java 9+)
        List<Integer> list4 = new ArrayList<>(List.of(10, 20, 30));
        System.out.println("List 4: " + list4);
    }
}
```

## IV. Các phương thức phổ biến của ArrayList

### Bảng tóm tắt các phương thức thường dùng

| Phương thức | Kiểu trả về | Mô tả | Ví dụ |
|-------------|-------------|-------|-------|
| `add(element)` | `boolean` | Thêm phần tử vào cuối | `list.add("Hello")` |
| `add(index, element)` | `void` | Chèn phần tử tại vị trí | `list.add(0, "First")` |
| `get(index)` | `E` | Lấy phần tử tại vị trí | `String s = list.get(0)` |
| `set(index, element)` | `E` | Thay thế phần tử tại vị trí | `list.set(0, "New")` |
| `remove(index)` | `E` | Xóa phần tử tại vị trí | `list.remove(0)` |
| `remove(element)` | `boolean` | Xóa phần tử đầu tiên khớp | `list.remove("Hello")` |
| `size()` | `int` | Số lượng phần tử | `int size = list.size()` |
| `isEmpty()` | `boolean` | Kiểm tra rỗng | `if (list.isEmpty())` |
| `contains(element)` | `boolean` | Kiểm tra chứa phần tử | `if (list.contains("Hello"))` |
| `indexOf(element)` | `int` | Vị trí xuất hiện đầu tiên | `int idx = list.indexOf("Hello")` |
| `lastIndexOf(element)` | `int` | Vị trí xuất hiện cuối cùng | `int idx = list.lastIndexOf("Hello")` |
| `clear()` | `void` | Xóa tất cả phần tử | `list.clear()` |
| `toArray()` | `Object[]` | Chuyển thành mảng | `Object[] arr = list.toArray()` |

### Chi tiết các phương thức

#### 1. add() - Thêm phần tử

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListAdd {
    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();
        
        // add(element) - Thêm vào cuối
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        System.out.println("Sau khi thêm: " + fruits);  // [Apple, Banana, Orange]
        
        // add(index, element) - Chèn vào vị trí
        fruits.add(1, "Mango");  // Chèn "Mango" vào vị trí 1
        System.out.println("Sau khi chèn: " + fruits);  // [Apple, Mango, Banana, Orange]
        
        // Thêm nhiều phần tử
        fruits.add("Grapes");
        fruits.add("Pineapple");
        System.out.println("Danh sách cuối: " + fruits);
    }
}
```

#### 2. get() - Lấy phần tử

```java
public class ArrayListGet {
    public static void main(String[] args) {
        List<String> colors = new ArrayList<>();
        colors.add("Red");
        colors.add("Green");
        colors.add("Blue");
        
        // get(index) - Lấy phần tử tại vị trí
        String first = colors.get(0);   // "Red"
        String second = colors.get(1);  // "Green"
        String last = colors.get(colors.size() - 1);  // "Blue"
        
        System.out.println("Màu đầu tiên: " + first);
        System.out.println("Màu cuối cùng: " + last);
        
        // ❌ LỖI: IndexOutOfBoundsException nếu index không hợp lệ
        // String invalid = colors.get(10);  // Lỗi!
    }
}
```

#### 3. set() - Thay thế phần tử

```java
public class ArrayListSet {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        
        System.out.println("Trước: " + numbers);  // [10, 20, 30]
        
        // set(index, element) - Thay thế phần tử
        Integer oldValue = numbers.set(1, 25);  // Thay 20 bằng 25
        System.out.println("Giá trị cũ: " + oldValue);  // 20
        System.out.println("Sau: " + numbers);  // [10, 25, 30]
    }
}
```

#### 4. remove() - Xóa phần tử

```java
public class ArrayListRemove {
    public static void main(String[] args) {
        List<String> animals = new ArrayList<>();
        animals.add("Dog");
        animals.add("Cat");
        animals.add("Bird");
        animals.add("Dog");  // Trùng lặp
        
        System.out.println("Trước: " + animals);  // [Dog, Cat, Bird, Dog]
        
        // remove(index) - Xóa tại vị trí
        String removed = animals.remove(1);  // Xóa "Cat" tại vị trí 1
        System.out.println("Đã xóa: " + removed);  // Cat
        System.out.println("Sau remove(index): " + animals);  // [Dog, Bird, Dog]
        
        // remove(element) - Xóa phần tử đầu tiên khớp
        boolean removed2 = animals.remove("Dog");  // Xóa "Dog" đầu tiên
        System.out.println("Đã xóa Dog? " + removed2);  // true
        System.out.println("Sau remove(element): " + animals);  // [Bird, Dog]
        
        // removeAll() - Xóa tất cả phần tử trong collection
        animals.removeAll(List.of("Dog", "Cat"));
        System.out.println("Sau removeAll: " + animals);  // [Bird]
        
        // clear() - Xóa tất cả
        animals.clear();
        System.out.println("Sau clear: " + animals);  // []
    }
}
```

#### 5. size(), isEmpty(), contains()

```java
public class ArrayListSizeContains {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        
        // isEmpty() - Kiểm tra rỗng
        System.out.println("Rỗng? " + list.isEmpty());  // true
        
        list.add("Apple");
        list.add("Banana");
        list.add("Orange");
        
        // size() - Số lượng phần tử
        System.out.println("Số lượng: " + list.size());  // 3
        
        // contains(element) - Kiểm tra chứa phần tử
        System.out.println("Có 'Apple'? " + list.contains("Apple"));  // true
        System.out.println("Có 'Grape'? " + list.contains("Grape"));  // false
        
        // indexOf() - Vị trí xuất hiện đầu tiên
        int index = list.indexOf("Banana");
        System.out.println("Vị trí 'Banana': " + index);  // 1
        
        // lastIndexOf() - Vị trí xuất hiện cuối cùng
        list.add("Apple");  // Thêm trùng
        int lastIndex = list.lastIndexOf("Apple");
        System.out.println("Vị trí cuối của 'Apple': " + lastIndex);  // 3
    }
}
```

## V. Duyệt ArrayList

### Các cách duyệt ArrayList

**1. For loop với index**:
```java
List<String> fruits = new ArrayList<>(List.of("Apple", "Banana", "Orange"));

for (int i = 0; i < fruits.size(); i++) {
    System.out.println((i + 1) + ". " + fruits.get(i));
}
```

**2. Enhanced for loop (for-each)**:
```java
List<String> fruits = new ArrayList<>(List.of("Apple", "Banana", "Orange"));

for (String fruit : fruits) {
    System.out.println(fruit);
}
```

**3. Iterator**:
```java
import java.util.Iterator;

List<String> fruits = new ArrayList<>(List.of("Apple", "Banana", "Orange"));

Iterator<String> iterator = fruits.iterator();
while (iterator.hasNext()) {
    String fruit = iterator.next();
    System.out.println(fruit);
}
```

**4. forEach() với Lambda (Java 8+)**:
```java
List<String> fruits = new ArrayList<>(List.of("Apple", "Banana", "Orange"));

fruits.forEach(fruit -> System.out.println(fruit));
// Hoặc method reference
fruits.forEach(System.out::println);
```

**5. Stream API (Java 8+)**:
```java
List<String> fruits = new ArrayList<>(List.of("Apple", "Banana", "Orange"));

fruits.stream()
      .forEach(fruit -> System.out.println(fruit));
```

### Ví dụ tổng hợp

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class ArrayListIteration {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>(List.of(10, 20, 30, 40, 50));
        
        System.out.println("=== CÁCH 1: For loop ===");
        for (int i = 0; i < numbers.size(); i++) {
            System.out.print(numbers.get(i) + " ");
        }
        System.out.println();
        
        System.out.println("\n=== CÁCH 2: Enhanced for loop ===");
        for (Integer num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();
        
        System.out.println("\n=== CÁCH 3: Iterator ===");
        Iterator<Integer> iterator = numbers.iterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
        System.out.println();
        
        System.out.println("\n=== CÁCH 4: forEach (Lambda) ===");
        numbers.forEach(num -> System.out.print(num + " "));
        System.out.println();
        
        System.out.println("\n=== CÁCH 5: forEach (Method Reference) ===");
        numbers.forEach(System.out::print);
        System.out.println();
    }
}
```

## VI. So sánh ArrayList và Array

### Bảng so sánh

| Đặc điểm | Array | ArrayList |
|----------|-------|-----------|
| **Kích thước** | Cố định | Động (tự động mở rộng) |
| **Khai báo** | `int[] arr = new int[10];` | `List<Integer> list = new ArrayList<>();` |
| **Kiểu dữ liệu** | Primitive hoặc Object | Chỉ Object (dùng Wrapper) |
| **Truy cập** | `arr[index]` | `list.get(index)` |
| **Thêm phần tử** | Khó (phải biết index) | Dễ (`list.add(element)`) |
| **Xóa phần tử** | Rất khó | Dễ (`list.remove(index)`) |
| **Tìm kiếm** | Phải tự code | `list.contains(element)` |
| **Sắp xếp** | `Arrays.sort(arr)` | `Collections.sort(list)` |
| **Hiệu năng** | Nhanh hơn (ít overhead) | Chậm hơn một chút (wrapper classes) |

### Ví dụ so sánh

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayVsArrayList {
    public static void main(String[] args) {
        // === ARRAY ===
        // Kích thước cố định
        int[] arr = new int[5];
        arr[0] = 10;
        arr[1] = 20;
        // Không thể thêm nếu đã đầy
        // arr[5] = 30;  // ❌ Lỗi: ArrayIndexOutOfBoundsException
        
        // === ARRAYLIST ===
        // Kích thước động
        List<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);  // ✅ OK - Tự động mở rộng
        list.add(40);
        list.add(50);
        
        // Có thể thêm tiếp
        list.add(60);  // ✅ OK - Tự động mở rộng
        
        System.out.println("Array length: " + arr.length);  // 5 (cố định)
        System.out.println("ArrayList size: " + list.size()); // 6 (động)
    }
}
```

## VII. Ví dụ thực tế

### Ví dụ 1: Quản lý danh sách sinh viên

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class StudentManager {
    private List<Student> students;
    
    public StudentManager() {
        this.students = new ArrayList<>();
    }
    
    // Thêm sinh viên
    public void addStudent(Student student) {
        students.add(student);
        System.out.println("✅ Đã thêm sinh viên: " + student.getName());
    }
    
    // Tìm sinh viên theo tên
    public List<Student> findStudentsByName(String name) {
        List<Student> results = new ArrayList<>();
        for (Student student : students) {
            if (student.getName().contains(name)) {
                results.add(student);
            }
        }
        return results;
    }
    
    // Xóa sinh viên theo ID
    public boolean removeStudent(String studentId) {
        for (int i = 0; i < students.size(); i++) {
            if (students.get(i).getStudentId().equals(studentId)) {
                Student removed = students.remove(i);
                System.out.println("✅ Đã xóa sinh viên: " + removed.getName());
                return true;
            }
        }
        System.out.println("❌ Không tìm thấy sinh viên với ID: " + studentId);
        return false;
    }
    
    // Hiển thị tất cả sinh viên
    public void displayAllStudents() {
        if (students.isEmpty()) {
            System.out.println("Danh sách rỗng!");
            return;
        }
        
        System.out.println("\n=== DANH SÁCH SINH VIÊN ===");
        for (int i = 0; i < students.size(); i++) {
            System.out.println((i + 1) + ". " + students.get(i));
        }
        System.out.println("Tổng số: " + students.size());
    }
    
    // Sắp xếp theo tên
    public void sortByName() {
        students.sort((s1, s2) -> s1.getName().compareTo(s2.getName()));
        System.out.println("✅ Đã sắp xếp theo tên");
    }
    
    // Lấy sinh viên có điểm cao nhất
    public Student getTopStudent() {
        if (students.isEmpty()) {
            return null;
        }
        
        Student top = students.get(0);
        for (Student student : students) {
            if (student.getGpa() > top.getGpa()) {
                top = student;
            }
        }
        return top;
    }
    
    public static void main(String[] args) {
        StudentManager manager = new StudentManager();
        
        // Thêm sinh viên
        manager.addStudent(new Student("SV001", "Nguyễn Văn A", 8.5));
        manager.addStudent(new Student("SV002", "Trần Thị B", 9.0));
        manager.addStudent(new Student("SV003", "Lê Văn C", 7.8));
        
        manager.displayAllStudents();
        
        // Tìm kiếm
        List<Student> results = manager.findStudentsByName("Văn");
        System.out.println("\nTìm thấy " + results.size() + " sinh viên có tên 'Văn'");
        
        // Sắp xếp
        manager.sortByName();
        manager.displayAllStudents();
        
        // Lấy top student
        Student top = manager.getTopStudent();
        System.out.println("\nSinh viên xuất sắc nhất: " + top);
    }
}

// Lớp Student đơn giản
class Student {
    private String studentId;
    private String name;
    private double gpa;
    
    public Student(String studentId, String name, double gpa) {
        this.studentId = studentId;
        this.name = name;
        this.gpa = gpa;
    }
    
    public String getStudentId() { return studentId; }
    public String getName() { return name; }
    public double getGpa() { return gpa; }
    
    @Override
    public String toString() {
        return String.format("ID: %s, Tên: %s, GPA: %.2f", studentId, name, gpa);
    }
}
```

### Ví dụ 2: Quản lý giỏ hàng

```java
import java.util.ArrayList;
import java.util.List;

public class ShoppingCart {
    private List<Product> items;
    
    public ShoppingCart() {
        this.items = new ArrayList<>();
    }
    
    // Thêm sản phẩm
    public void addProduct(Product product) {
        items.add(product);
        System.out.println("✅ Đã thêm: " + product.getName());
    }
    
    // Xóa sản phẩm
    public boolean removeProduct(String productId) {
        return items.removeIf(p -> p.getId().equals(productId));
    }
    
    // Tính tổng tiền
    public double calculateTotal() {
        double total = 0;
        for (Product product : items) {
            total += product.getPrice() * product.getQuantity();
        }
        return total;
    }
    
    // Hiển thị giỏ hàng
    public void displayCart() {
        if (items.isEmpty()) {
            System.out.println("Giỏ hàng trống!");
            return;
        }
        
        System.out.println("\n=== GIỎ HÀNG ===");
        for (int i = 0; i < items.size(); i++) {
            Product p = items.get(i);
            System.out.printf("%d. %s - %.2f VNĐ x %d = %.2f VNĐ%n",
                i + 1, p.getName(), p.getPrice(), p.getQuantity(),
                p.getPrice() * p.getQuantity());
        }
        System.out.println("Tổng tiền: " + calculateTotal() + " VNĐ");
    }
    
    // Xóa tất cả
    public void clearCart() {
        items.clear();
        System.out.println("✅ Đã xóa tất cả sản phẩm");
    }
    
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        
        cart.addProduct(new Product("P001", "Laptop", 15000000, 1));
        cart.addProduct(new Product("P002", "Mouse", 500000, 2));
        cart.addProduct(new Product("P003", "Keyboard", 1000000, 1));
        
        cart.displayCart();
        
        cart.removeProduct("P002");
        System.out.println("\nSau khi xóa Mouse:");
        cart.displayCart();
    }
}

// Lớp Product đơn giản
class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;
    
    public Product(String id, String name, double price, int quantity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }
    
    public String getId() { return id; }
    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }
}
```

## VIII. ArrayList với Wrapper Classes

### Vì sao phải dùng Wrapper Classes?

ArrayList chỉ chấp nhận **objects**, không chấp nhận **primitives**:

```java
// ❌ KHÔNG THỂ: ArrayList<int> numbers = new ArrayList<>();  // Lỗi!

// ✅ PHẢI DÙNG: Wrapper class
List<Integer> numbers = new ArrayList<>();  // ✅ OK
```

### Auto-boxing và Auto-unboxing

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListWithWrappers {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        
        // Auto-boxing: int → Integer
        numbers.add(10);   // Tự động chuyển int (10) → Integer
        numbers.add(20);
        numbers.add(30);
        
        // Auto-unboxing: Integer → int
        int first = numbers.get(0);  // Tự động chuyển Integer → int
        System.out.println("First: " + first);  // 10
        
        // Tính toán
        int sum = 0;
        for (Integer num : numbers) {
            sum += num;  // Auto-unboxing: Integer → int
        }
        System.out.println("Sum: " + sum);  // 60
    }
}
```

## IX. Lưu ý quan trọng

### 1. Capacity vs Size

- **Capacity**: Kích thước mảng bên trong (tự động quản lý)
- **Size**: Số lượng phần tử thực tế trong ArrayList

```java
List<String> list = new ArrayList<>(100);  // Capacity = 100, Size = 0
list.add("A");
list.add("B");
// Bây giờ: Capacity có thể > 2, Size = 2

System.out.println("Size: " + list.size());  // 2
// Không có phương thức getCapacity() - Capacity được quản lý tự động
```

### 2. Performance Considerations

**Tốt**:
- ✅ Truy cập phần tử theo index: `get(index)` - O(1)
- ✅ Thêm vào cuối: `add(element)` - O(1) amortized
- ✅ Thay thế: `set(index, element)` - O(1)

**Chậm**:
- ⚠️ Chèn vào giữa: `add(index, element)` - O(n)
- ⚠️ Xóa: `remove(index)` - O(n)
- ⚠️ Tìm kiếm: `contains(element)` - O(n)

**Ví dụ**:
```java
List<Integer> list = new ArrayList<>();

// ✅ TỐT: Thêm vào cuối (nhanh)
for (int i = 0; i < 1000; i++) {
    list.add(i);  // Nhanh - O(1) amortized
}

// ⚠️ CHẬM: Chèn vào đầu (chậm)
for (int i = 0; i < 100; i++) {
    list.add(0, i);  // Chậm - O(n) mỗi lần
}
```

### 3. ConcurrentModificationException

Không thể thay đổi ArrayList trong khi đang duyệt (trừ qua Iterator.remove()):

```java
List<String> list = new ArrayList<>(List.of("A", "B", "C"));

// ❌ LỖI: ConcurrentModificationException
// for (String item : list) {
//     if (item.equals("B")) {
//         list.remove(item);  // Lỗi!
//     }
// }

// ✅ OK: Sử dụng Iterator
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String item = iterator.next();
    if (item.equals("B")) {
        iterator.remove();  // OK
    }
}

// ✅ OK: Sử dụng removeIf() (Java 8+)
list.removeIf(item -> item.equals("B"));
```

## X. ArrayList vs LinkedList vs Vector

### So sánh nhanh

| Đặc điểm | ArrayList | LinkedList | Vector |
|----------|-----------|------------|--------|
| **Cấu trúc** | Mảng động | Danh sách liên kết | Mảng động |
| **Thread-safe** | ❌ Không | ❌ Không | ✅ Có (synchronized) |
| **Truy cập** | ⚡ O(1) - Nhanh | 🐌 O(n) - Chậm | ⚡ O(1) - Nhanh |
| **Chèn/Xóa đầu** | 🐌 O(n) - Chậm | ⚡ O(1) - Nhanh | 🐌 O(n) - Chậm |
| **Chèn/Xóa cuối** | ⚡ O(1) - Nhanh | ⚡ O(1) - Nhanh | ⚡ O(1) - Nhanh |
| **Memory** | Ít hơn | Nhiều hơn (lưu reference) | Ít hơn |

**Khuyến nghị**: Dùng **ArrayList** trong hầu hết trường hợp (nhanh hơn, đơn giản hơn).

## Tổng kết

Sau bài học này, bạn đã:

- ✅ Hiểu ArrayList là gì và tại sao nó quan trọng
- ✅ Nắm được các cách khai báo và khởi tạo ArrayList
- ✅ Sử dụng các phương thức phổ biến của ArrayList
- ✅ Duyệt ArrayList bằng nhiều cách khác nhau
- ✅ So sánh ArrayList với Array thông thường
- ✅ Áp dụng ArrayList vào các ví dụ thực tế
- ✅ Hiểu về hiệu năng và best practices

## Bài tập thực hành

1. **Tạo chương trình quản lý danh sách**:
   - Thêm, xóa, tìm kiếm phần tử
   - Sắp xếp danh sách
   - Hiển thị danh sách

2. **Tạo chương trình quản lý điểm**:
   - Lưu danh sách điểm
   - Tính điểm trung bình
   - Tìm điểm cao nhất, thấp nhất

3. **Tạo chương trình quản lý sản phẩm**:
   - Lưu danh sách sản phẩm
   - Tìm kiếm sản phẩm
   - Sắp xếp theo giá

## Tài liệu tham khảo

- [Oracle Java Tutorial - Collections](https://docs.oracle.com/javase/tutorial/collections/index.html)
- [Java ArrayList Documentation](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)
- [ArrayList vs LinkedList](https://www.baeldung.com/java-arraylist-vs-linkedlist)

---

© Copyright CCCAcademy
Khóa học này được tạo ra nhằm mục đích giáo dục và học tập.
