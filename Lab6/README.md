# Nhập Môn Xử Lý Ảnh Số - Lab 4  
## Phân Vùng Ảnh & Biến Đổi Đối Tượng Nhị Phân

**Sinh viên thực hiện:** Example  
**MSSV:** Example  
**Môn học:** Nhập môn Xử lý ảnh số  
**Giảng viên:** Đỗ Hữu Quân

---

## Giới thiệu

Bài lab này giúp mình thực hành các phương pháp phân vùng ảnh (segmentation) và các phép biến đổi hình thái học (morphological operations) trên ảnh nhị phân. Đây là các kỹ thuật quan trọng để tách đối tượng, làm sạch nhiễu và phân tích cấu trúc trong ảnh số.

**Công nghệ sử dụng:**  
- Python: Ngôn ngữ chính  
- OpenCV: Xử lý ảnh nâng cao  
- Pillow (PIL): Đọc, chuyển đổi, và lưu ảnh  
- NumPy: Xử lý ảnh dưới dạng mảng số học  
- ImageIO: Đọc file ảnh  
- Matplotlib: Hiển thị ảnh trực quan  
- Scikit-image: Các hàm phân ngưỡng và xử lý ảnh

---

## Chi tiết các phương pháp & công thức

### 1. Phân vùng theo histogram

#### a. Phương pháp Otsu

**Mục đích:**  
- Tự động tìm ngưỡng tối ưu để tách nền và đối tượng dựa trên histogram của ảnh xám.

**Ý nghĩa:**  
- Giúp mình tách đối tượng ra khỏi nền mà không cần chọn ngưỡng thủ công.

**Code chính:**  
```python
from skimage.filters.thresholding import threshold_otsu

data = Image.open('dalat.jpg').convert('L')
a = np.asarray(data)
thres = threshold_otsu(a)
b = a > thres
b = Image.fromarray(b)
plt.imshow(b)
plt.show()
```

---

#### b. Phương pháp Adaptive Thresholding

**Mục đích:**  
- Tính ngưỡng cục bộ cho từng vùng nhỏ trong ảnh, phù hợp với ảnh có ánh sáng không đều.

**Ý nghĩa:**  
- Giúp mình phân vùng tốt hơn khi ảnh bị bóng hoặc có vùng sáng/tối khác nhau.

**Code chính:**  
```python
from skimage.filters import threshold_local

data = Image.open('exercise/dalat.jpg').convert('L')
a = np.array(data)
b = threshold_local(a, 39, offset=10)
b = Image.fromarray(b)
plt.imshow(b)
plt.show()
```

---

### 2. Phân vùng theo region (Watershed)

**Mục đích:**  
- Tách các vùng đối tượng dựa trên hình dạng và khoảng cách, thường dùng để tách các vật thể dính liền nhau.

**Ý nghĩa:**  
- Mình có thể tách các vật thể sát nhau thành từng vùng riêng biệt.

**Code chính:**  
```python
import cv2
from scipy.ndimage import label

data = cv2.imread('exercise/dalat.jpg')
a = cv2.cvtColor(data, cv2.COLOR_BGR2GRAY)
thresh, b1 = cv2.threshold(a, 0, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)
b2 = cv2.erode(b1, None, iterations=2)
dist_trans = cv2.distanceTransform(b2, 2, 3)
thresh, dt = cv2.threshold(dist_trans, 1, 255, cv2.THRESH_BINARY)
labelled, ncc = label(dt)
labelled = labelled.astype(np.int32)
cv2.watershed(data, labelled)
b = Image.fromarray(labelled)
plt.imshow(b)
plt.show()
```

---

### 3. Biến đổi đối tượng ảnh nhị phân (Morphological Operations)

#### a. Dilation (Giãn nở)

**Mục đích:**  
- Làm to vùng trắng (đối tượng), lấp đầy lỗ nhỏ hoặc nối các vùng gần nhau.

**Code chính:**  
```python
data = Image.open('Ball.gif').convert('L')
b = nd.binary_dilation(data, iterations=50)
c = Image.fromarray(b)
plt.imshow(c)
plt.show()
```

---

#### b. Opening (Mở)

**Mục đích:**  
- Xóa nhiễu nhỏ, giữ lại hình dạng chính của đối tượng.

**Code chính:**  
```python
s = [[0,1,0], [1,1,1], [0,1,0]]
b = nd.binary_opening(data, structure=s, iterations=25)
c = Image.fromarray(b)
plt.imshow(c)
plt.show()
```

---

#### c. Erosion (Co lại)

**Mục đích:**  
- Làm nhỏ vùng trắng, loại bỏ các điểm nhỏ lẻ.

**Code chính:**  
```python
s = [[0,1,0], [1,1,1], [0,1,0]]
b = nd.binary_erosion(data, structure=s, iterations=50)
c = Image.fromarray(b)
plt.imshow(c)
plt.show()
```

---

#### d. Closing (Đóng)

**Mục đích:**  
- Lấp đầy các lỗ nhỏ bên trong đối tượng, nối các vùng trắng gần nhau.

**Code chính:**  
```python
s = [[0,1,0], [1,1,1], [0,1,0]]
b = nd.binary_closing(data, structure=s, iterations=25)
c = Image.fromarray(b)
plt.imshow(c)
plt.show()
```

---

## Cấu trúc file

```
├── BuoiLab4.ipynb      
├── Ball.gif        
├── dalat.jpg
├── exercise/
│   └── dalat.jpg
├── README.md       
```

---

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
   - Thay đổi số lần lặp, cấu trúc kernel, hoặc ngưỡng trong từng cell để quan sát tác động thực tế

---

## Tài liệu tham khảo

- Digital Image Processing - Rafael C. Gonzalez
- Scikit-image: Image processing in Python
- OpenCV Documentation
- Slide bài giảng Nhập môn Xử lý ảnh số -