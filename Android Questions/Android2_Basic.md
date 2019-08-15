# Câu hỏi Android Cơ bản

- [Câu hỏi Android Cơ bản](#c%c3%a2u-h%e1%bb%8fi-android-c%c6%a1-b%e1%ba%a3n)
  - [Viewholder là gì](#viewholder-l%c3%a0-g%c3%ac)
  - [phân biệt activity và fragment](#ph%c3%a2n-bi%e1%bb%87t-activity-v%c3%a0-fragment)
    - [- Khi nào thì dùng Fragment, cho ví dụ trong thực tế](#khi-n%c3%a0o-th%c3%ac-d%c3%b9ng-fragment-cho-v%c3%ad-d%e1%bb%a5-trong-th%e1%bb%b1c-t%e1%ba%bf)
  - [Khi nào method onResume() được gọi?](#khi-n%c3%a0o-method-onresume-%c4%91%c6%b0%e1%bb%a3c-g%e1%bb%8di)
  - [4 Component chính trong Android là gì](#4-component-ch%c3%adnh-trong-android-l%c3%a0-g%c3%ac)
  - [Phân biệt Implicit và Explicit Intent](#ph%c3%a2n-bi%e1%bb%87t-implicit-v%c3%a0-explicit-intent)
  - [Phân biệt Service và IntentService](#ph%c3%a2n-bi%e1%bb%87t-service-v%c3%a0-intentservice)
  - [Phân biệt Service, Intent Service, AsyncTask và Thread.](#ph%c3%a2n-bi%e1%bb%87t-service-intent-service-asynctask-v%c3%a0-thread)
  - [Trình bày LifeCycle của Activity](#tr%c3%acnh-b%c3%a0y-lifecycle-c%e1%bb%a7a-activity)
  - [Trình bày LifeCycle của Fragment](#tr%c3%acnh-b%c3%a0y-lifecycle-c%e1%bb%a7a-fragment)
  - [Giải thích Back stack fragment manager](#gi%e1%ba%a3i-th%c3%adch-back-stack-fragment-manager)
  - [Giải thích dp, dpi, pt, sp trong Android](#gi%e1%ba%a3i-th%c3%adch-dp-dpi-pt-sp-trong-android)
  - [Cho biết công thức quy đổi giữa px và dp](#cho-bi%e1%ba%bft-c%c3%b4ng-th%e1%bb%a9c-quy-%c4%91%e1%bb%95i-gi%e1%bb%afa-px-v%c3%a0-dp)
  - [Khi 1 activity đang chạy, ta nhấn nút Home thì activity đó đi vào những trạng thái nào](#khi-1-activity-%c4%91ang-ch%e1%ba%a1y-ta-nh%e1%ba%a5n-n%c3%bat-home-th%c3%ac-activity-%c4%91%c3%b3-%c4%91i-v%c3%a0o-nh%e1%bb%afng-tr%e1%ba%a1ng-th%c3%a1i-n%c3%a0o)
  - [Khi 1 Activity đang chạy, ta chọn recent apps, quét qua để kill app đó thì activity đó đi vào những trạng thái nào](#khi-1-activity-%c4%91ang-ch%e1%ba%a1y-ta-ch%e1%bb%8dn-recent-apps-qu%c3%a9t-qua-%c4%91%e1%bb%83-kill-app-%c4%91%c3%b3-th%c3%ac-activity-%c4%91%c3%b3-%c4%91i-v%c3%a0o-nh%e1%bb%afng-tr%e1%ba%a1ng-th%c3%a1i-n%c3%a0o)
  - [Khi 1 Activity đang chạy mà bị crash, activity đó đi vào trạng thái nào](#khi-1-activity-%c4%91ang-ch%e1%ba%a1y-m%c3%a0-b%e1%bb%8b-crash-activity-%c4%91%c3%b3-%c4%91i-v%c3%a0o-tr%e1%ba%a1ng-th%c3%a1i-n%c3%a0o)
  - [Nếu thêm nhiều Fragment vào cùng 1 FrameLayout bằng FragmentManager thì thực tế hiển thị fragment nào, các fragment kia rơi vào trạng thái gì](#n%e1%ba%bfu-th%c3%aam-nhi%e1%bb%81u-fragment-v%c3%a0o-c%c3%b9ng-1-framelayout-b%e1%ba%b1ng-fragmentmanager-th%c3%ac-th%e1%bb%b1c-t%e1%ba%bf-hi%e1%bb%83n-th%e1%bb%8b-fragment-n%c3%a0o-c%c3%a1c-fragment-kia-r%c6%a1i-v%c3%a0o-tr%e1%ba%a1ng-th%c3%a1i-g%c3%ac)
  - [Khi đang ở trong Activity, xoay màn hình thì Activity đi vào những trạng thái nào](#khi-%c4%91ang-%e1%bb%9f-trong-activity-xoay-m%c3%a0n-h%c3%acnh-th%c3%ac-activity-%c4%91i-v%c3%a0o-nh%e1%bb%afng-tr%e1%ba%a1ng-th%c3%a1i-n%c3%a0o)
  - [Khi đang ở trong Activity, mở 1 AlertDialog thì activity đi vào những trạng thái nào](#khi-%c4%91ang-%e1%bb%9f-trong-activity-m%e1%bb%9f-1-alertdialog-th%c3%ac-activity-%c4%91i-v%c3%a0o-nh%e1%bb%afng-tr%e1%ba%a1ng-th%c3%a1i-n%c3%a0o)
  - [Tạo mới 1 Thread trong activity, khi mở activity mới thì Thread đó có còn chạy ko](#t%e1%ba%a1o-m%e1%bb%9bi-1-thread-trong-activity-khi-m%e1%bb%9f-activity-m%e1%bb%9bi-th%c3%ac-thread-%c4%91%c3%b3-c%c3%b3-c%c3%b2n-ch%e1%ba%a1y-ko)
  - [MediaPlayer đang chạy trong, tạo mới activity khác, player đó còn chạy ko](#mediaplayer-%c4%91ang-ch%e1%ba%a1y-trong-t%e1%ba%a1o-m%e1%bb%9bi-activity-kh%c3%a1c-player-%c4%91%c3%b3-c%c3%b2n-ch%e1%ba%a1y-ko)
  - [lúc nào onDestroy() được gọi mà không có onPause() và onStop()?](#l%c3%bac-n%c3%a0o-ondestroy-%c4%91%c6%b0%e1%bb%a3c-g%e1%bb%8di-m%c3%a0-kh%c3%b4ng-c%c3%b3-onpause-v%c3%a0-onstop)
  - [tại sao chỉ nên gọi setContentView() trong onCreate()](#t%e1%ba%a1i-sao-ch%e1%bb%89-n%c3%aan-g%e1%bb%8di-setcontentview-trong-oncreate)
  - [Giải thích về 4 launchmode: standard, singleTop, singleTask, singleInstance](#gi%e1%ba%a3i-th%c3%adch-v%e1%bb%81-4-launchmode-standard-singletop-singletask-singleinstance)
  - [Foreground và Background Service là gì, Bound service là gì](#foreground-v%c3%a0-background-service-l%c3%a0-g%c3%ac-bound-service-l%c3%a0-g%c3%ac)
  - [Phân biệt Serializable và Parcelable, cái nào tốt hơn](#ph%c3%a2n-bi%e1%bb%87t-serializable-v%c3%a0-parcelable-c%c3%a1i-n%c3%a0o-t%e1%bb%91t-h%c6%a1n)
  - [ANR là gì, khi nào nó xảy ra: Application not responding](#anr-l%c3%a0-g%c3%ac-khi-n%c3%a0o-n%c3%b3-x%e1%ba%a3y-ra-application-not-responding)
  - [So sánh LinearLayout và ConstrainLayout](#so-s%c3%a1nh-linearlayout-v%c3%a0-constrainlayout)
  - [Sự khác nhau giữ View.GONE và View.INVISIBLE](#s%e1%bb%b1-kh%c3%a1c-nhau-gi%e1%bb%af-viewgone-v%c3%a0-viewinvisible)
  - [Liệt kê một số thư viện http đã dùng](#li%e1%bb%87t-k%c3%aa-m%e1%bb%99t-s%e1%bb%91-th%c6%b0-vi%e1%bb%87n-http-%c4%91%c3%a3-d%c3%b9ng)
  - [Rest APIs là gì, tại sao lại dùng nó](#rest-apis-l%c3%a0-g%c3%ac-t%e1%ba%a1i-sao-l%e1%ba%a1i-d%c3%b9ng-n%c3%b3)
  - [Tại sao Android dùng db SQLite](#t%e1%ba%a1i-sao-android-d%c3%b9ng-db-sqlite)
  - [Android Gradle là gì](#android-gradle-l%c3%a0-g%c3%ac)
  - [Dependency injection là gì](#dependency-injection-l%c3%a0-g%c3%ac)
  - [Làm thế nào để upload 1 file ảnh trong máy Android lên server](#l%c3%a0m-th%e1%ba%bf-n%c3%a0o-%c4%91%e1%bb%83-upload-1-file-%e1%ba%a3nh-trong-m%c3%a1y-android-l%c3%aan-server)
  - [Application](#application)
  - [Context](#context)
  - [Tại sao bytecode không thể chạy được trong Android?](#t%e1%ba%a1i-sao-bytecode-kh%c3%b4ng-th%e1%bb%83-ch%e1%ba%a1y-%c4%91%c6%b0%e1%bb%a3c-trong-android)

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

là UI Độc lập, hiển thị 1 phần trong Activity, có thể sử dụng nhiều lần.
Ví dụ: nội dung của tab, a Dialog, a list, a ui of slider...

E:
We need a independent ui, to display on activity.
It a part of Activity.
Modular section of Activity.

Content of a tab, a Dialog, a list, a ui of slider...

## Khi nào method onResume() được gọi?

onResume() là một trong những activity lifecycle method. 
Gọi khi sau khi activity hiển thị lần nữa, sau khi ẩn đi bởi onPause.

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

- Service là một thành phần được sử dụng để thực hiện các tác vụ ở background ví dụ như chơi nhạc. Nó không có giao diện người dùng (user interface). Service có thể chạy ở trong background vô thời hạn ngay cả khi ứng dụng bị hủy.
- AsyncTask cho phép bạn thực hiện các công việc bất đồng bộ ở background thread và publish kết quả lên trên UI thread mà không yêu cầu bạn phải xử lý cách các thread hay handler hoạt động.
- IntentService là một loại Service để xử lý lần lượt các yêu cầu bất đồng bộ (thông qua Intent) ở background thread. Client sẽ gửi yêu cầu thông qua việc gọi tới startService(Intent) và nó cũng không yêu cầu bạn phải "động tay động chân" tới việc xử lý thread / handler.
- Một Thread là một luồng thực thi tuần tự trong một chương trình. Thread có thể được coi là một mini-process chạy ở trong main process.

- Shorter:
<https://developer.android.com/guide/components/services>
- Service: Là 1 Android Component, có thể Chạy Ngầm, ngay cả khi người dùng không tương tác. Chạy trong luồng chính.
- AsyncTask: Thực hiện công việc ngoài luồng chính, chỉ trong khi người dùng còn tương tác ứng dụng.

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

<https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb>

---
