# Câu hỏi Android Cơ bản

- [Câu hỏi Android Cơ bản](#câu-hỏi-android-cơ-bản)
  - [Viewholder là gì](#viewholder-là-gì)
  - [Activity](#activity)
  - [English:](#english)
  - [Fragment](#fragment)
  - [phân biệt activity và fragment](#phân-biệt-activity-và-fragment)
    - [- Khi nào thì dùng Fragment, cho ví dụ trong thực tế](#--khi-nào-thì-dùng-fragment-cho-ví-dụ-trong-thực-tế)
  - [4 Component chính trong Android là gì](#4-component-chính-trong-android-là-gì)
  - [Phân biệt Implicit và Explicit Intent](#phân-biệt-implicit-và-explicit-intent)
  - [Phân biệt Service và IntentService](#phân-biệt-service-và-intentservice)
  - [Phân biệt Service, Intent Service, AsyncTask và Thread.](#phân-biệt-service-intent-service-asynctask-và-thread)
    - [Service Android 8.0](#service-android-80)
  - [Trình bày LifeCycle của Fragment](#trình-bày-lifecycle-của-fragment)
  - [Giải thích Back stack fragment manager](#giải-thích-back-stack-fragment-manager)
  - [Giải thích dp, dpi, pt, sp trong Android](#giải-thích-dp-dpi-pt-sp-trong-android)
  - [Cho biết công thức quy đổi giữa px và dp](#cho-biết-công-thức-quy-đổi-giữa-px-và-dp)
  - [Khi 1 activity đang chạy, ta nhấn nút Home thì activity đó đi vào những trạng thái nào](#khi-1-activity-đang-chạy-ta-nhấn-nút-home-thì-activity-đó-đi-vào-những-trạng-thái-nào)
  - [Khi 1 Activity đang chạy, ta chọn recent apps, quét qua để kill app đó thì activity đó đi vào những trạng thái nào](#khi-1-activity-đang-chạy-ta-chọn-recent-apps-quét-qua-để-kill-app-đó-thì-activity-đó-đi-vào-những-trạng-thái-nào)
  - [Khi 1 Activity đang chạy mà bị crash, activity đó đi vào trạng thái nào](#khi-1-activity-đang-chạy-mà-bị-crash-activity-đó-đi-vào-trạng-thái-nào)
  - [Nếu thêm nhiều Fragment vào cùng 1 FrameLayout bằng FragmentManager thì thực tế hiển thị fragment nào, các fragment kia rơi vào trạng thái gì](#nếu-thêm-nhiều-fragment-vào-cùng-1-framelayout-bằng-fragmentmanager-thì-thực-tế-hiển-thị-fragment-nào-các-fragment-kia-rơi-vào-trạng-thái-gì)
  - [Khi đang ở trong Activity, xoay màn hình thì Activity đi vào những trạng thái nào](#khi-đang-ở-trong-activity-xoay-màn-hình-thì-activity-đi-vào-những-trạng-thái-nào)
  - [Khi đang ở trong Activity, mở 1 AlertDialog thì activity đi vào những trạng thái nào](#khi-đang-ở-trong-activity-mở-1-alertdialog-thì-activity-đi-vào-những-trạng-thái-nào)
  - [Tạo mới 1 Thread trong activity, khi mở activity mới thì Thread đó có còn chạy ko](#tạo-mới-1-thread-trong-activity-khi-mở-activity-mới-thì-thread-đó-có-còn-chạy-ko)
  - [MediaPlayer đang chạy trong, tạo mới activity khác, player đó còn chạy ko](#mediaplayer-đang-chạy-trong-tạo-mới-activity-khác-player-đó-còn-chạy-ko)
  - [lúc nào onDestroy() được gọi mà không có onPause() và onStop()?](#lúc-nào-ondestroy-được-gọi-mà-không-có-onpause-và-onstop)
  - [tại sao chỉ nên gọi setContentView() trong onCreate()](#tại-sao-chỉ-nên-gọi-setcontentview-trong-oncreate)
  - [Giải thích về 4 launchmode: standard, singleTop, singleTask, singleInstance](#giải-thích-về-4-launchmode-standard-singletop-singletask-singleinstance)
  - [Foreground và Background Service là gì, Bound service là gì](#foreground-và-background-service-là-gì-bound-service-là-gì)
  - [Phân biệt Serializable và Parcelable, cái nào tốt hơn](#phân-biệt-serializable-và-parcelable-cái-nào-tốt-hơn)
  - [ANR là gì, khi nào nó xảy ra: Application not responding](#anr-là-gì-khi-nào-nó-xảy-ra-application-not-responding)
  - [So sánh LinearLayout và ConstrainLayout](#so-sánh-linearlayout-và-constrainlayout)
  - [Sự khác nhau giữ View.GONE và View.INVISIBLE](#sự-khác-nhau-giữ-viewgone-và-viewinvisible)
  - [Liệt kê một số thư viện http đã dùng](#liệt-kê-một-số-thư-viện-http-đã-dùng)
  - [Rest APIs là gì, tại sao lại dùng nó](#rest-apis-là-gì-tại-sao-lại-dùng-nó)
  - [Tại sao Android dùng db SQLite](#tại-sao-android-dùng-db-sqlite)
  - [Android Gradle là gì](#android-gradle-là-gì)
  - [Dependency injection là gì](#dependency-injection-là-gì)
  - [Làm thế nào để upload 1 file ảnh trong máy Android lên server](#làm-thế-nào-để-upload-1-file-ảnh-trong-máy-android-lên-server)
  - [Application](#application)
  - [Context](#context)
  - [Tại sao bytecode không thể chạy được trong Android?](#tại-sao-bytecode-không-thể-chạy-được-trong-android)
  - [Sealed class, data class](#sealed-class-data-class)

## Viewholder là gì

Thiết kế cho Custom Adapter.
Mô tả Item View và Dữ liệu trong RecyclerView.
Giúp không cần dùng findViewId như trong ListView

## Activity

![activity lifecycle](images/activity_lifecycle.png)

OnCreate - onStart (onRestart) - onResume
OnPause - OnStop - onDestroy

- OnCreate: Activity Tạo lần đầu.
- OnStart: Activity hiển thị với User. xoay màn hình.
- OnResume: Gọi khi sau khi activity hiển thị lần nữa, sau khi ẩn đi bởi onPause.

- OnPause: Activity ẩn, nằm sau Activity khác (nhưng còn thấy, vd: ẩn sau FragmentDialog).
- OnStop: Activity ẩn hoàn toàn với user. không thấy nó nữa.
- OnDestroy: Activity bị giết bởi User hay Hệ thống.

## English:

- OnCreate: Call on Activity first create.
Screen Rotate.
- OnStart: Activity become visible to user.
- OnResume:  After hidden, Visible Again to user.
- OnPause: Activity hidden, below other Activity, but we can see it.
- OnStop: Activity invisible to user. we can not see it.
- OnDestroy: Activity had be kill by User, or System.

## Fragment

là UI Độc lập
hiển thị 1 phần trong Activity
có thể sử dụng nhiều lần.
VD: nội dung của tab, a Dialog, a list, a ui of slider...

Fragment là một phần giao diện người dùng hoặc hành vi của một ứng dụng. Fragment có thể được đặt trong Activity, nó có thể cho phép thiết kế activity với nhiều mô-đun. Có thể nói Fragment là một loại sub-Activity. Fragment cũng có layout của riêng của nó, cũng có các hành vi và vòng đời riêng.

## phân biệt activity và fragment

Fragment là một phần giao diện người dùng hoặc hành vi của một ứng dụng. 
Fragment có thể được đặt trong Activity, nó có thể cho phép thiết kế activity với nhiều mô-đun. Tái sử dụng trong nhiều Activity.
Có thể nói Fragment là một loại sub-Activity. 
Fragment cũng có layout của riêng của nó, cũng có các hành vi và vòng đời riêng.

### - Khi nào thì dùng Fragment, cho ví dụ trong thực tế

là UI Độc lập, hiển thị 1 phần trong Activity, có thể sử dụng nhiều lần.
Ví dụ: nội dung của tab, a Dialog, a list, a ui of slider...

English:
We need a independent ui, to display on activity.
It a part of Activity.
Modular section of Activity.

Content of a tab, a Dialog, a list, a ui of slider...

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

5. Intent
Tin nhắn, liên kết các Component lại

## Phân biệt Implicit và Explicit Intent

- Explicit Intent: tường minh, gọi trực tiếp tên ứng dụng
- Implicit Intent: ẩn ý, gọi chung chung, ứng dụng nào chạy thì chạy

## Phân biệt Service và IntentService

Service: Có thể chạy vô thời hạn.
IntentService: Tự dừng lại sau khi trả về kết quả, hay hàm **“onHandleIntent”** xử lý xong.

## Phân biệt Service, Intent Service, AsyncTask và Thread.

- Service là một thành phần được sử dụng để thực hiện các tác vụ ở background ví dụ như chơi nhạc. Nó không có giao diện người dùng (user interface).
- AsyncTask cho phép bạn thực hiện các công việc bất đồng bộ ở background thread và publish kết quả lên trên UI thread mà không yêu cầu bạn phải xử lý cách các thread hay handler hoạt động.
- IntentService là một loại Service để xử lý lần lượt các yêu cầu bất đồng bộ (thông qua Intent) ở background thread. Client sẽ gửi yêu cầu thông qua việc gọi tới startService(Intent) và nó cũng không yêu cầu bạn phải "động tay động chân" tới việc xử lý thread / handler.
- Một Thread là một luồng thực thi tuần tự trong một chương trình. Thread có thể được coi là một mini-process chạy ở trong main process.

- Shorter:
<https://developer.android.com/guide/components/services>
- Service: Là 1 Android Component, có thể Chạy Ngầm, ngay cả khi người dùng không tương tác. Chạy trong luồng chính.
- AsyncTask: Thực hiện công việc ngoài luồng chính, chỉ trong khi người dùng còn tương tác ứng dụng.

### Service Android 8.0

- Background Service: Chạy độc lập, không cần giao diện. Giới hạn tác vụ chạy nền, chỉ chạy vài phút 
- Foreground Service: chạy khi có Activity đang chạy, hay kèm Notification

## Trình bày LifeCycle của Fragment

![fragment lifecycle](images/fragment_lifecycle.png)

## Giải thích Back stack fragment manager

```java
// Thêm Fragment vào View(fragment_container)
// Hiện cả 2, không Pause Fragment cũ
MyFragment fragment = new MyFragment();
transaction.add(R.id.fragment_container, fragment, "fragment_tag");

// Xóa Fragment (destroy fragment)
transaction.remove(fragment);
// Thay thế Fagment hiện tại = fragment = remove + add (Pause fragment cũ)
transaction.replace(R.id.fragment_container, fragment, "fragment_tag");

// giống Remove, không đính kèm, còn lưu trạng thái (TAG)
transaction.detach(fragment);
// đính kèm Fragment bị Detach trở lại, (findFragmentByTag() != null)
transaction.attach(fragment);
```

## Giải thích dp, dpi, pt, sp trong Android

- dpi: (Dot per inch) là số lượng điểm ảnh hiển thị trên mỗi inch màn hình
- Pt:  1/72 inch kích thước màn hình.
- dp: density independent pixel. Phụ thuộc mật độ điểm ảnh.
- Sp: scale independent pixel. Co theo mật độ điểm ảnh.

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

onPause -> onStop

## Khi 1 Activity đang chạy, ta chọn recent apps, quét qua để kill app đó thì activity đó đi vào những trạng thái nào

onPause -> onStop -> onDestroy

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

## lúc nào onDestroy() được gọi mà không có onPause() và onStop()?

Khi finish() được gọi ở trong phương thức onCreate()

## tại sao chỉ nên gọi setContentView() trong onCreate()

onCreate chỉ gọi một lần
onResume onStart: gọi nhiều lần, tốn tài nguyên

## Giải thích về 4 launchmode: standard, singleTop, singleTask, singleInstance

- Standard: nhiều Activity tồn tại (khởi tạo nhiều lần)
- SingleTop: nhiều Activity tồn tại (khởi tạo nhiều lần). Nếu Activity đã khởi tạo ở trên cùng, chỉ gọi hàm onNewIntent. Nếu không trên cùng thì khởi tạo lại.
- SingleTask: Chỉ 1 Activity tồn tại. Nếu Activity đã khởi tạo, destroy các Activity sau nó.
- singleInstance: Chỉ 1 Activity tồn tại, Activity chạy Task khác. Nếu Activity đã khởi tạo, sẽ nhảy lên trên.

## Foreground và Background Service là gì, Bound service là gì

- Foreground Service: thực hiện hoạt động mà người dùng chú ý. (vd: nghe nhạc)
- Background Service: thực hiện hoạt động chạy ngầm. không cần báo người dùng.
- Bound Service: Component ràng buộc Service để lấy kết quả liên tục (như Client-Server)

## Phân biệt Serializable và Parcelable, cái nào tốt hơn

- Serializable: Chuyển Object(data) thành 1 dạng lưu trữ (text để lưu trữ và phục hồi)
- Parcelable: Gởi Object(data) thông qua các Bunble trong Android

## ANR là gì, khi nào nó xảy ra: Application not responding

- ANR: Ứng dụng đóng băng, không phải hồi cử chỉ người dùng.

## So sánh LinearLayout và ConstrainLayout

- LinearLayout: các View con sắp theo 1 chiều (dọc, ngang).
- ConstrainLayout: các View con sắp xếp có liên kết với nhau.

## Sự khác nhau giữ View.GONE và View.INVISIBLE

- Gone: View biến mất, không giữ kích thước hiện tại.
- Invisible: View biến mất, vẫn giữ kích thước hiện tại.

## Liệt kê một số thư viện http đã dùng

- Retrofit, HttpRequest

## Rest APIs là gì, tại sao lại dùng nó

- REST (Representation State Stranfer): một tiêu chuẩn dùng trong việc thết kế các thiết kế API cho các ứng dụng web.
- API (Application Programming Interface): Giao diện lập trình ứng dụng.
- RESTful API: ứng dụng sử dụng REST

## Tại sao Android dùng db SQLite

- Không phải cài đặt
- Không cần mô hình Client - Server
- Chỉ lưu trữ 1 file
- Chiếm ít bộ nhớ
- Hỗ trợ truy vấn SQL

## Android Gradle là gì

- Gradle là một hệ thống tự động build mã nguồn mở

## Dependency injection là gì

- Là phương pháp giảm sự phụ thuộc 1 module trong 1 module
- Thay vì khởi tạo 1 object trong 1 object, ta khởi tạo nó bên ngoài. Rồi tim vào bên trong qua: constructer, setter, interface...

## Làm thế nào để upload 1 file ảnh trong máy Android lên server

- Tạo 1 Restfull Api upload ảnh
- Upload ảnh bằng thư viện Retrofit

## Application

- Application là lớp cơ sở trg Android App.
- Chứa tất cả Component khác (activity, service...)
- Khởi tạo đầu tiên, khi ứng dụng được chạy.

## Context

- Context là một đối tượng để phục vụ các xử lý liên quan tới hệ thống 
- hay cung cấp thông tin của môi trường hệ thống
- Application Context: là context gắn với Vòng đời của ứng dụng

## Tại sao bytecode không thể chạy được trong Android?

Android sử dụng DVM - Dalvik Virtual Machine và và ART - Android Runtime (>5.0)
Không dùng: JVM (Java Virtual Machine)

## Sealed class, data class

- Sealed class: là lớp trừu tượng (Abstract class - SubClass phải cùng file), mở rộng của Enum class (có thể sử dụng when), 


<https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb>

---
