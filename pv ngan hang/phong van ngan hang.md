## tối ưu bộ nhớ như thế nào?

* Không giữ reference đến `Activity/Context` quá lâu (tránh dùng static, dùng `applicationContext` hoặc `WeakReference`)
* Dọn dẹp resource đúng lifecycle (`onDestroy`, `onDestroyView`) (unregister receiver, remove callback / listener, clear binding)
* Dùng component lifecycle-aware như `ViewModel`, `lifecycleScope` để tự động huỷ task

# xử lý tình trạng Memory Leak

* Tránh leak từ `Handler`, `Thread`, `Listener`, (tránh giữ reference của android reference, dùng weak reference)
* Sử dụng tool như **LeakCanary**, check profiler, để phát hiện memory leak

👉 **Tóm lại:** *Quản lý lifecycle đúng + không giữ reference thừa + cleanup đầy đủ là cách chính để tránh Memory Leak.*

## Ứng dụng nhiều tính năng chạy ngầm hoặc cần load data liên tục

* ✅ **Dùng WorkManager / Coroutine thay vì chạy liên tục**
  * Tránh giữ thread sống lâu → giảm tốn RAM & pin

* ✅ **Áp dụng caching**
  * Lưu data vào **Room / memory cache**
  * Chỉ gọi API khi cần (cache first → network later)

* ✅ **Optimize gọi API**
  * Dùng **debounce / throttle**
  * Polling có kiểm soát (interval hợp lý, không spam)

* ✅ **Lifecycle-aware**
  * Dùng `lifecycleScope`, `ViewModel`
  * Auto stop khi UI bị destroy

* ✅ **Sử dụng Paging**
  * Load data theo trang → tránh load toàn bộ 1 lần

* ✅ **Giới hạn background task**
  * Không chạy quá nhiều task song song
  * Ưu tiên queue (WorkManager)

👉 *Giảm load liên tục bằng cache + tối ưu gọi API + dùng background task có kiểm soát và lifecycle-aware để tiết kiệm tài nguyên.* 🚀

## Làm sao để bảo mật data lưu dưới local (SharePreferences/Keychain)?

* ✅ Không lưu plain text → dùng mã hoá (Encryption)
* ✅ Dùng thư viện có sẵn:
  * Android: `EncryptedSharedPreferences`, `Keystore`
  * iOS: `Keychain`
* ✅ Không lưu thông tin nhạy cảm như PIN/password/token lâu dài
* ✅ Dùng **Android Keystore System** để lưu key an toàn, không hardcode key trong app
* ✅ Enable Proguard/R8 để giảm reverse engineering
* ✅ Có thể kết hợp thêm data expiry / refresh token
* **Biometric Authentication:** xác thực bằng sinh trắc học trước khi gọi API thanh toán.

👉 **Tóm lại:** *Luôn mã hoá dữ liệu + dùng secure storage (Keystore/Keychain) + không lưu dữ liệu nhạy cảm dạng plain text.*

## triển khai SSL Pinning

  * Dùng để đảm bảo app chỉ giao tiếp với server hợp lệ
  * Em thường dùng cấu hình **CertificatePinner trong OkHttpClient**
  * chống tấn công MITM attack (Man-in-the-Middle) (fake certificate)

## chống Root/Jailbreak cho app

  * Kiểm tra thiết bị bị root/jailbreak bằng cách:
    * Check file hệ thống (`/system/xbin/su`)
    * Check root package (Magisk, SuperSU, Frida)
    * Kiểm tra root **RootBeer (Android)**
    * Kiểm tra bảo bật bằng **Play Integrity API** (máy đã root, mở khóa bootloader) 
  * Nếu phát hiện → hạn chế tính năng hoặc block app

👉 **Tóm lại:** *SSL Pinning bảo vệ data khi truyền, còn Root/Jailbreak giúp giảm rủi ro từ môi trường thiết bị không an toàn.*

## Phân biệt giữa MVVM và Clean Architecture. 

**MVVM và Clean Architecture khác nhau ở mục đích và phạm vi áp dụng:**

* ✅ **MVVM (Model – View – ViewModel):**
  * Là **pattern cho tầng UI**
  * Giúp tách UI (`Activity/Fragment`) khỏi logic hiển thị
  * `ViewModel` xử lý data, expose qua `LiveData/Flow`
  * 👉 Tập trung vào **presentation layer**

* ✅ **Clean Architecture:**
  * Là **kiến trúc tổng thể cho toàn bộ app**
  * Chia thành nhiều layer:
    * Presentation (UI, ViewModel)
    * Domain (UseCase, business logic)
    * Data (Repository, API, DB)
  * Nguyên tắc: **Dependency chỉ đi từ ngoài → trong**
  * 👉 Tập trung vào **tách biệt logic, dễ test, dễ scale**

👉 *MVVM là pattern cho UI, còn Clean Architecture là kiến trúc tổng thể — thường sẽ dùng MVVM bên trong Clean Architecture.* 🚀


## Tại sao ứng dụng quy mô lớn như Mobile Banking lại cần Modularization (chia nhỏ module)?"

* ✅ **Dễ maintain & scale**
  * Code tách nhỏ → dễ sửa, dễ thêm feature, không ảnh hưởng nhau

* ✅ **Tăng tốc build**
  * Chỉ build lại module thay đổi → giảm thời gian build

* ✅ **Tái sử dụng code**
  * Module có thể dùng lại cho nhiều feature hoặc project khác

* ✅ **Phân tách rõ trách nhiệm**
  * Ví dụ: `core`, `data`, `feature-login`, `feature-home`

* ✅ **Dễ test & debug**
  * Test độc lập từng module → phát hiện lỗi nhanh hơn

* ✅ **Team làm việc song song tốt hơn**
  * Mỗi team phụ trách 1 module → giảm conflict code

👉 *Modularization giúp app dễ quản lý, build nhanh, dễ mở rộng và hỗ trợ teamwork tốt hơn.* 🚀

* Chia dự án thành các dynamic feature modules
* core/data/domain/feature modules
* Module Chuyển Tiền và Module Tiết Kiệm
* giao tiếp thông qua một Navigator trung gian (Dependency Injection / Interface Routing)

## **Architecture Pattern:** Nắm vững **MVVM** hoặc **MVI** kết hợp với **Clean Architecture**. 

Hãy chuẩn bị giải thích luồng đi của dữ liệu từ RemoteDataSource -> Repository -> UseCase/Interactor -> ViewModel -> UI (Activity/Fragment/Compose).

## **Dependency Injection (DI):** Khả năng cao họ dùng **Hilt** hoặc **Koin**. 

Bạn cần giải thích được scope của Component (ví dụ: @Singleton, @ActivityRetainedScoped cho ViewModel) để chứng minh mình hiểu cách quản lý vòng đời của Object nhằm tránh rò rỉ bộ nhớ.

## **Kotlin Coroutines & Flow:** App bank load dữ liệu liên tục và cần xử lý song song nhiều tác vụ ngầm.

   * Phân biệt được StateFlow và SharedFlow (khi nào dùng để lưu trạng thái UI, khi nào dùng để bắn event một lần như hiển thị Dialog lỗi).
   * Cách switch luồng (Dispatchers.IO cho API/DB, Dispatchers.Main cho UI, Dispatchers.Default cho tính toán nặng như parse chuỗi JSON danh sách lịch sử giao dịch lớn).

## **Memory Leak (Rò rỉ bộ nhớ):** Giải thích cách dùng **LeakCanary** để phát hiện leak. 

Các lỗi kinh điển như giữ reference của Context/View trong một Thread chạy ngầm/Coroutine không được cancel khi Activity đã bị destroy (onDestroy()).

## **Xử lý dữ liệu nhạy cảm của UI:** 

Khi người dùng bấm nút Home để ẩn app xuống Background, làm sao để màn hình biến thành một màu trắng hoặc logo Bank để tránh bị chụp trộm màn hình (chụp snapshot hệ thống)? (Trả lời: Dùng LayoutParam.FLAG_SECURE trong Activity).


# Nhóm câu hỏi Tình huống (Behavioral)

## “Nếu sát ngày Go-live (realease sản phẩm) mà bên Kiểm thử (QA/QC) phát hiện ra một lỗi nghiêm trọng, nhưng PO vẫn ép phải deploy đúng hạn để chạy chiến dịch Marketing, em sẽ xử lý thế nào?”

* ✅ **Đánh giá mức độ ảnh hưởng (impact)**
  * Bug có ảnh hưởng đến user chính không? (crash, mất data, security)
  * Xác định rõ mức độ nghiêm trọng và phạm vi

* ✅ **Trao đổi rõ với PO/Stakeholder**
  * Trình bày rủi ro nếu release (ảnh hưởng user, brand, doanh thu)
  * Đưa ra lựa chọn: delay, fix nóng (hotfix), hoặc workaround

* ✅ **Đề xuất giải pháp thay thế**
  * Tắt feature lỗi bằng **feature flag**
  * Giới hạn rollout (staged rollout)
  * Release tạm version ổn định trước

* ✅ **Nếu buộc phải release**
  * Chuẩn bị sẵn **hotfix plan**
  * Monitor kỹ (Crashlytics, logs)
  * Sẵn sàng rollback nếu cần

👉 *Ưu tiên chất lượng & trải nghiệm user, communicate rõ rủi ro và luôn có phương án giảm thiểu (feature flag, hotfix, rollout).* 🚀


## “Kể lại một lần em và Tech Lead hoặc đồng nghiệp bất đồng ý kiến về giải pháp kiến trúc (Architecture). Em đã thuyết phục họ hoặc giải quyết xung đột đó ra sao?”

**Em từng có trường hợp bất đồng với Tech Lead về cách tổ chức kiến trúc (MVVM vs Clean + UseCase).**

* ✅ **Vấn đề:**
  * Em đề xuất dùng **Clean Architecture rõ ràng (UseCase, Domain layer)**
  * Tech Lead muốn giữ **MVVM đơn giản** để giảm độ phức tạp và nhanh tiến độ

* ✅ **Cách em xử lý:**
  * Không tranh luận cảm tính → **đưa ra dữ liệu cụ thể**
    * So sánh: maintain, testability, scale về sau
  * Đưa **use case thực tế của project**
    * Feature có thể mở rộng nhiều → Clean sẽ lợi hơn
  * Đề xuất **giải pháp trung hòa**
    * Áp dụng Clean cho module lớn/critical
    * Module nhỏ vẫn dùng MVVM đơn giản

* ✅ **Kết quả:**
  * Team thống nhất hybrid approach
  * Vừa đảm bảo tiến độ, vừa giữ được kiến trúc tốt ở phần quan trọng

👉 *Khi bất đồng, em luôn dựa vào data + use case thực tế và hướng tới giải pháp cân bằng giữa chất lượng và deadline, không bảo thủ theo quan điểm cá nhân.* 🚀

## User đang thực hiện chuyển khoản 10 triệu đồng, đúng lúc họ nhấn nút 'Xác nhận' thì mạng bị chập chờn (hoặc mất mạng đột ngột). Lỗi Timeout xảy ra. Trên app hiển thị gì và xử lý logic như thế nào để tránh việc user bấm lại lần nữa dẫn đến trừ tiền 2 lần?

   1. **Về phía UI:** Ngay khi user nhấn nút, lập tức disable nút đó và hiển thị Loading Overlay để block tương tác (tránh click trùng).
   2. **Về phía API/Logic:** Phải sử dụng cơ chế **Idempotency Key** (Mã định danh duy nhất cho mỗi phiên giao dịch, thường là mã UUID được sinh ra ở Client trước khi gửi request). Nếu request bị timeout, Client khi gửi lại (Retry mechanism) bắt buộc phải đính kèm đúng Key đó. Phía Backend thấy Key trùng sẽ không thực hiện giao dịch mới mà chỉ trả về trạng thái của giao dịch cũ.
   3. **Về trạng thái:** Nếu Timeout, không được báo "Thành công" hay "Thất bại" một cách vội vã. Phải đưa UI về trạng thái *"Giao dịch đang được xử lý, vui lòng kiểm tra lại lịch sử hoặc số dư"* để an toàn cho cả khách hàng và ngân hàng.

## App OCB OMNI hiện tại có lượng user rất lớn và cấu trúc tính năng thay đổi liên tục theo các chiến dịch Marketing của ngân hàng. Nếu mỗi lần thay đổi nhỏ ở trang chủ (như đổi banner, đổi thứ tự các nút chức năng nhanh) lại bắt user cập nhật app trên Google Play thì tỷ lệ drop rất cao. Em có giải pháp nào không?

   * Áp dụng kiến trúc **Server-Driven UI (SDUI)**. Cấu trúc, bố cục (Layout), thứ tự các component và nội dung hiển thị của trang chủ sẽ do Backend định nghĩa và trả về dưới dạng một file JSON dynamic.
   * Phía Android Client sẽ build sẵn các Component/Widget chuẩn (ví dụ bằng Jetpack Compose). Khi nhận được JSON từ Server, app sẽ tự động parse và render giao diện tương ứng theo real-time mà không cần release version mới trên Store.
   * Kết hợp sử dụng **Firebase Remote Config** để thực hiện A/B Testing hoặc bật/tắt nhanh các tính năng (Feature Toggle) khi có sự cố.

# Kinh nghiệm "ghi điểm" khi phỏng vấn OCB:

Ngân hàng rất thích những dev có tư duy "Defensive Programming" (Lập trình phòng thủ) – tức là viết code luôn nghĩ đến trường hợp xấu nhất (mất mạng, timeout, dữ liệu rác, hacker phá...). Khi trả lời bất kỳ câu hỏi nào, hãy luôn lồng ghép yếu tố: Logging (ghi vết), Security (bảo mật) và Monitor (giám sát hệ thống). Đó chính là ngôn ngữ chung của dân IT Bank

# Tips "Sống Sót" Cho Vòng Phỏng Vấn Với Giám Đốc (Vòng 3)

1. **Thể hiện tính kỷ luật và quy trình:** IT Bank cực kỳ sợ các "ngôi sao cô đơn" thích tự ý sửa code không qua quy trình. Hãy thể hiện bạn là người tuân thủ: làm việc dựa trên Jira, viết unit test kỹ càng, tuân thủ chặt chẽ quy trình Code Review và CI/CD.

3. **Hỏi lại nhà tuyển dụng một cách thông minh:** Ở cuối buổi, khi được hỏi "Em có câu hỏi gì không?", hãy dùng cơ hội này để thể hiện sự quan tâm sâu sắc đến sản phẩm của họ:

   * *“Hiện tại team Android của mình đang dịch chuyển dần sang Jetpack Compose hoàn toàn chưa ạ, hay vẫn đang duy trì mô hình Hybrid với XML?”*