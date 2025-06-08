- Bài 1.1 . Biến đổi cường độ ảnh (Image inverse transformation)
- I. Công nghệ sử dụng : 
+ Sử dụng thư viện Pillow dùng để đọc và xử lý ảnh cở bản với các tính năng như mở ảnh , chuyển ảnh sang ảnh xám
+ Sử dụng thư viện numpy để chuyển ảnh thành mảng số để xử lý ma trận ảnh hoặc cường độ điểm ảnh
+ Sử dụng thư viện matplotlib.pylab để hiển thị ảnh gốc và ảnh sau khi biến đổi
- II. Thuật toán sử dụng : 
+ Biến đổi âm bản ảnh (Image inverse transformation) dựa vào công thức : Ảnh âm bản = 255 - ảnh gốc
- III. Giải thích cách hoạt động
- img = Image.open('balloons_noisy.png').convert('L')
+ img là một biến dùng để lưu trữ ảnh đã chuyển sang chế độ grayscale
+ Image.open('balloons_noisy.png') là dùng để mở ảnh có tên là balloons_noisy.png bằng thư viện PIL
+ .convert('L') là chuyển ảnh sang chế độ grayscale
- im_1 = np.asarray(img)
+ np.asarray(img) là dùng hàm asarray() của thư viện np để chuyển ảnh img thành một mảng array
+ Ảnh img lúc này là ảnh grayscale do đã convert'L' nên kết quả sẽ là 1 mảng 2 chiều
+ im_1 là biến numpy array chứa toàn bộ dữ liệu ảnh dưới dạng số
- im_2 = 255 - im_1
+ im_1 là ảnh grayscale dạng mảng numpy 2 chiều 
+ 255 - im_1 đây là công thức để tạo ảnh âm bản 
+ im_2 là mảng numpy chứa ảnh âm bản của im_1
- plt.figure(figsize=(10, 5))
+ dùng để tạo khung hiển thị ảnh có kích thước rộng 10 , cao 5 đơn vị tính bằng inch
- plt.subplot(1, 2, 1)
- plt.title("Ảnh gốc")
- plt.imshow(im_1, cmap='gray')
+ subplot là lệnh tạo biểu đồ con trong cửa sổ hiển thị
+ tham số 1 , 2 , 1 có nghĩa là 1 hàng 2 cột và đang chọn vị trí ô thứ 1 từ trái sang
+ title là thêm tiêu đề cho biểu đồ subplot
+ imshow(im_1) dùng để hiển thị ảnh im_1 đã là ảnh grayscale ở dạng mảng numpy và để đảm bảo ảnh được hiển thị đúng là ảnh xám thì cmap='gray' dùng để làm điều đó
- plt.subplot(1, 2, 2)
- plt.title("Ảnh âm bản")
- plt.imshow(im_2, cmap='gray')
+ 3 dòng code này tương tự với 3 dòng code trên......
- plt.tight_layout()
- plt.show()
+ tight_layout() dùng để tự động căn chỉnh lại bố cục các subplot hiển thị trong cửa sổ hiển thị sao cho các subplot không bị chồng lấn giữa 2 tiêu đề , trục và các ảnh -> nói chung là dùng để làm cho bố cục nhìn đẹp hơn thoii
+ plt.show() dùng để hiển thị tất cả cửa số chứa ảnh hoặc biểu đồ đã được code trước đó .
- Bài 1.2 . Thay đổi chất lượng ảnh với Power Law (Gamma-Correction)
- I. Công nghệ sử dụng : 
+ Sử dụng thư viện Pillow dùng để đọc và xử lý ảnh cở bản với các tính năng như mở ảnh , chuyển ảnh sang ảnh xám
+ Sử dụng thư viện numpy để chuyển ảnh thành mảng số để xử lý ma trận ảnh hoặc cường độ điểm ảnh
+ Sử dụng thư viện matplotlib.pylab để hiển thị ảnh gốc và ảnh sau khi biến đổi
- II. Thuận toán sử dụng :
+ Sử dụng công thức biến đổi gamma với công thức tổng quát là : s = c * r^y . Trong đó :
- s là giá trị đầu ra sau khi biến đổi
- c là hằng số
- r là giá trị đầu vào 
- y là hệ số gamma
- III. Giải thích cách hoạt động 
- img  = Image.open('balloons_noisy.png').convert('L')
+ img là một biến dùng để lưu trữ ảnh đã chuyển sang chế độ grayscale
+ Image.open('balloons_noisy.png') là dùng để mở ảnh có tên là balloons_noisy.png bằng thư viện PIL
+ .convert('L') là chuyển ảnh sang chế độ grayscale
- im_1 = np.asarray(img)
+ np.asarray(img) là dùng hàm asarray() của thư viện np để chuyển ảnh img thành một mảng array
+ Ảnh img lúc này là ảnh grayscale do đã convert'L' nên kết quả sẽ là 1 mảng 2 chiều
+ im_1 là biến numpy array chứa toàn bộ dữ liệu ảnh dưới dạng số
- gamma = 5 
+ khai báo 1 biến gamma và gán giá trị cho nó = 5 để xử lý ảnh grayscale với giá trị gamma y = 5 , gamma > 1 thì làm ảnh tối đi , gamma < 1 thì làm ảnh sáng lên , tùy theo yêu cầu của đề bài 
- b1 = im_1.astype(float) dòng code này có nghĩa là mình phải ép kiểu float để tính được giá trị chính xác hơn
- b2 = np.max(b1) dòng này tìm giá pixel lớn nhất gán vào b2 (trong khoảng 0-255)
- b3 = b1/b2 dòng này phải chuẩn hóa ảnh về khoảng [0,1] vì ở bài trước thầy có bảo mỗi pixel trong ảnh được chia cho giá trị lớn nhất nên giá trị pixel mới phải nằm trong khoảng [0,1]
- b4 = np.power(b3, gamma) dòng này áp dụng công thức biến đổi gamma với b4 = s , b3 = r , gammy = y 
- c = b4 * 255 khai báo biến c và nhân với 255 để trả ảnh về đúng với dạng gốc
- c1 = c.astype(np.uint8) dùng để ảnh hiển thị đúng định dạng uint8
- d = Image.fromarray(c1) khai báo biến d để tạo ảnh mới từ ma trận c1 sau khi đã biến đổi gamma
- Bài 1.3. Thay đổi cường độ điểm ảnh với Log Transformation
- I. Công nghệ sử dụng 
+ Sử dụng Log Transformation để tăng cường cường độ điểm ảnh ở các vùng tối giúp ảnh có độ tương phản tốt hơn
+ Sử dụng thư viện Pillow dùng để đọc và xử lý ảnh cở bản với các tính năng như mở ảnh , chuyển ảnh sang ảnh xám
+ Sử dụng thư viện numpy để chuyển ảnh thành mảng số để xử lý ma trận ảnh hoặc cường độ điểm ảnh
+ Sử dụng thư viện matplotlib.pylab để hiển thị ảnh gốc và ảnh sau khi biến đổi
- II. Thuật toán sử dụng
+ Sử dụng công thức Log Transformation với công thức tổng quát là : s = c * log(1 + r)
+ Log Transformation giúp tăng tương phản ở vùng có cường độ điểm ảnh thấp
- III. Giải thích cách hoạt động
- img  = Image.open('balloons_noisy.png').convert('L')
+ img là một biến dùng để lưu trữ ảnh đã chuyển sang chế độ grayscale
+ Image.open('balloons_noisy.png') là dùng để mở ảnh có tên là balloons_noisy.png bằng thư viện PIL
+ .convert('L') là chuyển ảnh sang chế độ grayscale
- im_1 = np.asarray(img)
+ np.asarray(img) là dùng hàm asarray() của thư viện np để chuyển ảnh img thành một mảng array
+ Ảnh img lúc này là ảnh grayscale do đã convert'L' nên kết quả sẽ là 1 mảng 2 chiều
+ im_1 là biến numpy array chứa toàn bộ dữ liệu ảnh dưới dạng số
- b1 = im_1.astype(float) ép kiểu sang float để tính toán chính xác hơn
- b2 = np.max(b1) dùng để lấy giá trị pixel lớn nhất để chuẩn hóa công thức Log Transformation
- c = (128.0 * np.log(1 + b1)) / np.log(1 + b2) áp dụng công thức Log với công thức gốc là s = c * log(1 + r) , c ở đoạn code là biến được khai báo , 128 là hằng số c trong công thức gốc , b1 = r và b2 = max(r).
- c1 = c.astype(np.uint8) sau khi xử lý bằng công log , ảnh có thể chứa các giá trị số lẻ , dùng uint8 để ép kiểu để hiển thị đúng định dạng ảnh 
- d = Image.fromarray(c1) dùng để tạo ảnh mới từ ma trận c1


