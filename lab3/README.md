- Lab 3 : Biến đổi hình học 
- Giới thiệu : bài lab này nhằm mục đích thực hành thao tác cắt một vùng ảnh cụ thể từ ảnh gốc màu và tịnh tiến ảnh , ngoài ra còn thay đổi được kích thước ảnh , xoay ảnh và biến đổi .
- Công nghệ sử dụng : 
+ Python: Ngôn ngữ chính
+ NumPy: Xử lý ảnh dưới dạng mảng số học
+ ImageIO: Đọc và lưu ảnh với định dạng hiện đại (.jpg, .png, ...)
+ Matplotlib: Hiển thị ảnh trực quan và so sánh ảnh trước – sau
- 1.1 Chọn đối tượng trong ảnh (cắt ảnh trong vùng chọn)
* Mục đích : 
- Cắt ảnh (Cropping) là thao tác chọn một vùng con (ROI - Region of Interest) trong ảnh gốc để:
+ Tập trung xử lý vùng quan trọng (ví dụ: vật thể cần nhận diện)
+ Giảm kích thước ảnh, tăng hiệu quả tính toán
+ Tách đối tượng khỏi nền để phân tích riêng
+ Tiền xử lý dữ liệu cho các bước xử lý ảnh tiếp theo
* Code chính : 
- bmg = data[800:1200, 570:980]
- iio.imsave('orange.jpg', bmg)
- 1.2 Tịnh tiến đơn hay còn gọi là dịch chuyển đơn 
* Mục đích :
- Dịch chuyển ảnh là một phép biến đổi hình học cơ bản trong xử lý ảnh nhằm:
+ Di chuyển vị trí đối tượng trong ảnh mà không làm biến dạng
+ Tiền xử lý ảnh trong nhận diện, theo dõi vật thể (object tracking)
+ Mô phỏng chuyển động trong video hoặc chuỗi ảnh
+ So khớp ảnh khi các vật thể hoặc camera bị lệch vị trí
* Công thức toán học :
Cho ảnh 2 chiều 𝑓(𝑥,𝑦) phép dịch chuyển được mô tả bằng công thức:
𝑔(𝑥,𝑦)=𝑓(𝑥−Δ𝑥,𝑦−Δ𝑦)
Trong đó:
𝑓: ảnh gốc
𝑔: ảnh sau khi dịch chuyển
Δ𝑥,Δ𝑦: độ dịch chuyển theo trục x (ngang) và y (dọc)
* Code chính :
- bdata = nd.shift(data, shift=(100, 25))
- 1.3 Thay đổi kích thước ảnh 
* Mục đích : 
- Thay đổi kích thước ảnh là một thao tác quan trọng trong xử lý ảnh, được sử dụng để:
+ Phóng to hoặc thu nhỏ ảnh mà vẫn giữ đúng tỷ lệ
+ Tiền xử lý ảnh đầu vào cho mạng nơ-ron (CNN, ML)
+ Tăng tốc độ xử lý bằng cách thu nhỏ ảnh
+ Chuẩn hóa kích thước ảnh trong cùng một tập dữ liệu
- Đoạn code minh họa 3 tình huống:
+ Phóng to toàn bộ ảnh lên gấp đôi
+ Phóng to ảnh theo chiều cao và chiều rộng
+ Thu nhỏ ảnh theo tỉ lệ không đều (50% chiều cao, 90% chiều rộng)
* Code chính :
- Phóng to toàn bộ lên gấp đôi 
bdata = nd.zoom(data, 2)
- Phóng to ảnh theo chiều cao và chiều rộng
data2 = nd.zoom(data, (2, 2, 1))
- Thu nhỏ ảnh theo tỉ lệ không đều 
data3 = nd.zoom(data, (0.5, 0.9, 1))
- 1.4 Xoay ảnh
* Mục đích :
- Phép xoay ảnh là một trong các phép biến đổi hình học cơ bản, thường được sử dụng để:
+ Chuẩn hóa góc nhìn của ảnh (ví dụ ảnh bị nghiêng)
+ Tăng cường dữ liệu (data augmentation) trong học máy
+ Chuyển đổi tọa độ trong ảnh vệ tinh, y tế, công nghiệp
+ Phân tích ảnh đa hướng trong thị giác máy
* Code chính : 
d1 = nd.rotate(data, 20)
d2 = nd.rotate(data, 20, reshape=False)
- 1.5 Dilation và Erosion
* Mục đích : 
- Dilation là một phép biến đổi hình thái học (morphological transformation) được sử dụng rộng rãi trong xử lý ảnh nhị phân nhằm:
+ Làm dày các đối tượng trong ảnh nhị phân
+ Lấp các lỗ nhỏ (noise) bên trong vật thể
+ Kết nối các vùng gần nhau, giúp nối các thành phần rời rạc
+ Tăng độ nổi bật của hình dạng để phân tích đặc trưng
* Code chính : 
# Nhị phân hóa ảnh (ngưỡng = 0.5)
binary_data = data > 0.5
# Giãn ảnh 1 lần
d1 = nd.binary_dilation(binary_data)
# Giãn ảnh 3 lần
d2 = nd.binary_dilation(binary_data, iterations=3)
- 1.6 Coordinate Mapping
* Mục đích : 
- Biến dạng ảnh (random warp) là kỹ thuật làm biến dạng không gian của ảnh một cách ngẫu nhiên nhằm:
+ Tăng cường dữ liệu (data augmentation) cho huấn luyện mô hình học sâu (deep learning)
+ Kiểm tra độ ổn định của các thuật toán nhận dạng, phân loại ảnh
+ Mô phỏng biến dạng thực tế do rung máy, méo ống kính, hoặc chuyển động không đều
* Code chính : 
V, H = data.shape  # Kích thước ảnh
# Tạo lưới tọa độ gốc
M = np.indices((V, H))  # M.shape = (2, V, H)
# Biến dạng ngẫu nhiên trong phạm vi [-d, d]
d = 5
q = 2 * d * np.random.rand(*M.shape) - d
# Cộng biến dạng vào lưới tọa độ
mp = M + q
# Lấy giá trị ảnh tại vị trí biến dạng
d1 = nd.map_coordinates(data, mp)
- 1.7 Biến đổi chung (Generic Transformation)
* Mục đích : 
- Phép biến dạng hình học là một kỹ thuật trong xử lý ảnh nhằm:
+ Tạo hiệu ứng thị giác đặc biệt cho ảnh (ví dụ: gợn sóng, biến dạng tròn, xoắn...)
+ Kiểm tra độ ổn định của các thuật toán nhận diện hình dạng
+ Dùng trong augmentation dữ liệu, tăng tính đa dạng ảnh trong học sâu
+ Mô phỏng các hiện tượng tự nhiên như méo ảnh do ống kính, sóng nước, chuyển động vật lý
+ Trong đoạn code này, phép biến dạng dựa trên hàm cos, tạo hiệu ứng ảnh bị uốn sóng theo cả chiều ngang và dọc
* Công thức toán học :
x′ = x+10*cos(10/x​)
y′ = y+10*cos(10/y)
- Với mỗi điểm ảnh ở vị trí đầu ra (x, y), ta truy xuất ngược tới tọa độ (x', y') ở ảnh gốc để lấy giá trị tương ứng (sử dụng nội suy)
* Code chính :  
# Định nghĩa hàm biến dạng hình học dựa trên cos
def GeoFun(outcoord):
    a = 10 * np.cos(outcoord[0] / 10.0) + outcoord[0]  # biến dạng theo chiều dọc
    b = 10 * np.cos(outcoord[1] / 10.0) + outcoord[1]  # biến dạng theo chiều ngang
    return a, b
# Áp dụng biến dạng hình học
d1 = nd.geometric_transform(data, GeoFun)


