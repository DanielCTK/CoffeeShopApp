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


**Nguyên tắc áp dụng thuật toán:**

*   **Sắp xếp (Sorting):** `Collections.sort`, `List.sort`, Java Streams API (`sorted()`) với `Comparator` tùy chỉnh. Áp dụng cho việc hiển thị dữ liệu trong bảng.
*   **Tìm kiếm (Searching):**
    *   **Tuyến tính/Lọc:** Java Streams API (`filter`), `String.contains()`.
    *   **Nhị phân (Binary Search):** `Collections.binarySearch` (yêu cầu danh sách đã được sắp xếp). Có thể dùng cho việc tìm kiếm nhanh trong danh sách sản phẩm/danh mục lớn đã được sắp xếp theo tên/ID.
    *   **Nâng cao:** Có thể xem xét các kỹ thuật như tìm kiếm mờ (fuzzy search) nếu muốn xử lý lỗi chính tả (phức tạp hơn).
*   **Băm (Hashing):** `HashMap`, `HashSet` để lưu trữ, tra cứu nhanh, kiểm tra trùng lặp, caching. Thuật toán băm mật khẩu (BCrypt) đã dùng.
*   **Cấu trúc dữ liệu khác:** `TreeMap` (Map đã sắp xếp), có thể dùng `PriorityQueue` cho một số tác vụ ưu tiên.

---

**1. Tài khoản Quản lý (Admin) - Nâng cấp với Thuật toán:**

Ngoài các chức năng CRUD cơ bản đã có:

*   **Dashboard Nâng cao:**
    *   **Tính năng:** Hiển thị Top N sản phẩm bán chạy nhất/ít chạy nhất (theo doanh thu/số lượng) trong khoảng thời gian tùy chọn. Hiển thị xu hướng doanh thu (tăng/giảm so với kỳ trước).
    *   **Thuật toán:**
        *   **Tổng hợp dữ liệu:** SQL `GROUP BY`, `SUM`, `COUNT`.
        *   **Sắp xếp (Sorting):** Sắp xếp kết quả tổng hợp (ví dụ: `List<ProductRevenue>` hoặc `Map<Product, Double>`) theo doanh thu/số lượng giảm dần/tăng dần để lấy Top N. Có thể dùng `Collections.sort` hoặc `Stream.sorted`.
        *   **Cấu trúc dữ liệu (Hashing):** Dùng `HashMap` để tổng hợp doanh thu/số lượng theo sản phẩm/ngày/tháng hiệu quả trước khi sắp xếp.
    *   **Lợi ích:** Cung cấp cái nhìn sâu sắc hơn về hiệu quả kinh doanh.

*   **Quản lý Sản phẩm Nâng cao:**
    *   **Tính năng:**
        *   **Sắp xếp Linh hoạt:** Cho phép sắp xếp danh sách sản phẩm trong bảng theo Tên, Giá, Danh mục, Số lượng tồn (nếu có) bằng cách nhấp vào tiêu đề cột.
        *   **Tìm kiếm Nâng cao:** Ô tìm kiếm cho phép tìm sản phẩm theo Tên, Mã sản phẩm (nếu có), hoặc Mô tả. Có thể hỗ trợ tìm kiếm không phân biệt chữ hoa/thường.
        *   **Kiểm tra Trùng lặp khi Thêm:** Khi Admin thêm sản phẩm mới, hệ thống kiểm tra nhanh xem có sản phẩm nào có Tên và Danh mục tương tự đã tồn tại hay không (để tránh tạo nhầm).
    *   **Thuật toán:**
        *   **Sắp xếp (Sorting):** Triển khai `Comparator` cho các thuộc tính khác nhau của `Product` và áp dụng khi người dùng nhấp vào header cột (thực hiện sắp xếp trên `ObservableList` của TableView).
        *   **Tìm kiếm (Searching):** Dùng `Stream.filter` với điều kiện `String.contains` (case-insensitive) trên danh sách sản phẩm đã tải hoặc xây dựng câu lệnh SQL `WHERE ... LIKE ...` động.
        *   **Băm (Hashing):** Dùng `HashSet<String>` để lưu trữ một "khóa định danh" (ví dụ: `product.getName().toLowerCase() + "_" + category.getId()`) của các sản phẩm hiện có. Khi thêm mới, tạo khóa tương tự và kiểm tra sự tồn tại trong `HashSet` (`contains()`) - tốc độ O(1) trung bình.
    *   **Lợi ích:** Quản lý sản phẩm hiệu quả, nhanh chóng và tránh dữ liệu rác.

*   **Quản lý Đơn hàng Nâng cao:**
    *   **Tính năng:**
        *   **Sắp xếp & Lọc Đơn hàng:** Cho phép sắp xếp đơn hàng theo Ngày tạo, Tổng tiền, Trạng thái, Mã nhân viên tạo. Thêm bộ lọc để xem đơn hàng theo khoảng ngày, theo trạng thái, theo nhân viên.
        *   **Tìm kiếm Đơn hàng:** Tìm kiếm đơn hàng theo Mã đơn hàng, Tên khách hàng (nếu có), Tên sản phẩm có trong đơn hàng.
    *   **Thuật toán:**
        *   **Sắp xếp (Sorting):** Tương tự quản lý sản phẩm, sắp xếp `ObservableList` của `Order` theo các trường khác nhau.
        *   **Tìm kiếm/Lọc (Searching/Filtering):** Dùng `Stream.filter` hoặc xây dựng câu lệnh SQL `WHERE` phức tạp hơn với các điều kiện lọc/tìm kiếm. Để tìm theo sản phẩm trong đơn, cần join với bảng `order_details` và `products` trong SQL hoặc xử lý logic sau khi lấy dữ liệu.
    *   **Lợi ích:** Dễ dàng tra cứu, phân tích và quản lý lịch sử đơn hàng lớn.

*   **Quản lý Người dùng Nâng cao:**
    *   **Tính năng:**
        *   **Sắp xếp & Lọc Người dùng:** Sắp xếp theo Tên đăng nhập, Họ tên, Vai trò, Trạng thái (Active/Inactive). Lọc theo Vai trò hoặc Trạng thái.
        *   **Tìm kiếm Người dùng:** Tìm kiếm theo Tên đăng nhập hoặc Họ tên.
    *   **Thuật toán:**
        *   **Sắp xếp (Sorting):** Sắp xếp danh sách `User` trong TableView.
        *   **Tìm kiếm/Lọc (Searching/Filtering):** `Stream.filter` hoặc SQL `WHERE` clause.
    *   **Lợi ích:** Quản lý nhân viên hiệu quả hơn khi số lượng lớn.

---

**2. Tài khoản Nhân viên (Staff) - Nâng cấp với Thuật toán:**

Ngoài các chức năng cơ bản đã có:

*   **Tạo Đơn hàng Thông minh:**
    *   **Tính năng:**
        *   **Tìm kiếm Sản phẩm Nhanh:** Khi thêm sản phẩm vào đơn hàng, ô tìm kiếm cho phép tìm nhanh sản phẩm theo Tên hoặc Mã. Có thể hiển thị gợi ý (autocomplete).
        *   **Hiển thị Sản phẩm Hay Bán/Mới:** Có thể ưu tiên hiển thị các sản phẩm bán chạy gần đây hoặc sản phẩm mới ở đầu danh sách chọn.
        *   **(Nâng cao) Gợi ý Combo/Mua kèm:** Dựa trên sản phẩm đang chọn, gợi ý các sản phẩm khác thường được mua kèm (ví dụ: chọn Cà phê -> gợi ý Bánh ngọt).
    *   **Thuật toán:**
        *   **Tìm kiếm (Searching):** `Stream.filter` trên danh sách sản phẩm đã cache hoặc query SQL `LIKE`. Cho autocomplete, có thể dùng cấu trúc dữ liệu Trie (nếu cache) hoặc query DB liên tục.
        *   **Sắp xếp (Sorting):** Lấy dữ liệu thống kê (từ `ReportService` hoặc một service khác) về sản phẩm bán chạy/mới và dùng `Comparator` để sắp xếp danh sách sản phẩm hiển thị khi chọn.
        *   **Phân tích Mẫu (Pattern Analysis - cho gợi ý):** Yêu cầu phân tích lịch sử `order_details` để tìm các cặp sản phẩm thường xuyên xuất hiện cùng nhau (có thể dùng `HashMap<Integer, HashMap<Integer, Integer>>` để đếm số lần xuất hiện cùng nhau của các cặp productID). -> **Đây là tính năng khá phức tạp, cân nhắc kỹ.**
    *   **Lợi ích:** Tăng tốc độ tạo đơn hàng, cải thiện trải nghiệm nhân viên, tiềm năng tăng doanh số qua gợi ý.

*   **Quản lý Sản phẩm (Giới hạn):**
    *   **Tính năng:**
        *   **Sắp xếp Linh hoạt:** Cho phép Staff sắp xếp danh sách sản phẩm họ được xem theo Tên, Giá, Danh mục.
        *   **Tìm kiếm Sản phẩm:** Cho phép Staff tìm kiếm nhanh trong danh sách sản phẩm họ được xem.
    *   **Thuật toán:**
        *   **Sắp xếp (Sorting):** Tương tự Admin, nhưng áp dụng trên tập dữ liệu Staff được phép xem.
        *   **Tìm kiếm (Searching):** `Stream.filter` hoặc SQL `LIKE`.
    *   **Lợi ích:** Giúp Staff tra cứu thông tin sản phẩm nhanh hơn.

*   **Quản lý Đơn hàng (Giới hạn):**
    *   **Tính năng:**
        *   **Sắp xếp & Lọc Đơn hàng Cá nhân:** Cho phép sắp xếp các đơn hàng *của mình* hoặc đơn hàng gần đây theo Ngày tạo, Tổng tiền, Trạng thái. Lọc theo trạng thái.
        *   **Tìm kiếm Đơn hàng Cá nhân:** Tìm kiếm trong các đơn hàng của mình theo Mã đơn hoặc tên sản phẩm.
    *   **Thuật toán:**
        *   **Sắp xếp (Sorting):** Sắp xếp danh sách đơn hàng giới hạn Staff được xem.
        *   **Tìm kiếm/Lọc (Searching/Filtering):** `Stream.filter` hoặc SQL `WHERE` với điều kiện lọc bổ sung (`userId = currentUserId`).
    *   **Lợi ích:** Giúp Staff theo dõi các đơn hàng mình phụ trách dễ dàng hơn.

---

## Công nghệ sử dụng (Technologies Used)

*   **Ngôn ngữ:** Java (JDK 11 hoặc mới hơn)
*   **Giao diện người dùng (UI):** JavaFX (sử dụng FXML và Scene Builder)
*   **Cơ sở dữ liệu:** MySQL Server (phiên bản 8.0 hoặc tương thích)
*   **Thư viện Biểu đồ:** JFreeChart
*   **Kết nối CSDL:** JDBC (thông qua MySQL Connector/J)
*   **Mã hóa Mật khẩu:** jBCrypt (hoặc thư viện tương tự)
*   **IDE:** Eclipse IDE for Java Developers (hoặc IntelliJ IDEA)
*   **Quản lý Mã nguồn:** Git & GitHub

---

## Thư viện Ngoài (External Libraries)

Các thư viện sau cần được thêm vào project (trong thư mục `lib/` hoặc quản lý qua Maven/Gradle):

*   **MySQL Connector/J:** `mysql-connector-j-x.x.x.jar` (Thay `x.x.x` bằng phiên bản cụ thể) - Để kết nối Java với MySQL.
*   **JFreeChart:** `jfreechart-x.x.x.jar` - Để vẽ biểu đồ.
*   **JCommon:** `jcommon-x.x.x.jar` - Thư viện phụ thuộc của JFreeChart.
*   **jBCrypt:** `jbcrypt-x.x.jar` (Ví dụ: `jbcrypt-0.4.jar`) - Để băm và xác thực mật khẩu an toàn.
*   **(Nếu dùng Java 11+ và JavaFX riêng):** Các module JavaFX SDK (ví dụ: `javafx-controls`, `javafx-fxml`, `javafx-graphics`, `javafx-base`, `javafx-swing-interop` cho JFreeChart).

---

## Cài đặt Môi trường (Environment Setup)

Để chạy và phát triển ứng dụng này, bạn cần cài đặt:

1.  **Java Development Kit (JDK):** Phiên bản 11 hoặc cao hơn. Đảm bảo đã cấu hình biến môi trường `JAVA_HOME`.
2.  **MySQL Server:** Phiên bản 8.0 hoặc tương thích. Tạo một database (ví dụ: `coffeeshop_db`) và một user có quyền truy cập vào database đó.
3.  **IDE (Khuyến nghị):** Eclipse IDE for Java Developers hoặc IntelliJ IDEA.
4.  **Scene Builder:** (Tùy chọn nhưng rất khuyến khích) Để chỉnh sửa file FXML trực quan. Cần cấu hình đường dẫn tới Scene Builder trong IDE.
5.  **Git:** Để quản lý mã nguồn và làm việc nhóm.

---

## Hướng dẫn Cài đặt & Chạy Ứng dụng (Setup & Run Instructions)

1.  **Clone Repository:**
    Mở terminal hoặc Git Bash và chạy lệnh sau (thay `<your-repo-url>` bằng link public GitHub của bạn):
    ```bash
    git clone <your-repo-url>
    cd coffeeshopapp
    ```
    *(Ví dụ Link Repo: `https://github.com/yourusername/coffeeshopapp.git`)*

2.  **Import Project vào IDE:**
    *   **Eclipse:** Chọn `File -> Import... -> General -> Existing Projects into Workspace`, chọn thư mục `coffeeshopapp` vừa clone về.
    *   **IntelliJ IDEA:** Chọn `File -> Open...` và chọn thư mục `coffeeshopapp`.

3.  **Thêm Thư viện (Nếu không dùng Maven/Gradle):**
    *   Trong Eclipse: Chuột phải vào project -> `Build Path -> Configure Build Path... -> Libraries -> Classpath -> Add JARs...` (hoặc `Add External JARs...`) và chọn tất cả các file `.jar` trong thư mục `lib/`.
    *   Trong IntelliJ: `File -> Project Structure... -> Modules -> Dependencies -> + -> JARs or directories...` và chọn các file `.jar` trong `lib/`.

4.  **Thiết lập Cơ sở dữ liệu:**
    *   Sử dụng một công cụ quản lý CSDL (MySQL Workbench, DBeaver,...) để kết nối tới MySQL Server của bạn.
    *   Tạo database: `CREATE DATABASE IF NOT EXISTS coffeeshop_db;`
    *   Chọn database: `USE coffeeshop_db;`
    *   Chạy script tạo bảng: Thực thi nội dung file `resources/sql/schema.sql`.
    *   (Tùy chọn) Chạy script chèn dữ liệu mẫu: Thực thi nội dung file `resources/sql/data.sql` (Đặc biệt là tài khoản Admin ban đầu).
    *   **Cấu hình Kết nối:** Mở file `resources/config/db.properties` và cập nhật các giá trị `db.url`, `db.username`, `db.password` cho phù hợp với cấu hình MySQL của bạn.
        *   Ví dụ `db.url`: `jdbc:mysql://localhost:3306/coffeeshop_db`

5.  **Chạy Ứng dụng:**
    *   Tìm lớp `com.youruniversity.coffeeshop.MainApp.java` trong IDE.
    *   Chuột phải vào file `MainApp.java` và chọn `Run As -> Java Application`.
    *   Màn hình đăng nhập sẽ xuất hiện. Sử dụng tài khoản Admin đã tạo trong `data.sql` (hoặc tạo thủ công) để đăng nhập lần đầu.

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


**Các Thao tác Git cơ bản trong Eclipse (EGit):**

Bạn sẽ chủ yếu tương tác với Git qua các view sau:

*   **`Package Explorer` hoặc `Project Explorer`:** Hiển thị các dấu hiệu thay đổi trên file/folder (ví dụ: `>` cho file đã thay đổi, `*` cho file mới chưa được track).
*   **`Git Staging` View:** Đây là view quan trọng nhất để thực hiện Add (Stage) và Commit. Mở nó qua `Window -> Show View -> Other... -> Git -> Git Staging`.
*   **`Git Repositories` View:** Quản lý các repository local và remote, thực hiện Pull, Push, xem nhánh... Mở qua `Window -> Show View -> Other... -> Git -> Git Repositories`.
*   **`History` View:** Xem lịch sử commit. Mở bằng cách chuột phải vào project/file -> `Team -> Show in History`.

**Quy trình làm việc thông thường:**

1.  **Clone Repository từ GitHub (Nếu bắt đầu dự án đã có trên GitHub):**
    *   Mở view `Git Repositories`.
    *   Nhấp vào biểu tượng "Clone a Git repository" (biểu tượng giống mũi tên xanh lục tải xuống).
    *   Trong hộp thoại "Clone Git Repository":
        *   **URI:** Dán URL của repository GitHub của bạn (ví dụ: `https://github.com/yourusername/coffeeshopapp.git`). Các trường khác thường tự điền.
        *   **Authentication:** Nhập Username GitHub của bạn. Đối với Password, **hãy sử dụng Personal Access Token (PAT)** thay vì mật khẩu GitHub thông thường. Bạn cần tạo PAT trên GitHub với quyền `repo`.
        *   Chọn nhánh (branch) bạn muốn clone (thường là `main` hoặc `develop`).
        *   Chọn thư mục local để lưu repository.
    *   Nhấn `Next` và `Finish`.
    *   Sau khi clone xong, chuột phải vào repository vừa clone trong view `Git Repositories` -> `Import Projects...` để đưa project vào workspace Eclipse của bạn.

2.  **Chia sẻ Project hiện có lên Git (Nếu bắt đầu dự án local):**
    *   Chuột phải vào project của bạn trong `Package Explorer`.
    *   Chọn `Team -> Share Project...`.
    *   Chọn `Git` và nhấn `Next`.
    *   Tick vào ô vuông cạnh tên project của bạn.
    *   Nhấn `Create Repository` -> `Finish`. Thao tác này sẽ tạo một kho Git local trong thư mục project của bạn.
    *   Bạn cần tạo một repository trống trên GitHub, sau đó liên kết remote và push lần đầu (xem bước Push).

3.  **Thực hiện thay đổi Code:** Sửa, thêm, xóa file như bình thường trong Eclipse. (***Chú ý từ mục này trở về sau***)

4.  **Staging Changes (Tương đương `git add`):**
    *   Mở view `Git Staging`.
    *   Các file bạn đã thay đổi sẽ xuất hiện trong ô **`Unstaged Changes`**.
    *   **Cách Stage:**
        *   **Kéo và thả:** Kéo các file/thư mục từ `Unstaged Changes` sang ô **`Staged Changes`**.
        *   **Nút (+):** Chọn các file trong `Unstaged Changes` và nhấp vào nút `+` (Add selected files to index).
        *   **Chuột phải:** Chuột phải vào file trong `Package Explorer` -> `Team -> Add to Index`.
    *   Chỉ những thay đổi trong ô `Staged Changes` mới được đưa vào commit tiếp theo.

5.  **Committing Changes (Tương đương `git commit`):**
    *   Trong view `Git Staging`:
        *   Đảm bảo các thay đổi bạn muốn commit đã nằm trong ô `Staged Changes`.
        *   Nhập một **Commit Message** rõ ràng, có ý nghĩa vào ô `Commit Message`.
        *   Kiểm tra thông tin Author và Committer (thường được lấy từ cấu hình Git global).
        *   Nhấn nút **`Commit`**. Thao tác này chỉ lưu commit vào **repository local** của bạn.
        *   (Tùy chọn) Nhấn **`Commit and Push...`**: Thực hiện commit local và **ngay lập tức** mở hộp thoại Push để đẩy lên remote (GitHub).

6.  **Pushing Changes (Tương đương `git push`):** Đẩy các commit local lên remote repository (GitHub).
    *   **Cách 1 (Sau khi Commit):** Nếu bạn chỉ nhấn `Commit`, hãy chuột phải vào project -> `Team -> Push Branch 'branch_name'...` (ví dụ: `Push Branch 'develop'...`) hoặc `Push to Upstream`.
    *   **Cách 2 (Từ Git Repositories):** Mở view `Git Repositories`, tìm repository của bạn, mở rộng `Branches -> Local Branches`, chuột phải vào nhánh muốn push (ví dụ `develop`) -> `Push Branch...`.
    *   **Cách 3 (Commit and Push):** Như đã đề cập ở bước Commit.
    *   **Hộp thoại Push:**
        *   Chọn `Remote` (thường là `origin`).
        *   Cấu hình `Ref mappings` (thường EGit tự động đề xuất đúng).
        *   Nhấn `Preview` để xem trước, sau đó nhấn `Push`.
        *   Bạn có thể cần nhập lại **Personal Access Token** nếu chưa lưu.

7.  **Pulling Changes (Tương đương `git pull`, tức là `git fetch` + `git merge`):** Lấy các thay đổi mới nhất từ remote (GitHub) về và trộn vào nhánh local của bạn.
    *   **Cách 1:** Chuột phải vào project -> `Team -> Pull`. EGit sẽ tự động fetch từ remote `origin` và merge vào nhánh hiện tại của bạn.
    *   **Cách 2 (Từ Git Repositories):** Mở view `Git Repositories`, chuột phải vào tên repository -> `Pull`.
    *   **Quan trọng:** **Luôn Pull trước khi bạn bắt đầu code một tính năng mới hoặc trước khi Push code của bạn lên**, để đảm bảo bạn đang làm việc trên phiên bản mới nhất và giảm thiểu xung đột (conflicts).
    *   **Conflicts:** Nếu có xung đột giữa thay đổi của bạn và thay đổi trên remote, EGit sẽ báo lỗi. Các file bị conflict sẽ được đánh dấu đặc biệt trong `Git Staging`. Bạn cần:
        *   Chuột phải vào file conflict -> `Merge Tool` để mở trình giải quyết conflict của Eclipse.
        *   Hoặc mở file và sửa thủ công các đoạn đánh dấu `<<<<<<<`, `=======`, `>>>>>>>`.
        *   Sau khi giải quyết xong, **phải Stage (Add to Index)** file đó lại.
        *   Cuối cùng, thực hiện một commit mới để hoàn tất việc merge.

8.  **Xem lịch sử (History):**
    *   Chuột phải vào project hoặc file cụ thể -> `Team -> Show in History`.
    *   View `History` sẽ hiển thị danh sách các commit, bạn có thể xem chi tiết thay đổi của từng commit.


