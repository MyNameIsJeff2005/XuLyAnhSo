# Nhập Môn Xử Lý Ảnh Số - Lab 5  
## Nhận Dạng Đối Tượng & Đặc Trưng Hình Dạng

**Sinh viên thực hiện:** Nguyễn Hồng Thanh
**MSSV:** 2374802010455 
**Môn học:** Nhập môn Xử lý ảnh số  
**Giảng viên:** Đỗ Hữu Quân

---

## Giới thiệu

Ở Lab 5 này, mình sẽ thực hành các kỹ thuật nhận dạng đối tượng và phân tích đặc trưng hình dạng trong ảnh nhị phân. Đây là bước quan trọng để máy tính có thể "nhìn" và phân biệt các vật thể khác nhau trong ảnh.

**Công nghệ sử dụng:**  
- Python: Ngôn ngữ chính  
- OpenCV: Xử lý ảnh nâng cao  
- Pillow (PIL): Đọc, chuyển đổi, và lưu ảnh  
- NumPy: Xử lý ảnh dưới dạng mảng số học  
- Matplotlib: Hiển thị ảnh trực quan  
- Scikit-image: Các hàm phân tích đặc trưng

## Nội dung chính & ý nghĩa
### 1. Phát hiện và đếm số lượng đối tượng
- **Mục đích:**  
  Mình dùng các hàm phân vùng và gán nhãn (labeling) để xác định từng đối tượng riêng biệt trong ảnh nhị phân, sau đó đếm số lượng đối tượng.
- **Ý nghĩa:**  
  Đây là bước đầu tiên để phân tích ảnh, ví dụ: đếm số tế bào, số vật thể, số đồng xu...

### 2. Tính toán các đặc trưng hình dạng
- **Mục đích:**  
  Sau khi đã tách được từng đối tượng, mình sẽ tính các đặc trưng như: diện tích (area), chu vi (perimeter), tâm (centroid), hình chữ nhật bao quanh (bounding box), độ tròn (circularity), tỷ lệ dài/rộng...
- **Ý nghĩa:**  
  Các đặc trưng này giúp mình phân biệt các loại đối tượng, nhận dạng hình dạng, hoặc phân loại vật thể.

### 3. Vẽ và hiển thị kết quả
- **Mục đích:**  
  Mình sẽ vẽ các bounding box, centroid, hoặc chú thích lên ảnh để trực quan hóa kết quả nhận dạng.
- **Ý nghĩa:**  
  Giúp mình kiểm tra lại kết quả xử lý và dễ dàng trình bày cho người khác.

## Cấu trúc file

```
├── BuoiLab5.ipynb      
├── image.png        
├── README.md       
```

## Hướng dẫn
1. **Cài đặt môi trường**  
   Cài Python, sau đó cài các thư viện:
   ```
   pip install pillow numpy matplotlib imageio opencv-python scikit-image
   ```
2. **Chạy notebook**  
   - Mở Jupyter Notebook trên VSCode/Colab  
   - Chạy từng cell để xem kết quả của các thuật toán  
   - Nếu có lỗi không tìm thấy ảnh, đảm bảo file ảnh đã được đặt đúng vị trí
3. **Tùy chỉnh tham số**  
   - Thay đổi ngưỡng phân vùng, hoặc thử với các ảnh khác để quan sát tác động thực tế
