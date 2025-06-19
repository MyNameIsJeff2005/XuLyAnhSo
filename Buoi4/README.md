# GIẢI THÍCH CODE TRONG FILE [Buoi4.ipynb](./Buoi4.ipynb)

## Phần bài tập về nhà

### Bài tập 3: Viết chương trình tạo menu cho phép người dùng chọn các phương pháp biến đổi ảnh như sau: (Fast Fourier, Butterworth Lowpass Filter, Butterworth Highpass Filter)

Khi chạy hàm `main()`, thì nó sẽ biểu diễn chạy như sau:

 - Sẽ hiện thanh dòng nhập, bắt mình nhập một phím (`F`, `L`, hoặc `H`) — không nhất thiết phải ghi ra chữ hoa hoặc chữ thường nhờ vào lệnh `.upper()`.

 - Nếu nhập gõ sai ngoài 1 trong 3 kí tự chữ (`F`, `L`, và `H`) sẽ thông báo `Nhập không hợp lệ`

 - Sau đó load từng ảnh từ thư mục `exercise/`

 - Ảnh sẽ được chuyển sang ảnh **xám (grayscale)** bằng `Image.open(path).convert("L")`

 - Chuyển ảnh sang mảng `np.array()` để dễ xử lý giá trị pixel

 - `F`: Biến đổi Fourier nhanh (Fast Fourier Transform) là sẽ hiển thị phổ biên độ trong tần số của ảnh

 - `L`: Bộ lọc Butterworth thông thấp là ảnh làm mờ, bỏ qua chi tiết cao

 - `H`: Bộ lọc Butterworth thông cao sẽ nhấn mạnh biên, làm sắc ảnh theo kiểu trắng đen 

 - Sau khi hoàn thành xử lý xong bởi lệnh `matplotlib`, những hình ảnh đã xử lý sẽ hiển thị dưới phần kết quả đã làm.
