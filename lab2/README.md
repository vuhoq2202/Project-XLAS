Bài 1.1 . Biến đổi cường độ ảnh (Image inverse transformation)
I. Công nghệ sử dụng : 
- Sử dụng thư viện Pillow dùng để đọc và xử lý ảnh cở bản với các tính năng như mở ảnh , chuyển ảnh sang ảnh xám
- Sử dụng thư viện numpy để chuyển ảnh thành mảng số để xử lý ma trận ảnh hoặc cường độ điểm ảnh
- Sử dụng thư viện matplotlib.pylab để hiển thị ảnh gốc và ảnh sau khi biến đổi
II. Thuật toán sử dụng : 
- Biến đổi âm bản ảnh (Image inverse transformation) dựa vào công thức : Ảnh âm bản = 255 - ảnh gốc
III. Giải thích cách hoạt động
img = Image.open('balloons_noisy.png').convert('L')
-> img là một biến dùng để lưu trữ ảnh đã chuyển sang chế độ grayscale
-> Image.open('balloons_noisy.png') là dùng để mở ảnh có tên là balloons_noisy.png bằng thư viện PIL
-> .convert('L') là chuyển ảnh sang chế độ grayscale
im_1 = np.asarray(img)
-> np.asarray(img) là dùng hàm asarray() của thư viện np để chuyển ảnh img thành một mảng array
*Ảnh img lúc này là ảnh grayscale do đã convert'L' nên kết quả sẽ là 1 mảng 2 chiều
-> im_1 là biến numpy array chứa toàn bộ dữ liệu ảnh dưới dạng số
im_2 = 255 - im_1
-> im_1 là ảnh grayscale dạng mảng numpy 2 chiều 
-> 255 - im_1 đây là công thức để tạo ảnh âm bản 
-> im_2 là mảng numpy chứa ảnh âm bản của im_1
plt.figure(figsize=(10, 5))
-> dùng để tạo khung hiển thị ảnh có kích thước rộng 10 , cao 5 đơn vị tính bằng inch
plt.subplot(1, 2, 1)
plt.title("Ảnh gốc")
plt.imshow(im_1, cmap='gray')
-> subplot là lệnh tạo biểu đồ con trong cửa sổ hiển thị
-> tham số 1 , 2 , 1 có nghĩa là 1 hàng 2 cột và đang chọn vị trí ô thứ 1 từ trái sang
-> title là thêm tiêu đề cho biểu đồ subplot
-> imshow(im_1) dùng để hiển thị ảnh im_1 đã là ảnh grayscale ở dạng mảng numpy và để đảm bảo ảnh được hiển thị đúng là ảnh xám thì cmap='gray' dùng để làm điều đó
plt.subplot(1, 2, 2)
plt.title("Ảnh âm bản")
plt.imshow(im_2, cmap='gray')
-> 3 dòng code này tương tự với 3 dòng code trên......
plt.tight_layout()
plt.show()
-> tight_layout() dùng để tự động căn chỉnh lại bố cục các subplot hiển thị trong cửa sổ hiển thị sao cho các subplot không bị chồng lấn giữa 2 tiêu đề , trục và các ảnh -> nói chung là dùng để làm cho bố cục nhìn đẹp hơn thoii
-> plt.show() dùng để hiển thị tất cả cửa số chứa ảnh hoặc biểu đồ đã được code trước đó .


