# 🫁 Sleep Apnea Warning System (Real-time)

## 🇻🇳 Giới thiệu

Đây là **hệ thống phần mềm theo dõi và cảnh báo ngừng thở khi ngủ** được xây dựng bằng **C/C++**. Hệ thống được thiết kế để xử lý luồng dữ liệu hô hấp liên tục theo thời gian thực, với mục tiêu phân tích và phát hiện ngay lập tức các sự kiện ngừng thở nguy hiểm.

Ứng dụng phù hợp cho:
* Tiền xử lý và phân tích tín hiệu hô hấp (Respiratory signals).
* Tích hợp vào các thiết bị theo dõi sức khỏe tại nhà (Wearables / Non-contact sensors).
* Phục vụ nghiên cứu thuật toán xử lý tín hiệu trong Kỹ thuật Y Sinh.

---

## 🇬🇧 Overview

This is a **Python based real-time sleep apnea warning system** designed to continuously process respiratory data streams. By leveraging advanced signal processing, the software accurately detects apnea events and instantly triggers warnings.

---

## 🧠 Chức năng chính

### 1. 📥 Nhận và Quản lý dữ liệu (Data Handling)
* Khởi tạo hồ sơ và các chỉ số sức khỏe nền (baseline metrics) của bệnh nhân.
* Nhận luồng dữ liệu hô hấp liên tục theo thời gian thực.
* Quản lý bộ nhớ tối ưu bằng mảng và con trỏ (Pointers & Dynamic Arrays) để đảm bảo hệ thống chạy liên tục không bị gián đoạn.

### 2. 🧮 Xử lý tín hiệu với FFT (Fast Fourier Transform)
* Biến đổi tín hiệu hô hấp thô từ **miền thời gian (Time Domain)** sang **miền tần số (Frequency Domain)**.
* Cách ly và trích xuất các dải tần số tương ứng với nhịp thở bình thường của con người.
* Phát hiện sự sụt giảm biên độ đột ngột trong các dải tần số này.

### 3. ⚠️ Đánh giá rủi ro & Cảnh báo (Risk Scoring & Warning)
* Tính toán **Điểm rủi ro (Risk Score)** liên tục dựa trên kết quả đầu ra của FFT.
* Kích hoạt giao thức cảnh báo ngay lập tức nếu Risk Score vượt qua ngưỡng an toàn (thể hiện việc bệnh nhân ngừng thở).
* Ghi log sự kiện để phục vụ đánh giá y khoa sau giấc ngủ.

---

## ⚙️ Cấu trúc Dữ liệu & Thuật toán

### Signal Processing: FFT
Thuật toán cốt lõi giúp hệ thống "hiểu" được tín hiệu hô hấp thay vì chỉ nhìn vào biến động sóng thô.

```c
// Pseudo-code minh họa luồng xử lý cốt lõi
void processRespiratoryData(double* raw_signal, int length) {
    // 1. Áp dụng thuật toán FFT, 
    applyFFT(raw_signal, length, frequency_output);
    Thuật toán tính toán dao động: Dense Optical Flow (Phương pháp Farneback)
    
    // 2. Phân tích dải tần số nhịp thở
    double breathing_amplitude = analyzeBreathingBand(frequency_output);
    
    // 3. Tính điểm rủi ro và cảnh báo
    int risk_score = calculateRisk(breathing_amplitude);
    if (risk_score > DANGER_THRESHOLD) {
        triggerApneaWarning();
    }
}
▶️ Cách chạy chương trình (Hướng dẫn biên dịch)
1. Yêu cầu hệ thống
Trình biên dịch C/C++ (GCC/MinGW) hoặc IDE (Visual Studio, VS Code, CLion).
Tải file mô hình: Invoke-WebRequest -Uri "https://storage.googleapis.com/mediapipe-models/pose_landmarker/pose_landmarker_lite/float16/latest/pose_landmarker_lite.task" -OutFile "pose_landmarker_lite.task"

2. Biên dịch và Chạy
Mở Terminal/Command Prompt tại thư mục dự án và chạy các lệnh sau:
# Biên dịch file mã nguồn
gcc main.c fft_core.c -o sleep_apnea_system.exe -lm

# Chạy chương trình
./sleep_apnea_system.exe

🚀 Hướng phát triển (Future Work)
[ ] Tối ưu hóa thuật toán FFT để giảm thiểu khối lượng tính toán.

[ ] Tích hợp trực tiếp với phần cứng cảm biến (cảm biến SpO2, gia tốc kế).

[ ] Xây dựng giao diện đồ họa (GUI) đơn giản để hiển thị sóng hô hấp và log cảnh báo theo thời gian thực.

👤 Tác giả
Group 2 - ET-E5-01-K70

Chuyên ngành: Kỹ thuật Y Sinh (ET-E5)

Mục đích: Báo cáo môn học & Nghiên cứu ứng dụng xử lý tín hiệu y sinh.

📜 License
Sử dụng cho mục đích học tập và nghiên cứu.
