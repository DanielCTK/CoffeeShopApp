# CoffeeShopApp

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

**Dưới đây là gợi ý phân chia task chi tiết, logic và an toàn, tập trung vào việc giảm thiểu xung đột (merge conflicts) và đảm bảo cả hai bạn đều nắm được các phần quan trọng của ứng dụng:**

**Nguyên tắc chung:**

*   **Ưu tiên nền tảng:** Xây dựng các thành phần cốt lõi, ít thay đổi trước (Database, Entities, Utils).
*   **Phân theo Layer/Module:** Một người tập trung hơn vào Backend (Data Access, Business Logic), người kia tập trung hơn vào Frontend (UI, Controller) nhưng cả hai cần hiểu sự kết nối.
*   **Giao tiếp qua Interfaces:** Định nghĩa các Interfaces (IDAO, IService) sớm để cả hai có thể làm việc song song dựa trên "hợp đồng" đã thống nhất.
*   **GitHub Flow:** Sử dụng `main` (hoặc `master`) là nhánh ổn định. Nhánh `develop` là nhánh tích hợp chính. Mỗi tính năng/task lớn nên làm trên một nhánh riêng (feature branch) rồi tạo Pull Request (PR) vào `develop`. Review code của nhau trước khi merge.
*   **Thường xuyên Commit & Push:** Commit nhỏ, thường xuyên với message rõ ràng. Push lên nhánh feature của mình và Pull từ `develop` về thường xuyên để giảm thiểu conflict lớn.

**Phân chia Task chi tiết:**

**Giai đoạn 1: Khởi tạo & Nền tảng (Cả hai cùng làm hoặc phân công rõ)**

1.  **Phúc (Lead) & Danh (Support/Review):**
    *   **Task 1.1:** Tạo GitHub Repository (private), mời Danh làm collaborator.
    *   **Task 1.2:** Thiết lập cấu trúc project chuẩn trong Eclipse (theo cấu trúc đã thống nhất).
    *   **Task 1.3:** Cấu hình file `.gitignore` chuẩn cho Java/Eclipse/Maven(nếu dùng).
    *   **Task 1.4:** Thêm các thư viện cần thiết vào `lib` (hoặc cấu hình `pom.xml`/`build.gradle` nếu dùng Maven/Gradle) - MySQL Connector, JFreeChart + JCommon, BCrypt.
    *   **Task 1.5:** Tạo file `db.properties` và lớp `DatabaseConnection.java` (quản lý kết nối DB). *(Phúc làm chính, Danh review)*
    *   **Task 1.6:** Thiết kế và viết script `schema.sql` (tạo các bảng: `users`, `categories`, `products`, `orders`, `order_details` - đảm bảo có đủ khóa chính, khóa ngoại, ràng buộc). *(Phúc làm chính, Danh review)*
    *   **Task 1.7:** Tạo lớp `PasswordUtils.java` (sử dụng BCrypt để hash và verify). *(Danh làm chính, Phúc review)*
    *   **Task 1.8:** Tạo các lớp `Entity` cơ bản (POJOs: `User.java`, `Category.java`, `Product.java`, `Order.java`, `OrderDetail.java`) chỉ với thuộc tính và getter/setter. *(Phúc làm chính, Danh review)*

    *Output Giai đoạn 1:* Project có cấu trúc chuẩn, kết nối được DB, có Entities cơ bản, sẵn sàng cho các tầng tiếp theo. Cả hai cần clone repo về và đảm bảo môi trường chạy giống nhau.

**Giai đoạn 2: Xây dựng Tầng Data Access (DAO) & Service Interfaces**

2.  **Phúc (Lead - DAO & Service Interfaces):**
    *   **Task 2.1:** Định nghĩa các Interfaces cho DAO: `IUserDAO.java`, `ICategoryDAO.java`, `IProductDAO.java`, `IOrderDAO.java`, `IOrderDetailDAO.java`. Xác định các phương thức CRUD cơ bản và các phương thức truy vấn đặc thù (ví dụ: `findByUsername`, `findAllByCategoryId`, `findOrdersByUserId`...).
    *   **Task 2.2:** Triển khai các lớp DAO cơ bản (`UserDaoImpl.java`, `CategoryDaoImpl.java`,...) với các phương thức `findById`, `findAll`. *(Phúc làm chính)*
    *   **Task 2.3:** Định nghĩa các Interfaces cho Service: `IAuthService.java`, `ICategoryService.java`, `IProductService.java`, `IOrderService.java`, `IReportService.java`. Xác định các phương thức nghiệp vụ chính. *(Phúc làm chính, Danh cần xem để hiểu cách gọi từ Controller)*

3.  **Danh (Lead - Setup UI cơ bản & Utils hỗ trợ):**
    *   **Task 2.4:** Tạo file `MainApp.java` để khởi chạy ứng dụng JavaFX.
    *   **Task 2.5:** Thiết kế (dùng Scene Builder) và tạo file FXML cơ bản cho màn hình Login (`LoginView.fxml`) và Khung chính/Dashboard (`MainView.fxml` hoặc `DashboardView.fxml`) với các layout chính, menu (nếu có).
    *   **Task 2.6:** Tạo lớp `SessionManager.java` để quản lý thông tin người dùng đăng nhập (có thể dùng `HashMap`).
    *   **Task 2.7:** (Optional) Tạo `BaseController.java` nếu muốn có các hàm tiện ích chung cho Controller.
    *   **Task 2.8:** Tạo file `styles.css` cơ bản.

    *Output Giai đoạn 2:* Có Interfaces cho DAO, Service. Có các DAO cơ bản. Có khung sườn UI ban đầu. Phúc và Danh có thể bắt đầu làm việc song song nhiều hơn dựa trên các Interfaces đã định nghĩa.

**Giai đoạn 3: Triển khai Tính năng cốt lõi (Login, Quản lý cơ bản)**

4.  **Phúc (Lead - Backend Logic):**
    *   **Task 3.1:** Hoàn thiện `UserDaoImpl.java` (thêm `findByUsername`, `save` - nhớ hash password, `update`...).
    *   **Task 3.2:** Triển khai `AuthService.java` (logic `login`, `logout`, gọi `UserDao`, `PasswordUtils`, `SessionManager`).
    *   **Task 3.3:** Hoàn thiện `CategoryDaoImpl.java`, `ProductDaoImpl.java` (đầy đủ CRUD).
    *   **Task 3.4:** Triển khai `CategoryService.java`, `ProductService.java` (logic nghiệp vụ cơ bản, gọi DAO tương ứng, validation đơn giản).

5.  **Danh (Lead - Frontend & Controller):**
    *   **Task 3.5:** Hoàn thiện `LoginView.fxml` (thêm `fx:id` cho các control).
    *   **Task 3.6:** Tạo và triển khai `LoginController.java` (liên kết FXML, xử lý sự kiện nút Login, gọi `AuthService.login()`, xử lý kết quả, chuyển màn hình nếu thành công, sử dụng `SessionManager`).
    *   **Task 3.7:** Hoàn thiện FXML cho Quản lý Danh mục (`CategoryManagementView.fxml`) và Sản phẩm (`ProductManagementView.fxml`) - Bảng hiển thị, các nút chức năng, form nhập liệu.
    *   **Task 3.8:** Tạo và triển khai `CategoryManagementController.java` và `ProductManagementController.java` (hiển thị danh sách từ Service, xử lý các nút Add/Edit/Delete, gọi các phương thức CRUD của Service tương ứng, cập nhật UI). *(Phần này cần Danh gọi các Service do Phúc viết)*

    *Output Giai đoạn 3:* Chức năng Đăng nhập hoạt động. Chức năng quản lý (CRUD) cho Danh mục và Sản phẩm hoạt động cơ bản. Cần tích hợp và kiểm thử kỹ luồng Login -> Quản lý.

**Giai đoạn 4: Hoàn thiện Tính năng (Orders, Dashboard, Profile) & Refine**

6.  **Phúc (Lead - Backend Orders & Reports):**
    *   **Task 4.1:** Hoàn thiện `OrderDaoImpl.java`, `OrderDetailDaoImpl.java` (CRUD, các hàm lấy đơn hàng theo điều kiện).
    *   **Task 4.2:** Triển khai `OrderService.java` (logic tạo đơn hàng - cần xử lý transaction nếu có thể, lấy danh sách đơn hàng...).
    *   **Task 4.3:** Triển khai `ReportService.java` (logic truy vấn, tổng hợp dữ liệu cho các biểu đồ - ví dụ: doanh thu theo ngày/tháng, sản phẩm bán chạy...). *(Cần cung cấp dữ liệu rõ ràng cho Danh)*
    *   **Task 4.4:** Hoàn thiện logic cập nhật Profile trong `UserService` / `AuthService` và `UserDao`.

7.  **Danh (Lead - Frontend Orders, Dashboard, Profile & Charts):**
    *   **Task 4.5:** Hoàn thiện FXML cho Quản lý Đơn hàng (`OrderManagementView.fxml`) và chi tiết đơn hàng.
    *   **Task 4.6:** Triển khai `OrderManagementController.java` (hiển thị danh sách đơn hàng, xem chi tiết, có thể thêm chức năng cập nhật trạng thái đơn hàng - gọi `OrderService`).
    *   **Task 4.7:** Tạo lớp `ChartUtils.java` (chứa các hàm tạo `JFreeChart` từ dữ liệu đầu vào và cách nhúng vào JavaFX - ví dụ dùng `SwingNode`).
    *   **Task 4.8:** Hoàn thiện FXML cho Dashboard (`DashboardView.fxml`), thêm các vùng để hiển thị biểu đồ.
    *   **Task 4.9:** Triển khai `DashboardController.java` (gọi `ReportService` để lấy dữ liệu, dùng `ChartUtils` để tạo và hiển thị các biểu đồ). *(Cần dữ liệu từ Phúc)*
    *   **Task 4.10:** Tạo FXML (`UserProfileView.fxml`) và Controller (`UserProfileController.java`) cho chức năng xem/sửa hồ sơ cá nhân (gọi Service tương ứng).

    *Output Giai đoạn 4:* Các chức năng chính hoàn thiện. Dashboard có biểu đồ. Có thể quản lý đơn hàng, hồ sơ. Cần test tích hợp toàn diện.

**Giai đoạn 5: Hoàn thiện, Kiểm thử, Đóng gói & Tài liệu (Cả hai cùng làm)**

8.  **Phúc & Danh:**
    *   **Task 5.1:** **Kiểm thử chéo:** Phúc test các chức năng Danh làm và ngược lại. Ghi nhận và sửa lỗi.
    *   **Task 5.2:** **Review Code:** Đọc lại code của nhau, góp ý về logic, performance, convention.
    *   **Task 5.3:** **Refactor & Tối ưu:** Cải thiện những đoạn code chưa tốt, tối ưu truy vấn DB nếu cần.
    *   **Task 5.4:** **Thêm tính năng phụ (Nếu có thời gian):** Tìm kiếm, lọc dữ liệu trên các bảng, phân trang... (Chia nhau làm).
    *   **Task 5.5:** **Viết Unit Test (Khuyến khích):** Viết test cho các lớp Service, Utils quan trọng.
    *   **Task 5.6:** **Hoàn thiện Tài liệu:**
        *   README.md (Hướng dẫn cài đặt, chạy, mô tả...).
        *   Báo cáo Word (Theo yêu cầu đề bài, chia nhau viết các phần, cùng review). Kiểm tra Turnitin.
        *   UML Diagrams (ERD, Class Diagram).
        *   Chuẩn bị file PPT.
    *   **Task 5.7:** **Quay Video Demo:** Chuẩn bị kịch bản, cả hai cùng tham gia trình bày.
    *   **Task 5.8:** **Đóng gói:** Đảm bảo mã nguồn sạch sẽ, tạo file nén cuối cùng theo yêu cầu.

**Lưu ý quan trọng:**

*   **Họp ngắn thường xuyên:** Hàng ngày hoặc cách ngày nên có buổi họp ngắn (15-30 phút) để cập nhật tiến độ, thảo luận khó khăn, thống nhất các điểm chung (ví dụ: cấu trúc dữ liệu trả về của Service).
*   **Pull Request & Code Review:** *Bắt buộc* phải tạo PR cho các feature branch vào `develop`. Người còn lại phải review (ít nhất là đọc hiểu và đặt câu hỏi) trước khi merge. Điều này giúp cả hai nắm được code của nhau và phát hiện lỗi sớm.
*   **Xử lý Conflicts:** Nếu có conflict khi merge hoặc pull, cần ngồi lại cùng nhau để giải quyết, đảm bảo không làm mất code của ai hoặc gây lỗi logic.
*   **Ưu tiên hoàn thành:** Nếu gần hết giờ, ưu tiên hoàn thành các chức năng *cốt lõi* theo yêu cầu Rubrics trước khi làm các tính năng mở rộng.

