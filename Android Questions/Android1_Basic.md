# Câu hỏi Android Cơ bản
## 4 Component chính trong Android là gì

1. Activities
Ra lệnh cho UI, sử lý sự kiện người dùng trên màn hình hiện tại
Là màn hình nhỏ, riêng lẻ

2. Services
Xử lý tiến trình chạy nền

3. Broadcast Receivers (nhận dự báo)
Xử lý giao tiếp Android và Người dùng

4. Content Providers
Xử lý dữ liệu, quản lý vấn đề

## UI

### làm sao biết view nào tiêu tốn nhiều tài nguyên ( dùng cái gì)

- Profiler: check thông tin tài nguyên hệ thống (cpu, ram) android khi mở View đó

### Giải thích pt, dp, sp trong Android

- Pt:  1/72 inch kích thước màn hình.
- dp: density independent pixel. Phụ thuộc mật độ điểm ảnh.
- Sp: scale independent pixel. Co theo mật độ điểm ảnh.

### Cho biết công thức quy đổi giữa px và dp

```java
public static float convertDpToPixel(float dp, Context context){
    return dp * ((float) context.getResources().getDisplayMetrics().densityDpi / DisplayMetrics.DENSITY_DEFAULT);
}

public static float convertPixelsToDp(float px, Context context){
    return px / ((float) context.getResources().getDisplayMetrics().densityDpi / DisplayMetrics.DENSITY_DEFAULT);
}

```

## Service là gì

Service trong Android là một thành phần chạy ngầm, không có giao diện, dùng để thực hiện các tác vụ chạy lâu dài như:
✅ Phát nhạc trong nền 🎵
✅ Đồng bộ dữ liệu với server 🔄
✅ Theo dõi vị trí GPS 📍
✅ Xử lý tác vụ khi ứng dụng bị đóng

### Phân biệt Service và IntentService

Service: Có thể chạy vô thời hạn.
IntentService: Tự dừng lại sau khi trả về kết quả, hay hàm **“onHandleIntent”** xử lý xong.

### Phân biệt Service, Intent Service, AsyncTask và Thread.

* Service: Là 1 Android Component. dùng để thực hiện các tác vụ ngầm ở background, ví dụ như chơi nhạc. Chạy trong Main Theard. Nó không có giao diện người dùng (user interface).
* IntentService: là 1 Android Service. Tự dừng lại sau khi trả về kết quả, hay hàm **“onHandleIntent”** xử lý xong.
* Thread: là một luồng thực thi tuần tự trong một chương trình. Thread có thể được coi là một mini-process chạy ở trong main process.
* AsyncTask: Thực hiện các công việc bất đồng bộ. Chạy trong background thread và publish kết quả lên trên UI thread. Mà Không yêu cầu bạn phải xử lý cách các thread hay handler hoạt động.
* Service: Là 1 Android Component, có thể Chạy Ngầm, ngay cả khi người dùng không tương tác. Chạy trong Main Thread.
* AsyncTask: Chạy trong Background Thread, chỉ chạy trong khi người dùng còn tương tác ứng dụng.

### Service Android 8.0

* Background Service: Chạy độc lập, không cần giao diện. Giới hạn tác vụ chạy nền, chỉ chạy vài phút
* Foreground Service: chạy khi có Activity đang chạy, hay kèm Notification

### Foreground và Background Service là gì, Bound service là gì

* Foreground Service: thực hiện hoạt động mà người dùng chú ý. (vd: nghe nhạc)
* Background Service: thực hiện hoạt động chạy ngầm. không cần báo người dùng. Cần có notification
* Bound Service: Component ràng buộc Service để lấy kết quả liên tục (như Client-Server)

### có mấy cách để start service

* bằng class name
* bằng text, dùng tên package + service

### ThreadPool (thuộc java)

Quản lý, điều tiết nhiều Thread

## Intent

### Phân biệt Implicit và Explicit Intent

* Explicit Intent: tường minh, gọi trực tiếp tên ứng dụng
* Implicit Intent: ẩn ý, gọi chung chung, ứng dụng nào chạy thì chạy

## Phân biệt Serializable và Parcelable, cái nào tốt hơn

* Serializable: một interface trong Java. Biến đổi một object thành byte stream để có thể lưu trữ hoặc truyền đi.
* Parcelable: một interface của Android. Giúp biến đổi object thành Parcel để truyền giữa các thành phần của hệ thống. Nhanh hơn.

## ANR là gì, khi nào nó xảy ra: Application not responding

* ANR: Ứng dụng đóng băng, không phải hồi cử chỉ người dùng.

## Liệt kê một số thư viện http đã dùng

* Retrofit, HttpRequest

## Rest APIs là gì, tại sao lại dùng nó

* REST (Representation State Stranfer): một tiêu chuẩn dùng trong việc thết kế các thiết kế API cho các ứng dụng web.
* API (Application Programming Interface): Giao diện lập trình ứng dụng.
* RESTful API: ứng dụng sử dụng REST

## Tại sao Android dùng db SQLite

* Không phải cài đặt
* Không cần mô hình Client - Server
* Chỉ lưu trữ 1 file
* Chiếm ít bộ nhớ
* Hỗ trợ truy vấn SQL

## Android Gradle là gì

* Gradle là một hệ thống tự động build mã nguồn mở

## Làm thế nào để upload 1 file ảnh trong máy Android lên server

* Tạo 1 Restfull Api upload ảnh
* Upload ảnh bằng thư viện Retrofit

## Application là gì

* Application là lớp cơ sở trg Android App.
* Chứa tất cả Component khác (activity, service...)
* Khởi tạo đầu tiên, khi ứng dụng được chạy.

## Context là gì

* Context: là 1 thành phần trong android. Cung cấp thông tin môi trường ứng dụng, truy cập tài nguyên, khởi chạy Activity, Service
* ApplicationContext: ngữ cảnh của Toàn ứng dụng
* BaseContext: lấy ngữ cảnh có thể sử dụng
* getContext trong View: lấy ngữ cảnh tạo View

## Tại sao bytecode không thể chạy được trong Android?

Android sử dụng DVM - Dalvik Virtual Machine và và ART - Android Runtime (>5.0)
Không dùng: JVM (Java Virtual Machine)

## Memory leak xảy ra khi nào?

xảy ra khi bộ nhớ đã cấp phát không được giải phóng, khiến ứng dụng tiêu tốn RAM ngày càng nhiều và có thể bị OutOfMemoryError (OOM).

### Phòng tránh memory leak

✅ Dùng Application Context thay vì Activity Context nếu không cần UI.
✅ Hủy Listener, BroadcastReceiver, Callback trong onDestroy().
✅ Dùng WeakReference hoặc ViewModel để giữ dữ liệu thay vì giữ Activity.
✅ Không giữ tham chiếu đến View trong Background Thread.
✅ Sử dụng LeakCanary để phát hiện Memory Leak nhanh chóng.

# Unit test là gì

Giúp kiểm tra logic code một cách độc lập, giảm lỗi khi phát triển ứng dụng.

## Cách viết code dễ cho unit test

✅ Dùng Dependency Injection (DI) để tránh khởi tạo cứng trong class.
✅ Dùng Interface và Mock Object để kiểm thử dễ dàng hơn.
✅ Tránh dùng Singleton và Static trong class.
✅ Không gọi API hoặc Database trực tiếp trong Unit Test.
✅ Dùng LiveData / Flow trong ViewModel để kiểm thử dễ hơn.
✅ Dùng Mockito hoặc Fake Repository để kiểm thử độc lập.

## 1 màn hình có 4 button để upload hình, và 1 nút Save

* Khi click 4 button thì chọn hình và upload, 4 hình upload chạy song song, khi nhấn nút Save thì làm sao để đợi 4 hình upload xong thì mới gọi API của nút Save

Cách 1:.
Chúng ta có thể sử dụng biến cờ để đếm Finish upload..
khi mỗi lần upload hoàn tất, chúng ta sẽ kiểm tra nó..
.
Cách 2:.
chúng ta có thể sử dụng AsyncTask để Kiểm tra. chúng ta chạy upload trênDoinBackground, sau đó kiểm tra nó trênPostExcute.
.
Cách 3:.
Sử dụng thư viện thứ ba như RxAndroid. .
Đưa mỗi phương thức Upload vào Observable
Dùng phương thức Zip để kiểm tra
.
Cách 4:
Sử dụng Coroutine
Đưa mỗi phương thức upload vào flow
Dùng phương thức Zip để kiểm tra

## dependency injection là gì

Làm giảm sự phụ thuộc của module này trong module kia.
Giảm khởi tạo Lớp trong lớp. Tránh leak memory.
.
Dùng : constructer, setter, interface....
Hay thư viện: hilt, dagger, koin.

## Các bước vẽ trên GG Map

* Tạo Google Player Service Project, lấy API_KEY
* Đăng kí key trong Manifest
* Cài Map Dependencies trong Gradle
* Khởi tạo Map trên View, và kolin file
* Khi Map Ready thì gọi hàm Vẽ

## Các bước Push Notification Firebase

* Tạo project, lấy key trên Firebase Console
* Đăng kí key trong Manifest
* Cài Dependencies trong Gradle
* Tạo file FirebaseMessagingService để hiện thông báo
* Xin quyền hiện Notification trong app trước khi hiện thông báo

## Các bước thanh toán google billing

* Tạo project, lấy key trên Google Cloud Console
* Tạo danh sách sản phẩm
* Đăng kí key trong Manifest
* Cài Dependencies trong Gradle
* Khi User nhấn thanh toán:
  - lấy danh sách sản phẩm về, hiện lên
  - User thanh toán sản phẩm, Kiểm tra: thành công, thất bại, pedding
  - Nếu thành công thì gọi Consume sản phẩm
  - Nếu Pedding thì hiện thông báo, khi mở app Sẽ consume sản phẩm

## 1 số thư viện dependency Injection

Hilt, dagger, koin

## Các câu hỏi khác

### ...Là gì? dùng trong trường hợp nào

Thuật toán tìm đường đi ngắn nhất, qua nhiều điểm
Thuật toán sắp xếp kho hàng

* FragA->add FragB a qua trạng thái nào-> replace B with C B qua trạng thái nào->popC thì C qua trạng thái nào và A như thế nào
* nếu a bằng null gọi m a khác null gọi n ko dùng if
* viết When có trường hợp loại trừ

---

## Reference

[https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb](https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb)

---