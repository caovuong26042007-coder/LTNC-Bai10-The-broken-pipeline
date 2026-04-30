Lỗi 1: Không tìm thấy tệp cấu hình Maven (Lỗi Checkout Code)

Đoạn log: Error:  The goal you specified requires a project to execute but there is no POM in this directory (/home/runner/work/LTNC-Bai10-The-broken-pipeline/LTNC-Bai10-The-broken-pipeline). Please verify you invoked Maven from the correct directory. -> [Help 1]

Giải thích nguyên nhân kỹ thuật: Khi GitHub Actions khởi tạo một máy ảo (runner) để chạy CI, máy ảo này mặc định là một môi trường hoàn toàn trống rỗng. Vì trong tệp ci.yml bị thiếu bước gọi Action actions/checkout, máy ảo không thực hiện việc tải (clone/pull) mã nguồn từ repository về. Hậu quả là khi lệnh mvn package được kích hoạt, nó không tìm thấy tệp pom.xml trong thư mục gốc để bắt đầu quá trình build, dẫn đến lỗi sập toàn bộ tiến trình.


Lỗi 2: Không tìm thấy phiên bản thư viện (Lỗi Dependency Resolution)

Vị trí lỗi: Tệp pom.xml (Khai báo sai phiên bản trong thẻ <dependency> của logback-classic).

Đoạn log: 

Error:  Failed to execute goal on project shipping-app: Could not resolve dependencies for project com.lab:shipping-app:jar:1.0-SNAPSHOT

Error:  dependency: ch.qos.logback:logback-classic:jar:9.9.9 (compile)

Error:  	Could not find artifact ch.qos.logback:logback-classic:jar:9.9.9 in central (https://repo.maven.apache.org/maven2)

Giải thích nguyên nhân kỹ thuật: Trong tệp pom.xml, dự án yêu cầu Maven tải thư viện logback-classic với phiên bản là 9.9.9 từ kho lưu trữ trung tâm (Maven Central). Tuy nhiên, phiên bản 9.9.9 này không hề tồn tại trên thực tế. Vì Maven không thể tìm và tải xuống gói phụ thuộc bắt buộc này, quá trình build thể tiếp tục và buộc phải dừng lại kèm theo thông báo lỗi không tìm thấy artifact.

