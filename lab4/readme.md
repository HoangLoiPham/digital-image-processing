Câu 1

<img width="773" height="404" alt="image" src="https://github.com/user-attachments/assets/b90e3884-3c33-4efa-9a3c-ead8e8e97ea9" />

Giải thích code 

x, y, w, h = 126, 268, 312, 66

Các dòng này định nghĩa tọa độ và kích thước cho một vùng quan tâm (ROI) hình chữ nhật sẽ được cắt từ ảnh.

x: tọa độ x (cột) của góc trên bên trái vùng cắt.

y: tọa độ y (hàng) của góc trên bên trái vùng cắt.

w: chiều rộng của vùng cắt.

h: chiều cao của vùng cắt.

crop = image[y:y+h, x:x+w]

Dòng này thực hiện việc cắt ảnh.

Trong cách cắt mảng NumPy cho ảnh, cấu trúc là [hàng_bắt_đầu:hàng_kết_thúc, cột_bắt_đầu:cột_kết_thúc].

y:y+h chọn các hàng từ y đến (nhưng không bao gồm) y+h.

x:x+w chọn các cột từ x đến (nhưng không bao gồm) x+w.

Kết quả, crop, là một ảnh mới (một phần dữ liệu của image gốc) chỉ chứa vùng hình chữ nhật được chỉ định.

gray = cv2.cvtColor(crop, cv2.COLOR_BGR2GRAY)

Dòng này chuyển đổi ảnh crop từ BGR sang ảnh đen trắng (grayscale).

Chuyển đổi sang ảnh đen trắng thường là điều kiện tiên quyết cho nhiều phép toán xử lý ảnh, đặc biệt là ngưỡng, vì nó giảm ảnh xuống còn một kênh duy nhất đại diện cho cường độ.

_, mask = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)

Dòng này áp dụng một phép toán ngưỡng (thresholding) cho ảnh gray để tạo ra một mặt nạ nhị phân.

cv2.threshold() trả về hai giá trị: giá trị ngưỡng được sử dụng (bị bỏ qua ở đây bởi _) và mask kết quả.

gray: Ảnh xám đầu vào.

0: Giá trị ngưỡng ban đầu (bị bỏ qua khi sử dụng THRESH_OTSU).

255: Giá trị tối đa được sử dụng cho các pixel vượt quá ngưỡng.

cv2.THRESH_BINARY: Chỉ định rằng các pixel trên ngưỡng trở thành 255, và các pixel dưới ngưỡng trở thành 0.

cv2.THRESH_OTSU: Đây là phương pháp nhị phân hóa của Otsu. Nó tự động xác định giá trị ngưỡng tối ưu từ biểu đồ ảnh. Điều này rất hữu ích khi điều kiện ánh sáng hoặc thuộc tính ảnh có thể thay đổi. Giá trị 0 ngưỡng ban đầu chỉ là một giá trị giữ chỗ khi sử dụng phương pháp Otsu.

mask sẽ là một ảnh nhị phân trong đó các pixel trắng (255) đại diện cho tiền cảnh (hoặc vùng quan tâm được xác định bởi phương pháp Otsu) và các pixel đen (0) đại diện cho nền.

segmented = cv2.bitwise_and(crop, crop, mask=mask)

Dòng này thực hiện phép toán AND bitwise giữa ảnh crop và chính nó, sử dụng mask.

cv2.bitwise_and(): Đối với mỗi pixel, nếu pixel tương ứng trong mask khác 0 (trắng, 255), pixel từ crop sẽ được giữ lại trong segmented. Nếu pixel mask bằng 0 (đen, 0), pixel tương ứng trong segmented sẽ trở thành đen (0).

Thực tế, phép toán này trích xuất "tiền cảnh" (phần của crop tương ứng với các vùng màu trắng trong mask) và làm cho mọi thứ khác trở thành màu đen. Đây là một kỹ thuật phổ biến để phân đoạn ảnh.

cv2.imwrite("lang_biang.jpg", segmented)

kết quả 

<img width="1517" height="197" alt="image" src="https://github.com/user-attachments/assets/e2ce532d-0100-49d7-b5b6-1e0f6da8e0ed" />


Câu 2

<img width="727" height="701" alt="image" src="https://github.com/user-attachments/assets/21288d5b-ce7b-4b83-936a-250af035107f" />

crop = image[y:y+h, x:x+w]

Dòng này thực hiện việc cắt ảnh. Nó tạo ra một ảnh mới, crop, chứa chỉ vùng hình chữ nhật được chỉ định từ image gốc.

gray = cv2.cvtColor(crop, cv2.COLOR_BGR2GRAY)

Dòng này chuyển đổi ảnh crop từ không gian màu BGR sang ảnh đen trắng (grayscale). Việc này cần thiết cho bước ngưỡng thích ứng tiếp theo.

adaptive = cv2.adaptiveThreshold(gray, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 11, 60)

Đây là một bước quan trọng. Dòng này áp dụng ngưỡng thích ứng (adaptive thresholding) cho ảnh gray. Không giống như ngưỡng toàn cục (như Otsu), ngưỡng thích ứng tính toán một ngưỡng riêng cho các vùng nhỏ khác nhau của ảnh. Điều này rất hữu ích khi có sự thay đổi đáng kể về điều kiện ánh sáng trong ảnh 

kết quả 

<img width="1509" height="417" alt="image" src="https://github.com/user-attachments/assets/e3986267-4399-4124-9a67-41bbda0c8794" />

Câu 3 

<img width="908" height="215" alt="image" src="https://github.com/user-attachments/assets/5e14c456-7426-4752-abb9-79ad410523fc" />

giải thích 

closed = binary_closing(thresholded, structure=np.ones((5, 5))).astype(np.uint8) * 255
Dilatation (Giãn nở): Mở rộng các vùng trắng (tiền cảnh).

Erosion (Xói mòn): Thu nhỏ các vùng trắng (tiền cảnh).

thresholded = (normalized > 100).astype(np.uint8) * 255

Kết quả, thresholded, là một ảnh nhị phân: các pixel có giá trị cường độ gốc (sau khi chuẩn hóa) lớn hơn 100 sẽ là trắng, còn lại là đen.

kết qảu

<img width="1516" height="551" alt="image" src="https://github.com/user-attachments/assets/3751da7b-24d0-4711-b68a-49f271fe1511" />

Câu 4

<img width="970" height="398" alt="image" src="https://github.com/user-attachments/assets/409fdeed-1091-4016-8490-c7389e800e64" />

<img width="729" height="246" alt="image" src="https://github.com/user-attachments/assets/e4c6c858-24b4-4b4e-bfd6-9981434b4dab" />

giải thích 

main_choice = input("Chọn nhóm chức năng (1 hoặc 2): ").strip()

Dòng này hiển thị một lời nhắc cho người dùng trên bảng điều khiển: "Chọn nhóm chức năng (1 hoặc 2): "

input(...) đọc đầu vào của người dùng từ bàn phím. Đầu vào này sẽ luôn là một chuỗi (string).

.strip() là một phương thức chuỗi loại bỏ bất kỳ khoảng trắng nào (bao gồm khoảng trắng, tab, xuống dòng) ở đầu và cuối chuỗi. Điều này hữu ích để ngăn lỗi nếu người dùng vô tình nhập khoảng trắng trước hoặc sau số lựa chọn của họ (ví dụ: "1 " thay vì "1").

Dòng này gọi một hàm có tên geometric_transformation_menu().

kết quả 

<img width="612" height="434" alt="image" src="https://github.com/user-attachments/assets/bc1e753e-4d3e-4f54-8c0c-1189791f2ac3" />
<img width="1484" height="548" alt="image" src="https://github.com/user-attachments/assets/e2ba55a7-bb53-4ac8-a4b6-3154f040d9f1" />











