# Hệ thống 20 Đề tài Project OOP - Java Console Application

## 📚 Mục đích

Tài liệu này cung cấp 20 đề tài project OOP cho sinh viên thực hiện bài tập nhóm, bao phủ nhiều lĩnh vực khác nhau trong đời sống. Mỗi đề tài có mô tả chi tiết, yêu cầu cụ thể và phạm vi phù hợp.

---

## 🎯 Yêu cầu Chung cho Tất cả Projects

### Kiến thức cần áp dụng

- ✅ **Encapsulation**: Private fields, public getters/setters
- ✅ **Inheritance**: Tạo class hierarchy phù hợp
- ✅ **Polymorphism**: Method overriding, upcasting
- ✅ **Abstraction**: Abstract classes và/hoặc Interfaces
- ✅ **Collections**: ArrayList để quản lý danh sách
- ✅ **Sorting**: Comparable/Comparator hoặc Lambda
- ✅ **Java IO**: Lưu/đọc dữ liệu từ file
- ✅ **Exception Handling**: Xử lý lỗi cơ bản

### Cấu trúc Project

```
ProjectName/
└── src/
    ├── entity/          # Các class đại diện cho đối tượng
    ├── service/         # Business logic (quản lý, xử lý)
    ├── util/            # Utilities (validation, helper)
    └── main/            # Main class với menu
```

### Menu cơ bản

Mỗi project cần có menu với các chức năng:
- Hiển thị danh sách
- Thêm mới
- Cập nhật
- Xóa
- Tìm kiếm
- Sắp xếp
- Lưu/Đọc file
- Thống kê (tùy chọn)

---

## 📋 DANH SÁCH 20 ĐỀ TÀI PROJECT

### 1. Hệ thống Quản lý Thư viện (Library Management System) 📚

**Lĩnh vực**: Giáo dục - Thư viện

**Mô tả**: 
Xây dựng hệ thống quản lý thư viện cho phép quản lý sách, thành viên, mượn/trả sách.

**Yêu cầu chi tiết**:

1. **Class `Book`**:
   - Fields: `isbn`, `title`, `author`, `publisher`, `year`, `category`, `available` (boolean)
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`, `borrow()`, `return()`

2. **Class `Member`**:
   - Fields: `memberId`, `name`, `email`, `phone`, `address`, `membershipType`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Class `BorrowRecord`**:
   - Fields: `recordId`, `book`, `member`, `borrowDate`, `returnDate`, `status`
   - Methods: `calculateFine()` (nếu trả muộn)

4. **Class `LibraryService`**:
   - Quản lý ArrayList<Book>, ArrayList<Member>, ArrayList<BorrowRecord>
   - Methods: CRUD cho Book và Member
   - `borrowBook(String isbn, String memberId)`: boolean
   - `returnBook(String isbn)`: boolean
   - `searchBook(String keyword)`: List<Book>
   - `displayBorrowedBooks()`
   - `displayOverdueBooks()`
   - `saveToFile()`, `loadFromFile()`

5. **Menu chức năng**:
   - Quản lý sách (CRUD)
   - Quản lý thành viên (CRUD)
   - Mượn sách
   - Trả sách
   - Tìm kiếm sách
   - Xem sách đang mượn
   - Xem sách quá hạn
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Tính phí mượn trả
- Thống kê: Sách mượn nhiều nhất, Thành viên mượn nhiều nhất
- Đặt trước sách (Reservation)

---

### 2. Hệ thống Quản lý Bệnh viện (Hospital Management System) 🏥

**Lĩnh vực**: Y tế - Chăm sóc sức khỏe

**Mô tả**: 
Xây dựng hệ thống quản lý bệnh viện để quản lý bệnh nhân, bác sĩ, lịch hẹn khám.

**Yêu cầu chi tiết**:

1. **Abstract class `Person`**:
   - Fields: `id`, `name`, `age`, `gender`, `phone`, `address`
   - Abstract method `displayInfo()`

2. **Class `Patient` extends `Person`**:
   - Thêm: `patientId`, `bloodType`, `medicalHistory`
   - Implement `displayInfo()`

3. **Class `Doctor` extends `Person`**:
   - Thêm: `doctorId`, `specialization`, `experience`, `consultationFee`
   - Implement `displayInfo()`

4. **Class `Appointment`**:
   - Fields: `appointmentId`, `patient`, `doctor`, `appointmentDate`, `time`, `status`
   - Methods: `displayInfo()`, `cancel()`

5. **Class `HospitalService`**:
   - Quản lý ArrayList<Patient>, ArrayList<Doctor>, ArrayList<Appointment>
   - Methods:
     - CRUD cho Patient và Doctor
     - `bookAppointment(String patientId, String doctorId, String date, String time)`: boolean
     - `cancelAppointment(String appointmentId)`: boolean
     - `viewAppointmentsByDoctor(String doctorId)`: List<Appointment>
     - `viewAppointmentsByPatient(String patientId)`: List<Appointment>
     - `searchDoctorBySpecialization(String specialization)`: List<Doctor>
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý bệnh nhân
   - Quản lý bác sĩ
   - Đặt lịch hẹn
   - Hủy lịch hẹn
   - Xem lịch hẹn
   - Tìm kiếm bác sĩ
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Quản lý phòng khám
- Tính phí khám
- Thống kê: Bác sĩ khám nhiều nhất, Bệnh nhân khám nhiều nhất

---

### 3. Hệ thống Quản lý Nhà hàng (Restaurant Management System) 🍽️

**Lĩnh vực**: Ẩm thực - Dịch vụ nhà hàng

**Mô tả**: 
Xây dựng hệ thống quản lý nhà hàng để quản lý menu, đơn hàng, khách hàng.

**Yêu cầu chi tiết**:

1. **Abstract class `MenuItem`**:
   - Fields: `id`, `name`, `basePrice`
   - Abstract method `calculatePrice()`
   - Method `displayInfo()`

2. **Class `Food` extends `MenuItem`**:
   - Thêm: `category` (Appetizer, Main, Dessert), `spiceLevel`
   - Implement `calculatePrice()` (category ảnh hưởng giá)

3. **Class `Drink` extends `MenuItem`**:
   - Thêm: `size` (Small, Medium, Large), `isAlcoholic`
   - Implement `calculatePrice()` (size ảnh hưởng giá)

4. **Class `Order`**:
   - Fields: `orderId`, `customerName`, `orderDate`, `items` (ArrayList<MenuItem>), `status`
   - Methods: `addItem(MenuItem item)`, `removeItem(String id)`, `calculateTotal()`, `displayOrder()`

5. **Class `RestaurantService`**:
   - Quản lý ArrayList<MenuItem>, ArrayList<Order>
   - Methods:
     - CRUD cho MenuItem
     - `createOrder(String customerName)`: Order
     - `addItemToOrder(String orderId, String itemId)`: boolean
     - `completeOrder(String orderId)`: boolean
     - `viewOrdersByDate(String date)`: List<Order>
     - `searchMenuItem(String keyword)`: List<MenuItem>
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý menu
   - Tạo đơn hàng
   - Thêm món vào đơn
   - Hoàn thành đơn
   - Xem đơn hàng
   - Tìm kiếm món
   - Thống kê doanh thu
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Discount cho đơn lớn
- Quản lý bàn (Table management)
- Thống kê món bán chạy nhất

---

### 4. Hệ thống Quản lý Khách sạn (Hotel Management System) 🏨

**Lĩnh vực**: Du lịch - Dịch vụ lưu trú

**Mô tả**: 
Xây dựng hệ thống quản lý khách sạn để quản lý phòng, khách hàng, đặt phòng.

**Yêu cầu chi tiết**:

1. **Class `Room`**:
   - Fields: `roomNumber`, `roomType` (Single, Double, Suite), `price`, `available` (boolean), `amenities`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`, `book()`, `checkout()`

2. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `idCard`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Class `Booking`**:
   - Fields: `bookingId`, `customer`, `room`, `checkInDate`, `checkOutDate`, `totalPrice`, `status`
   - Methods: `calculateTotalPrice()`, `displayInfo()`, `cancel()`

4. **Class `HotelService`**:
   - Quản lý ArrayList<Room>, ArrayList<Customer>, ArrayList<Booking>
   - Methods:
     - CRUD cho Room và Customer
     - `bookRoom(String customerId, String roomNumber, String checkIn, String checkOut)`: boolean
     - `checkout(String bookingId)`: boolean
     - `searchAvailableRooms(String checkIn, String checkOut, String roomType)`: List<Room>
     - `viewBookingsByCustomer(String customerId)`: List<Booking>
     - `viewBookingsByDate(String date)`: List<Booking>
     - `saveToFile()`, `loadFromFile()`

5. **Menu chức năng**:
   - Quản lý phòng
   - Quản lý khách hàng
   - Đặt phòng
   - Check-out
   - Tìm phòng trống
   - Xem đặt phòng
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Tính phí dịch vụ thêm
- Quản lý nhân viên
- Thống kê: Phòng được đặt nhiều nhất, Doanh thu theo tháng

---

### 5. Hệ thống Quản lý Cửa hàng Điện thoại (Phone Store Management System) 📱

**Lĩnh vực**: Thương mại điện tử - Bán lẻ

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng điện thoại để quản lý sản phẩm, khách hàng, đơn hàng.

**Yêu cầu chi tiết**:

1. **Class `Phone`**:
   - Fields: `id`, `brand`, `model`, `price`, `storage`, `ram`, `color`, `quantity`, `warranty`
   - Encapsulation đầy đủ
   - Implement `Comparable<Phone>` (sort by price)
   - Methods: `displayInfo()`, `isAvailable()`

2. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `address`, `memberType` (Regular, VIP)
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Interface `PaymentMethod`**:
   - Method `pay(double amount)`: boolean
   - Method `getPaymentInfo()`: String

4. **Class `CashPayment` implements `PaymentMethod`**
5. **Class `CardPayment` implements `PaymentMethod`**

6. **Class `Order`**:
   - Fields: `orderId`, `customer`, `phone`, `quantity`, `paymentMethod`, `orderDate`, `totalPrice`
   - Methods: `calculateTotal()`, `processPayment()`, `displayInfo()`

7. **Class `PhoneStoreService`**:
   - Quản lý ArrayList<Phone>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho Phone và Customer
     - `createOrder(String customerId, String phoneId, int quantity, PaymentMethod payment)`: boolean
     - `searchPhone(String keyword)`: List<Phone>
     - `searchPhoneByPriceRange(double min, double max)`: List<Phone>
     - `sortPhonesByPrice()`: Sử dụng Comparable
     - `sortPhonesByBrand()`: Sử dụng Comparator
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

8. **Menu chức năng**:
   - Quản lý điện thoại
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tìm kiếm điện thoại
   - Sắp xếp điện thoại
   - Thống kê doanh thu
   - Lưu/Đọc dữ liệu

**Phạm vi**: Nâng cao

**Gợi ý mở rộng**:
- Discount cho VIP customers
- Quản lý nhà cung cấp
- Thống kê: Điện thoại bán chạy nhất, Doanh thu theo brand

---

### 6. Hệ thống Quản lý Trường học (School Management System) 🎓

**Lĩnh vực**: Giáo dục - Quản lý trường học

**Mô tả**: 
Xây dựng hệ thống quản lý trường học để quản lý học sinh, giáo viên, lớp học, điểm số.

**Yêu cầu chi tiết**:

1. **Abstract class `Person`**:
   - Fields: `id`, `name`, `age`, `gender`, `email`, `phone`
   - Abstract method `displayInfo()`

2. **Class `Student` extends `Person`**:
   - Thêm: `studentId`, `classId`, `gpa`
   - Implement `displayInfo()`
   - Implement `Comparable<Student>` (sort by GPA)

3. **Class `Teacher` extends `Person`**:
   - Thêm: `teacherId`, `subject`, `experience`, `salary`
   - Implement `displayInfo()`

4. **Class `Class`**:
   - Fields: `classId`, `className`, `teacher`, `students` (ArrayList<Student>), `maxStudents`
   - Methods: `addStudent(Student s)`, `removeStudent(String id)`, `displayInfo()`

5. **Class `Grade`**:
   - Fields: `gradeId`, `student`, `subject`, `score`, `semester`
   - Methods: `displayInfo()`, `getGradeLetter()`

6. **Class `SchoolService`**:
   - Quản lý ArrayList<Student>, ArrayList<Teacher>, ArrayList<Class>, ArrayList<Grade>
   - Methods:
     - CRUD cho Student, Teacher, Class
     - `assignStudentToClass(String studentId, String classId)`: boolean
     - `addGrade(String studentId, String subject, double score)`: boolean
     - `calculateGPA(String studentId)`: double
     - `getTopStudents(int n)`: List<Student>
     - `getStudentsByClass(String classId)`: List<Student>
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý học sinh
   - Quản lý giáo viên
   - Quản lý lớp học
   - Gán học sinh vào lớp
   - Nhập điểm
   - Xem điểm
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Nâng cao

**Gợi ý mở rộng**:
- Quản lý môn học
- Thống kê: Lớp có điểm cao nhất, Học sinh xuất sắc nhất

---

### 7. Hệ thống Quản lý Phòng Gym (Gym Management System) 💪

**Lĩnh vực**: Thể thao - Sức khỏe

**Mô tả**: 
Xây dựng hệ thống quản lý phòng gym để quản lý hội viên, gói tập, lịch tập.

**Yêu cầu chi tiết**:

1. **Class `Member`**:
   - Fields: `memberId`, `name`, `age`, `gender`, `phone`, `email`, `membershipType`, `joinDate`, `expiryDate`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`, `isActive()`

2. **Class `MembershipPackage`**:
   - Fields: `packageId`, `packageName`, `duration` (months), `price`, `features`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Class `Trainer`**:
   - Fields: `trainerId`, `name`, `specialization`, `experience`, `hourlyRate`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

4. **Class `WorkoutSession`**:
   - Fields: `sessionId`, `member`, `trainer`, `date`, `time`, `duration`, `status`
   - Methods: `displayInfo()`, `calculateCost()`

5. **Class `GymService`**:
   - Quản lý ArrayList<Member>, ArrayList<MembershipPackage>, ArrayList<Trainer>, ArrayList<WorkoutSession>
   - Methods:
     - CRUD cho Member, Package, Trainer
     - `registerMember(String name, String packageId)`: boolean
     - `bookSession(String memberId, String trainerId, String date, String time)`: boolean
     - `renewMembership(String memberId, String packageId)`: boolean
     - `searchTrainerBySpecialization(String specialization)`: List<Trainer>
     - `getActiveMembers()`: List<Member>
     - `getExpiredMembers()`: List<Member>
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý hội viên
   - Quản lý gói tập
   - Quản lý huấn luyện viên
   - Đăng ký hội viên
   - Gia hạn gói
   - Đặt lịch tập
   - Tìm kiếm
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Quản lý thiết bị
- Thống kê: Hội viên tập nhiều nhất, Doanh thu theo tháng

---

### 8. Hệ thống Quản lý Rạp chiếu phim (Cinema Management System) 🎬

**Lĩnh vực**: Giải trí - Điện ảnh

**Mô tả**: 
Xây dựng hệ thống quản lý rạp chiếu phim để quản lý phim, suất chiếu, vé, khách hàng.

**Yêu cầu chi tiết**:

1. **Class `Movie`**:
   - Fields: `movieId`, `title`, `director`, `genre`, `duration`, `releaseDate`, `rating`
   - Encapsulation đầy đủ
   - Implement `Comparable<Movie>` (sort by rating)
   - Methods: `displayInfo()`

2. **Class `Showtime`**:
   - Fields: `showtimeId`, `movie`, `screen`, `date`, `time`, `availableSeats`, `price`
   - Methods: `displayInfo()`, `bookSeat(int numberOfSeats)`: boolean

3. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

4. **Class `Ticket`**:
   - Fields: `ticketId`, `customer`, `showtime`, `numberOfSeats`, `totalPrice`, `purchaseDate`
   - Methods: `displayInfo()`, `calculateTotal()`

5. **Class `CinemaService`**:
   - Quản lý ArrayList<Movie>, ArrayList<Showtime>, ArrayList<Customer>, ArrayList<Ticket>
   - Methods:
     - CRUD cho Movie, Showtime, Customer
     - `bookTicket(String customerId, String showtimeId, int seats)`: boolean
     - `searchMovie(String keyword)`: List<Movie>
     - `searchShowtimeByMovie(String movieId)`: List<Showtime>
     - `searchShowtimeByDate(String date)`: List<Showtime>
     - `getTopMovies(int n)`: List<Movie>
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý phim
   - Quản lý suất chiếu
   - Quản lý khách hàng
   - Đặt vé
   - Tìm kiếm phim
   - Xem suất chiếu
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Quản lý ghế (Seat management)
- Discount cho học sinh/sinh viên
- Thống kê: Phim được xem nhiều nhất, Doanh thu theo phim

---

### 9. Hệ thống Quản lý Cửa hàng Quần áo (Clothing Store Management System) 👕

**Lĩnh vực**: Thời trang - Bán lẻ

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng quần áo để quản lý sản phẩm, đơn hàng, khách hàng.

**Yêu cầu chi tiết**:

1. **Abstract class `Product`**:
   - Fields: `id`, `name`, `brand`, `basePrice`
   - Abstract method `calculatePrice()`
   - Method `displayInfo()`

2. **Class `Clothing` extends `Product`**:
   - Thêm: `category` (Shirt, Pants, Dress, etc.), `size`, `color`, `material`, `quantity`
   - Implement `calculatePrice()` (category và material ảnh hưởng giá)

3. **Class `Accessory` extends `Product`**:
   - Thêm: `type` (Bag, Shoes, Hat, etc.), `quantity`
   - Implement `calculatePrice()`

4. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `size`, `memberType`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

5. **Class `Order`**:
   - Fields: `orderId`, `customer`, `items` (ArrayList<Product>), `orderDate`, `totalPrice`, `status`
   - Methods: `addItem(Product item)`, `removeItem(String id)`, `calculateTotal()`, `displayInfo()`

6. **Class `ClothingStoreService`**:
   - Quản lý ArrayList<Product>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho Product và Customer
     - `createOrder(String customerId)`: Order
     - `addItemToOrder(String orderId, String productId)`: boolean
     - `searchProduct(String keyword)`: List<Product>
     - `searchProductBySize(String size)`: List<Product>
     - `searchProductByCategory(String category)`: List<Product>
     - `sortProductsByPrice()`: Sử dụng Lambda
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý sản phẩm
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tìm kiếm sản phẩm
   - Sắp xếp sản phẩm
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Quản lý size và số lượng
- Discount theo memberType
- Thống kê: Sản phẩm bán chạy nhất, Doanh thu theo category

---

### 10. Hệ thống Quản lý Tài chính Cá nhân (Personal Finance Management System) 💰

**Lĩnh vực**: Tài chính - Quản lý cá nhân

**Mô tả**: 
Xây dựng hệ thống quản lý tài chính cá nhân để quản lý thu chi, phân loại, thống kê.

**Yêu cầu chi tiết**:

1. **Abstract class `Transaction`**:
   - Fields: `transactionId`, `amount`, `date`, `description`
   - Abstract method `getType()`: String
   - Method `displayInfo()`

2. **Class `Income` extends `Transaction`**:
   - Thêm: `source` (Salary, Bonus, Investment, etc.)
   - Implement `getType()`: return "Income"

3. **Class `Expense` extends `Transaction`**:
   - Thêm: `category` (Food, Transport, Entertainment, etc.)
   - Implement `getType()`: return "Expense"

4. **Class `Budget`**:
   - Fields: `budgetId`, `category`, `limit`, `spent`
   - Methods: `displayInfo()`, `isExceeded()`: boolean

5. **Class `FinanceService`**:
   - Quản lý ArrayList<Transaction>, ArrayList<Budget>
   - Methods:
     - `addIncome(String source, double amount, String date, String description)`: boolean
     - `addExpense(String category, double amount, String date, String description)`: boolean
     - `getTotalIncome()`: double
     - `getTotalExpense()`: double
     - `getBalance()`: double
     - `getExpensesByCategory(String category)`: List<Expense>
     - `getTransactionsByDate(String date)`: List<Transaction>
     - `setBudget(String category, double limit)`: boolean
     - `checkBudget()`: List<Budget>
     - `getMonthlyReport(String month)`: String
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Thêm thu nhập
   - Thêm chi tiêu
   - Xem tổng thu
   - Xem tổng chi
   - Xem số dư
   - Xem chi tiêu theo category
   - Đặt ngân sách
   - Kiểm tra ngân sách
   - Xem báo cáo tháng
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Biểu đồ thống kê (text-based)
- Dự báo chi tiêu
- Nhắc nhở khi sắp vượt ngân sách

---

### 11. Hệ thống Quản lý Vận tải (Transportation Management System) 🚚

**Lĩnh vực**: Giao thông - Vận tải

**Mô tả**: 
Xây dựng hệ thống quản lý vận tải để quản lý phương tiện, tài xế, chuyến hàng.

**Yêu cầu chi tiết**:

1. **Abstract class `Vehicle`**:
   - Fields: `vehicleId`, `licensePlate`, `brand`, `model`, `year`, `capacity`
   - Abstract method `calculateMaintenanceCost()`: double
   - Method `displayInfo()`

2. **Class `Truck` extends `Vehicle`**:
   - Thêm: `loadCapacity`, `fuelType`
   - Implement `calculateMaintenanceCost()`

3. **Class `Van` extends `Vehicle`**:
   - Thêm: `passengerCapacity`
   - Implement `calculateMaintenanceCost()`

4. **Class `Driver`**:
   - Fields: `driverId`, `name`, `licenseNumber`, `experience`, `phone`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

5. **Class `Shipment`**:
   - Fields: `shipmentId`, `sender`, `receiver`, `vehicle`, `driver`, `pickupDate`, `deliveryDate`, `status`, `weight`, `distance`
   - Methods: `displayInfo()`, `calculateCost()`: double

6. **Class `TransportService`**:
   - Quản lý ArrayList<Vehicle>, ArrayList<Driver>, ArrayList<Shipment>
   - Methods:
     - CRUD cho Vehicle và Driver
     - `createShipment(String sender, String receiver, String vehicleId, String driverId, double weight, double distance)`: boolean
     - `assignDriver(String shipmentId, String driverId)`: boolean
     - `updateShipmentStatus(String shipmentId, String status)`: boolean
     - `searchAvailableVehicles()`: List<Vehicle>
     - `getShipmentsByDriver(String driverId)`: List<Shipment>
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý phương tiện
   - Quản lý tài xế
   - Tạo chuyến hàng
   - Gán tài xế
   - Cập nhật trạng thái
   - Tìm phương tiện trống
   - Xem chuyến hàng
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Tracking vị trí (giả lập)
- Tính phí theo khoảng cách và trọng lượng
- Thống kê: Tài xế làm nhiều nhất, Phương tiện sử dụng nhiều nhất

---

### 12. Hệ thống Quản lý Công viên Giải trí (Amusement Park Management System) 🎢

**Lĩnh vực**: Du lịch - Giải trí

**Mô tả**: 
Xây dựng hệ thống quản lý công viên giải trí để quản lý trò chơi, vé, khách hàng.

**Yêu cầu chi tiết**:

1. **Class `Ride`**:
   - Fields: `rideId`, `name`, `type` (Roller Coaster, Ferris Wheel, etc.), `capacity`, `duration`, `price`, `minHeight`, `maxHeight`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`, `isEligible(int age, double height)`: boolean

2. **Class `Ticket`**:
   - Fields: `ticketId`, `ticketType` (Single, Day Pass, Season Pass), `price`, `validity`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Class `Visitor`**:
   - Fields: `visitorId`, `name`, `age`, `height`, `phone`, `ticket`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`, `canRide(Ride ride)`: boolean

4. **Class `RideSession`**:
   - Fields: `sessionId`, `ride`, `visitor`, `sessionTime`, `status`
   - Methods: `displayInfo()`

5. **Class `AmusementParkService`**:
   - Quản lý ArrayList<Ride>, ArrayList<Ticket>, ArrayList<Visitor>, ArrayList<RideSession>
   - Methods:
     - CRUD cho Ride, Ticket, Visitor
     - `purchaseTicket(String visitorId, String ticketType)`: boolean
     - `bookRide(String visitorId, String rideId)`: boolean
     - `searchRidesByType(String type)`: List<Ride>
     - `getEligibleRides(String visitorId)`: List<Ride>
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý trò chơi
   - Quản lý vé
   - Quản lý khách
   - Mua vé
   - Đặt chỗ trò chơi
   - Tìm kiếm trò chơi
   - Xem trò chơi phù hợp
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Quản lý hàng đợi
- Discount cho trẻ em/người già
- Thống kê: Trò chơi được chơi nhiều nhất

---

### 13. Hệ thống Quản lý Cửa hàng Thú cưng (Pet Store Management System) 🐾

**Lĩnh vực**: Thú cưng - Chăm sóc động vật

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng thú cưng để quản lý thú cưng, khách hàng, dịch vụ.

**Yêu cầu chi tiết**:

1. **Abstract class `Pet`**:
   - Fields: `petId`, `name`, `species`, `breed`, `age`, `price`, `available` (boolean)
   - Abstract method `getCareInstructions()`: String
   - Method `displayInfo()`

2. **Class `Dog` extends `Pet`**:
   - Thêm: `size` (Small, Medium, Large)
   - Implement `getCareInstructions()`

3. **Class `Cat` extends `Pet`**:
   - Thêm: `isIndoor`
   - Implement `getCareInstructions()`

4. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `address`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

5. **Class `Service`**:
   - Fields: `serviceId`, `serviceName`, `description`, `price`, `duration`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

6. **Class `PetStoreService`**:
   - Quản lý ArrayList<Pet>, ArrayList<Customer>, ArrayList<Service>
   - Methods:
     - CRUD cho Pet, Customer, Service
     - `adoptPet(String customerId, String petId)`: boolean
     - `searchPet(String keyword)`: List<Pet>
     - `searchPetBySpecies(String species)`: List<Pet>
     - `getAvailablePets()`: List<Pet>
     - `bookService(String customerId, String serviceId)`: boolean
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý thú cưng
   - Quản lý khách hàng
   - Quản lý dịch vụ
   - Nhận nuôi thú cưng
   - Đặt dịch vụ
   - Tìm kiếm thú cưng
   - Xem thú cưng có sẵn
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Quản lý thức ăn và phụ kiện
- Lịch tiêm phòng
- Thống kê: Loài thú cưng được nhận nuôi nhiều nhất

---

### 14. Hệ thống Quản lý Cửa hàng Sách (Bookstore Management System) 📖

**Lĩnh vực**: Văn hóa - Giáo dục

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng sách để quản lý sách, khách hàng, đơn hàng.

**Yêu cầu chi tiết**:

1. **Class `Book`**:
   - Fields: `isbn`, `title`, `author`, `publisher`, `year`, `category`, `price`, `quantity`, `rating`
   - Encapsulation đầy đủ
   - Implement `Comparable<Book>` (sort by rating)
   - Methods: `displayInfo()`, `isAvailable()`

2. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `memberType` (Regular, Premium)
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Class `Order`**:
   - Fields: `orderId`, `customer`, `books` (ArrayList<Book>), `orderDate`, `totalPrice`, `status`
   - Methods: `addBook(Book book)`, `removeBook(String isbn)`, `calculateTotal()`, `displayInfo()`

4. **Class `BookstoreService`**:
   - Quản lý ArrayList<Book>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho Book và Customer
     - `createOrder(String customerId)`: Order
     - `addBookToOrder(String orderId, String isbn)`: boolean
     - `searchBook(String keyword)`: List<Book>
     - `searchBookByAuthor(String author)`: List<Book>
     - `searchBookByCategory(String category)`: List<Book>
     - `getTopBooks(int n)`: List<Book>
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

5. **Menu chức năng**:
   - Quản lý sách
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tìm kiếm sách
   - Sắp xếp sách
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Discount cho Premium members
- Quản lý tác giả
- Thống kê: Sách bán chạy nhất, Tác giả bán chạy nhất

---

### 15. Hệ thống Quản lý Dự án (Project Management System) 🚀

**Lĩnh vực**: Công nghệ - Quản lý dự án

**Mô tả**: 
Xây dựng hệ thống quản lý dự án để quản lý projects, tasks, team members.

**Yêu cầu chi tiết**:

1. **Abstract class `WorkItem`**:
   - Fields: `id`, `title`, `description`, `status`, `priority`, `assignee`
   - Abstract method `calculateProgress()`: double
   - Method `displayInfo()`

2. **Class `Project` extends `WorkItem`**:
   - Thêm: `startDate`, `endDate`, `budget`, `tasks` (ArrayList<Task>)
   - Implement `calculateProgress()`

3. **Class `Task` extends `WorkItem`**:
   - Thêm: `projectId`, `dueDate`, `estimatedHours`
   - Implement `calculateProgress()`

4. **Class `TeamMember`**:
   - Fields: `memberId`, `name`, `role`, `email`, `phone`, `skills`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

5. **Interface `Assignable`**:
   - Method `assign(TeamMember member)`: boolean
   - Method `unassign()`: boolean

6. **Class `ProjectService`**:
   - Quản lý ArrayList<Project>, ArrayList<Task>, ArrayList<TeamMember>
   - Methods:
     - CRUD cho Project, Task, TeamMember
     - `createTask(String projectId, String title, String description)`: boolean
     - `assignTask(String taskId, String memberId)`: boolean
     - `updateTaskStatus(String taskId, String status)`: boolean
     - `getTasksByProject(String projectId)`: List<Task>
     - `getTasksByMember(String memberId)`: List<Task>
     - `getProjectsByStatus(String status)`: List<Project>
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý dự án
   - Quản lý công việc
   - Quản lý thành viên
   - Tạo công việc
   - Gán công việc
   - Cập nhật trạng thái
   - Xem tiến độ
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Nâng cao

**Gợi ý mở rộng**:
- Gantt chart (text-based)
- Thống kê: Thành viên làm nhiều nhất, Dự án hoàn thành đúng hạn

---

### 16. Hệ thống Quản lý Cửa hàng Đồ chơi (Toy Store Management System) 🧸

**Lĩnh vực**: Giải trí - Đồ chơi

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng đồ chơi để quản lý sản phẩm, khách hàng, đơn hàng.

**Yêu cầu chi tiết**:

1. **Abstract class `Toy`**:
   - Fields: `toyId`, `name`, `brand`, `basePrice`, `ageRange`, `quantity`
   - Abstract method `calculatePrice()`: double
   - Method `displayInfo()`

2. **Class `ElectronicToy` extends `Toy`**:
   - Thêm: `batteryType`, `features`
   - Implement `calculatePrice()`

3. **Class `EducationalToy` extends `Toy`**:
   - Thêm: `subject`, `skillLevel`
   - Implement `calculatePrice()`

4. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `childAge`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

5. **Class `Order`**:
   - Fields: `orderId`, `customer`, `toys` (ArrayList<Toy>), `orderDate`, `totalPrice`
   - Methods: `addToy(Toy toy)`, `removeToy(String id)`, `calculateTotal()`, `displayInfo()`

6. **Class `ToyStoreService`**:
   - Quản lý ArrayList<Toy>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho Toy và Customer
     - `createOrder(String customerId)`: Order
     - `addToyToOrder(String orderId, String toyId)`: boolean
     - `searchToy(String keyword)`: List<Toy>
     - `getToysByAgeRange(int age)`: List<Toy>
     - `getToysByCategory(String category)`: List<Toy>
     - `sortToysByPrice()`: Sử dụng Lambda
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý đồ chơi
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tìm kiếm đồ chơi
   - Gợi ý đồ chơi theo tuổi
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Gợi ý đồ chơi phù hợp với độ tuổi
- Discount cho đơn lớn
- Thống kê: Đồ chơi bán chạy nhất

---

### 17. Hệ thống Quản lý Spa & Làm đẹp (Spa & Beauty Management System) 💆

**Lĩnh vực**: Làm đẹp - Chăm sóc sức khỏe

**Mô tả**: 
Xây dựng hệ thống quản lý spa để quản lý dịch vụ, khách hàng, lịch hẹn.

**Yêu cầu chi tiết**:

1. **Class `Service`**:
   - Fields: `serviceId`, `serviceName`, `category` (Facial, Massage, Hair, etc.), `duration`, `price`, `description`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

2. **Class `Therapist`**:
   - Fields: `therapistId`, `name`, `specialization`, `experience`, `rating`, `hourlyRate`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

3. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `memberType` (Regular, VIP)
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

4. **Class `Appointment`**:
   - Fields: `appointmentId`, `customer`, `service`, `therapist`, `appointmentDate`, `time`, `duration`, `totalPrice`, `status`
   - Methods: `displayInfo()`, `calculatePrice()`: double, `cancel()`

5. **Class `SpaService`**:
   - Quản lý ArrayList<Service>, ArrayList<Therapist>, ArrayList<Customer>, ArrayList<Appointment>
   - Methods:
     - CRUD cho Service, Therapist, Customer
     - `bookAppointment(String customerId, String serviceId, String therapistId, String date, String time)`: boolean
     - `cancelAppointment(String appointmentId)`: boolean
     - `searchServiceByCategory(String category)`: List<Service>
     - `searchTherapistBySpecialization(String specialization)`: List<Therapist>
     - `viewAppointmentsByDate(String date)`: List<Appointment>
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý dịch vụ
   - Quản lý nhân viên
   - Quản lý khách hàng
   - Đặt lịch hẹn
   - Hủy lịch hẹn
   - Tìm kiếm
   - Xem lịch hẹn
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Package services (gói dịch vụ)
- Discount cho VIP members
- Thống kê: Dịch vụ được đặt nhiều nhất

---

### 18. Hệ thống Quản lý Cửa hàng Hoa (Flower Shop Management System) 🌸

**Lĩnh vực**: Dịch vụ - Quà tặng

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng hoa để quản lý hoa, đơn hàng, khách hàng.

**Yêu cầu chi tiết**:

1. **Class `Flower`**:
   - Fields: `flowerId`, `name`, `color`, `price`, `quantity`, `season`, `occasion` (Wedding, Birthday, etc.)
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`, `isAvailable()`

2. **Class `Bouquet`**:
   - Fields: `bouquetId`, `name`, `flowers` (ArrayList<Flower>), `price`, `description`
   - Methods: `addFlower(Flower flower)`, `removeFlower(String id)`, `calculatePrice()`, `displayInfo()`

3. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `address`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

4. **Class `Order`**:
   - Fields: `orderId`, `customer`, `items` (ArrayList<Object> - Flower hoặc Bouquet), `orderDate`, `deliveryDate`, `deliveryAddress`, `totalPrice`, `status`
   - Methods: `addItem(Object item)`, `calculateTotal()`, `displayInfo()`

5. **Class `FlowerShopService`**:
   - Quản lý ArrayList<Flower>, ArrayList<Bouquet>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho Flower, Bouquet, Customer
     - `createOrder(String customerId)`: Order
     - `addItemToOrder(String orderId, String itemId, String type)`: boolean
     - `searchFlower(String keyword)`: List<Flower>
     - `searchFlowerByOccasion(String occasion)`: List<Flower>
     - `searchFlowerBySeason(String season)`: List<Flower>
     - `createBouquet(String name, List<String> flowerIds)`: Bouquet
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

6. **Menu chức năng**:
   - Quản lý hoa
   - Quản lý bó hoa
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tạo bó hoa
   - Tìm kiếm hoa
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Gợi ý hoa theo dịp
- Tính phí giao hàng
- Thống kê: Hoa bán chạy nhất, Dịp được đặt nhiều nhất

---

### 19. Hệ thống Quản lý Cửa hàng Đồ thể thao (Sports Store Management System) ⚽

**Lĩnh vực**: Thể thao - Bán lẻ

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng đồ thể thao để quản lý sản phẩm, khách hàng, đơn hàng.

**Yêu cầu chi tiết**:

1. **Abstract class `SportsItem`**:
   - Fields: `id`, `name`, `brand`, `basePrice`, `category`, `quantity`
   - Abstract method `calculatePrice()`: double
   - Method `displayInfo()`

2. **Class `Equipment` extends `SportsItem`**:
   - Thêm: `type` (Ball, Racket, etc.), `material`
   - Implement `calculatePrice()`

3. **Class `Apparel` extends `SportsItem`**:
   - Thêm: `size`, `color`, `sportType`
   - Implement `calculatePrice()`

4. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `sportInterest`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

5. **Class `Order`**:
   - Fields: `orderId`, `customer`, `items` (ArrayList<SportsItem>), `orderDate`, `totalPrice`
   - Methods: `addItem(SportsItem item)`, `removeItem(String id)`, `calculateTotal()`, `displayInfo()`

6. **Class `SportsStoreService`**:
   - Quản lý ArrayList<SportsItem>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho SportsItem và Customer
     - `createOrder(String customerId)`: Order
     - `addItemToOrder(String orderId, String itemId)`: boolean
     - `searchItem(String keyword)`: List<SportsItem>
     - `searchItemByCategory(String category)`: List<SportsItem>
     - `searchItemBySport(String sport)`: List<SportsItem>
     - `sortItemsByPrice()`: Sử dụng Lambda
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

7. **Menu chức năng**:
   - Quản lý sản phẩm
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tìm kiếm sản phẩm
   - Sắp xếp sản phẩm
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Gợi ý sản phẩm theo sở thích thể thao
- Discount cho đơn lớn
- Thống kê: Sản phẩm bán chạy nhất, Môn thể thao phổ biến nhất

---

### 20. Hệ thống Quản lý Cửa hàng Đồ nội thất (Furniture Store Management System) 🪑

**Lĩnh vực**: Nội thất - Bán lẻ

**Mô tả**: 
Xây dựng hệ thống quản lý cửa hàng đồ nội thất để quản lý sản phẩm, khách hàng, đơn hàng.

**Yêu cầu chi tiết**:

1. **Abstract class `Furniture`**:
   - Fields: `id`, `name`, `category` (Chair, Table, Sofa, etc.), `material`, `basePrice`, `dimensions`, `quantity`
   - Abstract method `calculatePrice()`: double
   - Method `displayInfo()`

2. **Class `Chair` extends `Furniture`**:
   - Thêm: `hasArmrest`, `hasWheels`
   - Implement `calculatePrice()`

3. **Class `Table` extends `Furniture`**:
   - Thêm: `tableType` (Dining, Coffee, etc.), `seatingCapacity`
   - Implement `calculatePrice()`

4. **Class `Sofa` extends `Furniture`**:
   - Thêm: `seatingCapacity`, `isReclining`
   - Implement `calculatePrice()`

5. **Class `Customer`**:
   - Fields: `customerId`, `name`, `email`, `phone`, `address`
   - Encapsulation đầy đủ
   - Methods: `displayInfo()`

6. **Class `Order`**:
   - Fields: `orderId`, `customer`, `items` (ArrayList<Furniture>), `orderDate`, `deliveryDate`, `deliveryAddress`, `totalPrice`, `status`
   - Methods: `addItem(Furniture item)`, `removeItem(String id)`, `calculateTotal()`, `displayInfo()`

7. **Class `FurnitureStoreService`**:
   - Quản lý ArrayList<Furniture>, ArrayList<Customer>, ArrayList<Order>
   - Methods:
     - CRUD cho Furniture và Customer
     - `createOrder(String customerId)`: Order
     - `addItemToOrder(String orderId, String itemId)`: boolean
     - `searchFurniture(String keyword)`: List<Furniture>
     - `searchFurnitureByCategory(String category)`: List<Furniture>
     - `searchFurnitureByMaterial(String material)`: List<Furniture>
     - `sortFurnitureByPrice()`: Sử dụng Lambda
     - `getTotalRevenue()`: double
     - `saveToFile()`, `loadFromFile()`

8. **Menu chức năng**:
   - Quản lý nội thất
   - Quản lý khách hàng
   - Tạo đơn hàng
   - Tìm kiếm nội thất
   - Sắp xếp nội thất
   - Thống kê
   - Lưu/Đọc dữ liệu

**Phạm vi**: Trung bình - Nâng cao

**Gợi ý mở rộng**:
- Tính phí vận chuyển theo kích thước
- Gợi ý nội thất theo phong cách
- Thống kê: Nội thất bán chạy nhất, Material phổ biến nhất

---

## 📊 Tổng kết 20 Đề tài

| STT | Đề tài | Lĩnh vực | Mức độ |
|-----|--------|----------|--------|
| 1 | Thư viện | Giáo dục | Trung bình - Nâng cao |
| 2 | Bệnh viện | Y tế | Trung bình - Nâng cao |
| 3 | Nhà hàng | Ẩm thực | Trung bình - Nâng cao |
| 4 | Khách sạn | Du lịch | Trung bình - Nâng cao |
| 5 | Điện thoại | Thương mại | Nâng cao |
| 6 | Trường học | Giáo dục | Nâng cao |
| 7 | Phòng Gym | Thể thao | Trung bình - Nâng cao |
| 8 | Rạp chiếu phim | Giải trí | Trung bình - Nâng cao |
| 9 | Quần áo | Thời trang | Trung bình - Nâng cao |
| 10 | Tài chính cá nhân | Tài chính | Trung bình - Nâng cao |
| 11 | Vận tải | Giao thông | Trung bình - Nâng cao |
| 12 | Công viên giải trí | Du lịch | Trung bình - Nâng cao |
| 13 | Thú cưng | Chăm sóc động vật | Trung bình - Nâng cao |
| 14 | Sách | Văn hóa | Trung bình - Nâng cao |
| 15 | Dự án | Công nghệ | Nâng cao |
| 16 | Đồ chơi | Giải trí | Trung bình - Nâng cao |
| 17 | Spa & Làm đẹp | Làm đẹp | Trung bình - Nâng cao |
| 18 | Hoa | Dịch vụ | Trung bình - Nâng cao |
| 19 | Đồ thể thao | Thể thao | Trung bình - Nâng cao |
| 20 | Nội thất | Nội thất | Trung bình - Nâng cao |

---

## 📝 Hướng dẫn Sử dụng

### Cho Giáo viên

1. **Phân nhóm**: Chia sinh viên thành nhóm 3-4 người
2. **Giao đề tài**: Phân công đề tài cho từng nhóm (có thể random hoặc để nhóm chọn)
3. **Thời gian**: 4-6 tuần (tùy mức độ)
4. **Đánh giá**: Dựa trên:
   - Code quality (Encapsulation, Inheritance, Polymorphism, Abstraction)
   - Functionality (đầy đủ chức năng)
   - Code organization (cấu trúc project)
   - Documentation (comments, README)

### Cho Sinh viên

1. **Phân công công việc**: Mỗi thành viên phụ trách một phần
2. **Làm theo yêu cầu**: Đảm bảo áp dụng đầy đủ các khái niệm OOP
3. **Test kỹ**: Kiểm tra các chức năng hoạt động đúng
4. **Documentation**: Viết README và comments trong code

---

## 🎯 Tiêu chí Đánh giá

### Bắt buộc (60 điểm)

- ✅ Encapsulation: Private fields, getters/setters (10 điểm)
- ✅ Inheritance: Class hierarchy phù hợp (15 điểm)
- ✅ Polymorphism: Method overriding, upcasting (15 điểm)
- ✅ Abstraction: Abstract classes/Interfaces (10 điểm)
- ✅ Collections: ArrayList (5 điểm)
- ✅ Java IO: Lưu/đọc file (5 điểm)

### Nâng cao (40 điểm)

- ✅ Code organization: Cấu trúc project rõ ràng (10 điểm)
- ✅ Exception handling: Xử lý lỗi (5 điểm)
- ✅ Validation: Kiểm tra dữ liệu đầu vào (5 điểm)
- ✅ Sorting: Sử dụng Comparable/Comparator/Lambda (5 điểm)
- ✅ Search: Tìm kiếm hiệu quả (5 điểm)
- ✅ Statistics: Thống kê (5 điểm)
- ✅ Documentation: Comments, README (5 điểm)

---

**Chúc các bạn thực hiện project thành công!** 🎓

---

*Tài liệu này cung cấp 20 đề tài project OOP cho bài tập nhóm*
*Cập nhật: 2025-01-XX*
