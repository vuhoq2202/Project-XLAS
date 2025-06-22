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
- Bài 1.4 Histogram equalization
- I. Công nghệ sử dụng
+ PIL (Python Imaging Library): Thư viện PIL (thông qua module Image) được sử dụng để mở và xử lý ảnh (balloons_noisy.png). Nó chuyển ảnh sang định dạng grayscale (đơn sắc) với chế độ L
+ NumPy: Thư viện numpy được sử dụng để xử lý mảng dữ liệu ảnh (im1), tính toán histogram, và thực hiện các phép toán trên mảng
+ Matplotlib: Thư viện matplotlib.pylab được sử dụng để hiển thị ảnh gốc và ảnh đã được cân bằng histogram
- II. Thuật toán sử dụng 
+ Thuật toán được sử dụng trong code là Histogram Equalization (Cân bằng histogram), một kỹ thuật xử lý ảnh nhằm cải thiện độ tương phản của ảnh. Cụ thể :
Histogram Equalization: Thuật toán này điều chỉnh giá trị cường độ sáng (intensity) của các pixel trong ảnh để phân bố đều hơn trên toàn bộ dải giá trị (từ 0 đến 255 trong ảnh grayscale). Điều này giúp làm nổi bật chi tiết ở những vùng sáng hoặc tối, cải thiện chất lượng hình ảnh, đặc biệt với ảnh có độ tương phản thấp hoặc nhiễu
- III. Giải thích cách hoạt động 
- img = Image.open('balloons_noisy.png').convert('L')
- im1 = np.asarray(img)
+ Code mở file ảnh balloons_noisy.png bằng PIL.Image.open
+ Chuyển ảnh sang chế độ grayscale (đơn sắc) bằng .convert('L'). Ở chế độ này, mỗi pixel được biểu diễn bằng một giá trị từ 0 (đen) đến 255 (trắng)
+ huyển ảnh thành mảng NumPy (im1) để dễ dàng xử lý các giá trị pixel bằng các phép toán
- hist, bins = np.histogram(im1, 256, [0, 255])
- cdf = hist.cumsum()
+ np.histogram(im1, 256, [0, 255]) tính histogram của ảnh với 256 bin (tương ứng với 256 mức xám từ 0 đến 255)
+ hist: Mảng chứa số lượng pixel cho mỗi mức xám
+ bins: Mảng chứa các giá trị biên của bin
+ hist.cumsum() tính hàm phân bố tích lũy (Cumulative Distribution Function - CDF), tức là tổng tích lũy của số lượng pixel từ mức xám 0 đến mức xám hiện tại. CDF cho biết số pixel có giá trị nhỏ hơn hoặc bằng một mức xám nhất định
- cdf_m = np.ma.masked_equal(cdf, 0)
- cdf_m = (cdf_m - cdf_m.min()) * 255 / (cdf_m.max() - cdf_m.min())
- cdf = np.ma.filled(cdf_m, 0).astype('uint8')
+ np.ma.masked_equal(cdf, 0): Loại bỏ các giá trị CDF bằng 0 (nếu có) để tránh lỗi chia cho 0 trong bước chuẩn hóa
+ Công thức (cdf_m - cdf_m.min()) * 255 / (cdf_m.max() - cdf_m.min()) chuẩn hóa CDF về dải giá trị [0, 255] theo như em search được trên chat thì nó phân tích công thức như thế này : cdf_m.min() dùng để trừ đi giá trị nhỏ nhất của CDF để đưa giá trị đó về giá trị nhỏ nhất là 0 , cdf_m.max() - cdf_m.min() dùng để chia hiệu số giữa giá trị lớn nhất và giá trị nhỏ nhất để đưa giá trị về dải [0,1] , * 255 dùng để mở rộng dải giá trị về [0,255]
+ np.ma.filled(cdf_m, 0) dùng để thay thế các giá trị masked bằng 0
+ .astype('uint8') dùng để chuyển đổi kiểu dữ liệu của CDF thành uint8 (số nguyên 8-bit không dấu), phù hợp với định dạng ảnh grayscale
- im2 = cdf[im1]
- im3 = Image.fromarray(im2)
+ cdf[im1] dùng để ánh xạ từng giá trị pixel trong ảnh gốc (im1) sang giá trị mới dựa trên CDF đã chuẩn hóa
+ Image.fromarray(im2) dùng để chuyển mảng im2 (ảnh đã được cân bằng histogram) trở lại định dạng ảnh PIL để hiển thị
- Bài 1.5 Thay đổi ảnh với Contrast Stretching
- Công nghệ sử dụng : 
+ PIL, NumPy, Matplotlib
- Thuật toán sử dụng : 
+ Contrast Stretching (Kéo dãn độ tương phản)
- Giải thích cách hoạt động : 
+ Đọc ảnh và chuyển sang grayscale
+ Tìm giá trị min (a) và max (b) của pixel
+ Chuẩn hóa tuyến tính giá trị pixel sang dải [0, 255]
+ Chuyển mảng đã xử lý thành ảnh
+ Hiển thị ảnh gốc và ảnh đã xử lý
- Bài 1.6.1 Biến đổi ảnh với Fast Fourier
- Công nghệ sử dụng : 
+ PIL, NumPy, SciPy (fftpack), Matplotlib
- Thuật toán sử dụng : 
+ Fast Fourier Transform (FFT) 2D và FFT Shift
- Giải thích cách hoạt động : 
+ Đọc ảnh và chuyển sang grayscale
+ Tính biến đổi Fourier 2D để chuyển ảnh sang miền tần số
+ Dịch chuyển phổ Fourier để đặt tần số 0 vào trung tâm
+ Chuyển đổi phổ thành ảnh grayscale (với ép kiểu uint8)
+ Hiển thị ảnh gốc và phổ Fourier
- Bài 1.6.2 Lọc ảnh trong miền tần suất
- Công nghệ sử dụng : 
+ PIL , NumPy , SciPy , Matplotlib
- Thuật toán sử dụng : 
+ Thuật toán chính được sử dụng trong code là lọc thông thấp (Low-Pass Filtering) trong miền tần số, sử dụng biến đổi Fourier nhanh (FFT) 
+ Fast Fourier Transform (FFT) dùng để chuyển đổi ảnh từ miền không gian sang miền tần số để phân tích các thành phần tần số của ảnh
+ Low-Pass Filter (Butterworth) áp dụng bộ lọc thông thấp Butterworth trong miền tần số để giảm nhiễu (tần số cao) trong ảnh, giữ lại các thành phần tần số thấp
+ Inverse Fast Fourier Transform (IFFT) dùng để chuyển đổi ngược từ miền tần số về miền không gian để tạo ra ảnh đã được lọc
+ FFT Shift 
- Giải thích cách hoạt động 
+ Đọc ảnh và chuyển sang grayscale
- c = abs(scipy.fftpack.fft2(im1))
- d = scipy.fftpack.fftshift(c)
+ scipy.fftpack.fft2(im1) thực hiện biến đổi Fourier nhanh hai chiều (2D FFT) trên mảng ảnh im1, tạo ra mảng phức c biểu diễn phổ tần số của ảnh và
mỗi phần tử trong c chứa thông tin về biên độ và pha của một tần số
+ abs(c) lấy giá trị tuyệt đối (biên độ) của phổ Fourier, loại bỏ thông tin pha
+ scipy.fftpack.fftshift(c) dịch chuyển tần số zero (DC component) từ góc trái trên của mảng c về trung tâm của mảng d
+ Tạo bộ lọc thông thấp Butterworth 
+ Áp dụng bộ lọc và biến đổi ngược
+ Hiển thị kết quả
- Bài tập 1 : 
- Công nghệ sử dụng : 
+ PIL , NumPy , Matplotlib và hệ điều hành os : Thư viện Python để tương tác với hệ thống tệp (như là tạo thư mục , liệt kê tệp)
- Thuật toán sử dụng : 
+ Image Inverse Transformation (Đảo ngược ảnh)
+ Gamma Correction (Hiệu chỉnh Gamma)
+ Log Transformation (Biến đổi Logarit)
+ Histogram Equalization (Cân bằng histogram)
+ Contrast Stretching (Kéo giãn tương phản)
- Giải thích cách hoạt động : 
+ Tạo thư mục output và liệt kê các tệp .png trong thư mục exercise
+ Hiển thị menu với các tương tác như đề bài cho là : I (đảo ngược), G (gamma correction), L (log transformation), H (cân bằng histogram), C (kéo giãn tương phản), E (thoát) và người dùng nhập lựa chọn
+ Xử lý ảnh bằng hàm process_images : 
- Duyệt qua từng ảnh .png -> đọc ảnh và chuyển sang grayscale và áp dụng thuật toán tương ứng như Inverse , Gamma , Log , Histogram Equalization , Contrast Stretching
- Lưu kết quả vào output
- Hiển thị ảnh gốc và ảnh xử lý cạnh nhau bằng Matplotlib
- Quay lại menu cho đến khi người dùng chọn E để thoát
- Bài tập 2 : 
- Công nghệ sử dụng : 
+ os , PIL , NumPy , Matplotlib , scipy.fftpack (biến đổi Fourier nhanh (FFT) và biến đổi ngược (IFFT)) , math
- Thuật toán sử dụng : 
+ Fast Fourier Transform (FFT) : Biến đổi ảnh từ miền không gian sang miền tần số bằng FFT 2D , Công thức: F = fft2(img)
+ Butterworth Lowpass Filter : Bộ lọc thông thấp Butterworth giữ lại các tần số thấp (chi tiết mịn, giảm nhiễu) , Công thức bộ lọc: H(u,v) = 1 / (1 + (D(u,v)/D0)^(2n)), với D0 là tần số cắt, n là bậc (mặc định 1) , làm cho ảnh mịn, giảm chi tiết sắc nét và nhiễu
+ Butterworth Highpass Filter : Bộ lọc thông cao Butterworth giữ lại các tần số cao (cạnh, chi tiết sắc nét) , Công thức bộ lọc: H(u,v) = 1 / (1 + (D0/D(u,v))^(2n)), với D0 và n tương tự , làm cho ảnh nổi bật cạnh loại bỏ các vùng mịn 
- Giải thích cách hoạt động : 
+ Tổng thể gồm thư mục đầu vào , thư mục đầu ra , menu tương tác và xử lý ảnh 
+ Các hàm chính như : 
1. hienthi_anh dùng để hiển thị ảnh gốc và ảnh đã xử lý cạnh nhau bằng Matplotlib với cmap='gray' (grayscale) và sử dụng plt.subplot để tạo hai ô hiển thị
2. Hàm biendoi_fft dùng để thực hiện FFT 2D trên mảng ảnh (fft2) và dịch chuyển tần số thấp về trung tâm (fftshift)
3. Hàm boloc_butterworthlow dùng để thực hiện FFT 2D và dịch chuyển tần số (fft2, fftshift) và tạo bộ lọc thông thấp Butterworth (H) dựa trên khoảng cách D từ tâm và tần số cắt D0 , nhân phổ tần số với bộ lọc (F * H), sau đó biến đổi ngược (ifft2) , chuẩn hóa và trả về ảnh mịn
4. Hàm boloc_butterworthhigh giống hàm boloc_butterworthlow nhưng dùng bộ lọc thông cao Butterworth làm nổi bật các tần số cao (cạnh) và trả về ảnh với chi tiết sắc nét
5. Hàm xu_ly_anh dùng để duyệt qua danh sách ảnh trong exercise , đọc ảnh, chuyển sang grayscale, và áp dụng thuật toán tương ứng (F, L, hoặc H) , ưu ảnh kết quả vào output_fft và cuối cùng hiển thị ảnh gốc và ảnh xử lý
6. Hàm menu_chinh dùng để hiển thị menu và nhận lựa chọn người dùng và gọi xu_ly_anh nếu lựa chọn hợp lệ (F, L, H) hoặc thoát nếu chọn E
7. Luồng code hoạt động : Đầu tiên code khởi chạy hàm menu_chinh tiếp theo người dùng nhập lựa chọn (ví dụ: L cho Butterworth Lowpass) sau đó hàm xu_ly_anh duyệt từng ảnh trong exercise như đọc ảnh chuyển ảnh sang grayscale , áp dụng thuật toán , lưu kết quả vào output_fft và hiển thị ảnh gốc và ảnh xử lý . Cuối cùng quay lại menu cho đến khi người dùng chọn E
- Bài tập 3 : 
- Công nghệ sử dụng : 
+ os , PIL , NumPy , Matplotlib , random
- Thuật toán sử dụng : 
+ Shuffle RGB Channels dùng để tráo ngẫu nhiên thứ tự các kênh màu RGB (Red, Green, Blue) của ảnh
+ Image Inverse với công thức I_out = 255 - I_in dùng để đảo ngược giá trị pixel trên ảnh grayscale
+ Gamma Correction với coogn thức I_out = 255 * (I_in / 255)^γ dùng để điều chỉnh độ sáng/tối của ảnh grayscale
+ Log Transformation với công thức I_out = c * log(1 + I_in), với c = 255 / log(1 + max(I_in)) dùng để nén dải động, làm nổi bật vùng tối
+ Histogram Equalization dùng để chuẩn hóa histogram để tăng độ tương phản bằng cách phân phối lại giá trị pixel dựa trên CDF và tăng cường chi tiết ở vùng có độ tương phản thấp
+ Contrast Stretching với coogn thức I_out = 255 * (I_in - min(I_in)) / (max(I_in) - min(I_in)) dùng để kéo giãn dải giá trị pixel về [0, 255] để tăng độ tương phản
+ Random Transformation dùng để chọn ngẫu nhiên một trong năm thuật toán trên để áp dụng lên ảnh grayscale
- Giải thích cách hoạt động : 
+ Thư mục đầu ra đầu vào giống bài 2 nhưng khác xử lý ảnh , tất cả các ảnh đuôi jpg tự động xử lý bằng cách tráo kênh RGB chuyển sang grayscale, áp dụng một thuật toán ngẫu nhiên, lưu kết quả, và hiển thị
+ Với các hàm chính : 
1. Hàm inverse_image dùng để đảo ngược ảnh grayscale: 255 - pixel để tạo ảnh âm bản
2. Hàm gamma_correction dùng để chuẩn hóa pixel về [0, 1], áp dụng lũy thừa gamma (0.5), nhân lại 255 để điều chỉnh độ sáng tối
3. Hàm log_transformation thì áp dụng công thức logarit với hằng số chuẩn hóa c và nén dải động, làm nổi bật vùng tối
4. Hàm histogram_equalization dùng để tính histogram, CDF, chuẩn hóa CDF về [0, 255], ánh xạ pixel để tăng độ tương phản
5. Hàm contrast_stretching dùng để kéo giãn dải pixel từ [min, max] về [0, 255] cũng để làm tăng độ tương phản
6. Hàm shuffle_rgb dùng để tráo ngẫu nhiên thứ tự kênh RGB và trả về mảng ảnh đã tráo và tên thứ tự
7. Hàm apply_random_transformation dùng để chọn ngẫu nhiên một trong năm thuật toán (I, G, L, H, C) để áp dụng lên ảnh grayscale và trả về ảnh đã xử lý và tên phương pháp
8. Hàm display_images dùng để hiển thị ảnh RGB đã tráo kênh và ảnh grayscale đã xử lý cạnh nhau bằng Matplotlib
9. Hàm process_rgb_images dùng để duyệt từng ảnh jpg cụ thể đọc ảnh và chuyển ảnh sang RGB , tráo ngẫu nhiên RGB , chuyển ảnh RGB đã tráo sang grayscale và ấp dùng 1 thuật toán ngẫu nhiên lên ảnh grayscale sau đó lưu ảnh kết quả vào output_rgb cuối cùng hiển thị ảnh RGB đã tráo và ảnh xử lý
- Bài tập 4 : 
- Công nghệ sử dụng : 
+ os , PIL , NumPy , Matplotlib , scipy.fftpack (biến đổi Fourier nhanh (FFT) và biến đổi ngược (IFFT)) , math , random và định dạng ảnh .png, .jpg, .jpeg, xử lý ảnh RGB và grayscale ('L')
- Thuật toán sử dụng : 
+ Shuffle RGB Channels tráo ngẫu nhiên thứ tự kênh RGB
+ Fast Fourier Transform (FFT) dùng để biến đổi ảnh grayscale từ miền không gian sang miền tần số bằng FFT 2D với công thức F = fft2(img) để hiển thị phổ tần số của ảnh
+ Butterworth Lowpass Filter + Min Filter là bộ lọc thông thấp Butterworth giữ tần số thấp (làm mịn ảnh) với công thức H(u,v) = 1 / (1 + (D(u,v)/D0)^(2n)), D0 = 30, n = 1 và áp dụng thêm MinFilter (3x3) để lấy giá trị pixel nhỏ nhất trong vùng lân cận để làm mịn ảnh, giảm nhiễu và chi tiết sắc nét
+ Butterworth Highpass Filter + Max Filter là bộ lọc thông cao Butterworth giữ tần số cao (làm nổi bật cạnh) với công thức H(u,v) = 1 / (1 + (D0/D(u,v))^(2n)), D0 = 30, n = 1 và áp dụng thêm MaxFilter (3x3) để lấy giá trị pixel lớn nhất trong vùng lân cận để làm nổi bật cạnh và chi tiết
+ Random Transformation dùng để chọn ngẫu nhiên một trong ba phương pháp: FFT, Butterworth Lowpass + Min, hoặc Butterworth Highpass + Max
- Giải thích cách hoạt động : 
+ Tổng thể đầu ra và đầu vào giống bài 3
+ Với các hàm chính : 
1. Hàm hienthi_anh dùng để hiển thị ảnh RGB đã tráo kênh và ảnh grayscale xử lý cạnh nhau bằng Matplotlib và sử dugnj cmap='gray' cho ảnh xử lý
2. Hàm biendoi_fft dùng để thực hiện FFT 2D, dịch chuyển tần số thấp về trung tâm (fftshift) và trả về phổ tần số dưới dạng ảnh grayscale
3. Hàm boloc_butterworthlow dùng để thực hiện FFT 2D, tạo bộ lọc thông thấp Butterworth dựa trên khoảng cách D và D0 và nhân phổ tần số với bộ lọc, biến đổi ngược (ifft2) để chuẩn hóa và trả về ảnh mịn
4. Hàm boloc_butterworthhigh tương tự boloc_butterworthlow nhưng tạo bộ lọc thông cao Butterworth để trả về ảnh với cạnh nổi bật
5. Hàm shuffle_rgb dùng để tráo ngẫu nhiên thứ tự kênh RGB và trả về mảng ảnh đã tráo và tên thứ tự
6. Hàm process_rgb_fft_images duyệt qua từng ảnh cụ thể như : đọc ảnh và chuyển ảnh sang RGB tiếp theo tráo ngẫu nhiên kênh RGB và chuyển ảnh RGB đã tráo sang grayscale cuối cùng chọn ngẫu nhiên một phương pháp như : FFT dùng để tạo phổ tần số , Butterworth Low + Min: Làm mịn bằng bộ lọc thông thấp, thêm MinFilter , Butterworth High + Max: Làm nổi cạnh bằng bộ lọc thông cao, thêm MaxFilter và lưu ảnh kết quả vào output_fft_rgb , hiển thị ảnh RGB đã tráo và ảnh xử lý