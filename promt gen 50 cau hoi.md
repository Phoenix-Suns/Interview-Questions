# PROMPT TẠO CÂU HỎI PHỎNG VẤN ANDROID

## VAI TRÒ
Bạn là một Senior Android Developer có kinh nghiệm phỏng vấn ứng viên từ Junior đến Senior level.

## YÊU CẦU
Tạo **50 câu hỏi và câu trả lời phỏng vấn** về **[CHỦ ĐỀ]** cho Android Developer.

### CẤU TRÚC TỔ CHỨC
- Phân chia theo **3 cấp độ**: Junior (Cơ bản), Mid-level (Trung cấp), Senior (Nâng cao)
- Mỗi cấp độ chia thành **nhiều chủ đề con** liên quan
- Mỗi chủ đề con có **3-7 câu hỏi**

### CẤU TRÚC MỖI CÂU HỎI
Mỗi câu hỏi phải bao gồm **4 phần** theo thứ tự:

#### 1. **Câu hỏi**
- Viết dưới dạng **tình huống thực tế** hoặc **vấn đề cần giải quyết**
- **KHÔNG** chứa keyword
- **KHÔNG** có tính gợi nhớ, không chứa hint, hay tips
- Mục đích: Kiểm tra hiểu biết thực tế, không phải ghi nhớ thuật ngữ

**Ví dụ tốt:**
- ✅ "Làm thế nào để lưu trữ dữ liệu nhạy cảm an toàn trên thiết bị?"
- ✅ "Hiện tượng đối tượng không thể bị dọn rác là gì?"

**Ví dụ xấu:**
- ❌ "EncryptedSharedPreferences là gì?"
- ❌ "Memory Leak là gì?"

#### 2. **Ý chính**
- **BẮT ĐẦU bằng Keyword/Thuật ngữ chuyên môn** (in đậm)
- Sau keyword là dấu gạch ngang `-` rồi đến giải thích ngắn gọn
- Viết **đơn giản, dễ hiểu, dễ ghi nhớ** nhất có thể
- Độ dài: 1-2 câu

**Format chuẩn:**
```
**Ý chính:** [Keyword] - [Giải thích ngắn gọn, dễ hiểu]
```

**Ví dụ:**
```
**Ý chính:** Memory Leak (Rò rỉ bộ nhớ) - Đối tượng không còn dùng nhưng không thể bị dọn rác (GC) vì bị một thằng khác giữ chặt.
```

#### 3. **Diễn giải**
- Giải thích **chi tiết hơn** nhưng vẫn **ngắn gọn** (2-4 câu)
- Làm rõ **tại sao**, **khi nào**, **ảnh hưởng như thế nào**
- Có thể bổ sung **best practices** hoặc **lưu ý quan trọng**

#### 4. **Ví dụ**
- Code phải **đơn giản, dễ hiểu** nhất có thể
- Bọc trong **code block** với ngôn ngữ phù hợp (`kotlin`, `xml`, `yaml`, `json`, `cpp`, `proguard`)
- Nên có **cả ví dụ SAI và ĐÚNG** để so sánh (nếu phù hợp)
- Thêm **comment giải thích** trong code khi cần thiết

**Format code block:**
````
```kotlin
// SAI: Mô tả lỗi
[code sai]

// ĐÚNG: Mô tả đúng
[code đúng]
```
````

---

## FORMAT ĐẦU RA

```markdown
# CÂU HỎI ÔN TẬP [TÊN CHỦ ĐỀ]

## CẤP ĐỘ 1: JUNIOR (CƠ BẢN)

### Chủ đề: [Tên chủ đề con 1]

#### 1. [Câu hỏi không có keyword]

**Ý chính:** [Keyword] - [Giải thích ngắn gọn]

**Diễn giải:** [Giải thích chi tiết hơn, 2-4 câu]

**Ví dụ:**

```kotlin
// SAI: [Mô tả]
[code sai]

// ĐÚNG: [Mô tả]
[code đúng]
```

#### 2. [Câu hỏi tiếp theo]
...

---

### Chủ đề: [Tên chủ đề con 2]
...

---

## CẤP ĐỘ 2: MID-LEVEL (TRUNG CẤP)

### Chủ đề: [Tên chủ đề con 3]
...

---

## CẤP ĐỘ 3: SENIOR (NÂNG CAO)

### Chủ đề: [Tên chủ đề con 5]
...
```

---

## QUY TẮC QUAN TRỌNG

### ✅ NÊN:
1. Câu hỏi phải **thực tế**, gần với công việc hàng ngày
2. Keyword phải xuất hiện **ĐẦU TIÊN** trong phần Ý chính
3. Code ví dụ phải **chạy được** và **dễ hiểu**
4. Sử dụng **dấu phân cách `---`** giữa các chủ đề
5. Đánh số câu hỏi **liên tục** từ 1-50

### ❌ KHÔNG NÊN:
1. Câu hỏi dạng "X là gì?" (trừ khi thực sự cần thiết)
2. Giải thích quá dài dòng, học thuật
3. Code ví dụ phức tạp, khó hiểu
4. Lặp lại nội dung giữa Ý chính và Diễn giải
5. Thiếu code block hoặc format sai

---

## PHÂN BỔ CÂU HỎI GỢI Ý

- **Junior (15-20 câu)**: Khái niệm cơ bản, cú pháp, API cơ bản
- **Mid-level (15-20 câu)**: Best practices, patterns, debugging, optimization
- **Senior (10-15 câu)**: Architecture, advanced patterns, security, performance tuning

---

## VÍ DỤ MẪU

### CẤP ĐỘ 1: JUNIOR (CƠ BẢN)

#### Chủ đề: Core Concepts

##### 1. Làm thế nào để xử lý nhiều tác vụ bất đồng bộ mà không làm treo ứng dụng?

**Ý chính:** Coroutine - Luồng gọn nhẹ (Lightweight thread) chạy bất đồng bộ.

**Diễn giải:** Coroutine không phải là Thread (luồng hệ điều hành). Nhiều Coroutine có thể chạy chung trên một Thread mà không làm treo Thread đó nhờ cơ chế tạm dừng (Suspending).

**Ví dụ:**

```kotlin
// Tạo 100,000 Coroutines - app vẫn mượt
repeat(100_000) {
    GlobalScope.launch {
        delay(1000L)
        println(".")
    }
}

// Tạo 100,000 Threads - app sẽ crash vì hết bộ nhớ
```

---

## CÁCH SỬ DỤNG PROMPT NÀY

Thay thế **[CHỦ ĐỀ]** bằng chủ đề cụ thể, ví dụ:
- "Jetpack Compose"
- "Room Database"
- "Retrofit & Networking"
- "Testing (Unit Test & UI Test)"
- "Material Design 3"
- "WorkManager"
- "Navigation Component"
- v.v.

**Ví dụ prompt hoàn chỉnh:**
```
Bạn là một Senior Android Developer có kinh nghiệm phỏng vấn ứng viên từ Junior đến Senior level.

Tạo 50 câu hỏi và câu trả lời phỏng vấn về **Jetpack Compose** cho Android Developer.

[Tiếp tục với toàn bộ nội dung prompt ở trên...]
```

---

**Lưu ý:** Prompt này được thiết kế để tạo ra câu hỏi phỏng vấn **chất lượng cao**, **thực tế**, và **dễ ôn tập** cho Android Developers ở mọi cấp độ.