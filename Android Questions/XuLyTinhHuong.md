# Các giải pháp xử lý trong dự án

## Lưu ý:

Họ muốn nghe cách bạn tư duy phản biện (Critical Thinking):
- Xác định rủi ro trước: (Ví dụ: "Case này nếu sửa ẩu sẽ bị...").
- Đưa ra giải pháp ngắn hạn (Hotfix) để cứu Production trước.
- Đưa ra giải pháp dài hạn (Long-term architecture) để không bao giờ lặp lại lỗi đó nữa.

# Nhóm 1: Architecture & Modernization (Tái cấu trúc & Kiến trúc)

## Cách chia nhỏ 1 class 5000 dòng ()

Analyze → Add Tests → Create Interface → Extract Responsibilities → Strangler Pattern → Rollout Gradually

- Phân tích các lớp phụ thuộc (dependency) và các luồng chính (critical)
- Tạo Characterization (đặc tính) Test (thường là Integration Test) để làm mạng lưới an toàn (safety net). 
- Tạo interface để cô lập God Object
- Tách dần theo từng trách nhiệm (responsibility) nhỏ, 
kiểm thử sau mỗi bước và rollout có kiểm soát để tránh ảnh hưởng hệ thống đang chạy.

## Giải pháp như đổi banner, đổi thứ tự các nút chức năng ở trang chủ, mà không cần cập nhật ứng dụng

- Áp dụng kiến trúc **Server-Driven UI (SDUI)**. Cấu trúc, bố cục (Layout), thứ tự các component và nội dung hiển thị của trang chủ sẽ do Backend định nghĩa và trả về dưới dạng một file JSON dynamic.
- Phía Android Client sẽ build sẵn các Component/Widget chuẩn (ví dụ bằng Jetpack Compose). Khi nhận được JSON từ Server, app sẽ tự động parse và render giao diện tương ứng theo real-time mà không cần release version mới trên Store.
- Kết hợp sử dụng **Firebase Remote Config** để thực hiện A/B Testing hoặc bật/tắt nhanh các tính năng (Feature Toggle) khi có sự cố.

## Lộ trình để chuyển sang kiến trúc Modularization và Clean Architecture mà không làm gián đoạn tiến độ phát triển tính năng mới?

- Áp dụng chiến lược chiến lược siết cổ (Strangler Pattern). 
- Ưu tiên tách các feature mới hoặc ít phụ thuộc trước. 
- Song song đó, xây dựng các module core và abstraction layer để cô lập các mã cũ (legacy code). 
- Mỗi lần phát triển hoặc sửa một feature sẽ là cơ hội để migrate dần sang Clean Architecture. 
- Cách tiếp cận này giúp giảm rủi ro, không làm gián đoạn roadmap sản phẩm và vẫn cải thiện kiến trúc theo thời gian.

## Khi chia nhỏ dự án thành các module (ví dụ: :core, :feature:auth, :feature:payment), bạn xử lý vấn đề Dependency Resolution và Navigation giữa các module như thế nào để tránh vòng lặp phụ thuộc (circular dependency)?

- Thiết kế dependency theo nguyên tắc một chiều (unidirectional dependency). 
- không cho phép Feature không được phụ thuộc lẫn nhau. 
- Các dependency dùng chung sẽ được đưa vào core module hoặc định nghĩa dưới dạng contract/interface. 
- Đối với navigation, tôi sử dụng Navigation Contract hoặc Deep Link thay vì gọi trực tiếp giữa các feature để tránh circular dependency.

## Khi chuyển đổi một màn hình phức tạp từ XML (View-based) sang Jetpack Compose, những rủi ro nào về mặt hiệu năng (Recomposition) có thể xảy ra và bạn tối ưu hóa nó bằng cách nào? Làm sao để đảm bảo 'pixel-perfect' với thiết kế Figma phức tạp?

Khi chuyển từ XML sang Compose, rủi ro lớn nhất là hiệu năng. 
Nếu quản lý state không tốt, một thay đổi nhỏ trên màn hình có thể khiến nhiều thành phần UI bị vẽ lại (recompose) không cần thiết, dẫn đến giật lag, đặc biệt với danh sách dài hoặc màn hình phức tạp.

Để tối ưu, tôi sẽ chia màn hình thành các Composable nhỏ, chỉ truyền dữ liệu cần thiết cho từng phần. 
Như vậy khi dữ liệu thay đổi, chỉ phần liên quan được cập nhật thay vì toàn bộ màn hình. 
Ngoài ra tôi sẽ đo bằng các công cụ profiling của Android Studio để xác định đúng điểm nghẽn trước khi tối ưu.

Đối với yêu cầu pixel-perfect theo Figma, tôi thường xây dựng Design System chung cho màu sắc, font chữ, spacing và component. 
Sau đó đối chiếu trực tiếp với Figma trên nhiều kích thước màn hình và density khác nhau. 
Với các màn hình quan trọng, tôi dùng Screenshot Test để đảm bảo giao diện không bị lệch sau mỗi lần thay đổi.

## StateFlow và SharedFlow trong Kotlin Coroutines? Trong kiến trúc MVVM, bạn sẽ dùng cái nào cho trạng thái UI (UI State) và cái nào cho sự kiện một lần (One-shot event như hiển thị Toast, Navigation)?

- StateFlow đại diện cho trạng thái hiện tại và luôn giữ giá trị mới nhất, nên rất phù hợp cho UI State. 
- SharedFlow phù hợp cho các sự kiện xảy ra một lần, nó không đại diện cho trạng thái và không cần phát lại khi màn hình được tạo lại như Navigation, Toast hoặc Snackbar vì. 
Trong MVVM, tôi thường dùng StateFlow cho UI State và SharedFlow cho One-shot Event để tránh các lỗi như Toast hoặc Navigation bị thực hiện lại sau khi rotate màn hình.

## Khi refactor code cũ, bạn thường dùng công cụ gì (ví dụ: Android Profiler, LeakCanary) để phát hiện Memory Leak? Hãy kể lại một case phức tạp về leak dữ liệu do Threading hoặc Lifecycle mà bạn từng xử lý.

# Nhóm 2: Banking-Grade Security (Bảo mật cấp độ Ngân hàng - Key Point)

Certificate Pinning: "Bạn triển khai Certificate Pinning trên Android như thế nào (Network Security Config hay OkHttpClient)? Chuyện gì sẽ xảy ra khi Chứng chỉ (Certificate) của Ngân hàng hết hạn/thay đổi đột ngột ở phía Backend, và bạn thiết kế cơ chế fallback/update từ xa như thế nào để app không bị crash hoặc block user?"

Secure Storage: "Để lưu trữ Token (Access/Refresh Token) hoặc dữ liệu nhạy cảm của user cục bộ, bạn sử dụng EncryptedSharedPreferences hay Android Keystore System? Cơ chế mã hóa dưới nền tảng hoạt động ra sao để chống bẻ khóa trên thiết bị đã Root?"

Root & Tamper Detection: "Làm thế nào để ứng dụng Ngân hàng phát hiện thiết bị của người dùng đã bị Root, đang chạy trên Emulator, hoặc đang bị đính kèm các công cụ Hooking như Frida/Xposed? Bạn xử lý thế nào khi phát hiện các mối đe dọa này?"

Obfuscation (Xáo trộn mã): "Ngoài việc bật minifyEnabled true bằng ProGuard/R8, bạn cấu hình các rules như thế nào để đảm bảo các Model class (Dùng để parse API) không bị lỗi runtime nhưng các logic xử lý nghiệp vụ quan trọng (như mã hóa dữ liệu) vẫn được bảo vệ an toàn tối đa?"

Biometric Authentication: "Khi tích hợp Biometric (Vân tay/FaceID), làm sao bạn đảm bảo được tính toàn vẹn của kết quả trả về? Làm sao để ngăn chặn việc bypass Biometrics bằng cách chỉnh sửa luồng logic ở runtime?"

# Nhóm 3: Concurrency, Data Sync & API Orchestration
JD yêu cầu: Threading, complex offline data synchronization, RESTful API lifecycle, token-based authentication flows.

Token Flows: "Hãy mô tả chi tiết cách bạn cấu hình OkHttp Authenticator và Interceptor để tự động xử lý luồng Refresh Token khi nhận mã lỗi 401 Unauthorized từ Gateway, đảm bảo tính Thread-safe khi có nhiều request đồng thời bị lỗi 401."

Offline Data Sync: "App ngân hàng cần hiển thị lịch sử giao dịch ngay cả khi mất mạng. Bạn thiết kế cơ chế Offline Synchronization (đồng bộ dữ liệu ngoại tuyến) như thế nào bằng cách phối hợp Room Database, Retrofit và WorkManager để đảm bảo dữ liệu không bị sai lệch (data race condition)?"

Coroutines Tuning: "Nếu một tác vụ nền cần tính toán toán học phức tạp hoặc xử lý ảnh (ví dụ: quét QR/OCR), bạn sẽ đẩy nó vào Dispatchers.Default hay Dispatchers.IO? Tại sao?"

# Nhóm 4: Engineering Rigor & Testing Culture (Văn hóa kiểm thử)
JD yêu cầu: Unit Tests, Automated UI Tests, API Mocks/Stubs, SOLID, YAGNI, KISS.

Testing Architecture: "Để một đoạn code có thể viết Unit Test dễ dàng (Testable code), bạn cần tuân thủ nguyên tắc nào trong SOLID? Hãy đưa ra ví dụ về cách áp dụng Dependency Inversion để Mock một API Service khi viết Test."

Mocking & Stubbing: "Bạn phân biệt thế nào giữa Mock và Spy trong Mockito/MockK? Khi viết Integration Test cho một luồng chuyển tiền, bạn sẽ Mock API response như thế nào để test các trường hợp biên (như Timeout, lỗi hệ thống 500)?"

UI Testing: "Bạn đã từng triển khai Espresso hoặc Compose UI Test chưa? Làm thế nào để xử lý vấn đề 'Flaky Tests' (Test lúc chạy đúng lúc chạy sai) do độ trễ của mạng hoặc hiệu năng thiết bị?"

# Nhóm 5: Strategic, Plus Skills & Core Competencies (Kỹ năng nâng cao)
JD đề cập: Kotlin Multiplatform (KMP), AI-SDLC, Technical Leadership, Mentoring, eKYC/OCR.

Kotlin Multiplatform (KMP): "JD của chúng tôi có đề cập đến KMP. Theo bạn, app Ngân hàng có nên chuyển đổi phần Business Logic (như validation, encryption, api gọi vốn) sang KMP để dùng chung cho cả Android và iOS không? Đâu là lợi ích và rủi ro lớn nhất?"

AI-SDLC (Ứng dụng AI): "Bạn tận dụng các công cụ AI (như GitHub Copilot, ChatGPT) như thế nào trong quy trình phát triển phần mềm hàng ngày? Nó giúp ích gì cho bạn trong việc tăng tốc độ viết Unit Test hoặc Refactor code?"

Advanced Features (eKYC/Chatbot): "Bạn đã từng làm việc với các giải pháp eKYC (Định danh điện tử) chưa? Khi tích hợp SDK nhận diện khuôn mặt hoặc OCR (như đọc CCCD), làm sao bạn tối ưu dung lượng bộ nhớ (RAM) và kích thước file APK của ứng dụng?"

Technical Leadership & Mentoring: "Là một Senior Engineer, khi bạn làm Code Review cho một bạn Junior và phát hiện bạn đó viết code chạy được nhưng vi phạm nghiêm trọng nguyên tắc SOLID hoặc gây nguy cơ bảo mật, bạn sẽ xử lý và hướng dẫn bạn đó như thế nào để vừa đảm bảo chất lượng vừa giữ được tinh thần cởi mở của team?"

# Nhóm 6: Câu hỏi tình huống nghiệp vụ Ngân hàng (Fintech Scenarios)
Các tình huống thực tế khi vận hành app tài chính có hàng triệu người dùng.

High-Traffic & Crash Handling: "Vào ngày nhận lương (ngày 5 hàng tháng), lượng traffic tăng đột biến và app xuất hiện nhiều lỗi Out Of Memory (OOM) hoặc Timeout trên môi trường Production. Bạn sẽ tiếp cận, phân tích log (qua Firebase Crashlytics) và cô lập lỗi này như thế nào?"

Transaction Integrity: "Người dùng đang thực hiện nhấn nút 'Chuyển tiền', ngay lúc đó họ bị mất kết nối mạng (hoặc app bị kill ngầm do hết pin). Bạn thiết kế luồng xử lý ở phía Client như thế nào để đảm bảo người dùng không bị bấm double-click (gửi 2 lần tiền) hoặc hoang mang không biết giao dịch đã thành công hay chưa?"

# Nhóm câu hỏi Tình huống (Behavioral)

## Sát ngày Go-live (realease sản phẩm) mà bên Kiểm thử (QA/QC) phát hiện ra một lỗi nghiêm trọng, nhưng PO vẫn ép phải deploy đúng hạn để chạy chiến dịch Marketing, em sẽ xử lý thế nào?”

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

## Cách thuyết phục dùng Jetpack Compose thay cho XML (Tốn thời gian học, chậm tiến độ)

- Compose giúp giảm boilerplate, tăng khả năng tái sử dụng component, phù hợp với kiến trúc hiện đại và giảm chi phí bảo trì dài hạn mà không ảnh hưởng lớn đến tiến độ dự án.
- Chứng minh bằng số liệu như thời gian phát triển màn hình, số lượng bug UI và chi phí bảo trì hiện tại. 
- Sau đó triển khai Compose theo hướng di cư từ từ (incremental migration): màn hình mới dùng Compose, màn hình cũ giữ XML. 

## Trường hợp Modularization quá đà (Over-engineering) chưa? Khi nào thì việc chia module trở thành gánh nặng cho CI/CD và làm chậm tốc độ build app?

Có, tôi từng thấy dự án chia module quá nhỏ khiến việc sửa một feature phải thay đổi nhiều module, 
làm tăng độ phức tạp và thời gian build CI.
Nếu chi phí quản lý module lớn hơn lợi ích thì đó là dấu hiệu đang over-engineering.

Cân nhắc trước khi module:
- Feature lớn, độc lập (Music, Navigation, Settings)
- Nhiều team cùng phát triển
- Có khả năng tái sử dụng
- Muốn build/test độc lập