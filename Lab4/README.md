# GIẢI THÍCH CODE TRONG FILE [BuoiLab2.ipynb](./BuoiLab2.ipynb)

## Phần bài tập về nhà

### Bài tập 3: Viết chương trình tạo menu cho phép người dùng chọn các phương pháp biến đổi ảnh như sau: (Fast Fourier, Butterworth Lowpass Filter, Butterworth Highpass Filter)

Khi chạy hàm `main()`, thì nó sẽ biểu diễn chạy như sau:

 - Sẽ hiện thanh dòng nhập, bắt mình nhập một phím (`F`, `L`, hoặc `H`) — không nhất thiết phải ghi ra chữ hoa hoặc chữ thường nhờ vào lệnh `.upper()`.

 - Nếu nhập gõ sai ngoài 1 trong 3 kí tự chữ (`F`, `L`, và `H`) sẽ thông báo `Nhập không hợp lệ`

 - Sau đó load từng ảnh từ thư mục `exercise/`

 - Ảnh sẽ được chuyển sang ảnh **xám (grayscale)** bằng `Image.open(path).convert("L")`

 - Chuyển ảnh sang mảng `np.array()` để dễ xử lý giá trị pixel

 - Sử dụng hàm `def fast_fourier_transform()` và `def butterworth_filter()` chứa các phương thức dùng để xử lý ảnh trong miền tần số theo từng phím tương ứng:

   - `F`: Biến đổi Fourier nhanh (Fast Fourier Transform) là sẽ hiển thị phổ biên độ trong tần số của ảnh

   - `L`: Bộ lọc Butterworth thông thấp là ảnh làm mờ, bỏ qua chi tiết cao

   - `H`: Bộ lọc Butterworth thông cao sẽ nhấn mạnh biên, làm sắc ảnh theo kiểu trắng đen 

 - Sau khi hoàn thành xử lý xong bởi lệnh `matplotlib`, những hình ảnh đã xử lý sẽ hiển thị dưới phần kết quả đã làm.


### Bài tập 4: Viết chương trình thay đổi thứ tự màu RGB của ảnh trong thư mục exercise và sử dụng ngẫu nhiên một trong các phép biến đổi ảnh (Image inverse transformation, Gamma-Correction, Log Transformation, Histogram equalization, Contrast Stretching).

Khi chạy `process_images()`, quá trình sẽ diễn ra như sau:

 - Đầu tiên sẽ lượt qua tất cả ảnh có trong `exercise/`  

 - Dùng vòng lặp `if` sẽ kiểm tra định dạng file ảnh (`jpg`, `jpeg`, `png`), nếu chúng không định dạng được dạng file ảnh sẽ không thực hiện phần kế tiếp coi như sẽ xóa vòng lặp và kết thúc ngay

 - Trường hợp đã định dạng được sẽ qua đọc ảnh từ đường dẫn từ dòng lệnh `img = iio.imread(path)`

 - Nếu ảnh là ảnh xám (grayscale), chuyển sang RGB bằng cách nhân bản kênh theo dòng lệnh `if img.ndim == 2:` và `img = np.stack([img]*3, axis=-1)`

 - Xáo trộn ngẫu nhiên thứ tự `shuffle_rgb()` các kênh màu RGB thay vì chỉ hiện một thể loại theo yêu cầu của đề bài 

 - Sau đó chọn, sử dụng lệnh `apply_random_transformation()` để áp dụng ngẫu nhiên một phương pháp biến đổi ảnh

 - Hoàn thành xử lý hoán đổi sẽ hiển thị `matplotlib` và sẽ trình bày dưới kết quả thực hiện:
     - `plt.imshow(transformed)`  
     - `plt.title(f"{filename}")`  
     - `plt.axis('off')`  
     - `plt.show()`


