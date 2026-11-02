**Báo cáo Thực hành Session 16: Trình duyệt – Công cụ làm việc của Developer**  
**Phần A – Thiết lập Profile và Bookmark chuẩn Dev**  
**1. Rủi ro khi dùng chung 1 Profile cho cả GitHub cá nhân và GitHub công ty**  
Nếu tiếp tục dùng chung 1 Profile Chrome cho cả hai tài khoản, khi đăng nhập song song sẽ xảy ra hiện tượng **xung đột phiên đăng nhập (Session/Cookie Collision)** và  **rò rỉ kho khóa bảo mật (Git SSH/Personal Access Token)**. Trình duyệt chỉ lưu một tập hợp cookie định danh cho mỗi tên miền (github.com) tại một thời điểm. Điều này dẫn đến việc khi bạn thao tác đẩy mã nguồn (git push) vào các repository công ty, Git có thể sử dụng nhầm khóa hoặc tài khoản cá nhân, gây sai lệch lịch sử commit hoặc vi phạm chính sách bảo mật dữ liệu của công ty.  
**2. Mô hình 3 Profile chuẩn Developer**  
| | | |  
|-|-|-|  
| **Profile** | **Tên đặt** | **Mục đích sử dụng** |   
| **1** | Personal | Dùng cho việc cá nhân, giải trí, xem YouTube, mạng xã hội và quản lý GitHub cá nhân. |   
| **2** | Company_Work | Dùng chuyên biệt cho công việc công ty, kết nối tài khoản GitHub công ty, Slack, Lark Suite và truy cập hệ thống nội bộ. |   
| **3** | Sandbox/Test | Dùng làm môi trường thử nghiệm sạch (không có extension chặn quảng cáo/bảo mật can thiệp), kiểm thử tính năng web và debug code. |   
   
**3. Cấu trúc Bookmark chuẩn 3 thư mục**  
- **Thư mục 1: ** **01_Work_Internal**  
  - 1.PTIT LMS (https://lms.ptit.edu.vn)  
  - 2.Internal Tool Test (http://test.internal-tool.com)  
- **Thư mục 2: ** **02_Dev_Resources**  
  - 1.GitHub Enterprise / Company Repos (https://github.com)  
  - 2.MDN Web Docs (https://developer.mozilla.org)  
- **Thư mục 3: ** **03_Tools_Utilities**  
  - 1.JSON Formatter Online (https://jsonformatter.curiousconcept.com)  
  - 2.Can I use (https://caniuse.com)  
**4. Cho đồng nghiệp mượn máy 5 phút**  
Cho đồng nghiệp sử dụng **Chế độ ẩn danh (Incognito Window)** hoặc  **Guest Profile** (nếu mở một cửa sổ Profile tạm thời).  
- *Giải thích ngắn gọn:* Chế độ này không lưu lại lịch sử duyệt web, cookie hay dữ liệu phiên đăng nhập của các tài khoản cá nhân/công ty hiện tại, giúp bảo vệ toàn bộ dữ liệu nhạy cảm của bạn khỏi việc bị truy cập trái phép.  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANklEQVR4nO3OQQmAABRAsSfYxZo/jzlMYQLPJrCCNxG2BFtmZquOAAD4i3Ot7mr/egIAwGvXA4q7Bc870TqdAAAAAElFTkSuQmCC)  
**Phần B – Chọn đúng Extension hỗ trợ**  
**1. Xử lý đường link API JSON thô**  
- **Nhóm Extension:** Thuộc nhóm  **Dev Suite** (Công cụ hỗ trợ nhà phát triển).  
- **Tên tiện ích đề xuất:** **JSON Formatter** hoặc  **JSON Viewer**.  
- *Vì sao 2 nhóm còn lại không phù hợp:* Nhóm  *Productivity Suite* (tăng năng suất như quản lý tab, ghi chú) và nhóm  *Security Suite* (bảo mật, chặn quảng cáo, VPN) không có tính năng phân tích, định dạng cấu trúc cây (tree view) và làm đẹp (pretty-print) dữ liệu JSON thô, không đáp ứng được nhu cầu đọc hiểu API của Developer.  
**2. Cấu hình quyền Site Access**  
- **Cấu hình:** Chọn  **On click** (Khi nhấp vào).  
- *Giải thích theo quy tắc quản trị Extensions:* Cấu hình On click giúp extension chỉ chạy và quét dữ liệu khi người dùng chủ động bấm vào biểu tượng trên thanh công cụ của trang web cụ thể đó. Điều này giúp tối ưu hóa hiệu năng trình duyệt, ngăn chặn extension tự động đọc và thu thập dữ liệu trên mọi trang web (tránh rủi ro bảo mật với các trang nội bộ nhạy cảm như test.internal-tool.com).  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANElEQVR4nO3OQQmAABRAsad4FCtY9ecwnkms4E2ELcGWmTmrKwAA/uLeqrU6vp4AAPDa/gDzUgM9+S8z3AAAAABJRU5ErkJggg==)  
**Phần C – Phân tích luồng HTTP Request**  
**1. Thứ tự 4 giai đoạn xử lý HTTP Request Flow**  
1. **DNS Lookup:** Phân giải tên miền test.internal-tool.com thành địa chỉ IP của máy chủ.  
2. **TCP Handshake & TLS (nếu HTTPS):** Thiết lập kết nối bắt tay 3 bước an toàn giữa trình duyệt (Client) và Server.  
3. **HTTP Request:** Trình duyệt đóng gói yêu cầu (Method, Headers, Cookies) gửi lên Server.  
4. **Server Response:** Server tiếp nhận, xử lý logic và trả về mã trạng thái HTTP kèm theo nội dung dữ liệu (HTML/JSON/CSS).  
**2. So sánh mã trạng thái và hướng debug**  
| | | | |  
|-|-|-|-|  
| **Mã trạng thái** | **Ý nghĩa** | **Lỗi nằm ở đâu?** | **Hướng debug ban đầu** |   
| **404 Not Found** | Không tìm thấy tài nguyên yêu cầu trên server. | **Client** (hoặc cấu hình đường dẫn Routing phía Server bị sai). | Kiểm tra lại URL, đường dẫn endpoint API, chính tả đường dẫn, hoặc cấu hình file định tuyến (Router). |   
| **500 Internal Server Error** | Lỗi hệ thống nội bộ từ phía máy chủ trong quá trình xử lý. | **Server** | Kiểm tra Log của Server/Backend, bắt lỗi ngoại lệ (Exception), kiểm tra kết nối Database hoặc lỗi cú pháp mã nguồn. |   
   
**3. Tab DevTools xem mã trạng thái HTTP**  
- **Tab được chọn:** **Network**.  
- *Vì sao không chọn các Tab còn lại:*  
  - Tab *Elements* dùng để kiểm tra và chỉnh sửa cấu trúc DOM/CSS giao diện.  
  - Tab *Console* dùng để xem log lỗi JavaScript hoặc chạy lệnh script.  
  - Tab *Application* dùng để quản lý Storage (Cookies, Local Storage, Session Storage, Cache).  
  - Chỉ có tab **Network** là nơi ghi lại toàn bộ các phiên truyền tải gói tin HTTP/HTTPS theo thời gian thực, hiển thị chi tiết mã trạng thái (Status Code), Header và Payload của từng request.  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANUlEQVR4nO3OMQ2AABAAsSNBCUpfD6ZYGZDAgAU2QtIq6DIzW7UHAMBfHGt1V+fXEwAAXrseHCoGAe/SKtAAAAAASUVORK5CYII=)  
**Phần D – Chẩn đoán Cache và Cookies**  
**1. Lỗi CSS không cập nhật khi F5**  
- **Nguyên nhân:** Trình duyệt đang tải lại file CSS cũ từ  **Browser Cache** thay vì yêu cầu tải mới từ Server.  
- **Thao tác khắc phục:** Thực hiện  **Hard Reload** bằng tổ hợp phím  **Ctrl + Shift + R** (trên Windows) hoặc mở DevTools (F12), chuột phải vào nút Refresh và chọn  **"Empty Cache and Hard Reload"**.  
**2. Rủi ro bảo mật khi Cookie thiếu dấu tích **HttpOnly  
- **Rủi ro cụ thể:** Cookie phiên đăng nhập (session_id) có thể bị truy cập và đánh cắp thông qua các đoạn mã JavaScript độc hại chạy trên trình duyệt (thông qua lệnh document.cookie).  
- **Tên loại tấn công:** **Cross-Site Scripting (XSS)**. Khi kẻ tấn công chèn được mã độc JS vào trang web, chúng sẽ lấy được session_id để giả mạo danh tính người dùng.  
**3. Xóa phiên đăng nhập nhưng vẫn giữ Cache ảnh/CSS**  
- **Thao tác:**  
  1. Mở DevTools (F12) \rightarrow Chọn tab **Application**.  
  2. Ở cột bên trái, mục **Storage**, bấm vào  **Cookies**\rightarrow Chọn tên miền trang web.  
  3. Nhấp chuột phải vào riêng cookie session_id (hoặc nhấn nút Clear) để xóa thủ công mục này, đồng thời giữ nguyên các phần Cache Storage / HTTP Cache khác.  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANklEQVR4nO3OQQmAABRAsScYxpg/h5VMYARvRrCCNxG2BFtmZquOAAD4i3Ot7mr/egIAwGvXA224BcUMk6pDAAAAAElFTkSuQmCC)  
**Phần E – Debug bằng Inspect Element và Network Tab**  
**1. Sửa màu nút "Đăng nhập" trực tiếp trên trình duyệt**  
1. Nhấn F12 (hoặc chuột phải vào nút Đăng nhập \rightarrow chọn **Inspect**).  
2. Tại tab **Elements**, chọn đúng thẻ HTML của nút "Đăng nhập".  
3. Nhìn sang khung **Styles** bên cạnh, tìm thuộc tính màu sắc (ví dụ: background-color hoặc color).  
4. Nhấp đúp vào mã màu hiện tại và gõ mã màu mới theo yêu cầu thiết kế để kiểm tra trực quan ngay trên giao diện trước khi báo dev sửa code gốc.  
**2. Quy trình 4 Bước Debugging cho API lỗi**  
1. **Bước 1: Reproduce (Tái hiện lỗi):** Thực hiện lại thao tác gây ra lỗi API trên trang và giữ nguyên tab Network để quan sát dòng request bị đỏ (mã lỗi 4xx hoặc 5xx).  
2. **Bước 2: Inspect (Kiểm tra chi tiết):** Nhấp vào dòng request màu đỏ đó, kiểm tra tab  **Response** hoặc  **Preview** để xem thông điệp lỗi (Error Message) từ server trả về, đồng thời kiểm tra tab  **Headers** để xem Request URL và Payload truyền lên có đúng chuẩn không.  
3. **Bước 3: Isolate (Khoanh vùng nguyên nhân):** Xác định xem lỗi do dữ liệu truyền từ Client lên sai định dạng (4xx) hay do lỗi xử lý logic tính toán từ Server (5xx).  
4. **Bước 4: Fix & Verify (Sửa và kiểm chứng):** Đề xuất hướng sửa (hoặc test trực tiếp trên tab Fetch/Console hoặc Postman), sau đó kiểm chứng lại kết quả sau khi sửa.  
**3. Thiết lập bộ lọc trên Network Tab**  
1. **Lọc loại request API:** Trên thanh công cụ của tab Network, bấm vào nút phân loại  **Fetch/XHR** để chỉ hiển thị các lời gọi API bất đồng bộ.  
2. **Vô hiệu hóa Cache:** Tích chọn ô vuông  **"Disable cache"** nằm ở thanh menu phụ ngay phía trên tab Network để đảm bảo mọi request đều gọi trực tiếp về Server lấy dữ liệu mới nhất mỗi khi tải lại trang.  
