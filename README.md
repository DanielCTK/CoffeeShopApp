# CoffeeShopApp


## Mục đích Ứng dụng (Application Purpose)

Đây là một **Ứng dụng Quản lý Nội bộ dạng Desktop cho Quán Cà Phê**, được xây dựng bằng Java (với JavaFX cho giao diện người dùng), kết nối tới cơ sở dữ liệu MySQL và sử dụng thư viện JFreeChart để trực quan hóa dữ liệu.

Ứng dụng này nhằm mục đích **số hóa và hợp lý hóa các hoạt động quản lý hàng ngày** của quán, cung cấp các công cụ cho hai vai trò người dùng chính: **Quản lý (Admin)** và **Nhân viên (Staff)**.

**Các chức năng chính bao gồm:**

1.  **Xác thực và Phân quyền:**
    *   Hệ thống đăng nhập/đăng xuất an toàn (sử dụng mật khẩu băm).
    *   Phân quyền truy cập chức năng rõ ràng dựa trên vai trò (Admin/Staff).
2.  **Quản lý Dữ liệu Cốt lõi (CRUD):**
    *   **Quản lý Sản phẩm:** Cho phép xem, thêm, sửa, xóa các món đồ uống/thức ăn (Admin có toàn quyền, Staff có thể bị giới hạn quyền).
    *   **Quản lý Danh mục:** Tổ chức sản phẩm theo loại (Admin có toàn quyền, Staff chỉ xem).
    *   **Quản lý Đơn hàng:** Xem lịch sử đơn hàng, chi tiết đơn hàng (Admin xem toàn bộ, Staff xem giới hạn/đơn của mình, có thể có chức năng tạo đơn cho Staff).
    *   **Quản lý Người dùng (Chỉ Admin):** Admin có khả năng tạo, xem, sửa, và quản lý (vô hiệu hóa/kích hoạt) tài khoản cho nhân viên.
3.  **Theo dõi và Báo cáo (Dashboard):**
    *   Cung cấp một giao diện tổng quan (Dashboard) hiển thị các số liệu và biểu đồ thống kê (sử dụng JFreeChart).
    *   Giúp theo dõi hiệu suất kinh doanh (ví dụ: doanh thu, sản phẩm bán chạy). Admin có thể xem báo cáo chi tiết hơn Staff.
4.  **Quản lý Hồ sơ cá nhân:** Cho phép cả Admin và Staff xem và cập nhật thông tin cá nhân của họ, bao gồm thay đổi mật khẩu.

**Tóm lại, ứng dụng này phục vụ như một công cụ trung tâm giúp:**
*   **Nhân viên (Staff):** Thực hiện các tác vụ vận hành cơ bản (quản lý sản phẩm giới hạn, xử lý đơn hàng nếu có) và tự quản lý hồ sơ.
*   **Quản lý (Admin):** Giám sát toàn bộ hoạt động, quản lý dữ liệu cốt lõi (sản phẩm, danh mục), theo dõi hiệu suất kinh doanh qua báo cáo chi tiết, và quản lý tài khoản nhân viên.


## Phân Chia Chức Năng Cụ Thể:

**1. Tài khoản Quản lý (Admin):**

*   **Mục đích:** Quản lý toàn bộ hoạt động của quán trên hệ thống, bao gồm cả quản lý nhân viên và cấu hình cơ bản. Có quyền truy cập cao nhất.
*   **Chức năng cụ thể:**
    *   **Login / Logout:** Có thể đăng nhập và đăng xuất.
    *   **Xem Dashboard:** Xem *tất cả* các báo cáo thống kê (Doanh thu tổng, sản phẩm bán chạy nhất toàn thời gian, hiệu suất theo nhân viên (nếu có),...).
    *   **Quản lý Sản phẩm:** **Toàn quyền CRUD** (Xem danh sách, Thêm mới, Sửa thông tin chi tiết, Xóa sản phẩm).
    *   **Quản lý Danh mục:** **Toàn quyền CRUD** (Xem, Thêm, Sửa, Xóa danh mục sản phẩm).
    *   **Quản lý Đơn hàng:** Xem *tất cả* lịch sử đơn hàng, xem chi tiết đơn hàng, có thể có quyền cập nhật trạng thái đơn hàng (ví dụ: hủy đơn).
    *   **Quản lý Người dùng:** **Đây là quyền đặc trưng của Admin:**
        *   Xem danh sách *tất cả* người dùng (cả Admin khác và Staff).
        *   **Tạo tài khoản mới cho Nhân viên (Staff).**
        *   Sửa thông tin tài khoản của Nhân viên (ví dụ: cập nhật tên, email, reset mật khẩu).
        *   Vô hiệu hóa/Kích hoạt lại tài khoản Nhân viên.
        *   (Tùy chọn) Xóa tài khoản Nhân viên.
    *   **Xem/Sửa Hồ sơ cá nhân:** Xem và sửa thông tin cá nhân của chính mình (bao gồm đổi mật khẩu).

**2. Tài khoản Nhân viên (Staff):**

*   **Mục đích:** Thực hiện các tác vụ vận hành hàng ngày trên hệ thống, ghi nhận hoạt động bán hàng (nếu có chức năng tạo đơn), quản lý sản phẩm ở mức độ cơ bản. Quyền truy cập bị giới hạn.
*   **Chức năng cụ thể:**
    *   **Login / Logout:** Có thể đăng nhập và đăng xuất.
    *   **Xem Dashboard:** Xem các báo cáo cơ bản, liên quan đến hoạt động trong ngày hoặc cá nhân (Ví dụ: Doanh thu ca làm việc (nếu có), sản phẩm bán chạy trong ngày, các đơn hàng gần đây). *Một số biểu đồ chi tiết chỉ dành cho Admin.*
    *   **Quản lý Sản phẩm:**
        *   **Xem danh sách sản phẩm.**
        *   (Tùy chọn, nên cân nhắc) Có thể được phép **Sửa** một số thông tin giới hạn như *số lượng tồn kho* (nếu có quản lý kho) hoặc *giá* (nếu được phép).
        *   **Không được phép** Thêm sản phẩm mới hoặc Xóa sản phẩm.
    *   **Quản lý Danh mục:** Chỉ được **Xem** danh sách danh mục để biết sản phẩm thuộc loại nào. **Không** được Thêm/Sửa/Xóa.
    *   **Quản lý Đơn hàng:**
        *   (Nếu có chức năng POS) **Tạo đơn hàng mới.**
        *   Xem lịch sử các đơn hàng *do mình tạo* hoặc các đơn hàng *gần đây*.
        *   Có thể được phép cập nhật trạng thái đơn hàng *do mình phụ trách* (ví dụ: "Đang chuẩn bị", "Đã xong").
        *   **Không** được xem toàn bộ lịch sử đơn hàng của người khác (trừ khi có cấu hình khác). **Không** được xóa đơn hàng.
    *   **Quản lý Người dùng:** **Không có quyền này.** Không thể xem danh sách người dùng khác, không thể tạo/sửa/xóa tài khoản.
    *   **Xem/Sửa Hồ sơ cá nhân:** Chỉ xem và sửa thông tin cá nhân của chính mình (bao gồm đổi mật khẩu).



```
CoffeeShopApp/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/youruniversity/coffeeshop/
│   │   │       ├── MainApp.java              # (1) Lớp chính khởi chạy ứng dụng JavaFX
│   │   │       │
│   │   │       ├── controller/               # (2) Chứa các lớp Controller của JavaFX (liên kết với FXML)
│   │   │       │   ├── LoginController.java
│   │   │       │   ├── DashboardController.java
│   │   │       │   ├── ProductManagementController.java
│   │   │       │   ├── OrderManagementController.java
│   │   │       │   ├── CategoryManagementController.java
│   │   │       │   ├── UserProfileController.java
│   │   │       │   └── BaseController.java       # (Optional) Lớp cơ sở cho các controller (chứa logic chung)
│   │   │       │
│   │   │       ├── model/                    # (3) Chứa các lớp liên quan đến dữ liệu và logic nghiệp vụ (Model trong MVC)
│   │   │       │   ├── entity/               # (3a) Các lớp thực thể (POJO) ánh xạ bảng CSDL (OOP - Encapsulation)
│   │   │       │   │   ├── User.java
│   │   │       │   │   ├── Product.java
│   │   │       │   │   ├── Category.java
│   │   │       │   │   ├── Order.java
│   │   │       │   │   └── OrderDetail.java
│   │   │       │   │   └── Role.java          # (Optional) Enum hoặc class cho vai trò User
│   │   │       │   │
│   │   │       │   ├── dao/                  # (3b) Data Access Objects - Truy cập dữ liệu (OOP - Abstraction/Interface)
│   │   │       │   │   ├── impl/             # Chứa các lớp triển khai cụ thể cho DAO (kết nối MySQL)
│   │   │       │   │   │   ├── UserDaoImpl.java
│   │   │       │   │   │   ├── ProductDaoImpl.java
│   │   │       │   │   │   ├── CategoryDaoImpl.java
│   │   │       │   │   │   ├── OrderDaoImpl.java
│   │   │       │   │   │   └── OrderDetailDaoImpl.java
│   │   │       │   │   │
│   │   │       │   │   ├── IUserDAO.java     # Interface định nghĩa các phương thức CRUD cho User
│   │   │       │   │   ├── IProductDAO.java
│   │   │       │   │   ├── ICategoryDAO.java
│   │   │       │   │   ├── IOrderDAO.java
│   │   │       │   │   └── IOrderDetailDAO.java
│   │   │       │   │
│   │   │       │   └── service/              # (3c) Lớp dịch vụ - Xử lý logic nghiệp vụ phức tạp, điều phối DAO (OOP - Encapsulation)
│   │   │       │       ├── impl/             # Chứa các lớp triển khai cụ thể cho Service
│   │   │       │       │   ├── AuthService.java      # Xử lý đăng nhập, đăng xuất, quản lý session
│   │   │       │       │   ├── ProductService.java   # Logic liên quan đến sản phẩm (validation, tính toán...)
│   │   │       │       │   ├── OrderService.java     # Logic tạo/quản lý đơn hàng, tính tổng tiền
│   │   │       │       │   ├── CategoryService.java
│   │   │       │       │   └── ReportService.java    # Logic chuẩn bị dữ liệu cho biểu đồ (JFreeChart)
│   │   │       │       │
│   │   │       │       ├── IAuthService.java     # Interface cho dịch vụ xác thực
│   │   │       │       ├── IProductService.java
│   │   │       │       ├── IOrderService.java
│   │   │       │       ├── ICategoryService.java
│   │   │       │       └── IReportService.java
│   │   │       │
│   │   │       ├── util/                     # (4) Các lớp tiện ích dùng chung
│   │   │       │   ├── DatabaseConnection.java # Quản lý kết nối đến MySQL (Connection Pool)
│   │   │       │   ├── PasswordUtils.java      # Tiện ích mã hóa/kiểm tra mật khẩu (Thuật toán Hashing - BCrypt)
│   │   │       │   ├── Constants.java          # Chứa các hằng số (ví dụ: vai trò người dùng, tên session...)
│   │   │       │   ├── ValidatorUtils.java     # Tiện ích kiểm tra dữ liệu đầu vào
│   │   │       │   ├── DateUtils.java          # Tiện ích xử lý ngày tháng
│   │   │       │   └── SessionManager.java     # Quản lý thông tin người dùng đang đăng nhập (Data Structure - HashMap)
│   │   │       │   └── ChartUtils.java         # Tiện ích tạo và hiển thị JFreeChart trong JavaFX
│   │   │       │
│   │   │       ├── exception/                # (5) Các lớp Exception tùy chỉnh
│   │   │       │   ├── AuthenticationException.java
│   │   │       │   ├── DatabaseException.java
│   │   │       │   └── ValidationException.java
│   │   │       │
│   │   │       └── view/                     # (6) Có thể chứa các thành phần UI tùy chỉnh (không phải FXML) hoặc View Helper
│   │   │           └── component/            # Ví dụ: Một TableView tùy chỉnh
│   │   │
│   │   └── resources/                # (7) Chứa các tài nguyên không phải code
│   │       ├── fxml/                 # (7a) Các file FXML thiết kế bằng Scene Builder
│   │       │   ├── LoginView.fxml
│   │       │   ├── DashboardView.fxml
│   │       │   ├── ProductManagementView.fxml
│   │       │   ├── OrderManagementView.fxml
│   │       │   ├── CategoryManagementView.fxml
│   │       │   ├── UserProfileView.fxml
│   │       │   └── MainView.fxml       # (Optional) Khung chính chứa các view con
│   │       │
│   │       ├── css/                  # (7b) Các file CSS để tạo kiểu cho giao diện
│   │       │   └── styles.css
│   │       │
│   │       ├── images/               # (7c) Hình ảnh, icons
│   │       │   └── logo.png
│   │       │
│   │       ├── config/               # (7d) File cấu hình
│   │       │   └── db.properties     # Chứa thông tin kết nối CSDL (url, user, password) -> Tránh hardcode
│   │       │
│   │       └── sql/                  # (7e) Các script SQL
│   │           ├── schema.sql        # Script tạo cấu trúc bảng CSDL
│   │           └── data.sql          # (Optional) Script chèn dữ liệu mẫu ban đầu
│   │
│   └── test/
│       └── java/                     # (8) Chứa code Unit Test (JUnit) - Rất khuyến khích
│           └── com/youruniversity/coffeeshop/
│               ├── service/
│               │   └── AuthServiceTest.java
│               └── dao/
│                   └── UserDaoTest.java # (Cần mocking hoặc test db)
│
├── lib/                            # (9) Chứa các thư viện ngoài (JAR files) nếu không dùng Maven/Gradle
│   ├── mysql-connector-j-x.x.x.jar
│   ├── jfreechart-x.x.x.jar
│   └── jcommon-x.x.x.jar           # Thư viện phụ thuộc của JFreeChart
│   └── bcrypt-x.x.x.jar            # Thư viện mã hóa mật khẩu (ví dụ: jBCrypt)
│
├── pom.xml                         # (10) Hoặc build.gradle - Nếu dùng Maven/Gradle để quản lý thư viện
│
└── README.md                       # (11) Hướng dẫn cài đặt, chạy dự án, mô tả cấu trúc...
```

**Giải thích chi tiết các thành phần:**

1.  **`MainApp.java`**:
    *   **Tính năng:** Điểm khởi đầu của ứng dụng. Kế thừa `javafx.application.Application`. Load FXML chính (ví dụ: `LoginView.fxml` hoặc `MainView.fxml`), thiết lập `Stage` (cửa sổ chính).
    *   **Logic:** Thiết lập cửa sổ ban đầu, gọi view đầu tiên.

2.  **`controller` package**:
    *   **Tính năng:** Các lớp này là "chất keo" giữa View (FXML) và Model (Service/DAO). Mỗi file FXML chính sẽ có một Controller tương ứng được khai báo trong FXML (`fx:controller="..."`).
    *   **Logic:** Chứa các phương thức xử lý sự kiện từ UI (nhấn nút, chọn item...), lấy dữ liệu từ các trường nhập liệu, gọi các `Service` để thực hiện nghiệp vụ, và cập nhật lại UI dựa trên kết quả trả về. Ví dụ: `LoginController` xử lý nút "Đăng nhập", gọi `AuthService`, chuyển màn hình nếu thành công. `ProductManagementController` hiển thị danh sách sản phẩm lấy từ `ProductService`, xử lý thêm/sửa/xóa sản phẩm.
    *   **Scene Builder:** Các `@FXML` annotation trong Controller sẽ liên kết với các thành phần UI (Button, TextField, TableView...) đã đặt `fx:id` trong Scene Builder.
    *   **OOP:** Có thể có lớp `BaseController` để chứa các phương thức chung (như hiển thị thông báo lỗi, chuyển màn hình) áp dụng **Inheritance**.

3.  **`model` package**: Đây là trái tim của ứng dụng, tuân thủ chặt chẽ nguyên tắc **Separation of Concerns** (Tách biệt các mối quan tâm).
    *   **`entity` (3a):**
        *   **Tính năng:** Định nghĩa cấu trúc dữ liệu. Mỗi lớp tương ứng với một bảng trong CSDL MySQL.
        *   **Logic:** Chỉ chứa các thuộc tính (private) và phương thức getters/setters (public) - ví dụ `Product` có `id`, `name`, `price`, `categoryId`, `description`... Đây là nơi áp dụng **Encapsulation** của OOP.
        *   **Data Structures:** Bản thân các lớp này là cấu trúc dữ liệu tùy chỉnh.
    *   **`dao` (3b):** Data Access Object
        *   **Tính năng:** Trừu tượng hóa việc truy cập CSDL. Cung cấp các phương thức CRUD (Create, Read, Update, Delete) và các phương thức truy vấn cụ thể cho từng `entity`.
        *   **Logic:** Chứa code JDBC (hoặc JPA/Hibernate nếu dùng) để thực thi các câu lệnh SQL tương tác với MySQL. Sử dụng `DatabaseConnection` để lấy kết nối. Các phương thức thường nhận/trả về các đối tượng `entity`.
        *   **OOP:** Sử dụng **Interfaces** (`IUserDAO`, `IProductDAO`...) để định nghĩa "hợp đồng" và lớp `impl` để triển khai cụ thể. Điều này giúp dễ dàng thay đổi cách triển khai (ví dụ: chuyển sang CSDL khác) mà không ảnh hưởng nhiều đến phần còn lại của ứng dụng (Polymorphism, Loose Coupling).
        *   **Data Structures:** Thường trả về `List<Entity>` (ví dụ `ArrayList<Product>`) khi lấy nhiều bản ghi, hoặc `Optional<Entity>` khi lấy một bản ghi để xử lý trường hợp không tìm thấy.
    *   **`service` (3c):**
        *   **Tính năng:** Thực hiện các quy tắc và logic nghiệp vụ (business logic). Điều phối hoạt động của các DAO.
        *   **Logic:** Ví dụ: `AuthService.login(username, password)` sẽ gọi `UserDao.findByUsername()`, sau đó dùng `PasswordUtils.checkPassword()` để xác thực, và nếu thành công thì tạo session trong `SessionManager`. `OrderService.createOrder(Order, List<OrderDetail>)` sẽ gọi `OrderDao.save(Order)`, sau đó lặp qua `List<OrderDetail>` để gọi `OrderDetailDao.save()`, có thể cần cập nhật tồn kho sản phẩm (gọi `ProductDao.updateStock`). `ReportService.getRevenueByMonth()` sẽ gọi các phương thức DAO phù hợp để lấy dữ liệu thô từ CSDL, sau đó xử lý/tổng hợp dữ liệu này thành định dạng phù hợp cho JFreeChart.
        *   **OOP:** Cũng nên dùng **Interfaces** và **Implementations** như DAO. Đảm bảo **Encapsulation** logic nghiệp vụ.
        *   **Algorithms/Data Structures:** Nơi áp dụng các thuật toán phức tạp hơn (nếu cần), xử lý dữ liệu bằng `ArrayList`, `HashMap`, `TreeMap` (ví dụ: tạo thống kê, sắp xếp dữ liệu trước khi trả về Controller).

4.  **`util` package**:
    *   **Tính năng:** Chứa các lớp tiện ích dùng chung, không thuộc về một nghiệp vụ cụ thể nào.
    *   **Logic:** `DatabaseConnection` quản lý singleton hoặc pool kết nối MySQL (đọc cấu hình từ `db.properties`). `PasswordUtils` dùng thư viện như jBCrypt để hash (lưu vào DB) và verify mật khẩu (khi đăng nhập) - **Thuật toán Hashing**. `SessionManager` dùng `HashMap<String, User>` để lưu trữ thông tin người dùng đang đăng nhập (Key là session token hoặc đơn giản là username nếu chỉ cho đăng nhập 1 nơi). `ChartUtils` chứa code để tạo các đối tượng `JFreeChart` (BarChart, PieChart...) từ dữ liệu được cung cấp bởi `ReportService` và nhúng chúng vào các container của JavaFX (ví dụ: `SwingNode`).

5.  **`exception` package**:
    *   **Tính năng:** Định nghĩa các loại lỗi nghiệp vụ hoặc kỹ thuật cụ thể, giúp việc bắt và xử lý lỗi rõ ràng hơn.
    *   **OOP:** Sử dụng **Inheritance** từ `Exception` hoặc `RuntimeException`.

6.  **`view` package**:
    *   **Tính năng:** (Ít quan trọng hơn khi dùng FXML) Có thể chứa các thành phần giao diện JavaFX tùy chỉnh được viết bằng code Java thuần túy (nếu cần) hoặc các lớp hỗ trợ cho View.

7.  **`resources` package**:
    *   **Tính năng:** Chứa tất cả các file không phải là mã nguồn Java.
    *   **Logic:** `fxml` chứa file định nghĩa giao diện (tạo bằng Scene Builder). `css` để tùy chỉnh giao diện. `images` chứa tài nguyên đồ họa. `config` chứa file cấu hình (`db.properties` giúp dễ thay đổi thông tin CSDL mà không cần biên dịch lại code). `sql` chứa script để người khác dễ dàng tạo lại CSDL.

8.  **`test` package**:
    *   **Tính năng:** Chứa mã kiểm thử đơn vị (Unit Tests) dùng các framework như JUnit.
    *   **Logic:** Viết test cho các lớp `Service` (quan trọng nhất), `DAO` (có thể cần mocking hoặc DB test riêng), `Util`. Giúp đảm bảo code hoạt động đúng và dễ dàng phát hiện lỗi khi thay đổi code (Regression Testing).

9.  **`lib` package**:
    *   **Tính năng:** Chứa các file thư viện `.jar` cần thiết nếu bạn không sử dụng công cụ quản lý phụ thuộc như Maven hoặc Gradle. Bạn cần thêm các JAR này vào Build Path của project trong Eclipse.

10. **`pom.xml` / `build.gradle`**:
    *   **Tính năng:** File cấu hình cho Maven/Gradle. Khai báo các thư viện phụ thuộc (JavaFX, MySQL Connector, JFreeChart, jBCrypt...), công cụ build sẽ tự động tải về và quản lý chúng. **Rất khuyến khích sử dụng** thay vì quản lý thủ công trong `lib`.

11. **`README.md`**:
    *   **Tính năng:** File văn bản dạng Markdown cung cấp thông tin tổng quan về dự án, hướng dẫn cách cài đặt môi trường, cách build và chạy ứng dụng, mô tả cấu trúc thư mục, các công nghệ sử dụng... Rất quan trọng cho việc cộng tác và bàn giao.

**Lợi ích của cấu trúc này:**

*   **Xịn xò & Mạnh mẽ:** Dựa trên mẫu MVC và các best practices, phân tách rõ ràng các lớp trách nhiệm.
*   **Logic & Dễ hiểu:** Các package được đặt tên rõ ràng theo chức năng. Dễ dàng tìm thấy code liên quan đến một tính năng cụ thể.
*   **Chặt chẽ:** Các tầng (Controller, Service, DAO) tương tác với nhau qua Interfaces, giảm sự phụ thuộc cứng (Loose Coupling).
*   **Dễ xây dựng:** Bắt đầu từ `entity`, `dao`, rồi đến `service`, `controller`, và cuối cùng là `view` (FXML).
*   **Dễ fix & Bảo trì:** Khi có lỗi hoặc cần thay đổi, dễ khoanh vùng vị trí cần sửa (ví dụ: lỗi hiển thị -> `Controller`/`FXML`, lỗi nghiệp vụ -> `Service`, lỗi CSDL -> `DAO`).
*   **Đáp ứng yêu cầu:** Tích hợp rõ ràng JavaFX (Controller, FXML), MySQL (DAO, Util), JFreeChart (Util, Service, Controller), OOP (Entity, Interface/Impl, Inheritance), Data Structures (Util, Service), Algorithms (Util - Hashing, Service/Controller - Sort/Search).
*   **Tích hợp Scene Builder:** Hoàn toàn tương thích, FXML nằm riêng trong `resources`, Controller liên kết qua `fx:controller` và `@FXML`.

# PHÂN CHIA TASK (PHÚC - DANH)

**Dưới đây là gợi ý phân chia task chi tiết, logic và an toàn, tập trung vào việc giảm thiểu xung đột (merge conflicts) và đảm bảo cả hai đều nắm được các phần quan trọng của ứng dụng:**

**Nguyên tắc chung:**

*   **Interfaces là hợp đồng:** Hoàn thành sớm các Interfaces (IDAO, IService) để cả hai có thể code song song.
*   **Backend đi trước (logic):** Phúc tập trung xây dựng logic nghiệp vụ (Service) và truy cập dữ liệu (DAO).
*   **Frontend theo sau (giao diện):** Danh tập trung xây dựng giao diện (FXML), Controller và liên kết với Backend qua Interfaces.
*   **Phân quyền xuyên suốt:** Việc kiểm tra vai trò (`ADMIN`/`STAFF`) cần được tích hợp vào các Controller để điều khiển UI và luồng xử lý.
*   **GitHub Flow:** Nhánh `main` ổn định, `develop` tích hợp, mỗi task/feature lớn làm trên nhánh riêng (`feature/ten-task`), tạo Pull Request (PR) vào `develop`, review code chéo trước khi merge. Commit nhỏ, thường xuyên.

---

**Phân chia Task Chi Tiết:**

**Giai đoạn 1: Khởi tạo & Nền tảng Vững Chắc (Cả hai phối hợp chặt chẽ)**

1.  **Phúc & Danh (Phối hợp, Review chéo):**
    *   **Task 1.1:** Thiết lập GitHub Repository, cấu trúc project Eclipse, file `.gitignore`, thêm thư viện (JARs hoặc Maven/Gradle).
    *   **Task 1.2 (Phúc làm chính, Danh review):** Thiết kế `schema.sql` bao gồm bảng `users` với cột `role ENUM('ADMIN', 'STAFF') NOT NULL`, các bảng `categories`, `products`, `orders`, `order_details` với đầy đủ khóa, ràng buộc.
    *   **Task 1.3 (Phúc làm chính, Danh review):** Tạo các lớp `Entity` (`User.java` có thuộc tính `Role role` và `enum Role { ADMIN, STAFF }`, `Category.java`, `Product.java`, `Order.java`, `OrderDetail.java`).
    *   **Task 1.4 (Danh làm chính, Phúc review):** Tạo lớp `PasswordUtils.java` (BCrypt hash & verify).
    *   **Task 1.5 (Phúc làm chính, Danh review):** Tạo `db.properties` và lớp `DatabaseConnection.java`.
    *   **Task 1.6 (Phúc làm chính, Danh review):** Tạo script `data.sql` để chèn sẵn ít nhất 1 tài khoản **Admin** (với mật khẩu đã hash và `role='ADMIN'`).

    *Output Giai đoạn 1:* Project chuẩn, kết nối DB, có Entities (bao gồm Role), Utils cơ bản, tài khoản Admin ban đầu. Sẵn sàng cho các tầng logic.

**Giai đoạn 2: Xây dựng Interfaces & Khung sườn Backend/Frontend**

2.  **Phúc (Định nghĩa Backend Contracts & DAO cơ bản):**
    *   **Task 2.1:** Định nghĩa **đầy đủ** các Interfaces: `IUserDAO`, `ICategoryDAO`, `IProductDAO`, `IOrderDAO`, `IOrderDetailDAO`. Xác định rõ các phương thức cần thiết (CRUD cơ bản, `findByUsername`, `findAll`, `findById`, các hàm tìm kiếm/lọc nếu dự định).
    *   **Task 2.2:** Định nghĩa **đầy đủ** các Interfaces: `IAuthService`, `IUserService` (thêm các hàm quản lý user như `createUser`, `findAllUsers`, `updateUserStatus`), `ICategoryService`, `IProductService`, `IOrderService` (thêm `createOrder`), `IReportService`.
    *   **Task 2.3:** Triển khai các lớp `...Impl` cho **DAO** với các phương thức cơ bản nhất (`findById`, `findAll` nếu có) để Danh có thể bắt đầu test gọi Service.

3.  **Danh (Xây dựng Khung Frontend & Utils liên quan):**
    *   **Task 2.4:** Tạo `MainApp.java` khởi chạy JavaFX.
    *   **Task 2.5:** Thiết kế và tạo FXML **khung sườn** cho các màn hình chính: `LoginView.fxml`, `MainView.fxml` (hoặc `DashboardView.fxml` làm khung chính, có thể chứa MenuBar/Sidebar).
    *   **Task 2.6:** Tạo `SessionManager.java` (lưu `User` object sau khi login, có `getCurrentUser()`, `logout()`).
    *   **Task 2.7:** Tạo `Constants.java` (chứa hằng số, ví dụ tên vai trò).
    *   **Task 2.8:** Tạo `styles.css` cơ bản.

    *Output Giai đoạn 2:* Có "hợp đồng" Interfaces rõ ràng. Có các DAO skeleton. Có khung UI ban đầu và Session Manager. Giảm thiểu xung đột khi làm song song giai đoạn sau.

**Giai đoạn 3: Triển khai Tính năng Login & Quản lý Cơ bản (Phân quyền bắt đầu)**

4.  **Phúc (Backend Logic cho Login, User, Category, Product):**
    *   **Task 3.1:** Hoàn thiện **`UserDaoImpl.java`** (bao gồm `findByUsername`, `save` - hash pass, `update` - cho profile và quản lý user, `findAll`).
    *   **Task 3.2:** Triển khai **`AuthService.java`** (logic `login` - kiểm tra pass, lưu `User` vào `SessionManager`, `logout` - xóa session).
    *   **Task 3.3:** Hoàn thiện **`CategoryDaoImpl.java`** và **`ProductDaoImpl.java`** (đầy đủ CRUD).
    *   **Task 3.4:** Triển khai **`CategoryService.java`** và **`ProductService.java`** (logic nghiệp vụ cơ bản, gọi DAO).
    *   **Task 3.5:** Triển khai các phương thức cơ bản trong **`UserService.java`** (ví dụ: `findUserById`, `updateProfile`, *chưa cần* các hàm quản lý user phức tạp).

5.  **Danh (Frontend & Controller cho Login, Category, Product):**
    *   **Task 3.6:** Hoàn thiện `LoginView.fxml` (thêm `fx:id`).
    *   **Task 3.7:** Triển khai **`LoginController.java`** (gọi `AuthService.login()`, xử lý kết quả, lưu session, điều hướng tới `MainView`/`DashboardView`).
    *   **Task 3.8:** Hoàn thiện FXML `CategoryManagementView.fxml` và `ProductManagementView.fxml`.
    *   **Task 3.9:** Triển khai **`CategoryManagementController.java`** và **`ProductManagementController.java`**.
        *   Gọi Service tương ứng để lấy và hiển thị dữ liệu (`ObservableList` -> `TableView`).
        *   Xử lý sự kiện nút Add/Edit/Delete.
        *   **Quan trọng:** Bắt đầu **kiểm tra vai trò** (`SessionManager.getInstance().getCurrentUser().getRole()`) để **ẩn/hiện/vô hiệu hóa** các nút/chức năng chỉ dành cho Admin (ví dụ: nút Xóa Product, nút Thêm/Sửa/Xóa Category).

    *Output Giai đoạn 3:* Login hoạt động. Quản lý Category, Product hoạt động với phân quyền cơ bản trên UI. Nền tảng vững chắc cho các tính năng phức tạp hơn.

**Giai đoạn 4: Triển khai Tính năng Nâng cao (Orders, User Mgmt, Dashboard)**

6.  **Phúc (Backend Logic cho Orders, User Mgmt, Reports):**
    *   **Task 4.1:** Hoàn thiện **`OrderDaoImpl.java`** và **`OrderDetailDaoImpl.java`** (CRUD, các hàm tìm kiếm).
    *   **Task 4.2:** Triển khai **`OrderService.java`** (logic `createOrder` - **quan trọng: xử lý transaction**, lấy danh sách đơn hàng...).
    *   **Task 4.3:** Hoàn thiện **`UserService.java`** (thêm các phương thức **quản lý user**: `createUser`, `updateUserStatus`, `findAllUsers`...).
    *   **Task 4.4:** Triển khai **`ReportService.java`** (logic truy vấn, tổng hợp dữ liệu cho các biểu đồ). Cần xác định rõ dữ liệu trả về cho Danh.

7.  **Danh (Frontend & Controller cho Orders, User Mgmt, Dashboard, Profile):**
    *   **Task 4.5:** Tạo FXML và Controller cho **Tạo Đơn Hàng** (`CreateOrderView.fxml`, `CreateOrderController.java`) - Dành cho cả Staff và Admin. Gọi `OrderService.createOrder`.
    *   **Task 4.6:** Hoàn thiện FXML và Controller cho **Quản lý Đơn Hàng** (`OrderManagementView.fxml`, `OrderManagementController.java`). Hiển thị danh sách đơn hàng (có thể lọc khác nhau cho Admin/Staff).
    *   **Task 4.7:** Tạo FXML và Controller cho **Quản lý Người Dùng** (`UserManagementView.fxml`, `UserManagementController.java`) - **Chỉ Admin mới truy cập/nhìn thấy được View này.** Gọi các phương thức quản lý user của `UserService`.
    *   **Task 4.8:** Tạo `ChartUtils.java` để tạo `JFreeChart` và nhúng vào JavaFX.
    *   **Task 4.9:** Hoàn thiện FXML và Controller cho **Dashboard** (`DashboardView.fxml`, `DashboardController.java`). Gọi `ReportService`, dùng `ChartUtils` để hiển thị biểu đồ. **Kiểm tra vai trò để hiển thị biểu đồ phù hợp.**
    *   **Task 4.10:** Tạo FXML và Controller cho **Hồ sơ cá nhân** (`UserProfileView.fxml`, `UserProfileController.java`). Gọi `UserService` để lấy và cập nhật thông tin.

    *Output Giai đoạn 4:* Tất cả các chức năng chính (bao gồm tạo đơn hàng, quản lý user, dashboard có biểu đồ) hoạt động với phân quyền đầy đủ.

**Giai đoạn 5: Hoàn thiện, Kiểm thử, Đóng gói & Tài liệu (Cả hai cùng làm)**

8.  **Phúc & Danh (Phối hợp chặt chẽ):**
    *   **Task 5.1:** **Kiểm thử chức năng chéo & toàn diện:** Test tất cả các luồng, các vai trò, các trường hợp biên. Ghi nhận và sửa lỗi (bug fixing).
    *   **Task 5.2:** **Code Review:** Đọc và góp ý code của nhau (logic, convention, tối ưu).
    *   **Task 5.3:** **Refactoring:** Cải thiện code nếu cần.
    *   **Task 5.4:** **Thêm tính năng phụ (Nếu còn thời gian):** Tìm kiếm/lọc nâng cao, phân trang, xuất dữ liệu... (Chia nhau làm).
    *   **Task 5.5:** **Hoàn thiện Tài liệu:**
        *   Viết `README.md` chi tiết (bao gồm mô tả mục đích, chức năng theo vai trò, hướng dẫn cài đặt/chạy).
        *   Viết Báo cáo Word đầy đủ theo yêu cầu (chia nhau viết các mục, review chung). Kiểm tra Turnitin.
        *   Vẽ UML Diagrams (ERD, Class Diagram chính).
        *   Chuẩn bị file PPT trình bày.
    *   **Task 5.6:** **Quay Video Demo:** Chuẩn bị kịch bản, cả hai cùng trình bày rõ ràng các chức năng và vai trò.
    *   **Task 5.7:** **Đóng gói:** Dọn dẹp code, đảm bảo chạy ổn định, tạo file nén cuối cùng.

---

**Lưu ý khi thực hiện:**

*   **Giao tiếp liên tục:** Họp nhanh hàng ngày/cách ngày để đồng bộ.
*   **Pull Request (PR) là bắt buộc:** Review code trước khi merge vào `develop`.
*   **Giải quyết Conflict cùng nhau:** Nếu xảy ra conflict, cả hai cùng ngồi lại xử lý.
*   **Ưu tiên Core Features:** Hoàn thành các yêu cầu chính trong Rubrics trước khi làm thêm tính năng phụ.

Bảng phân công này chi tiết hơn, tích hợp đầy đủ các yêu cầu mới và được thiết kế để Phúc và Danh có thể làm việc song song hiệu quả hơn trên GitHub. Chúc hai bạn thành công!

