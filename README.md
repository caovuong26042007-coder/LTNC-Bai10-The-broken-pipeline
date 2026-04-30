Lỗi 1: Không tìm thấy tệp cấu hình Maven (Lỗi Checkout Code)

Đoạn log: Error:  The goal you specified requires a project to execute but there is no POM in this directory (/home/runner/work/LTNC-Bai10-The-broken-pipeline/LTNC-Bai10-The-broken-pipeline). Please verify you invoked Maven from the correct directory. -> [Help 1]

Giải thích nguyên nhân kỹ thuật: Khi GitHub Actions khởi tạo một máy ảo (runner) để chạy CI, máy ảo này mặc định là một môi trường hoàn toàn trống rỗng. Vì trong tệp ci.yml bị thiếu bước gọi Action actions/checkout, máy ảo không thực hiện việc tải (clone/pull) mã nguồn từ repository về. Hậu quả là khi lệnh mvn package được kích hoạt, nó không tìm thấy tệp pom.xml trong thư mục gốc để bắt đầu quá trình build, dẫn đến lỗi sập toàn bộ tiến trình.


Lỗi 2: 

