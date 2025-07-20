Câu 2.1

<img width="819" height="555" alt="image" src="https://github.com/user-attachments/assets/22e26490-9516-4e2e-88be-c44f0a737b9d" />

giải thích 

Tải và Chuyển sang ảnh xám: Mở ảnh geometric.png và chuyển nó thành ảnh đen trắng (xám).

Ngưỡng Otsu: Tính toán một ngưỡng tự động (Otsu) để chuyển ảnh xám thành ảnh nhị phân (chỉ đen và trắng), giúp tách biệt các đối tượng khỏi nền.

Gắn nhãn đối tượng: Tìm và gán một số duy nhất cho từng đối tượng (vùng liền kề) trong ảnh nhị phân.

Lưu ảnh nhãn: Lưu ảnh đã được gán nhãn (với các màu sắc khác nhau cho mỗi đối tượng) ra tệp label_output.jpg.

Trích xuất thuộc tính: Tính toán các thuộc tính như hộp giới hạn cho mỗi đối tượng đã được gắn nhãn.

Hiển thị và Vẽ hộp: Hiển thị ảnh đã gán nhãn và sau đó vẽ các hình chữ nhật bao quanh từng đối tượng được phát hiện.

kết quả 

<img width="652" height="362" alt="image" src="https://github.com/user-attachments/assets/aa0782d2-1f89-4c3d-bace-cd136a92be8d" />


Câu 2.3

<img width="356" height="112" alt="image" src="https://github.com/user-attachments/assets/fcc37463-d58c-4a49-9b53-27b6ba975a01" />

Tính đạo hàm theo trục Y (Sobel dọc): Áp dụng bộ lọc Sobel theo chiều dọc (axis=0) lên ảnh để tìm các cạnh ngang (thay đổi cường độ theo chiều dọc).

Tính đạo hàm theo trục X (Sobel ngang): Áp dụng bộ lọc Sobel theo chiều ngang (axis=1) lên ảnh để tìm các cạnh dọc (thay đổi cường độ theo chiều ngang).

Tính cường độ gradient: Tổng giá trị tuyệt đối của hai kết quả Sobel (ngang và dọc) để tạo ra ảnh bmg thể hiện cường độ của các cạnh (gradient magnitude).

kết quả 

<img width="679" height="376" alt="image" src="https://github.com/user-attachments/assets/9f16d92d-0408-4c8d-a750-6e1e742e31db" />


Câu 2.4

<img width="372" height="353" alt="image" src="https://github.com/user-attachments/assets/a457591f-6c9c-4b78-bf4e-da40d20c21cc" />

giải thích 

Tính đạo hàm Sobel: Tính toán đạo hàm ảnh theo hướng x (x) và y (y) bằng bộ lọc Sobel để phát hiện sự thay đổi cường độ pixel.

Tính tích các đạo hàm: Bình phương các đạo hàm (xl, yl) và tính tích của chúng (xy).

Làm mờ Gaussian: Áp dụng bộ lọc Gaussian lên xl, yl, xy để làm mượt và tổng hợp thông tin cục bộ.

Tính ma trận tự tương quan: Từ các giá trị đã làm mượt, tính toán định thức (detC) và vết (trC) của ma trận tự tương quan (một đại diện cho sự thay đổi cường độ theo các hướng khác nhau).

Tính điểm Harris: Sử dụng công thức đặc trưng của Harris Corner Detector (detC - alpha * trC**2) để tạo ra một bản đồ điểm đáp ứng R. Các điểm có giá trị R cao cho thấy khả năng là một góc.

kết quả 

<img width="687" height="376" alt="image" src="https://github.com/user-attachments/assets/9b6e8ea5-b509-45e3-bc3f-7bd923dbeb33" />


Câu 2.5.1


<img width="595" height="542" alt="image" src="https://github.com/user-attachments/assets/a969771a-8467-4e8e-a7da-015315d0ccce" />

giải thích 

huẩn bị: Khởi tạo "không gian Hough" (ho) để lưu trữ phiếu bầu cho các đường thẳng và tập hợp các góc để kiểm tra.

Lặp và Bỏ phiếu: Lặp đi lặp lại để tìm các điểm ảnh nổi bật (có cường độ cao) trong ảnh gốc. Với mỗi điểm nổi bật được tìm thấy, nó tính toán tất cả các đường thẳng có thể đi qua điểm đó và tăng phiếu bầu cho những đường thẳng này trong không gian Hough.

Kết quả: Trả về không gian Hough, nơi các điểm có phiếu bầu cao nhất đại diện cho các đường thẳng được phát hiện trong ảnh.

kết quả 

<img width="231" height="525" alt="image" src="https://github.com/user-attachments/assets/0b510543-1db1-489a-9531-04c68144d813" />

Câu 2.5.2

<img width="495" height="102" alt="image" src="https://github.com/user-attachments/assets/a85703b1-bd7d-4952-b2b1-ff47bc214e15" />

giải thích 

huyển sang ảnh xám: Chuyển đổi ảnh màu vừa đọc sang định dạng ảnh đen trắng (grayscale).

Phát hiện góc Harris: Áp dụng thuật toán Harris Corner Detector lên ảnh xám để tìm ra các điểm có khả năng là góc. Kết quả coordinate sẽ là một mảng (hoặc bản đồ) thể hiện cường độ của các góc.

kết quả 

<img width="1151" height="850" alt="image" src="https://github.com/user-attachments/assets/1d1bd5ee-ec0c-4793-8450-c9ce9c35bf44" />

Câu 2.6

<img width="924" height="592" alt="image" src="https://github.com/user-attachments/assets/537be4db-c583-4660-b1b8-1e2c2845af0d" />

<img width="877" height="657" alt="image" src="https://github.com/user-attachments/assets/78689ba9-15d8-426c-b6e2-8e2536a3d762" />

<img width="738" height="521" alt="image" src="https://github.com/user-attachments/assets/1bc3a8e3-377d-40ac-9450-ead781a1f6a2" />

kết quả 

<img width="1148" height="390" alt="image" src="https://github.com/user-attachments/assets/92868a53-32bd-4ea5-903a-0dc6e75d03a2" />












