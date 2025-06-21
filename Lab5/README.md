# Giải thích các bài tập thực hành Lab 3 - Biến đổi hình học

## Bài 1: Biến đổi tịnh tiến và hiệu ứng sóng cho quả kiwi

Ở bài này, khi chạy bởi dòng lệnh ta sẽ thấy:
- Đọc ảnh gốc, sau đó cắt ra vùng chứa quả kiwi.
- Dùng hàm `nd.shift` để tịnh tiến quả kiwi 50 pixel sang phải và 30 pixel xuống dưới.
- Tạo hiệu ứng sóng bằng cách biến đổi tọa độ điểm ảnh với hàm sin, sử dụng `nd.map_coordinates`.
- Cuối cùng, in và lưu ảnh kết quả ra file `kiwi_wave.jpg` và hiển thị lên màn hình.


## Bài 2: Đổi màu gradient và ghép ảnh với alpha channel

Ở bài này, khi chạy bởi các dòng lệnh ta sẽ thấy:
- Đọc ảnh đu đủ và dưa hấu, tạo mask để xác định vùng quả (phân biệt với nền trắng). "ở đây là file `dudu.jpg` và `duahau.jpg`"
- Đổi màu quả đu đủ thành gradient từ đỏ sang xanh lá bằng cách thay đổi giá trị màu theo chiều dọc bởi hai dòng lệnh:
    - `color = [255 * (1-t), 255 * t, 0]` và
    - `np.dstack([dudu[..., :3], mask_dudu.astype(np.uint8) * 255])`
- Đổi màu dưa hấu thành gradient từ vàng sang tím cũng theo chiều dọc cũng như bởi dòng lệnh: 
    - `color = [255 * (1-t) + 128 * t, 255 * (1-t), 128 * t]` và
    - `np.dstack([duahau[..., :3], mask_duahau.astype(np.uint8) * 255])`
- Ghép hai quả lên một nền trong suốt (canvas alpha channel), mỗi quả một bên.
- Lưu ảnh kết quả dưới dạng PNG để giữ được độ trong suốt.
(đổi thành tên file là `fruit_composite.png` sau khi xử lý chạy chung một ảnh thay vì 2 ảnh tách rời theo yêu cầu bài)


## Bài 3: Xoay, phản chiếu và ghép ảnh núi & thuyền

Ở bài này,khi chạy bởi các dòng lệnh ta sẽ thấy:
- Đọc ảnh núi và thuyền. (ở đây là file thuyền là `thuyen.jpg` và núi là `nui.png`)
- Xoay mỗi ảnh 45 độ bằng `nd.rotate`, giữ nguyên kích thước gốc (`reshape=False`).
- Tạo hiệu ứng phản chiếu dọc bằng cách lật ngược ảnh theo chiều dọc (`np.flipud`).
- Ghép cả hai ảnh gốc và hai ảnh phản chiếu lên một canvas trắng lớn.
- Lưu ảnh kết quả ra file. 
(theo như đề bài thì dòng lệnh `iio.imsave()` để chuyển sang file ảnh `mountain_boat_mirror.jpg` thay vì chuyển 2 ảnh tách rời không như theo yêu cầu bài)


## Bài 4: Phóng to và uốn cong ảnh ngôi chùa

Ở bài này,khi chạy bởi các dòng lệnh ta sẽ thấy
- Đọc ảnh ngôi chùa. (ở đây là file `pagoda.jpg`)
- Phóng to ảnh lên 5 lần bằng `nd.zoom`.
- Định nghĩa một hàm biến đổi hình học (warp) sử dụng hàm sin để làm cho ảnh bị uốn cong theo trục ngang.
- Áp dụng biến đổi này với `nd.geometric_transform`.
- Lưu ảnh kết quả ra file.
(cũng như các bài trên áp dụng vào lệnh `iio.imsave()` để lưu lại ảnh dưới dạng ảnh "tùy thuộc dạng ảnh file" sau xử lý chạy thành tên file là: `pagoda_warped.jpg` chương trình theo yêu cầu bài)


## Bài 5: Menu tương tác các phép biến đổi hình học

Ở bài này, ta sẽ:
- Hiển thị danh sách ảnh để người dùng chọn.
- Hiển thị menu các phép biến đổi: tịnh tiến, xoay, phóng to/thu nhỏ, làm mờ Gaussian, biến đổi sóng.
- Nhập các thông số cần thiết cho từng phép biến đổi (ví dụ: số pixel tịnh tiến, góc xoay, hệ số zoom, sigma làm mờ, biên độ sóng).
- Thực hiện phép biến đổi tương ứng bằng các hàm của `scipy.ndimage`.
- Hiển thị kết quả lên màn hình.