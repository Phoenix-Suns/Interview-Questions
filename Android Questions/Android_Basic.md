# Câu hỏi Android Cơ bản

## Viewholder là gì

Thiết kế cho Custom Adapter.
Mô tả Item View và Dữ liệu trong RecyclerView.
Giúp không cần dùng findViewId như trong ListView

## phân biệt activity và fragment

Fragment là một phần giao diện người dùng hoặc hành vi của một ứng dụng. 
Fragment có thể được đặt trong Activity, nó có thể cho phép thiết kế activity với nhiều mô-đun. Tái sử dụng trong nhiều Activity.
Có thể nói Fragment là một loại sub-Activity. 
Fragment cũng có layout của riêng của nó, cũng có các hành vi và vòng đời riêng.

### - Khi nào thì dùng Fragment, cho ví dụ trong thực tế

Dùng cho UI Độc lập, hiển thị trong Activity, có thể sử dụng nhiều lần.
Ví dụ: nội dung của tab, a Dialog, a list, a ui of slider...

E:
We need a independent ui, to display on activity.
It a part of Activity.
Modular section of Activity.

Content of a tab, a Dialog, a list, a ui of slider...

## Khi nào method onResume() được gọi?

onResume() là một trong những activity lifecycle method. 
Gọi khi sau khi activity hiện thị lần nữa, sau khi ẩn đi bở onPause.


## 4 Component chính trong Android là gì

1. Activities:
Ra lệnh cho UI, sử lý sự kiện người dùng trên màn hình hiện tại
Là màn hình nhỏ, riêng lẻ

2. Services
Xử lý tiến trình chạy nền

3. Broadcast Receivers (nhận dự báo)
Xử lý giao tiếp Android và Người dùng

4. Content Providers
Xử lý dữ liệu, quản lý vấn đề

5. Intent
Tin nhắn, liên kết các Component lại

## Phân biệt Implicit và Explicit Intent

- Explicit Intent: tường minh, gọi trực tiếp tên ứng dụng
- Implicit Intent: ẩn ý, gọi chung chung, ứng dụng nào chạy thì chạy

## Phân biệt Service và IntentService

Service: Có thể chạy vô thời hạn.
IntentService: Tự dừng lại sau khi trả về kết quả, hay hàm **“onHandleIntent”** xử lý xong.

## Trình bày LifeCycle của Activity

![activity lifecycle](images/activity_lifecycle.png)

OnCreate - onStart (onRestart) - onResume
OnPause - OnStop - onDestroy

- OnCreate: Call on Activity first create.
Screen Rotate.
- OnStart: Activity become visible to user.
- OnResume:  After hidden, Visible Again to user.
- OnPause: Activity hidden, below other Activity, but we can see it.
- OnStop: Activity invisible to user. we can not see it.
- OnDestroy: Activity had be kill by User, or System.

## Trình bày LifeCycle của Fragment

![fragment lifecycle](images/fragment_lifecycle.png)

## Giải thích Back stack fragment manager

```java
// Thêm Fragment vào View(fragment_container)
// Nếu thêm nữa thì sẽ hiện cả 2, không Pause Fragment cũ
MyFragment fragment = new MyFragment();
transaction.add(R.id.fragment_container, fragment, "fragment_tag");

// Xóa Fragment
transaction.remove(fragment);
// Thay thế Fagment hiện tại = fragment = remove + add (Pause fragment cũ)
transaction.replace(R.id.fragment_container, fragment, "fragment_tag");

// giống Remove, không đính kèm, còn lưu trạng thái (TAG)
transaction.detach(fragment);
// đính kèm Fragment bị Detach trở lại, (findFragmentByTag() != null)
transaction.attach(fragment);
```

## Giải thích dp, dpi, pt, sp trong Android

dpi: (Dot per inch) là số lượng điểm ảnh hiển thị trên mỗi inch màn hình
Pt:  1/72 inch kích thước màn hình.

dp: density independent pixel. Phụ thuộc mật độ điểm ảnh.
Sp: scale independent pixel. Co theo mật độ điểm ảnh.

## Cho biết công thức quy đổi giữa px và dp

```java
public static float convertDpToPixel(float dp, Context context){
    return dp * ((float) context.getResources().getDisplayMetrics().densityDpi / DisplayMetrics.DENSITY_DEFAULT);
}

public static float convertPixelsToDp(float px, Context context){
    return px / ((float) context.getResources().getDisplayMetrics().densityDpi / DisplayMetrics.DENSITY_DEFAULT);
}
```

## Khi 1 activity đang chạy, ta nhấn nút Home thì activity đó đi vào những trạng thái nào

onStop

## Khi 1 Activity đang chạy, ta chọn recent apps, quét qua để kill app đó thì activity đó đi vào những trạng thái nào

onPause

## Khi 1 Activity đang chạy mà bị crash, activity đó đi vào trạng thái nào

onStop or onDestroy.
Tùy vị trí Crash Activity hay Application.

## Nếu thêm nhiều Fragment vào cùng 1 FrameLayout bằng FragmentManager thì thực tế hiển thị fragment nào, các fragment kia rơi vào trạng thái gì

- Hiển thị tất cả chồng lên nhau.
- Không rơi vào trạng thái nào. Trạng thái cuối là onResume

## Khi đang ở trong Activity, xoay màn hình thì Activity đi vào những trạng thái nào

onStart -> onResume

## Khi đang ở trong Activity, mở 1 AlertDialog thì activity đi vào những trạng thái nào

Không có

## Tạo mới 1 Thread trong activity, khi mở activity mới thì Thread đó có còn chạy ko

Vẫn chạy kể cả khi finish Activity

## MediaPlayer đang chạy trong, tạo mới activity khác, player đó còn chạy ko

Vẫn chạy

## Giải thích về 4 launchmode: standard, singleTop, singleTask, singleInstance

- Standard: Activity có thể khởi tạo nhiều lần
- SingleTop: (giống Standard). Nếu Activity ở Top, không khởi tạo, chỉ gọi lại onNewIntent.

- SingleTask: Chỉ có 1 Activity được khởi tạo. Mỗi lần Start Activity, clear Activity sau nó.
- singleInstance: Activity sẽ chạy Task khác. Nếu gọi Activity đã khởi tạo sẽ nhảy lên trên (clear Activity sau nó).

## Foreground và Background Service là gì, Bound service là gì

- Foreground Service: thực hiện hoạt động mà người dùng chú ý. (vd: nghe nhạc)
- Background Service: thực hiện hoạt động chạy ngầm. không cần báo người dùng.
- Bound Service: Component ràng buộc Service để lấy kết quả liên tục (như Client-Server)

## Phân biệt Serializable và Parcelable, cái nào tốt hơn

- Serializable: Chuyển Object(data) thành 1 dạng lưu trữ (text để lưu trữ và phục hồi)
- Parcelable: Gởi Object(data) thông qua các Bunble trong Android

## ANR là gì, khi nào nó xảy ra: Application not responding

- ANR: Ứng dụng đóng băng, không phải hồi cử chỉ người dùng.
- 

## So sánh LinearLayout và ConstrainLayout

- LinearLayout: các View con sắp theo 1 chiều (dọc, ngang).
- ConstrainLayout: các View con sắp xếp có liên kết với nhau.

## Sự khác nhau giữ View.GONE và View.INVISIBLE

- Gone: View biến mất, không giữ kích thước hiện tại.
- Invisible: View biến mất, vẫn giữ kích thước hiện tại.

## Liệt kê một số thư viện http đã dùng

- Retrofit, HttpRequest

## Rest APIs là gì, tại sao lại dùng nó

REST (Representation State Stranfer): một tiêu chuẩn dùng trong việc thết kế các thiết kế API cho các ứng dụng web.
API (Application Programming Interface): Giao diện lập trình ứng dụng.
RESTful API: ứng dụng sử dụng REST

## Tại sao Android dùng db SQLite

- Không phải cài đặt
- Không cần mô hình Client - Server
- Chỉ lưu trữ 1 file
- Chiếm ít bộ nhớ
- Hỗ trợ truy vấn SQL

## Android Gradle là gì

Gradle là một hệ thống tự động build mã nguồn mở

## Dependency injection là gì

- Là phương pháp giảm sự phụ thuộc 1 module trong 1 module
- Thay vì khởi tạo 1 object trong 1 object, ta khởi tạo nó bên ngoài. Rồi tim vào bên trong qua: constructer, setter, interface...

## Làm thế nào để upload 1 file ảnh trong máy Android lên server

- Tạo 1 Restfull Api upload ảnh
- Upload ảnh bằng thư viện Retrofit

---
