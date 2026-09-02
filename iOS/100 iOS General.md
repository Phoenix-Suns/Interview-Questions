# 100 CÂU PHỎNG VẤN SENIOR iOS — TỔNG HỢP THEO CẤP ĐỘ & CHỦ ĐỀ

## PHÂN BỐ

| Cấp độ   |  Số câu | Trọng tâm                                                  |
| -------- | ------: | ---------------------------------------------------------- |
| Junior   |      20 | Swift, UIKit, SwiftUI, Networking, Persistence             |
| Middle   |      25 | ARC, UI, Concurrency, Architecture, DI                     |
| Senior   |      40 | Architecture, Concurrency, Networking, Performance, System |
| Senior+  |      15 | Design trade-off, system design, race condition, security  |
| **Tổng** | **100** |                                                            |

---

# CẤP ĐỘ 1 — JUNIOR

# 20 CÂU

---

## Chủ đề: Swift Core

### 1. Hai biến có cùng dữ liệu ban đầu nhưng thay đổi một biến lại không ảnh hưởng biến kia. Vì sao?

**Ý chính:** Value semantics.

**Ý diễn giải:**
Struct và enum là value type. Khi gán hoặc truyền, mỗi biến có giá trị độc lập.

**Ví dụ:**

```swift
struct User {
    var name: String
}

var a = User(name: "A")
var b = a

b.name = "B"

print(a.name) // A
print(b.name) // B
```

---

### 2. Nhiều biến cùng nhìn thấy thay đổi của một object. Vì sao?

**Ý chính:** Reference semantics.

**Ý diễn giải:**
Class là reference type. Các biến có thể cùng trỏ tới một instance.

**Ví dụ:**

```swift
final class User {
    var name = "A"
}

let a = User()
let b = a

b.name = "B"

print(a.name) // B
```

---

### 3. Một closure được gọi sau khi function đã return. Điều gì cho phép nó làm được?

**Ý chính:** `@escaping`.

**Ý diễn giải:**
Closure mặc định chỉ sống trong thời gian function thực thi. `@escaping` cho phép closure được lưu hoặc gọi sau khi function kết thúc.

**Ví dụ:**

```swift
func load(
    completion: @escaping (String) -> Void
) {
    DispatchQueue.global().async {
        completion("Done")
    }
}
```

---

### 4. Một JSON field có tên khác với property Swift. Bạn xử lý thế nào?

**Ý chính:** `CodingKeys`.

**Ý diễn giải:**
`Codable` cho phép mapping tên JSON với property Swift thông qua `CodingKeys`.

**Ví dụ:**

```swift
struct User: Decodable {

    let userId: Int

    enum CodingKeys: String, CodingKey {
        case userId = "user_id"
    }
}
```

---

## Chủ đề: UIKit

### 5. Khi nào một UIViewController thực sự load view?

**Ý chính:** Khi `view` được truy cập.

**Ý diễn giải:**
Một UIViewController có thể tồn tại mà view chưa được load. Khi view được yêu cầu, UIKit load view rồi gọi `viewDidLoad()`.

**Ví dụ:**

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    setupUI()
}
```

---

### 6. Bạn đặt setup UI một lần ở đâu?

**Ý chính:** `viewDidLoad`.

**Ý diễn giải:**
`viewDidLoad` phù hợp cho setup chỉ cần thực hiện một lần trong lifecycle của loaded view.

**Ví dụ:**

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    title = "Profile"
}
```

---

### 7. Bạn cần refresh dữ liệu mỗi lần màn hình xuất hiện. Dùng lifecycle nào?

**Ý chính:** `viewWillAppear`.

**Ý diễn giải:**
`viewWillAppear` được gọi mỗi lần controller sắp xuất hiện, phù hợp với dữ liệu cần refresh theo appearance.

**Ví dụ:**

```swift
override func viewWillAppear(
    _ animated: Bool
) {
    super.viewWillAppear(animated)

    refresh()
}
```

---

### 8. Một cell biến mất rồi được dùng cho item khác. Cơ chế nào giúp giảm số lượng cell?

**Ý chính:** Cell reuse.

**Ý diễn giải:**
UITableView/UICollectionView tái sử dụng cell thay vì tạo một cell mới cho từng item.

**Ví dụ:**

```swift
let cell = tableView.dequeueReusableCell(
    withIdentifier: "Cell",
    for: indexPath
)
```

---

## Chủ đề: SwiftUI

### 9. SwiftUI mô tả giao diện theo cách nào?

**Ý chính:** Declarative UI.

**Ý diễn giải:**
Bạn mô tả UI dựa trên state hiện tại. Khi state thay đổi, SwiftUI tính lại UI description.

**Ví dụ:**

```swift
struct CounterView: View {

    @State private var count = 0

    var body: some View {
        VStack {
            Text("\(count)")

            Button("Add") {
                count += 1
            }
        }
    }
}
```

---

### 10. Khi child cần thay đổi state do parent sở hữu, bạn dùng gì?

**Ý chính:** `@Binding`.

**Ý diễn giải:**
Binding cho phép child đọc/ghi state mà không sở hữu source of truth.

**Ví dụ:**

```swift
struct ChildView: View {

    @Binding var isOn: Bool

    var body: some View {
        Toggle(
            "Enabled",
            isOn: $isOn
        )
    }
}
```

---

## Chủ đề: Concurrency

### 11. Khi chờ network, làm thế nào để không block thread?

**Ý chính:** `async/await`.

**Ý diễn giải:**
Task có thể suspend tại `await` thay vì giữ thread đứng chờ.

**Ví dụ:**

```swift
func load() async throws -> Data {
    try await URLSession.shared
        .data(from: url)
        .0
}
```

---

### 12. Một task đang chạy nhưng user rời màn hình. Bạn xử lý thế nào?

**Ý chính:** Cancellation.

**Ý diễn giải:**
Task nên có lifecycle rõ ràng và được cancel khi kết quả không còn cần thiết.

**Ví dụ:**

```swift
var task: Task<Void, Never>?

func start() {
    task = Task {
        await load()
    }
}

func stop() {
    task?.cancel()
}
```

---

## Chủ đề: Networking

### 13. Có `Data` từ URLSession thì có chắc API thành công không?

**Ý chính:** Kiểm tra HTTP status.

**Ý diễn giải:**
Transport success và HTTP success là hai chuyện khác nhau. Server có thể trả 400/401/500 nhưng URLSession vẫn trả được response.

**Ví dụ:**

```swift
let (data, response) =
    try await session.data(for: request)

guard let http =
    response as? HTTPURLResponse
else {
    throw APIError.invalidResponse
}

guard (200..<300).contains(
    http.statusCode
) else {
    throw APIError.http(http.statusCode)
}
```

---

### 14. Access token nên lưu ở đâu?

**Ý chính:** Keychain.

**Ý diễn giải:**
Token là credential và cần secure storage thay vì UserDefaults.

**Ví dụ:**

```swift
// Conceptual
try keychain.save(
    accessToken,
    account: "access_token"
)
```

---

## Chủ đề: Persistence

### 15. Một boolean cho biết user đã xem onboarding nên lưu ở đâu?

**Ý chính:** UserDefaults.

**Ý diễn giải:**
UserDefaults phù hợp preference nhỏ và không nhạy cảm.

**Ví dụ:**

```swift
UserDefaults.standard.set(
    true,
    forKey: "hasSeenOnboarding"
)
```

---

### 16. Một configuration nhỏ cần lưu thành file. Bạn chọn gì?

**Ý chính:** Codable + FileManager.

**Ý diễn giải:**
Với dữ liệu nhỏ, không cần query phức tạp, encode/decode thành JSON là đủ đơn giản.

**Ví dụ:**

```swift
struct Settings: Codable {
    let theme: String
}

let data = try JSONEncoder()
    .encode(Settings(theme: "dark"))

try data.write(
    to: fileURL,
    options: .atomic
)
```

---

## Chủ đề: Memory

### 17. Vì sao closure có thể giữ object sống lâu hơn dự kiến?

**Ý chính:** Strong capture.

**Ý diễn giải:**
Closure có thể giữ `self` bằng strong reference. Nếu object cũng giữ closure, retain cycle có thể xảy ra.

**Ví dụ:**

```swift
final class ViewModel {

    var handler: (() -> Void)?

    func setup() {
        handler = {
            self.load()
        }
    }

    func load() {}
}
```

---

### 18. Weak khác unowned ở điểm nào?

**Ý chính:** `weak` có thể nil; `unowned` giả định object còn sống.

**Ý diễn giải:**
Weak an toàn hơn khi lifetime không chắc chắn. Unowned phù hợp khi quan hệ lifetime chắc chắn.

**Ví dụ:**

```swift
weak var delegate: Delegate?
```

---

## Chủ đề: Architecture

### 19. Một ViewController có cả API, database, validation và navigation. Vấn đề lớn nhất là gì?

**Ý chính:** Too many responsibilities / Massive ViewController.

**Ý diễn giải:**
Controller đang làm presentation, business, data access và navigation cùng lúc. Cần tách responsibility theo boundary phù hợp.

**Ví dụ:**

```text
ViewController
 ├── API
 ├── Database
 ├── Business Logic
 ├── Validation
 └── Navigation
```

---

### 20. Tại sao không nên tạo mọi layer chỉ vì đang dùng Clean Architecture?

**Ý chính:** Avoid over-engineering.

**Ý diễn giải:**
Layer phải giải quyết một vấn đề thật. Feature đơn giản không nhất thiết cần View → ViewModel → UseCase → Repository → DataSource.

**Ví dụ:**

```text
Feature đơn giản:

View
 ↓
Service
```

có thể đủ.

---

# CẤP ĐỘ 2 — MIDDLE

# 25 CÂU

---

# Chủ đề: Swift / Memory

### 21. Vì sao `struct` thường dễ reasoning hơn `class` trong concurrent code?

**Ý chính:** Value semantics.

**Ý diễn giải:**
Struct giảm shared mutable reference state. Khi dữ liệu được copy theo value, các task ít có khả năng cùng sửa một object.

**Ví dụ:**

```swift
struct User: Sendable {
    let id: Int
    let name: String
}
```

---

### 22. Một object không được giải phóng sau khi pop ViewController. Bạn debug từ đâu?

**Ý chính:** Memory Graph + retain path.

**Ý diễn giải:**
Tìm reference cuối cùng đang giữ object. Đừng chỉ thêm weak reference một cách ngẫu nhiên.

**Ví dụ:**

```swift
deinit {
    print("ViewModel released")
}
```

---

### 23. Vì sao singleton giữ nhiều object có thể không phải memory leak?

**Ý chính:** Cache growth ≠ ARC leak.

**Ý diễn giải:**
Nếu singleton chủ động sở hữu cache thì object vẫn reachable hợp lệ. Vấn đề có thể là cache không có eviction policy.

**Ví dụ:**

```swift
final class ImageCache {
    static let shared = ImageCache()

    var images: [URL: UIImage] = [:]
}
```

---

## Chủ đề: UIKit / UI

### 24. Một cell hiển thị sai ảnh sau khi scroll nhanh. Nguyên nhân thường là gì?

**Ý chính:** Reuse + stale async result.

**Ý diễn giải:**
Request cũ có thể hoàn thành sau khi cell đã được reuse. Cần cancel request hoặc kiểm tra identity.

**Ví dụ:**

```swift
override func prepareForReuse() {
    super.prepareForReuse()

    imageTask?.cancel()
    imageView?.image = placeholder
}
```

---

### 25. Intrinsic Content Size giúp Auto Layout như thế nào?

**Ý chính:** Natural size.

**Ý diễn giải:**
Một số UIKit view có thể tự mô tả kích thước tự nhiên dựa trên content, giúp giảm số constraint kích thước cần khai báo.

**Ví dụ:**

```swift
let label = UILabel()
label.text = "Hello"

print(label.intrinsicContentSize)
```

---

### 26. Content Hugging và Compression Resistance khác nhau thế nào?

**Ý chính:** Hugging chống phình; compression resistance chống co.

**Ý diễn giải:**
Hugging quyết định view không muốn lớn hơn intrinsic size. Compression resistance quyết định view không muốn bị nhỏ hơn intrinsic size.

**Ví dụ:**

```swift
label.setContentHuggingPriority(
    .required,
    for: .horizontal
)

label.setContentCompressionResistancePriority(
    .required,
    for: .horizontal
)
```

---

## Chủ đề: SwiftUI

### 27. Tại sao local state có thể mất sau khi list update?

**Ý chính:** Identity.

**Ý diễn giải:**
SwiftUI gắn state với view identity. Nếu identity thay đổi, framework có thể coi đó là view mới.

**Ví dụ:**

```swift
ForEach(items) { item in
    Row(item: item)
}
```

Item cần identity ổn định.

---

### 28. `.id(UUID())` trong SwiftUI có thể gây vấn đề gì?

**Ý chính:** Identity liên tục thay đổi.

**Ý diễn giải:**
Mỗi lần UUID mới xuất hiện, View có thể bị coi là identity mới và mất state continuity.

**Ví dụ:**

```swift
Text("Hello")
    .id(UUID()) // ❌ thường không nên
```

---

### 29. `@StateObject` khác `@ObservedObject` ở ownership nào?

**Ý chính:** `StateObject` owns; `ObservedObject` observes.

**Ý diễn giải:**
View tạo và quản lý lifecycle object thì StateObject. Object được truyền vào từ bên ngoài thì ObservedObject.

**Ví dụ:**

```swift
struct Parent: View {

    @StateObject
    private var vm = ViewModel()

    var body: some View {
        Child(vm: vm)
    }
}

struct Child: View {

    @ObservedObject
    var vm: ViewModel
}
```

---

### 30. Body chạy lại nhiều lần có nhất thiết là performance bug?

**Ý chính:** Body recomputation ≠ full rendering.

**Ý diễn giải:**
SwiftUI được thiết kế để recompute view description. Điều đáng lo là expensive work bên trong body.

**Ví dụ:**

```swift
var body: some View {

    let sorted =
        hugeArray.sorted()

    return List(sorted) {
        Text($0.name)
    }
}
```

---

## Chủ đề: Concurrency

### 31. Hai request độc lập muốn chạy đồng thời. Bạn dùng gì?

**Ý chính:** `async let`.

**Ý diễn giải:**
Async let phù hợp với số lượng operation cố định.

**Ví dụ:**

```swift
async let user = loadUser()
async let posts = loadPosts()

let result = try await (
    user,
    posts
)
```

---

### 32. Khi số lượng task phụ thuộc runtime, bạn dùng gì?

**Ý chính:** TaskGroup.

**Ý diễn giải:**
TaskGroup phù hợp dynamic concurrency.

**Ví dụ:**

```swift
let results =
    await withTaskGroup(
        of: Data.self
    ) { group in

        for url in urls {
            group.addTask {
                await load(url)
            }
        }

        var values: [Data] = []

        for await value in group {
            values.append(value)
        }

        return values
    }
```

---

### 33. `Task.cancel()` có kill task ngay không?

**Ý chính:** Cooperative cancellation.

**Ý diễn giải:**
Cancel chỉ truyền tín hiệu. Code phải kiểm tra cancellation hoặc sử dụng API hỗ trợ cancellation.

**Ví dụ:**

```swift
Task {
    try Task.checkCancellation()
    await work()
}
```

---

### 34. Actor giải quyết vấn đề gì?

**Ý chính:** Shared mutable state isolation.

**Ý diễn giải:**
Actor bảo vệ isolated mutable state khỏi data race. Nó không tự đảm bảo mọi business operation atomic.

**Ví dụ:**

```swift
actor Counter {

    private var value = 0

    func increment() {
        value += 1
    }
}
```

---

### 35. Vì sao `await` bên trong actor có thể tạo bug?

**Ý chính:** Actor reentrancy.

**Ý diễn giải:**
Khi actor suspend tại await, operation khác có thể chạy và thay đổi state.

**Ví dụ:**

```swift
actor Store {

    var value = 0

    func work() async {

        let old = value

        await externalWork()

        // value có thể đã thay đổi
        value = old
    }
}
```

---

## Chủ đề: Architecture / DI

### 36. Constructor Injection có ưu điểm gì?

**Ý chính:** Explicit required dependency.

**Ý diễn giải:**
Object được tạo ra với đầy đủ dependency bắt buộc và dễ test.

**Ví dụ:**

```swift
final class ViewModel {

    let repository: UserRepository

    init(
        repository: UserRepository
    ) {
        self.repository = repository
    }
}
```

---

### 37. Vì sao Service Locator dễ tạo hidden dependency?

**Ý chính:** Dependency không xuất hiện trong API của class.

**Ý diễn giải:**
Nhìn constructor không biết class cần gì. Muốn hiểu dependency phải đọc implementation.

**Ví dụ:**

```swift
final class ViewModel {

    func load() async {

        await AppContainer.shared
            .api
            .fetch()
    }
}
```

Trong khi:

```swift
ViewModel(
    api: api
)
```

rõ dependency hơn.

---

### 38. Factory và Dependency Container khác nhau thế nào?

**Ý chính:** Factory tạo object; Container compose dependency graph.

**Ý diễn giải:**
Container quản lý shared infrastructure/lifecycle. Factory tạo feature-specific object.

**Ví dụ:**

```swift
final class AppContainer {

    let api: API
    let database: Database
}

final class ProfileFactory {

    let container: AppContainer

    func makeViewModel()
        -> ProfileViewModel {

        ProfileViewModel(
            repository:
                makeRepository()
        )
    }
}
```

---

## Chủ đề: Persistence

### 39. NSCache có phải source of truth không?

**Ý chính:** Không. Cache chỉ là optimization.

**Ý diễn giải:**
NSCache có thể evict data và mất khi process terminate.

**Ví dụ:**

```swift
let cache =
    NSCache<NSURL, UIImage>()
```

---

### 40. Vì sao không nên lưu hàng trăm nghìn record vào một JSON file?

**Ý chính:** Poor query + serialization + migration.

**Ý diễn giải:**
Mỗi lần đọc/ghi có thể phải xử lý lượng dữ liệu lớn. Không có indexing/query/transaction như database.

**Ví dụ:**

```swift
let data = try JSONEncoder()
    .encode(hugeArray)
```

---

### 41. Managed object từ background context có nên truyền trực tiếp sang main context?

**Ý chính:** Context confinement.

**Ý diễn giải:**
Managed object gắn với context. Thường nên truyền `NSManagedObjectID` hoặc value model rồi fetch lại ở context đích.

**Ví dụ:**

```swift
let objectID = user.objectID

mainContext.perform {
    let user =
        mainContext.object(
            with: objectID
        )
}
```

---

## Chủ đề: Networking

### 42. HTTP 401 và 403 khác nhau thế nào?

**Ý chính:** Authentication vs authorization.

**Ý diễn giải:**
401 thường liên quan credential/authentication. 403 nghĩa server hiểu request nhưng không cho phép resource/action.

**Ví dụ:**

```swift
switch response.statusCode {
case 401:
    handleUnauthorized()

case 403:
    handleForbidden()

default:
    break
}
```

---

### 43. Có nên retry mọi HTTP error không?

**Ý chính:** Retry transient failure only.

**Ý diễn giải:**
400 validation không nên retry. 503/408/429 có thể retry theo policy.

**Ví dụ:**

```swift
func shouldRetry(
    statusCode: Int
) -> Bool {
    statusCode == 408 ||
    statusCode == 429 ||
    (500...599).contains(statusCode)
}
```

---

### 44. Vì sao timeout không có nghĩa server chưa xử lý request?

**Ý chính:** Client timeout ≠ server rollback.

**Ý diễn giải:**
Server có thể đã xử lý request nhưng response không tới client. Đây là lý do retry mutation cần idempotency.

**Ví dụ:**

```text
Client
  ↓ POST
Server
  ↓ process success
X response lost
  ↓
Client timeout
```

---

### 45. Tại sao reachability không nên quyết định tuyệt đối request được phép chạy?

**Ý chính:** Reachability chỉ là hint.

**Ý diễn giải:**
Network có thể thay đổi ngay sau khi check. Request thực tế mới là source of truth.

**Ví dụ:**

```swift
if reachability.isConnected {
    do {
        try await api.fetch()
    } catch {
        // Vẫn có thể fail
    }
}
```

---

# CẤP ĐỘ 3 — SENIOR

# 40 CÂU

---

# Chủ đề: Architecture

### 46. Khi nào Repository thực sự cần thiết?

**Ý chính:** Data abstraction + multiple sources + policy.

**Ý diễn giải:**
Repository đáng dùng khi cần che giấu Network/Database/Cache hoặc phối hợp nhiều nguồn. Nếu chỉ pass-through một function thì có thể không cần.

**Ví dụ:**

```swift
protocol UserRepository {
    func user(
        id: Int
    ) async throws -> User
}
```

---

### 47. Use Case khác Repository ở trách nhiệm nào?

**Ý chính:** Use Case = business operation; Repository = data access abstraction.

**Ý diễn giải:**
Repository biết dữ liệu lấy từ đâu. Use Case biết business operation cần thực hiện gì.

**Ví dụ:**

```swift
struct CheckoutUseCase {

    let cart: CartRepository
    let payment: PaymentService

    func execute() async throws {

        let cart =
            try await cart.currentCart()

        try await payment.pay(
            amount: cart.total
        )
    }
}
```

---

### 48. Nếu Use Case chỉ gọi một method của Repository rồi return, có chắc cần Use Case không?

**Ý chính:** Tránh pass-through abstraction.

**Ý diễn giải:**
Nếu không có business rule, transformation hoặc orchestration, thêm Use Case có thể chỉ tạo boilerplate.

---

### 49. Vì sao Feature-based Architecture thường scale tốt hơn folder theo layer?

**Ý chính:** Business ownership + feature cohesion.

**Ý diễn giải:**
Mỗi feature gom presentation/domain/data liên quan, dễ ownership và giảm cross-feature coupling.

**Ví dụ:**

```text
Features/
├── Profile/
│   ├── Presentation
│   ├── Domain
│   └── Data
│
└── Checkout/
    ├── Presentation
    ├── Domain
    └── Data
```

---

### 50. Module A → B → C → A. Bạn xử lý circular dependency thế nào?

**Ý chính:** Extract abstraction/shared module/invert dependency.

**Ý diễn giải:**
Tìm shared contract và đưa nó xuống module ổn định hơn hoặc đảo dependency direction.

**Ví dụ:**

```text
❌
A → B
B → C
C → A
```

Có thể:

```text
A ──→ Core ←── C
       ↑
       B
```

---

### 51. Một ViewModel có 15 dependency có phải architecture tốt vì mọi dependency đều explicit?

**Ý chính:** Explicit tốt; dependency explosion là smell.

**Ý diễn giải:**
Quá nhiều dependency thường cho thấy class có quá nhiều responsibility.

**Ví dụ:**

```swift
final class CheckoutViewModel {

    init(
        api: API,
        database: Database,
        payment: Payment,
        analytics: Analytics,
        cache: Cache,
        router: Router,
        logger: Logger,
        clock: Clock
    ) {
        // 🚨 Có thể quá nhiều responsibility
    }
}
```

---

### 52. Khi review architecture, bạn nhìn điều gì trước?

**Ý chính:** Dependency direction + state ownership + lifecycle + coupling.

**Ý diễn giải:**
Không bắt đầu bằng câu “Có dùng MVVM không?”. Hãy xem dependency đi đâu, ai sở hữu state và side effect nằm ở đâu.

**Ví dụ:**

```text
View
 ↓
ViewModel
 ↓
UseCase
 ↓
Repository
 ↓
DataSource
```

---

# Chủ đề: Concurrency

### 53. 5 request cùng lúc nhận 401. Refresh token nên được gọi mấy lần?

**Ý chính:** Single-flight refresh → một refresh operation.

**Ý diễn giải:**
Các request khác nên await cùng refresh task thay vì tạo refresh request riêng.

**Ví dụ:**

```swift
actor AuthManager {

    private var refreshTask:
        Task<Token, Error>?

    func validToken()
        async throws -> Token {

        if let task = refreshTask {
            return try await task.value
        }

        let task = Task {
            try await refresh()
        }

        refreshTask = task

        defer {
            refreshTask = nil
        }

        return try await task.value
    }
}
```

---

### 54. Tại sao `isRefreshing = true` chưa đủ để giải quyết concurrent refresh?

**Ý chính:** Cần chia sẻ kết quả refresh, không chỉ trạng thái.

**Ý diễn giải:**
Request B cần biết phải await operation nào. Boolean chỉ nói “đang refresh”, không cung cấp result/error.

**Ví dụ:**

```swift
actor AuthManager {

    var isRefreshing = false

    // Chưa đủ:
    // request khác không biết
    // phải await kết quả nào.
}
```

Tốt hơn:

```swift
private var refreshTask:
    Task<Token, Error>?
```

---

### 55. Làm sao tránh vòng lặp 401 → refresh → retry → 401 vô hạn?

**Ý chính:** Retry authentication tối đa một lần.

**Ý diễn giải:**
Request retry sau refresh nếu vẫn 401 thì authentication session thất bại.

**Ví dụ:**

```swift
if status == 401,
   !alreadyRetried {

    try await auth.refresh()

    return try await send(
        request,
        alreadyRetried: true
    )
}

throw APIError.unauthorized
```

---

### 56. Actor có đảm bảo một async method atomic từ đầu đến cuối không?

**Ý chính:** Không qua `await`.

**Ý diễn giải:**
Actor có thể re-enter khi operation suspend.

**Ví dụ:**

```swift
actor Store {

    var value = 0

    func update() async {

        value = 10

        await externalWork()

        // Một operation khác
        // có thể đã chạy ở đây.
    }
}
```

---

### 57. Một task CPU-heavy không dừng dù đã cancel. Vì sao?

**Ý chính:** Synchronous work không tự biết cancellation.

**Ý diễn giải:**
Cancellation cần checkpoint.

**Ví dụ:**

```swift
func calculate()
    async throws {

    for i in 0..<1_000_000 {

        try Task.checkCancellation()

        process(i)
    }
}
```

---

### 58. Task và Thread khác nhau thế nào?

**Ý chính:** Task = logical work; Thread = execution resource.

**Ý diễn giải:**
Task không được gắn cố định với một thread. Runtime quản lý scheduling và execution.

---

### 59. `Task.detached` có phải cách chuyển công việc sang background không?

**Ý chính:** Không.

**Ý diễn giải:**
Detached task không kế thừa context của task tạo nó. Nó không cấp background execution và làm isolation/Sendable phức tạp hơn.

**Ví dụ:**

```swift
Task.detached {
    await work()
}
```

---

### 60. Vì sao Structured Concurrency dễ reasoning hơn nhiều Task độc lập?

**Ý chính:** Lifecycle + cancellation + ownership.

**Ý diễn giải:**
Child task thuộc scope parent và parent quản lý lifecycle của chúng.

**Ví dụ:**

```swift
await withTaskGroup(
    of: Void.self
) { group in

    group.addTask {
        await taskA()
    }

    group.addTask {
        await taskB()
    }
}
```

---

### 61. Một TaskGroup có 10.000 task. Có vấn đề gì?

**Ý chính:** Unbounded concurrency.

**Ý diễn giải:**
Concurrent không có nghĩa càng nhiều càng nhanh. Cần giới hạn concurrency để tránh CPU/network/memory contention.

**Ví dụ:**

```text
10,000 tasks
      ↓
CPU contention
Memory pressure
Network pressure
Server overload
```

---

### 62. Continuation không resume thì điều gì xảy ra?

**Ý chính:** Suspended task có thể chờ vô hạn.

**Ý diễn giải:**
Mọi success/error/cancellation path phải đảm bảo continuation được resume đúng một lần.

**Ví dụ:**

```swift
try await withCheckedThrowingContinuation {
    continuation in

    legacyAPI { result in
        continuation.resume(
            with: result
        )
    }
}
```

---

### 63. Callback API trả event liên tục nên bridge bằng continuation hay AsyncStream?

**Ý chính:** Multiple events → `AsyncStream`.

**Ý diễn giải:**
Continuation phù hợp one-shot completion. AsyncStream phù hợp event stream.

**Ví dụ:**

```swift
func events()
    -> AsyncStream<Event> {

    AsyncStream { continuation in

        source.onEvent {
            continuation.yield($0)
        }

        source.onStop {
            continuation.finish()
        }
    }
}
```

---

# Chủ đề: Networking

### 64. Request POST timeout có nên retry ngay không?

**Ý chính:** Idempotency.

**Ý diễn giải:**
Server có thể đã xử lý thành công. Retry có thể tạo duplicate side effect. Cần idempotency key hoặc business semantics phù hợp.

**Ví dụ:**

```swift
request.setValue(
    UUID().uuidString,
    forHTTPHeaderField:
        "Idempotency-Key"
)
```

---

### 65. Exponential backoff giải quyết vấn đề gì?

**Ý chính:** Giảm retry pressure.

**Ý diễn giải:**
Khoảng retry tăng dần, tránh client spam server khi failure là transient.

**Ví dụ:**

```swift
let delay =
    pow(2.0, Double(attempt))

try await Task.sleep(
    for: .seconds(delay)
)
```

---

### 66. Jitter giải quyết vấn đề gì mà backoff chưa giải quyết?

**Ý chính:** Tránh synchronized retry.

**Ý diễn giải:**
Nhiều client có cùng backoff có thể retry cùng lúc. Jitter randomize thời điểm retry.

**Ví dụ:**

```swift
let base =
    pow(2.0, Double(attempt))

let jitter =
    Double.random(in: 0...0.5)

let delay =
    base + jitter
```

---

### 67. Nếu server trả 429, client nên làm gì?

**Ý chính:** Respect rate limit / Retry-After.

**Ý diễn giải:**
Không nên retry ngay lập tức. Nếu server cung cấp Retry-After thì nên tôn trọng giá trị đó.

**Ví dụ:**

```swift
if response.statusCode == 429 {

    let retryAfter =
        response.value(
            forHTTPHeaderField:
                "Retry-After"
        )
}
```

---

### 68. Vì sao nhiều request cùng resource nên deduplicate dù đã có cache?

**Ý chính:** Cache không xử lý in-flight request.

**Ý diễn giải:**
Nếu request đầu tiên vẫn đang chạy, cache chưa có data. Request mới cần join request đang chạy.

**Ví dụ:**

```swift
actor Loader {

    var inFlight:
        [URL: Task<Data, Error>] = [:]
}
```

---

### 69. WebSocket disconnect nên reconnect thế nào?

**Ý chính:** Backoff + jitter + lifecycle awareness.

**Ý diễn giải:**
Không reconnect liên tục. Cần retry policy và xem app đang foreground/background.

**Ví dụ:**

```swift
try await Task.sleep(
    for: .seconds(
        min(
            pow(2.0, Double(attempt)),
            30
        )
    )
)

connect()
```

---

### 70. Vì sao Background URLSession khác Task thông thường?

**Ý chính:** System-managed background transfer.

**Ý diễn giải:**
Task nằm trong app process. Background URLSession dành cho long-running transfer mà system có thể quản lý khi app không active.

**Ví dụ:**

```swift
let configuration =
    URLSessionConfiguration.background(
        withIdentifier:
            "downloads"
    )

let session = URLSession(
    configuration: configuration,
    delegate: self,
    delegateQueue: nil
)
```

---

# Chủ đề: Performance

### 71. CollectionView 1.000 ảnh scroll lag. Bạn debug từ đâu?

**Ý chính:** Profile whole pipeline.

**Ý diễn giải:**
Không kết luận ngay là cache. Kiểm tra CPU, main thread, image decode, resize, memory, reuse, layout, network và rendering.

**Ví dụ:**

```text
CollectionView
 ↓
Cell reuse
 ↓
Network
 ↓
Cache
 ↓
Decode
 ↓
Downsample
 ↓
Layout
 ↓
CALayer
 ↓
GPU
```

---

### 72. Tại sao image download nhanh nhưng scrolling vẫn lag?

**Ý chính:** Decode/rendering cost.

**Ý diễn giải:**
JPEG/PNG compressed bytes phải được decode thành raw pixels. Decode và resize có thể tốn CPU/memory nhiều hơn download.

**Ví dụ:**

```text
JPEG
 ↓
Decode
 ↓
Raw pixels
 ↓
Resize
 ↓
Render
```

---

### 73. Vì sao downsampling quan trọng?

**Ý chính:** Decode gần display size.

**Ý diễn giải:**
Không nên decode ảnh 4000×3000 chỉ để hiển thị thumbnail 100×75.

**Ví dụ:**

```text
Original:
4000 × 3000

Display:
100 × 75

→ Downsample
```

---

### 74. Time Profiler trả lời câu hỏi gì?

**Ý chính:** CPU hot path.

**Ý diễn giải:**
Nó cho biết CPU đang tiêu thời gian ở function/call stack nào.

---

### 75. Memory Graph dùng để tìm gì?

**Ý chính:** Object graph + retain path.

**Ý diễn giải:**
Dùng để xem object nào còn sống và reference nào đang giữ nó.

---

### 76. Memory tăng có chắc là leak?

**Ý chính:** Không.

**Ý diễn giải:**
Có thể là cache growth, temporary peak hoặc expected lifetime. Phải xem ownership graph.

---

### 77. Main thread bị block gây vấn đề gì?

**Ý chính:** Dropped frames + input lag.

**Ý diễn giải:**
Main thread xử lý UI event/layout/rendering. Synchronous work dài có thể phá frame budget.

**Ví dụ:**

```text
60 FPS
≈ 16.67 ms / frame
```

---

### 78. Một shadow phức tạp trên hàng trăm cell có thể ảnh hưởng gì?

**Ý chính:** Rendering/GPU cost.

**Ý diễn giải:**
Nhiều layer effect có thể làm tăng compositing/offscreen rendering cost.

**Ví dụ:**

```swift
view.layer.shadowOpacity = 0.3
view.layer.shadowRadius = 20
```

Cần profile thay vì mặc định tắt shadow.

---

### 79. Vì sao `shouldRasterize = true` không phải optimization universal?

**Ý chính:** Rasterization trade-off.

**Ý diễn giải:**
Rasterization có thể giúp content tĩnh được render lại ít hơn nhưng tăng memory hoặc trở nên vô ích với content thay đổi liên tục.

**Ví dụ:**

```swift
view.layer.shouldRasterize = true
view.layer.rasterizationScale =
    UIScreen.main.scale
```

---

### 80. Performance optimization nên bắt đầu bằng gì?

**Ý chính:** Measure → bottleneck → optimize → remeasure.

**Ý diễn giải:**
Không tối ưu theo cảm giác. Luôn đo trước và sau thay đổi.

---

# Chủ đề: System / iOS Internals

### 81. App là process hay thread?

**Ý chính:** App chạy trong process; process có nhiều thread.

**Ý diễn giải:**
Thread là execution resource nằm trong process.

**Ví dụ:**

```text
Application Process
 ├── Main Thread
 ├── Worker Thread
 └── Other Threads
```

---

### 82. RunLoop có nhiệm vụ gì?

**Ý chính:** Event processing loop.

**Ý diễn giải:**
RunLoop chờ và xử lý input, timers, sources và events.

**Ví dụ:**

```text
Wait
 ↓
Receive Event
 ↓
Process
 ↓
Layout / Display
 ↓
Wait again
```

---

### 83. Scene lifecycle khác application/process lifecycle thế nào?

**Ý chính:** Process lifetime ≠ scene lifetime.

**Ý diễn giải:**
Một process có thể chứa nhiều scene với UI state riêng.

**Ví dụ:**

```text
App Process
 ├── Scene A
 └── Scene B
```

---

### 84. App background có nghĩa Task chắc chắn tiếp tục chạy không?

**Ý chính:** Không.

**Ý diễn giải:**
Process có thể bị suspend hoặc terminate. Background execution phải dùng capability/API phù hợp.

**Ví dụ:**

```text
Active
 ↓
Background
 ↓
System
 ↓
Suspend / Resume / Terminate
```

---

### 85. BGTaskScheduler dùng để làm gì?

**Ý chính:** System-scheduled background work.

**Ý diễn giải:**
Cho phép đăng ký background work nhưng thời điểm chạy do system quyết định.

**Ví dụ:**

```swift
let request =
    BGProcessingTaskRequest(
        identifier:
            "com.example.cleanup"
    )

try BGTaskScheduler.shared
    .submit(request)
```

---

# CẤP ĐỘ 4 — SENIOR+

# 15 CÂU

---

# Chủ đề: Architecture / System Design

### 86. Bạn được yêu cầu dùng Clean Architecture cho toàn bộ app. Bạn có làm ngay không?

**Ý chính:** Architecture follows complexity.

**Ý diễn giải:**
Trước tiên đánh giá business complexity, change rate, team size, testability và data sources. Layer chỉ được tạo khi nó có giá trị.

**Ví dụ:**

```text
Simple Feature

View
 ↓
Service
```

có thể tốt hơn:

```text
View
 ↓
VM
 ↓
UseCase
 ↓
Repository
 ↓
DataSource
 ↓
Network
```

nếu feature chỉ có một operation đơn giản.

---

### 87. Domain layer phụ thuộc UIKit/Core Data/URLSession có vấn đề gì?

**Ý chính:** Dependency inversion violation.

**Ý diễn giải:**
Domain bị phụ thuộc infrastructure/framework, khó test và khó thay implementation.

**Ví dụ:**

```text
❌

Domain
 ↓
UIKit
CoreData
URLSession
```

Tốt hơn:

```text
Domain
 ↓
Protocol
 ↓
Infrastructure
```

---

### 88. Bạn thiết kế một app offline-first như thế nào?

**Ý chính:** Local database = UI source of truth; network = sync source.

**Ý diễn giải:**
UI observe local data. Network fetch/update database. User có thể sử dụng app ngay cả khi offline.

**Ví dụ:**

```text
Network
   ↓
Repository
   ↓
Database
   ↓
UI
```

Offline write:

```text
User edit
   ↓
Database
   ↓
UI immediately
   ↓
Pending sync
   ↓
Server
```

---

### 89. Nếu cache của user A được nhìn thấy bởi user B, bạn kiểm tra gì?

**Ý chính:** User-scoped cache key + invalidation.

**Ý diễn giải:**
Cache phải gắn user/session scope hoặc được clear khi authentication context thay đổi.

**Ví dụ:**

```swift
struct CacheKey: Hashable {
    let userID: String
    let resourceID: String
}
```

---

### 90. Một dependency container khổng lồ chứa toàn bộ service của app có vấn đề gì?

**Ý chính:** Global dependency graph + coupling + poor scope.

**Ý diễn giải:**
Container có thể trở thành God Object. Feature nên nhận dependency cần thiết thay vì giữ cả container.

**Ví dụ:**

```swift
// ❌
init(container: AppContainer)

// ✅
init(
    api: API,
    analytics: Analytics
)
```

---

# Chủ đề: Concurrency / Correctness

### 91. Một actor bảo vệ state nhưng workflow vẫn có logical race. Làm sao?

**Ý chính:** Actor chống data race, không tự chống logical race.

**Ý diễn giải:**
Nếu business operation được chia thành nhiều call với `await` ở giữa, state có thể thay đổi. Cần đưa invariant vào một isolated operation hoặc revalidate state.

**Ví dụ:**

```swift
if await store.hasItem(id) {
    await store.remove(id)
}
```

Có thể bị chen operation khác giữa hai call.

Tốt hơn:

```swift
await store.consumeIfAvailable(id)
```

---

### 92. 10.000 task cần gọi server nhưng server chỉ cho phép 10 concurrent requests. Bạn thiết kế thế nào?

**Ý chính:** Bounded concurrency / worker pool.

**Ý diễn giải:**
Không tạo unbounded request concurrency. Dùng queue/worker pool hoặc batch để giới hạn số operation active.

**Ví dụ:**

```text
10,000 items
      ↓
Queue
      ↓
10 workers
      ↓
Server
```

---

### 93. Vì sao semaphore truyền thống không phải lúc nào cũng phù hợp trong async code?

**Ý chính:** Blocking synchronization ≠ async suspension.

**Ý diễn giải:**
Một semaphore/lock blocking có thể giữ thread trong lúc chờ. Swift Concurrency nên ưu tiên async-aware coordination để tránh block execution resources.

**Ví dụ:**

```text
❌
Thread
 ↓
wait()
 ↓
BLOCKED
```

Trong async model nên hướng tới:

```text
Task
 ↓
SUSPEND
 ↓
Thread free
```

---

### 94. Một continuation bridge legacy API hỗ trợ cancellation. Bạn phải làm gì để cancellation truyền xuống API cũ?

**Ý chính:** Cancellation handler + cancel underlying operation.

**Ý diễn giải:**
Cancel Task không tự động cancel callback API. Wrapper phải kết nối hai lifecycle.

**Ví dụ:**

```swift
func load() async throws -> Data {

    try await withTaskCancellationHandler {

        try await withCheckedThrowingContinuation {
            continuation in

            startLegacyRequest(
                continuation: continuation
            )
        }

    } onCancel: {

        cancelLegacyRequest()
    }
}
```

---

# Chủ đề: Security

### 95. Certificate pinning có phải luôn nên bật cho mọi app không?

**Ý chính:** Threat model + operational trade-off.

**Ý diễn giải:**
Pinning có thể tăng trust control nhưng certificate/key rotation sẽ phức tạp hơn. Không nên bật máy móc nếu threat model không yêu cầu.

**Ví dụ:**

```text
TLS
 ↓
Trust validation
 ↓
Optional pinning
 ↓
Server
```

---

### 96. API secret hard-code trong binary rồi obfuscate có thực sự an toàn không?

**Ý chính:** Obfuscation ≠ secure secret storage.

**Ý diễn giải:**
Nếu client có thể sử dụng secret, attacker có thể reverse engineer hoặc observe runtime để lấy giá trị.

**Ví dụ:**

```swift
// ❌
let secret =
    decodeObfuscatedValue()
```

Giấu cách encode không biến secret thành trusted secret.

---

### 97. Jailbreak detection có thể được xem là security boundary không?

**Ý chính:** Không. Defense in depth.

**Ý diễn giải:**
Attacker có quyền kiểm soát thiết bị có thể patch/bypass detection. Server vẫn phải enforce authorization.

**Ví dụ:**

```text
Jailbreak Detection
        ↓
Risk Signal

NOT:

Jailbreak Detection
        ↓
Authorization
```

---

### 98. Biometric authentication thực sự bảo vệ cái gì?

**Ý chính:** User authentication/access control; không phải storage.

**Ý diễn giải:**
Face ID/Touch ID thường được dùng để gate access tới protected resource, ví dụ Keychain item. Không nên coi biometric là nơi lưu password/token.

**Ví dụ:**

```swift
let context = LAContext()

context.evaluatePolicy(
    .deviceOwnerAuthentication,
    localizedReason:
        "Xác thực để tiếp tục"
) { success, _ in

    if success {
        useProtectedCredential()
    }
}
```

---

# Chủ đề: Security + Performance + System

### 99. Một màn hình hiển thị OTP nhưng app đang chuyển background. Bạn bảo vệ dữ liệu thế nào?

**Ý chính:** Snapshot protection + sensitive UI handling.

**Ý diễn giải:**
Không thể ngăn tuyệt đối mọi hình thức capture, nhưng có thể che nội dung nhạy cảm khi app background và phản ứng với capture state phù hợp.

**Ví dụ:**

```swift
func applicationDidEnterBackground(
    _ application: UIApplication
) {
    privacyOverlay.isHidden = false
}

func applicationWillEnterForeground(
    _ application: UIApplication
) {
    privacyOverlay.isHidden = true
}
```

---

### 100. Nếu phải review toàn bộ một app iOS trước khi release production, bạn kiểm tra những gì?

**Ý chính:** `Security + Architecture + Lifecycle + Concurrency + Performance + Persistence`.

**Ý diễn giải:**
Senior review không nên chỉ kiểm tra “app có chạy”. Cần kiểm tra dependency direction, shared mutable state, cancellation, authentication, secure storage, logging, memory, rendering, background behavior, persistence và failure recovery.

**Ví dụ:**

```text
Production Readiness
        │
        ├── Architecture
        │      ↓
        │   Coupling / Dependency
        │
        ├── Concurrency
        │      ↓
        │   Race / Cancellation
        │
        ├── Networking
        │      ↓
        │   Auth / Retry / Timeout
        │
        ├── Persistence
        │      ↓
        │   Migration / Consistency
        │
        ├── Performance
        │      ↓
        │   CPU / Memory / UI
        │
        ├── Security
        │      ↓
        │   Token / Keychain / TLS
        │
        └── System
               ↓
            Lifecycle /
            Background
```

---

# 20 CÂU SENIOR QUAN TRỌNG NHẤT

Nếu không có nhiều thời gian ôn, ưu tiên:

```text
1.  401 concurrent → refresh mấy lần?
2.  Actor reentrancy là gì?
3.  Actor khác mutex thế nào?
4.  Task.cancel có kill task không?
5.  Task.detached khác Task thế nào?
6.  TaskGroup có nên tạo 10.000 task?
7.  Continuation phải resume mấy lần?
8.  Callback stream dùng AsyncStream thế nào?
9.  Repository khác Use Case thế nào?
10. Khi nào KHÔNG cần Clean Architecture?
11. Service Locator hidden dependency vì sao?
12. API POST timeout có retry không?
13. Retry cần idempotency thế nào?
14. Cache miss có gọi network ngay không?
15. Offline-first source of truth là gì?
16. CollectionView 1.000 ảnh lag debug từ đâu?
17. Memory tăng có chắc leak không?
18. App background Task có chạy tiếp không?
19. Hard-code API secret có thực sự secure không?
20. Client bị compromise thì security boundary nằm ở đâu?
```

# MASTER MAP — 100 CÂU

```text
                    100 CÂU SENIOR iOS
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
     JUNIOR              MIDDLE             SENIOR+
       │                   │                   │
   Core Swift          ARC / Memory        Architecture
   UIKit               UIKit               Concurrency
   SwiftUI             SwiftUI             Networking
   Network             Concurrency          Performance
   Persistence         Architecture         Security
                       DI                   System
                       Persistence
```

## Cách phân biệt level

```text
JUNIOR
→ "Cái này là gì?"

MIDDLE
→ "Dùng nó như thế nào?"

SENIOR
→ "Tại sao dùng nó?"
→ "Khi nào không dùng?"
→ "Trade-off là gì?"

SENIOR+
→ "Nếu hệ thống có 1 triệu user?"
→ "Nếu concurrent?"
→ "Nếu network fail?"
→ "Nếu app background?"
→ "Nếu state thay đổi giữa await?"
→ "Nếu client bị compromise?"
```

## Công thức tư duy Senior

```text
Requirement
    ↓
Ownership
    ↓
State
    ↓
Dependency
    ↓
Concurrency
    ↓
Lifecycle
    ↓
Failure
    ↓
Performance
    ↓
Security
    ↓
Trade-off
```

Một ứng viên Senior mạnh không phải người nhớ nhiều framework nhất, mà là người có thể nhìn một bài toán và trả lời được:

> **“Tôi chọn cách này vì nó giải quyết vấn đề X, nhưng trade-off là Y. Nếu constraint thay đổi thành Z thì tôi sẽ đổi thiết kế như thế nào?”**

# 100 CÂU PHỎNG VẤN SENIOR iOS — PHẦN 2

# CÂU 101 → 200

## PHÂN BỐ

| Cấp độ   |  Số câu |
| -------- | ------: |
| Middle+  |      20 |
| Senior   |      50 |
| Senior+  |      30 |
| **Tổng** | **100** |

---

# CẤP ĐỘ 2 — MIDDLE+

# 20 CÂU

---

# Chủ đề: SWIFT CORE

## 101. Một API nhận một object nhưng bạn muốn đảm bảo API không thể thay đổi object đó. Bạn thiết kế thế nào?

**Ý chính:** `let` + immutable abstraction.

**Ý diễn giải:**
Nếu dữ liệu chỉ cần đọc, ưu tiên immutable property và value type. Nếu API nhận reference type mutable, `let` chỉ khóa reference chứ không khóa nội dung object.

**Ví dụ:**

```swift
struct User {
    let id: Int
    let name: String
}

func display(_ user: User) {
    print(user.name)
}
```

---

## 102. Một class có property khai báo bằng `let`, nhưng object bên trong vẫn thay đổi được. Vì sao?

**Ý chính:** `let` trên reference chỉ khóa reference, không khóa object.

**Ý diễn giải:**
`let` với class nghĩa là biến không thể trỏ sang instance khác. Instance vẫn có thể mutable nếu property của object là `var`.

**Ví dụ:**

```swift
final class User {
    var name = "A"
}

let user = User()

user.name = "B"   // hợp lệ
// user = User()  // không hợp lệ
```

---

## 103. Một protocol có default implementation nhưng class conform lại có method cùng tên. Khi gọi qua protocol type, kết quả không như mong đợi. Vì sao?

**Ý chính:** `Protocol requirement dispatch` vs extension dispatch.

**Ý diễn giải:**
Nếu method không phải requirement của protocol, implementation trong extension có thể được chọn khi nhìn object qua protocol existential.

**Ví dụ:**

```swift
protocol P {
}

extension P {
    func hello() {
        print("Extension")
    }
}

struct A: P {
    func hello() {
        print("A")
    }
}

let value: any P = A()
value.hello()

// Có thể in:
// Extension
```

---

## 104. Một function generic chạy tốt với nhiều type nhưng bạn muốn ép các type phải tuân theo một capability cụ thể. Bạn làm thế nào?

**Ý chính:** Generic constraint.

**Ý diễn giải:**
Generic có thể kết hợp protocol constraint để giữ type safety và chỉ cho phép những type có capability cần thiết.

**Ví dụ:**

```swift
protocol IdentifiableEntity {
    associatedtype ID: Hashable
    var id: ID { get }
}

func find<T: IdentifiableEntity>(
    _ item: T,
    id: T.ID
) -> Bool {
    item.id == id
}
```

---

# Chủ đề: MEMORY

## 105. Closure chỉ được lưu 2 giây rồi bị giải phóng, nhưng object vẫn không deinit. Bạn sẽ tìm gì?

**Ý chính:** `Retain graph`.

**Ý diễn giải:**
Closure hết lifetime nhưng object vẫn có thể bị giữ bởi delegate, task, timer, notification, cache hoặc một closure khác.

**Ví dụ:**

```swift
deinit {
    print("released")
}
```

Dùng Memory Graph để tìm retain path thay vì chỉ nhìn closure.

---

## 106. Một object dùng `unowned` nhưng thỉnh thoảng crash khi callback chạy muộn. Nguyên nhân là gì?

**Ý chính:** `Lifetime assumption sai`.

**Ý diễn giải:**
`unowned` không biến thành nil. Nếu object target đã deallocate mà code vẫn truy cập, ứng dụng trap.

**Ví dụ:**

```swift
final class Child {

    unowned let parent: Parent

    init(parent: Parent) {
        self.parent = parent
    }
}
```

Nếu `parent` chết trước `child`, access sẽ gây runtime failure.

---

# Chủ đề: UIKIT / SWIFTUI

## 107. Một UIViewController đã pop nhưng `deinit` chưa chạy. Có phải navigation controller bị leak không?

**Ý chính:** Không kết luận ngay. `Retain path` cần được xác định.

**Ý diễn giải:**
Navigation controller có thể vẫn giữ controller nếu stack chưa thay đổi như bạn nghĩ, hoặc một object khác đang giữ controller. Cần kiểm tra memory graph.

**Ví dụ:**

```swift
deinit {
    print("Profile VC released")
}
```

---

## 108. Một SwiftUI row nhận cả một model lớn trong khi chỉ hiển thị một string. Điều gì có thể không tối ưu?

**Ý chính:** `Dependency granularity`.

**Ý diễn giải:**
Row chỉ nên phụ thuộc dữ liệu cần thiết nếu việc truyền model lớn khiến invalidation rộng hơn hoặc coupling tăng.

**Ví dụ:**

```swift
struct Row: View {

    let title: String

    var body: some View {
        Text(title)
    }
}
```

thay vì:

```swift
struct Row: View {

    let entireApplicationState: AppState

    var body: some View {
        Text(entireApplicationState.title)
    }
}
```

---

# Chủ đề: NETWORKING

## 109. API trả JSON thành công nhưng model decode fail. Bạn cần phân loại lỗi này thế nào?

**Ý chính:** `Transport success + decoding failure`.

**Ý diễn giải:**
Server có thể trả response hợp lệ nhưng contract không khớp model. Đây khác với network failure và nên được log/monitor riêng.

**Ví dụ:**

```swift
do {
    let user = try decoder.decode(
        User.self,
        from: data
    )
} catch {
    throw APIError.decoding
}
```

---

## 110. Một request có thể mất 20 giây nhưng user chỉ chờ 2 giây. Bạn chọn timeout hay cancellation?

**Ý chính:** Có thể dùng cả hai, nhưng semantics khác nhau.

**Ý diễn giải:**
Timeout là policy của operation. Cancellation là do caller không còn cần kết quả. UI search thường thiên về cancellation; API operation có SLA rõ có thể có timeout.

**Ví dụ:**

```swift
request.timeoutInterval = 2
```

và:

```swift
task.cancel()
```

---

# Chủ đề: PERSISTENCE

## 111. Bạn có 1 triệu bản ghi nhưng UI chỉ cần 50 bản ghi mỗi lần. Bạn xử lý thế nào?

**Ý chính:** `Pagination + fetch limit + indexing`.

**Ý diễn giải:**
Không fetch toàn bộ rồi lọc trong memory. Database phải query theo page/cursor với index phù hợp.

**Ví dụ:**

```swift
request.fetchLimit = 50
request.fetchOffset = 100
```

---

## 112. Tại sao cache không nên giữ vô hạn?

**Ý chính:** `Unbounded memory growth`.

**Ý diễn giải:**
Cache phải có eviction hoặc TTL. Nếu không, cache biến thành nguồn memory pressure.

**Ví dụ:**

```swift
struct CacheEntry<Value> {
    let value: Value
    let expiresAt: Date
}
```

---

# CẤP ĐỘ 3 — SENIOR

# 50 CÂU

---

# Chủ đề: SWIFT / DESIGN

## 113. Bạn có một class được dùng ở 50 nơi. Đổi nó sang struct có phải luôn là một cải tiến không?

**Ý chính:** `Semantics first`.

**Ý diễn giải:**
Không. Struct và class khác nhau về identity, ownership, inheritance và reference semantics. Chuyển type chỉ vì “struct tốt hơn” có thể phá behavior.

**Ví dụ:**

```swift
struct User {
    let id: Int
}

final class Session {
    let id: String
}
```

Session có lifecycle/identity rõ ràng thì class có thể hợp lý hơn.

---

## 114. Một API truyền class vào nhưng bạn không muốn caller giữ reference để mutate sau đó. Bạn có những lựa chọn nào?

**Ý chính:** Value snapshot / immutable type / copy semantics.

**Ý diễn giải:**
Có thể chuyển dữ liệu thành struct snapshot hoặc expose read-only abstraction. Chỉ `let` reference không ngăn caller thay đổi mutable object.

**Ví dụ:**

```swift
struct UserSnapshot {
    let id: Int
    let name: String
}
```

---

## 115. Khi nào type erasure là giải pháp tốt và khi nào nó che mất thông tin type có giá trị?

**Ý chính:** `Abstraction vs type information`.

**Ý diễn giải:**
Type erasure hữu ích khi cần lưu trữ nhiều concrete type trong một container. Nhưng nếu generic information có giá trị cho compiler hoặc API semantics, erase quá sớm sẽ làm mất type safety.

**Ví dụ:**

```swift
let sequence: AnySequence<Int> =
    AnySequence([1, 2, 3])
```

---

# Chủ đề: ARC / MEMORY

## 116. Một closure cần gọi self nhưng bạn không muốn giữ self sống lâu hơn lifecycle của operation. Bạn chọn strong hay weak?

**Ý chính:** `Ownership semantics`.

**Ý diễn giải:**
Không có câu trả lời luôn luôn là weak. Nếu operation cần self để hoàn thành và self phải sống cùng operation, strong có thể đúng. Nếu operation không được phép giữ object sống lâu, weak phù hợp hơn.

**Ví dụ:**

```swift
task = Task { [weak self] in
    guard let self else {
        return
    }

    await self.load()
}
```

---

## 117. Vì sao `[weak self]` đôi khi làm feature không hoạt động?

**Ý chính:** Self deallocated trước callback.

**Ý diễn giải:**
Weak chỉ giữ optional reference. Nếu không còn strong owner, self có thể biến mất trước khi callback chạy.

**Ví dụ:**

```swift
Task { [weak self] in

    try? await Task.sleep(
        for: .seconds(2)
    )

    self?.update()
}
```

Self có thể đã nil.

---

## 118. Bạn nghi ngờ retain cycle nhưng Memory Graph không cho thấy object nào “leak”. Điều gì có thể đang xảy ra?

**Ý chính:** `Expected long lifetime / hidden owner / cache`.

**Ý diễn giải:**
Object có thể vẫn reachable hợp lệ. Leaks không đồng nghĩa “object sống lâu hơn mong muốn”. Cần so sánh lifecycle expected với actual ownership.

---

# Chủ đề: SWIFTUI

## 119. `@State` lưu object reference có nghĩa object được SwiftUI giữ lifecycle như thế nào?

**Ý chính:** State storage theo View identity.

**Ý diễn giải:**
SwiftUI quản lý state storage qua identity của View. Khi identity thay đổi, state storage có thể thay đổi. Không nên xem `@State` đơn giản như một property bình thường.

**Ví dụ:**

```swift
@State private var count = 0
```

---

## 120. Một parent có 20 children nhưng chỉ một child cần một state. Bạn sẽ tổ chức state thế nào?

**Ý chính:** `Minimal state scope`.

**Ý diễn giải:**
Đặt state gần nơi sở hữu nhất có thể. State càng cao trong hierarchy, càng nhiều subtree có thể bị invalidated khi thay đổi.

**Ví dụ:**

```swift
struct Parent: View {

    var body: some View {
        VStack {
            Header()
            Detail()
        }
    }
}
```

State của Detail nên thuộc Detail nếu không cần parent.

---

## 121. Vì sao một object đưa vào Environment có thể tiện nhưng khó debug?

**Ý chính:** `Implicit dependency`.

**Ý diễn giải:**
View không khai báo dependency trong initializer. Khi chạy thiếu Environment value, lỗi có thể nằm xa nơi dependency được inject.

**Ví dụ:**

```swift
ProfileView()
    .environment(session)
```

---

## 122. Một SwiftUI list có 10.000 item và mỗi row chạy formatter phức tạp. Bạn xử lý ở đâu?

**Ý chính:** `Precompute / memoize / move expensive work outside rendering`.

**Ý diễn giải:**
Không nên thực hiện CPU-heavy transformation mỗi lần body được recompute. Có thể chuẩn bị presentation model trước.

**Ví dụ:**

```swift
struct RowModel {
    let title: String
    let subtitle: String
}
```

Row chỉ render dữ liệu đã chuẩn bị.

---

# Chủ đề: UIKIT

## 123. Auto Layout có thể đúng về mặt logic nhưng vẫn chậm. Vì sao?

**Ý chính:** `Constraint solving cost`.

**Ý diễn giải:**
Hierarchy lớn, nested views và self-sizing phức tạp có thể làm layout cost tăng. Correctness và performance là hai vấn đề khác nhau.

---

## 124. Vì sao self-sizing cell có thể gây performance problem?

**Ý chính:** `Repeated layout measurement`.

**Ý diễn giải:**
Cell phải tính kích thước dựa trên Auto Layout. Nếu hierarchy phức tạp, việc đo nhiều cell trong scrolling có thể tốn CPU.

**Ví dụ:**

```swift
tableView.rowHeight =
    UITableView.automaticDimension
```

---

## 125. Một cell có rất nhiều subview nhưng chỉ một số visible tại một thời điểm. Bạn tối ưu thế nào?

**Ý chính:** `Reduce hierarchy + lazy content + reuse`.

**Ý diễn giải:**
Không nhất thiết render mọi subview từ đầu nếu content có thể trì hoãn. Đơn giản hóa hierarchy cũng có thể giảm layout/render cost.

---

# Chủ đề: NETWORKING

## 126. Nếu 5 API cùng lúc 401, làm sao để chỉ refresh một lần?

**Ý chính:** `Single-flight`.

**Ý diễn giải:**
Auth manager giữ in-flight refresh task. Request mới join vào task hiện tại.

**Ví dụ:**

```swift
actor AuthManager {

    private var refreshTask:
        Task<Token, Error>?

    func refreshIfNeeded()
        async throws -> Token {

        if let refreshTask {
            return try await refreshTask.value
        }

        let task = Task {
            try await refreshToken()
        }

        refreshTask = task

        defer {
            refreshTask = nil
        }

        return try await task.value
    }
}
```

---

## 127. Nếu hai request cùng refresh nhưng request A thành công và request B thất bại, bạn cần suy nghĩ về điều gì?

**Ý chính:** `Single source of refresh truth`.

**Ý diễn giải:**
Nếu refresh operation thực sự được deduplicate, tình huống đó đã được thu hẹp. Nếu vẫn xảy ra, có thể có nhiều AuthManager instance hoặc race ở token storage.

---

## 128. Bạn có retry HTTP 500 ba lần. Nhưng mỗi lần đều tạo side effect ở server. Bạn đang thiếu gì?

**Ý chính:** `Idempotency`.

**Ý diễn giải:**
Retry không chỉ là technical mechanism. Mutation cần idempotent semantics hoặc idempotency key để tránh duplicate side effects.

**Ví dụ:**

```swift
request.setValue(
    operationID.uuidString,
    forHTTPHeaderField:
        "Idempotency-Key"
)
```

---

## 129. Vì sao client không nên tự map mọi HTTP status thành UI message?

**Ý chính:** `Layer separation`.

**Ý diễn giải:**
Networking layer nên phát technical/domain error. Presentation mới quyết định wording/localization.

**Ví dụ:**

```swift
enum APIError: Error {
    case unauthorized
    case forbidden
    case offline
    case server(Int)
}
```

---

## 130. Nếu network response rất lớn, ngoài CPU bạn còn quan tâm điều gì?

**Ý chính:** `Memory + copies + decoding`.

**Ý diễn giải:**
Data → decoding → model có thể tạo nhiều memory copies/intermediate objects. Cần xem peak memory và có thể streaming/batching nếu payload lớn.

---

# Chủ đề: PERSISTENCE

## 131. Bạn có local database và server cùng chứa dữ liệu. Ai là source of truth?

**Ý chính:** Phải định nghĩa rõ theo feature; không mặc định.

**Ý diễn giải:**
Offline-first thường local database là UI source of truth, còn server là authoritative backend source. Repository/sync layer quy định cách hai bên đồng bộ.

---

## 132. Một app ghi local thành công nhưng sync server thất bại. UI nên hiển thị gì?

**Ý chính:** `State reflects sync status`.

**Ý diễn giải:**
Không nên xóa local change chỉ vì server fail. Có thể hiển thị pending/syncing/error và retry theo policy.

**Ví dụ:**

```swift
enum SyncState {
    case synced
    case pending
    case failed(Error)
}
```

---

## 133. Hai thiết bị cùng sửa một record. Bạn xử lý conflict thế nào?

**Ý chính:** `Conflict resolution policy`.

**Ý diễn giải:**
Không có policy chung cho mọi app. Có thể server-wins, client-wins, field-level merge hoặc domain-specific resolution.

**Ví dụ:**

```swift
enum ConflictPolicy {
    case serverWins
    case clientWins
    case merge
}
```

---

## 134. Vì sao migration phải được test với dữ liệu thật hoặc fixture lịch sử?

**Ý chính:** `Historical schema compatibility`.

**Ý diễn giải:**
Production không chỉ chứa database của version gần nhất. User có thể update qua nhiều version khác nhau.

---

# Chủ đề: PERFORMANCE

## 135. CPU chỉ 20% nhưng scrolling vẫn dropped frames. Bạn điều tra gì?

**Ý chính:** GPU/render/layout/memory bandwidth.

**Ý diễn giải:**
Frame drop không nhất thiết do CPU. Kiểm tra compositing, transparency, shadow, blur, offscreen rendering và layout.

---

## 136. Memory cao nhưng app không crash. Bạn có cần sửa ngay không?

**Ý chính:** `Memory pressure / future risk`.

**Ý diễn giải:**
Không phải memory cao nào cũng bug, nhưng peak quá cao có thể dẫn đến termination hoặc performance degradation. Cần xem trend, device class và lifecycle.

---

## 137. Tại sao decode ảnh đúng kích thước hiển thị quan trọng?

**Ý chính:** `Downsampling`.

**Ý diễn giải:**
Raw pixel memory phụ thuộc resolution, không chỉ file size. Decode ảnh quá lớn gây CPU/memory waste.

---

## 138. Instruments cho thấy function chỉ chiếm 1% CPU nhưng code rất phức tạp. Bạn có tối ưu nó không?

**Ý chính:** `Optimize bottleneck, not complexity alone`.

**Ý diễn giải:**
Complexity về maintainability khác performance cost. Chỉ tối ưu performance khi nó thực sự ảnh hưởng measured workload.

---

# Chủ đề: SYSTEM

## 139. Scene A background nhưng Scene B active. Process có thể tiếp tục chạy không?

**Ý chính:** `Process lifecycle độc lập scene lifecycle`.

**Ý diễn giải:**
Một scene có thể background trong khi process vẫn hoạt động vì scene khác active. Không nên suy luận lifecycle process chỉ từ một scene.

---

## 140. App có thể bị terminate mà không nhận callback cuối cùng. Bạn thiết kế persistence thế nào?

**Ý chính:** `Persist incrementally`.

**Ý diễn giải:**
Critical state phải được lưu khi thay đổi hoặc ở những lifecycle points phù hợp, không phụ thuộc callback cuối.

---

# Chủ đề: SECURITY

## 141. Một API key public nằm trong iOS app có thực sự là secret không?

**Ý chính:** `Client-exposed credential ≠ server secret`.

**Ý diễn giải:**
Nếu binary/runtime chứa key mà app phải dùng, attacker có thể extract. Cần xác định key có thực sự cần secrecy hay chỉ là identifier/rate-limit mechanism.

---

## 142. Encryption có giải quyết được việc hard-code encryption key trong binary không?

**Ý chính:** Không nếu key cũng nằm trong client.

**Ý diễn giải:**
Nếu attacker có ciphertext và key trong cùng app, encryption không tạo trust boundary đáng kể.

---

# CẤP ĐỘ 4 — SENIOR+

# 30 CÂU

---

# Chủ đề: SYSTEM DESIGN

## 143. Thiết kế networking layer cho app có 100 API endpoint. Bạn tránh God Object như thế nào?

**Ý chính:** `Composable boundaries`.

**Ý diễn giải:**
Tách HTTP transport, auth, retry policy, decoder, endpoint definition và WebSocket thành component có responsibility rõ.

**Ví dụ:**

```text
APIClient
   ↓
HTTPTransport
AuthMiddleware
RetryPolicy
ResponseDecoder
Endpoint
```

---

## 144. Bạn có một AuthManager singleton và một AuthManager actor trong feature khác. Bạn lo ngại gì?

**Ý chính:** `Multiple sources of truth`.

**Ý diễn giải:**
Hai auth manager có thể giữ token/session state khác nhau. Authentication state nên có một owner rõ ràng.

**Ví dụ:**

```text
AuthManager A
   ↓
Token A

AuthManager B
   ↓
Token B

❌ Inconsistent session
```

---

## 145. Một feature có repository riêng nhưng 5 feature khác cũng cần cùng dữ liệu. Bạn có cho mỗi feature một repository instance không?

**Ý chính:** `Scope + shared state ownership`.

**Ý diễn giải:**
Không có câu trả lời cố định. Nếu repository stateless thì nhiều instance có thể ổn. Nếu có cache/session state, cần quyết định shared scope để tránh duplicate cache và inconsistent data.

---

## 146. Bạn có 3 module cùng cần User model. Nên đặt User ở đâu?

**Ý chính:** `Stable shared domain/core module` nếu semantics thực sự shared.

**Ý diễn giải:**
Không nên copy model giữa feature nếu chúng thực sự là cùng một domain concept. Nhưng cũng không nên đẩy mọi model vào Common chỉ vì tiện.

**Ví dụ:**

```text
Profile ─┐
Orders  ├──→ Identity/Core
Chat    ─┘
```

---

## 147. Một `Common` module ngày càng lớn. Bạn refactor thế nào?

**Ý chính:** `Split by capability + dependency analysis`.

**Ý diễn giải:**
Phân loại code theo responsibility và usage. Tách stable capabilities thành module riêng, loại bỏ dependency không cần thiết.

---

# Chủ đề: CONCURRENCY

## 148. Một actor có 1 triệu requests/giây đi qua. Actor có thể trở thành bottleneck không?

**Ý chính:** Có. `Serialization bottleneck`.

**Ý diễn giải:**
Actor giúp safety nhưng có thể giới hạn throughput nếu toàn bộ work dồn vào một isolation domain. Có thể partition state hoặc dùng nhiều actor theo key/shard khi semantics cho phép.

---

## 149. Bạn có nên chia một actor thành 100 actor để tăng performance không?

**Ý chính:** Không máy móc. `Parallelism vs coordination cost`.

**Ý diễn giải:**
Nhiều actor có thể tăng concurrency nhưng cũng tăng communication/complexity. Chỉ partition khi profiling cho thấy contention thực sự.

---

## 150. Một async function có 5 `await`, mỗi await gọi actor khác nhau. Điều gì cần chú ý?

**Ý chính:** `Multiple suspension points + interleaving + stale assumptions`.

**Ý diễn giải:**
State có thể thay đổi giữa mỗi await. Không được giả định workflow vẫn ở cùng state như lúc bắt đầu.

---

## 151. Bạn cần đảm bảo “check balance + deduct balance” là một business operation duy nhất. Làm sao?

**Ý chính:** `Atomic isolated operation`.

**Ý diễn giải:**
Đừng tách thành hai async calls nếu giữa chúng có thể bị chen operation khác. Đưa invariant vào cùng actor-isolated method.

**Ví dụ:**

```swift
actor Wallet {

    private var balance = 100

    func spend(_ amount: Int)
        -> Bool {

        guard balance >= amount else {
            return false
        }

        balance -= amount
        return true
    }
}
```

---

## 152. Một Task bị cancel nhưng side effect database vẫn xảy ra. Điều đó có sai không?

**Ý chính:** `Cancellation semantics vs committed side effect`.

**Ý diễn giải:**
Cancellation không rollback side effect đã thực hiện. Nếu business yêu cầu atomicity, phải dùng transaction/compensation chứ không dựa vào cancel.

**Ví dụ:**

```text
Task
 ↓
Write DB
 ↓
await
 ↓
Cancel

DB write có thể đã commit.
```

---

## 153. Cancellation có phải luôn được propagate tới child task không?

**Ý chính:** Structured child cancellation propagates; unstructured tasks cần quản lý riêng.

**Ý diễn giải:**
Không thể áp dụng một câu trả lời cho mọi loại task. Ownership model quyết định propagation.

---

# Chủ đề: NETWORKING / AUTH

## 154. Refresh token thành công nhưng 5 request retry vẫn nhận 401. Bạn nghi ngờ gì?

**Ý chính:** `Stale token propagation / request replay bug / server session invalidation`.

**Ý diễn giải:**
Có thể AuthManager giữ token mới nhưng request retry vẫn dùng header cũ, có nhiều token store hoặc server đã revoke session.

**Ví dụ:**

```text
Refresh success
   ↓
Token New

Retry
   ↓
Authorization: Bearer Old

❌ Replay bug
```

---

## 155. Một request đang retry thì user logout. Bạn có cho request đó tiếp tục không?

**Ý chính:** `Authentication lifecycle + cancellation`.

**Ý diễn giải:**
Thông thường không. Logout nên invalidate session, cancel pending authenticated work và ngăn retry dùng credential cũ.

**Ví dụ:**

```swift
func logout() {
    auth.invalidate()
    pendingRequests.forEach {
        $0.cancel()
    }
}
```

---

## 156. Request A đang refresh token, user logout, rồi refresh thành công. Bạn phải làm gì với token mới?

**Ý chính:** `Session generation / invalidation`.

**Ý diễn giải:**
Không được để refresh cũ resurrect session sau logout. Có thể dùng generation/version hoặc invalidate refresh task khi session thay đổi.

**Ví dụ:**

```swift
struct Session {
    let generation: Int
}
```

Refresh result phải kiểm tra generation trước khi commit.

---

## 157. Một app có nhiều account trên cùng device. Cache token và data nên scope thế nào?

**Ý chính:** `Account-scoped state`.

**Ý diễn giải:**
Credential, cache key, database records và pending operations cần gắn account/session để account A không thấy data của B.

**Ví dụ:**

```swift
struct CacheKey: Hashable {
    let accountID: String
    let resourceID: String
}
```

---

# Chủ đề: PERSISTENCE / CONSISTENCY

## 158. Local database commit thành công nhưng app crash trước khi sync queue được ghi. Điều gì xảy ra?

**Ý chính:** `Atomic persistence boundary`.

**Ý diễn giải:**
Nếu local mutation và pending sync record cần cùng tồn tại, nên thiết kế transaction để cả hai cùng commit hoặc cùng rollback.

**Ví dụ:**

```text
Transaction
 ├── Save User Change
 └── Add Pending Sync

Both success
OR
Both rollback
```

---

## 159. Bạn có thể dùng UserDefaults làm distributed lock giữa nhiều process không?

**Ý chính:** Không phù hợp.

**Ý diễn giải:**
UserDefaults không phải synchronization primitive. Shared state giữa app/extension cần cơ chế phù hợp với consistency/concurrency requirements.

---

## 160. Database có transaction rồi thì có cần actor không?

**Ý chính:** Có thể vẫn cần. `Transaction != concurrency isolation`.

**Ý diễn giải:**
Transaction bảo vệ tính atomic của database operation. Actor bảo vệ mutable state ở application layer. Hai thứ phục vụ hai tầng khác nhau.

---

# Chủ đề: PERFORMANCE / UI

## 161. App launch có 1 giây CPU nhưng first frame vẫn chậm. Bạn nghi ngờ gì?

**Ý chính:** `Post-main work / synchronous I/O / rendering / layout`.

**Ý diễn giải:**
CPU tổng không đủ để kết luận. Work có thể nằm trong I/O, blocking main thread, image decode hoặc first-frame layout/rendering.

---

## 162. Một optimization giảm CPU 20% nhưng battery không cải thiện. Vì sao?

**Ý chính:** `Battery bottleneck khác CPU bottleneck`.

**Ý diễn giải:**
Network radio, location, wakeups hoặc background activity có thể là nguồn tiêu pin chính.

---

## 163. Bạn giảm số lượng View nhưng UI vẫn chậm. Điều gì có thể xảy ra?

**Ý chính:** `Per-view cost > count`.

**Ý diễn giải:**
Một vài view với blur/shadow/mask/image processing nặng có thể đắt hơn hàng trăm view đơn giản.

---

## 164. SwiftUI body rất nhỏ nhưng scrolling vẫn lag. Bạn sẽ mở rộng phạm vi debug đến đâu?

**Ý chính:** `Body ≠ entire rendering pipeline`.

**Ý diễn giải:**
Kiểm tra image loading/decode, UIKit bridge, layout, environment invalidation, Core Animation và GPU.

---

# Chủ đề: SECURITY / SYSTEM

## 165. Nếu attacker kiểm soát thiết bị, bạn vẫn tin client-side role check không?

**Ý chính:** Không. `Server-side authorization`.

**Ý diễn giải:**
Client có thể bị patch. Role/permission phải được server kiểm tra.

**Ví dụ:**

```swift
// Client UI check
if user.isAdmin {
    showAdminButton()
}
```

Không thay thế:

```text
Server
 ↓
Check authorization
 ↓
Allow / Deny
```

---

## 166. Nếu app dùng certificate pinning nhưng attacker hook networking runtime thì sao?

**Ý chính:** `Client compromise can bypass client-side controls`.

**Ý diễn giải:**
Pinning tăng security nhưng không phải absolute defense nếu attacker kiểm soát runtime. Threat model cần defense in depth và server-side controls.

---

## 167. Secure logging nên làm gì với Authorization header?

**Ý chính:** `Redact`.

**Ý diễn giải:**
Không log token đầy đủ. Có thể bỏ hoàn toàn hoặc mask nếu cần debug correlation.

**Ví dụ:**

```swift
func redactedToken(
    _ token: String
) -> String {
    "\(token.prefix(4))****"
}
```

---

## 168. Screenshot protection có thể ngăn attacker dùng camera ngoài để chụp màn hình không?

**Ý chính:** Không. `No absolute screenshot prevention`.

**Ý diễn giải:**
App chỉ có thể giảm exposure trong những trường hợp system cho phép quan sát/can thiệp. Người dùng vẫn có thể dùng thiết bị khác để chụp.

---

# Chủ đề: SYSTEM DESIGN TỔNG HỢP

## 169. Một app cần realtime chat, offline messages và push notification. Bạn thiết kế data flow thế nào?

**Ý chính:** `Local DB source of truth + WebSocket realtime + Push signaling + sync`.

**Ý diễn giải:**
UI đọc local database. WebSocket ghi message vào database khi foreground/connected. Push đánh thức/signals khi cần. Sync layer đảm bảo missed messages được lấy lại.

**Ví dụ:**

```text
WebSocket ─────┐
               ↓
Push ─────────→ Sync Layer
               ↓
             Database
               ↓
               UI
```

---

## 170. Nếu WebSocket message và API response cùng update một record gần như đồng thời thì sao?

**Ý chính:** `Ordering + versioning + conflict policy`.

**Ý diễn giải:**
Không được dựa vào arrival time đơn thuần. Cần server sequence/version/timestamp hoặc domain-specific ordering để xác định state mới nhất.

**Ví dụ:**

```swift
struct MessageEvent {
    let version: Int
    let payload: Message
}
```

---

## 171. Một feature cần dữ liệu ngay lập tức, nhưng network có thể mất 30 giây. Bạn thiết kế UX/data flow thế nào?

**Ý chính:** `Local-first + stale data + background refresh`.

**Ý diễn giải:**
Hiển thị local snapshot nhanh, sau đó refresh network. UI nên thể hiện freshness/sync state khi cần.

**Ví dụ:**

```text
Open
 ↓
Local
 ↓
Show immediately
 ↓
Network refresh
 ↓
Persist
 ↓
Update UI
```

---

## 172. Một app vừa dùng SwiftUI vừa UIKit. Bạn quản lý navigation thế nào để tránh hai hệ thống cạnh tranh nhau?

**Ý chính:** `Single navigation owner per flow`.

**Ý diễn giải:**
Một flow nên có một navigation owner rõ. SwiftUI có thể quản lý state/navigation trong flow của nó, UIKit coordinator quản lý flow UIKit. Bridge ở boundary thay vì cả hai cùng push/present.

---

## 173. Nếu một feature đang migrate từ UIKit sang SwiftUI, state nên đặt ở đâu?

**Ý chính:** `Preserve source of truth; change presentation layer incrementally`.

**Ý diễn giải:**
Không cần chuyển state ownership cùng lúc với UI. Có thể giữ existing ViewModel/domain state và thay presentation layer từng bước.

**Ví dụ:**

```text
Existing
UIKit
 ↓
ViewModel
 ↓
Repository

Migration
SwiftUI
 ↓
ViewModel
 ↓
Repository
```

---

## 174. Bạn được yêu cầu hỗ trợ app trên thiết bị cũ với RAM thấp. Bạn ưu tiên tối ưu gì?

**Ý chính:** `Memory footprint + image size + cache policy + peak allocation`.

**Ý diễn giải:**
Không chỉ nhìn average memory. Peak memory và large images thường là vấn đề lớn. Giảm decoded image size và giới hạn cache trước khi micro-optimize code.

---

## 175. App crash chỉ xuất hiện trên thiết bị có RAM thấp khi mở gallery. Bạn kiểm tra gì?

**Ý chính:** `Peak memory + image decoding + cache`.

**Ý diễn giải:**
Gallery thường có hàng trăm ảnh. Decode full-resolution ảnh cùng lúc có thể tạo memory spike.

**Ví dụ:**

```text
Thumbnail 150 px
   ↓
Không decode 4000 px
   ↓
Downsample
   ↓
Reuse / cache bounded
```

---

## 176. Một app có 20 feature nhưng mọi feature cùng dùng một global mutable AppState. Rủi ro gì?

**Ý chính:** `Global mutable state + coupling`.

**Ý diễn giải:**
Một thay đổi có thể ảnh hưởng toàn app, khó test và khó xác định ownership. Chỉ nên globalize state thực sự global.

---

## 177. Bạn muốn một feature hoàn toàn độc lập để team khác phát triển và release riêng. Bạn cần thiết kế boundary gì?

**Ý chính:** `Module API + dependency contract + ownership`.

**Ý diễn giải:**
Feature nên expose entry point ổn định, hide implementation và nhận dependency từ composition root. Tránh import internal module khác.

**Ví dụ:**

```swift
public protocol ProfileFeatureFactory {
    func make() -> UIViewController
}
```

---

## 178. Nếu một module phải import 15 module khác mới build được, điều đó nói lên điều gì?

**Ý chính:** `High coupling`.

**Ý diễn giải:**
Module có thể không cohesive hoặc abstraction boundary chưa tốt. Nên kiểm tra dependency graph và xem có thể tách/fold responsibility hay không.

---

## 179. Một abstraction được dùng chỉ để mock một class trong duy nhất một test. Bạn có giữ abstraction không?

**Ý chính:** `Testability benefit vs abstraction cost`.

**Ý diễn giải:**
Không có quy tắc tuyệt đối. Nếu abstraction làm production architecture phức tạp chỉ để test một chi tiết implementation, có thể nên đổi cách test.

---

## 180. Làm sao phân biệt “architecture smell” với “code smell”?

**Ý chính:** `Local problem vs structural problem`.

**Ý diễn giải:**
Code smell có thể nằm trong một class/function. Architecture smell thường nằm ở dependency graph, ownership, module boundary và data flow.

---

## 181. Một service được dùng ở 50 feature nhưng mỗi feature cần behavior khác nhau. Bạn làm gì?

**Ý chính:** `Avoid giant shared abstraction`.

**Ý diễn giải:**
Có thể tách interface theo consumer để mỗi feature chỉ phụ thuộc capability mình cần.

**Ví dụ:**

```swift
protocol UserReader {
    func user() async throws -> User
}

protocol UserUpdater {
    func update(_ user: User) async throws
}
```

Thay vì:

```swift
protocol UserEverythingService {
    // 30 methods
}
```

---

## 182. Dependency Injection khiến constructor có 20 parameter. Bạn sẽ refactor theo tiêu chí nào?

**Ý chính:** `Cohesion`.

**Ý diễn giải:**
Nhóm dependency chỉ khi chúng thực sự thuộc cùng capability và lifecycle. Không gom tùy tiện chỉ để constructor ngắn.

**Ví dụ:**

```swift
struct AnalyticsDependencies {
    let analytics: Analytics
    let tracker: Tracker
}
```

Chỉ hợp lý nếu chúng cùng responsibility.

---

## 183. App có nhiều API client cho từng feature. Đây có phải duplicate architecture không?

**Ý chính:** Depends on boundary.

**Ý diễn giải:**
Nếu mỗi client có auth/retry/cache logic lặp lại thì không tốt. Nếu chúng chỉ encapsulate endpoint contract và chia sẻ common transport thì có thể hợp lý.

**Ví dụ:**

```text
ProfileAPI ─┐
CheckoutAPI ├──→ HTTPClient
SearchAPI   ─┘
```

---

## 184. Bạn có một global cache và một repository-local cache. Vấn đề gì có thể xảy ra?

**Ý chính:** `Duplicate cache + inconsistent invalidation`.

**Ý diễn giải:**
Hai cache có thể chứa hai giá trị khác nhau và có policy khác nhau. Thường nên xác định ownership/cache layer rõ ràng.

---

## 185. Database thay đổi dữ liệu nhưng UI không update. Bạn sẽ debug từ đâu?

**Ý chính:** `Observation path`.

**Ý diễn giải:**
Kiểm tra database save thành công, observation/query có refresh, mapping có tạo identity đúng và UI có subscribe đúng source of truth.

**Ví dụ:**

```text
Database changed
 ↓
Observation
 ↓
Repository
 ↓
ViewModel state
 ↓
UI
```

Tìm đoạn bị đứt.

---

## 186. Server trả data mới nhưng UI vẫn hiển thị cache cũ. Bạn tìm lỗi ở đâu?

**Ý chính:** `Cache invalidation / stale source`.

**Ý diễn giải:**
Kiểm tra write-back flow, cache key, TTL, database update và source of truth. Không chỉ xem network request.

---

## 187. Một task load data hoàn thành sau khi user logout và ghi data vào database. Tại sao nguy hiểm?

**Ý chính:** `Stale authenticated work`.

**Ý diễn giải:**
Task thuộc session cũ vẫn có thể mutate state sau khi session đã thay đổi. Cần cancellation hoặc session generation check.

**Ví dụ:**

```swift
let generationAtStart =
    session.generation

let data =
    try await load()

guard session.generation ==
      generationAtStart
else {
    return
}

save(data)
```

---

## 188. Nếu app có nhiều concurrent image requests, bạn ưu tiên tăng thread hay deduplicate request?

**Ý chính:** `Eliminate unnecessary work first`.

**Ý diễn giải:**
Tăng concurrency chỉ làm nhiều work hơn. Deduplicate có thể loại bỏ work hoàn toàn.

---

## 189. Một optimization giảm latency từ 500 ms xuống 300 ms nhưng tăng memory gấp 3 lần. Có đáng không?

**Ý chính:** `Trade-off`.

**Ý diễn giải:**
Không có optimization tuyệt đối. Nếu memory gây crash trên thiết bị thấp, latency improvement không đáng. Quyết định theo product SLO và device profile.

---

## 190. Một cache làm request nhanh hơn nhưng khiến dữ liệu stale. Bạn quyết định TTL thế nào?

**Ý chính:** `Business freshness requirement`.

**Ý diễn giải:**
TTL không nên chọn tùy ý. Xác định dữ liệu chấp nhận stale bao lâu và hậu quả business nếu stale.

---

## 191. Một background job tiêu 5% CPU nhưng app có hàng triệu user. Bạn có cần quan tâm không?

**Ý chính:** `Scale effect`.

**Ý diễn giải:**
Một cost nhỏ trên một device có thể trở thành infrastructure/battery/thermal issue ở quy mô lớn.

---

## 192. App sử dụng polling vì team chưa có WebSocket. Bạn cải thiện gì trước khi rewrite backend?

**Ý chính:** `Backoff + adaptive polling + lifecycle-aware polling`.

**Ý diễn giải:**
Không phải lúc nào cũng cần rewrite ngay. Có thể giảm tần suất khi app background, backoff khi không có thay đổi và dừng polling khi screen không active.

---

## 193. User scroll rất nhanh khiến 100 image requests được tạo. Bạn giải quyết ở tầng nào?

**Ý chính:** `Prefetch cancellation + request deduplication + concurrency limit`.

**Ý diễn giải:**
Không chỉ sửa cell. Image loader cũng cần cancellation và dedup. Collection layer có thể prefetch/cancel.

---

## 194. Một màn hình có 5 nguồn dữ liệu và một nguồn fail. Bạn có nên fail toàn bộ màn hình không?

**Ý chính:** `Partial failure semantics`.

**Ý diễn giải:**
Tùy UX. Dashboard có thể hiển thị 4 phần thành công và 1 phần lỗi. Business-critical screen có thể fail-fast.

**Ví dụ:**

```swift
enum SectionState<Value> {
    case loading
    case loaded(Value)
    case failed(Error)
}
```

---

## 195. Một request có thể bị timeout nhưng user vẫn muốn kết quả nếu nó hoàn thành sau. Bạn thiết kế sao?

**Ý chính:** `Request lifecycle vs UI lifecycle`.

**Ý diễn giải:**
Nếu UI timeout chỉ là presentation concern, operation có thể tiếp tục ở background; nếu work không còn giá trị, cancel. Không nên đồng nhất UI timeout với network cancellation.

---

## 196. Một API client singleton giữ `URLSession`, token, cache và delegate. Có vấn đề gì về lifecycle?

**Ý chính:** `Overloaded ownership`.

**Ý diễn giải:**
Singleton sống toàn app có thể giữ nhiều state rất lâu. Cần tách session-scoped state, user-scoped state và app-scoped infrastructure.

---

## 197. Một app có login/logout nhiều lần trong cùng process. Bạn quản lý session generation để làm gì?

**Ý chính:** `Prevent stale async work crossing sessions`.

**Ý diễn giải:**
Task từ session cũ có thể hoàn thành sau login mới. Generation/session ID giúp phát hiện kết quả cũ và bỏ qua.

**Ví dụ:**

```swift
struct SessionID: Equatable {
    let value: UUID
}
```

Operation giữ session ID lúc bắt đầu và validate trước khi commit.

---

## 198. Bạn muốn bảo vệ PII nhưng vẫn cần debug production issue. Bạn sẽ làm thế nào?

**Ý chính:** `Structured logging + redaction + correlation ID`.

**Ý diễn giải:**
Không log raw PII. Dùng stable non-sensitive identifiers, request ID và metadata đủ để trace issue.

**Ví dụ:**

```swift
logger.info(
    """
    request=\(requestID)
    status=\(statusCode)
    user=\(redactedUserID)
    """
)
```

---

## 199. Một app cần hỗ trợ thiết bị low-end nhưng team chỉ benchmark trên máy flagship. Vấn đề của cách đánh giá này là gì?

**Ý chính:** `Representative device profile`.

**Ý diễn giải:**
Performance, memory và battery phụ thuộc hardware. Benchmark flagship có thể che memory pressure, thermal throttling hoặc frame drop trên thiết bị yếu.

**Ví dụ:**

```text
Benchmark matrix

High-end
Mid-range
Low-memory
Old OS
Slow network
```

---

## 200. Bạn nhận một codebase lớn trước khi release. Làm thế nào quyết định cái gì phải sửa ngay và cái gì có thể để sau?

**Ý chính:** `Risk × impact × likelihood × cost`.

**Ý diễn giải:**
Senior không sửa mọi thứ. Ưu tiên crash, data loss, security vulnerability, race condition, authentication failure, severe performance và production blockers. Sau đó mới đến maintainability/cosmetic refactor.

**Ví dụ:**

```text
P0
→ Security / data loss / crash

P1
→ Major performance / auth / corruption

P2
→ Architecture debt / maintainability

P3
→ Refactor / cleanup
```

---

# 30 CÂU SENIOR+ QUAN TRỌNG NHẤT TRONG PHẦN 101–200

```text
143. Thiết kế API client mà không tạo God Object
144. Hai AuthManager → multiple source of truth
148. Actor có thể thành bottleneck không?
151. Check + mutation atomic trong actor
152. Cancellation không rollback side effect
154. Refresh thành công nhưng retry vẫn 401
156. Logout trong lúc refresh đang chạy
157. Multi-account cache/session isolation
158. Database + sync queue transaction
160. Transaction khác actor isolation
165. Client compromise → server authorization
169. Chat + WebSocket + Push + Offline DB
170. Ordering giữa WebSocket và API
171. Offline-first UX
172. UIKit + SwiftUI navigation ownership
174. Low-memory device optimization
176. Global mutable AppState
177. Feature module boundary
178. Module phụ thuộc quá nhiều module
182. 20 dependency trong constructor
184. Duplicate caches
185. Database → UI observation broken
186. Stale cache
187. Logout nhưng old task vẫn commit
188. Deduplicate trước khi tăng concurrency
189. Latency vs memory trade-off
190. TTL theo business freshness
191. Small cost × million users
193. 100 image requests khi scroll nhanh
194. Partial failure
195. UI timeout vs operation cancellation
196. Singleton lifecycle
197. Session generation
198. PII + secure logging
199. Low-end benchmark
200. Production risk prioritization
```

# MASTER MAP — 200 CÂU

```text
                         200 CÂU SENIOR iOS
                                │
        ┌───────────────────────┼───────────────────────┐
        │                       │                       │
      Swift                  UI / Data              Systems
        │                       │                       │
   ┌────┴────┐             ┌────┴────┐            ┌────┴────┐
   │         │             │         │            │         │
 Core      Memory       UIKit     SwiftUI       Network   Security
                                      │
                                Persistence
                                      │
                                Performance
                                      │
                                Concurrency
                                      │
                                Architecture
```

# CÔNG THỨC TƯ DUY CỦA 200 CÂU

Khi gặp một câu hỏi mới, thay vì nhớ “pattern nào”, hãy đi theo:

```text
Requirement
    ↓
State ownership
    ↓
Dependency ownership
    ↓
Lifecycle
    ↓
Concurrency
    ↓
Failure
    ↓
Persistence
    ↓
Performance
    ↓
Security
    ↓
Trade-off
```

Ở level Senior+, interviewer thường không hỏi:

```text
"Actor là gì?"
```

mà sẽ hỏi:

```text
"Actor đã bảo vệ state rồi,
tại sao code này vẫn có race?"
```

Không hỏi:

```text
"Cache là gì?"
```

mà hỏi:

```text
"Network trả data mới,
tại sao UI vẫn hiển thị data cũ?"
```

Không hỏi:

```text
"Dependency Injection là gì?"
```

mà hỏi:

```text
"Constructor có 20 dependency,
bạn sẽ làm gì?"
```

Không hỏi:

```text
"Background Task là gì?"
```

mà hỏi:

```text
"User logout trong lúc refresh token,
request cũ hoàn thành sau đó,
bạn ngăn session cũ ghi đè session mới thế nào?"
```

Đó là mức độ câu hỏi nên hướng tới khi ôn **Senior iOS thực chiến**.
