# Câu hỏi Android Cơ bản

- [Câu hỏi Android Cơ bản](#câu-hỏi-android-cơ-bản)
  - [4 Component chính trong Android là gì](#4-component-chính-trong-android-là-gì)
  - [Activity](#activity)
    - [So sánh onCreate() và onStart()?](#so-sánh-oncreate-và-onstart)
    - [Cách gởi Data từ Activity B \> A](#cách-gởi-data-từ-activity-b--a)
    - [Activity vs Fragment Activity vs AppCompatActivity](#activity-vs-fragment-activity-vs-appcompatactivity)
    - [Khi 1 activity đang chạy, ta nhấn nút Home thì activity đó đi vào những trạng thái nào](#khi-1-activity-đang-chạy-ta-nhấn-nút-home-thì-activity-đó-đi-vào-những-trạng-thái-nào)
    - [Khi 1 Activity đang chạy, ta chọn recent apps, quét qua để kill app đó thì activity đó đi vào những trạng thái nào](#khi-1-activity-đang-chạy-ta-chọn-recent-apps-quét-qua-để-kill-app-đó-thì-activity-đó-đi-vào-những-trạng-thái-nào)
    - [Khi 1 Activity đang chạy mà bị crash, activity đó đi vào trạng thái nào](#khi-1-activity-đang-chạy-mà-bị-crash-activity-đó-đi-vào-trạng-thái-nào)
    - [Khi đang ở trong Activity, xoay màn hình thì Activity đi vào những trạng thái nào](#khi-đang-ở-trong-activity-xoay-màn-hình-thì-activity-đi-vào-những-trạng-thái-nào)
    - [Khi đang ở trong Activity, mở 1 AlertDialog thì activity đi vào những trạng thái nào](#khi-đang-ở-trong-activity-mở-1-alertdialog-thì-activity-đi-vào-những-trạng-thái-nào)
    - [Tạo mới 1 Thread trong activity, khi mở activity mới thì Thread đó có còn chạy ko](#tạo-mới-1-thread-trong-activity-khi-mở-activity-mới-thì-thread-đó-có-còn-chạy-ko)
    - [MediaPlayer đang chạy trong, tạo mới activity khác, player đó còn chạy ko](#mediaplayer-đang-chạy-trong-tạo-mới-activity-khác-player-đó-còn-chạy-ko)
    - [lúc nào onDestroy() được gọi mà không có onPause() và onStop()?](#lúc-nào-ondestroy-được-gọi-mà-không-có-onpause-và-onstop)
    - [tại sao chỉ nên gọi setContentView() trong onCreate()](#tại-sao-chỉ-nên-gọi-setcontentview-trong-oncreate)
  - [Fragment](#fragment)
    - [Trình bày LifeCycle của Fragment](#trình-bày-lifecycle-của-fragment)
    - [phân biệt activity và fragment](#phân-biệt-activity-và-fragment)
    - [Khi nào thì dùng Fragment, cho ví dụ trong thực tế. (Khi nào dùng Fragment thay cho Activity?)](#khi-nào-thì-dùng-fragment-cho-ví-dụ-trong-thực-tế-khi-nào-dùng-fragment-thay-cho-activity)
    - [Nếu thêm nhiều Fragment vào cùng 1 FrameLayout bằng FragmentManager thì thực tế hiển thị fragment nào, các fragment kia rơi vào trạng thái gì](#nếu-thêm-nhiều-fragment-vào-cùng-1-framelayout-bằng-fragmentmanager-thì-thực-tế-hiển-thị-fragment-nào-các-fragment-kia-rơi-vào-trạng-thái-gì)
    - [Giải thích Back stack fragment manager](#giải-thích-back-stack-fragment-manager)
  - [UI](#ui)
    - [Constrain layout](#constrain-layout)
    - [Dialog vs Fragment dialog](#dialog-vs-fragment-dialog)
    - [Khác nhau include và merge](#khác-nhau-include-và-merge)
    - [làm sao biết view nào tiêu tốn nhiều tài nguyên ( dùng cái gì)](#làm-sao-biết-view-nào-tiêu-tốn-nhiều-tài-nguyên--dùng-cái-gì)
    - [So sánh LinearLayout và ConstrainLayout](#so-sánh-linearlayout-và-constrainlayout)
    - [Sự khác nhau giữ View.GONE và View.INVISIBLE](#sự-khác-nhau-giữ-viewgone-và-viewinvisible)
    - [Giải thích dp, dpi, pt, sp trong Android](#giải-thích-dp-dpi-pt-sp-trong-android)
    - [Cho biết công thức quy đổi giữa px và dp](#cho-biết-công-thức-quy-đổi-giữa-px-và-dp)
    - [RecyclerView](#recyclerview)
      - [Viewholder là gì](#viewholder-là-gì)
      - [làm recycler view giống view pager](#làm-recycler-view-giống-view-pager)
      - [Thay đổi 1 Phần ViewHolder](#thay-đổi-1-phần-viewholder)
      - [RecylerView Kiểm tra 2 item không trùng](#recylerview-kiểm-tra-2-item-không-trùng)
  - [Service](#service)
    - [Phân biệt Service và IntentService](#phân-biệt-service-và-intentservice)
    - [Phân biệt Service, Intent Service, AsyncTask và Thread.](#phân-biệt-service-intent-service-asynctask-và-thread)
    - [Service Android 8.0](#service-android-80)
    - [Foreground và Background Service là gì, Bound service là gì](#foreground-và-background-service-là-gì-bound-service-là-gì)
    - [có mấy cách để start service](#có-mấy-cách-để-start-service)
    - [ThreadPool (thuộc java)](#threadpool-thuộc-java)
  - [Intent](#intent)
    - [Phân biệt Implicit và Explicit Intent](#phân-biệt-implicit-và-explicit-intent)
  - [Giải thích về 4 launchmode: standard, singleTop, singleTask, singleInstance](#giải-thích-về-4-launchmode-standard-singletop-singletask-singleinstance)
  - [Phân biệt Serializable và Parcelable, cái nào tốt hơn](#phân-biệt-serializable-và-parcelable-cái-nào-tốt-hơn)
  - [ANR là gì, khi nào nó xảy ra: Application not responding](#anr-là-gì-khi-nào-nó-xảy-ra-application-not-responding)
  - [Liệt kê một số thư viện http đã dùng](#liệt-kê-một-số-thư-viện-http-đã-dùng)
  - [Rest APIs là gì, tại sao lại dùng nó](#rest-apis-là-gì-tại-sao-lại-dùng-nó)
  - [Tại sao Android dùng db SQLite](#tại-sao-android-dùng-db-sqlite)
  - [Android Gradle là gì](#android-gradle-là-gì)
  - [Dependency injection là gì](#dependency-injection-là-gì)
  - [Làm thế nào để upload 1 file ảnh trong máy Android lên server](#làm-thế-nào-để-upload-1-file-ảnh-trong-máy-android-lên-server)
  - [Application](#application)
  - [Context](#context)
  - [Tại sao bytecode không thể chạy được trong Android?](#tại-sao-bytecode-không-thể-chạy-được-trong-android)
  - [Memory leak xảy ra khi nào?](#memory-leak-xảy-ra-khi-nào)
    - [Phòng tránh memory leak](#phòng-tránh-memory-leak)
  - [Unit test](#unit-test)
    - [How to write code for easier unit testing](#how-to-write-code-for-easier-unit-testing)
  - [1 màn hình có 4 button để upload hình, và 1 nút Save](#1-màn-hình-có-4-button-để-upload-hình-và-1-nút-save)
  - [dependency injection - Tiêm phụ thuộc](#dependency-injection---tiêm-phụ-thuộc)
  - [Các bước vẽ trên GG Map](#các-bước-vẽ-trên-gg-map)
  - [Các bước Push Notification Firebase](#các-bước-push-notification-firebase)
  - [Các bước thanh toán google billing](#các-bước-thanh-toán-google-billing)
  - [Các câu hỏi khác](#các-câu-hỏi-khác)
    - [...Là gì? dùng trong trường hợp nào](#là-gì-dùng-trong-trường-hợp-nào)
  - [Reference](#reference)

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

### So sánh onCreate() và onStart()?

OnCreate: gọi khi Activity khởi tạo lần đầu, .
OnStart: gọi khi Activity hiển thị với người dùng..
.
Khi User quay lại Activity, gọi OnRestart > OnResume. .
Sau khi ứng dụng bị thu hồi bộ nhớ, gọi OnCreate lại.

### Cách gởi Data từ Activity B > A

1. Intent
put Extra to Inent, then start Activity with this Intent. 
   Intent intent = new Intent(ActA.this, ActB.class);
   intent.putExtra("key", sessionId);
   startActivity(intent);
ActivityB get 
   getIntent().getStringExtra("key").

2. Bundle
   Bundle b = new Bundle();
   b.putString("key", "value");
   indent.putExtra(b);

3. Use Static Medthod:
   String data = ActA.getData();

4. Shared Preferences
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor editor = sharedPref.edit();
editor.putInt(getString(R.string.saved_high_score_key), newHighScore);
editor.commit();

5. Database: SQLite, TextFile, ObjectFile

6. EventBus Third library, like: greenrobot EventBus

### Activity vs Fragment Activity vs AppCompatActivity

- Activity là lớp cơ sở
- Fragment Activity (extend Activity) có kèm quản lý fragment
- AppCompatActivity (extend FragmentActivity) có 1 số hàm tương thích Api Cũ

### Khi 1 activity đang chạy, ta nhấn nút Home thì activity đó đi vào những trạng thái nào

onPause -> onStop

### Khi 1 Activity đang chạy, ta chọn recent apps, quét qua để kill app đó thì activity đó đi vào những trạng thái nào

onPause -> onStop -> onDestroy

### Khi 1 Activity đang chạy mà bị crash, activity đó đi vào trạng thái nào

Crash ở Activity thì onDestroy.
Crash ở Application thì onStop.

### Khi đang ở trong Activity, xoay màn hình thì Activity đi vào những trạng thái nào

onStart -> onResume

### Khi đang ở trong Activity, mở 1 AlertDialog thì activity đi vào những trạng thái nào

Không có

### Tạo mới 1 Thread trong activity, khi mở activity mới thì Thread đó có còn chạy ko

Vẫn chạy kể cả khi finish Activity

### MediaPlayer đang chạy trong, tạo mới activity khác, player đó còn chạy ko

Vẫn chạy

### lúc nào onDestroy() được gọi mà không có onPause() và onStop()?

Khi finish() được gọi ở trong onCreate()

### tại sao chỉ nên gọi setContentView() trong onCreate()

onCreate: chỉ gọi một lần
onResume, onStart: gọi nhiều lần, tốn tài nguyên.

## Fragment

Fragment là một phần giao diện người dùng.
Hiển thị 1 phần trong Activity.
Có thể tái sử dụng nhiều lần hay 1 màn hình riêng biệt.
Có layout hành vi và vòng đời riêng.
VD: nội dung của tab, a Dialog, a list, a ui of slider...

### Trình bày LifeCycle của Fragment

onAttach. onCreate. onCreateView. onViewCreated.
onStart.
onResume.

onPause.
onStop.
onDestroyView. onDestroy. onDetach.

![fragment lifecycle](images/fragment_lifecycle.png)

### phân biệt activity và fragment

🔹 Dùng Activity khi:
✅ Màn hình hoạt động độc lập.
✅ Cần xử lý riêng biệt, không phụ thuộc vào giao diện khác.
✅ Ít có sự thay đổi giữa các giao diện.

🔹 Dùng Fragment khi:
✅ Muốn tái sử dụng UI trong nhiều màn hình.
✅ Cần hiển thị nhiều thành phần UI trong một Activity.
✅ Giao diện có thể thay đổi động (như máy tính bảng, màn hình lớn).

### Nếu thêm nhiều Fragment vào cùng 1 FrameLayout bằng FragmentManager thì thực tế hiển thị fragment nào, các fragment kia rơi vào trạng thái gì

- Hiển thị tất cả chồng lên nhau.
- Không rơi vào trạng thái nào. Trạng thái cuối là onResume

### Giải thích Back stack fragment manager

Quản lý việc điều hướng giữa các Fragment trong ứng dụng Android.
Khi một Fragment được thêm vào Back Stack, nó sẽ được lưu lại để có thể quay lại (Back) sau này.

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

## UI

### Constrain layout

Là Container View,
View con có mối quan hệ, ràng buộc với nhau và Parent View.
Tương tự như RelativeLayout, nhưng linh hoạt hơn.
Dễ sử dụng với Layout Editor của Android Studio.

### Fragment dialog

Hiện Fragment theo dạng Dialog, dialog phức tạp, tái sử dụng, khuyến khích dùng

### Khác nhau include và merge

Include hiển thị layout có Merge làm container

```xml
<LinearLayout><include></Linearlayout>

<merge>123...</merge> => <LinearLayout>123...</Linearlayout>
```

### làm sao biết view nào tiêu tốn nhiều tài nguyên ( dùng cái gì)

- Profiler: check thông tin tài nguyên hệ thống (cpu, ram) android khi mở View đó

### So sánh LinearLayout và ConstrainLayout

- LinearLayout: các View con sắp theo 1 chiều (dọc, ngang).
- ConstrainLayout: các View con sắp xếp có liên kết với nhau và view cha.

### Sự khác nhau giữ View.GONE và View.INVISIBLE

- Gone: View biến mất, không giữ kích thước.
- Invisible: View biến mất, vẫn giữ kích thước.

### Giải thích pt, dp, sp trong Android

- Pt:  1/72 inch kích thước màn hình.
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

### RecyclerView là gì

- Là một ViewGroup nâng cao.
- Để hiển thị danh sách hoặc lưới dữ liệu một cách hiệu quả trong Android.
- Nó là phiên bản cải tiến của ListView và GridView.
- Hiệu suất cao bằng cách tái sử dụng View và tối ưu bộ nhớ.

#### Viewholder là gì

Là một lớp trong RecyclerView.
Mô tả Item View và Dữ liệu trong RecyclerView..
Tối ưu hóa hiệu suất bằng cách tái sử dụng View, tránh việc gọi findViewById() nhiều lần, giúp cuộn danh sách mượt mà hơn.

#### làm recycler view giống view pager

SnapHelper Decoration

#### Thay đổi 1 Phần ViewHolder

onBindViewHolder payloads

#### RecylerView Kiểm tra 2 item không trùng

DiffUtil

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

- Service: Là 1 Android Component. dùng để thực hiện các tác vụ ngầm ở background, ví dụ như chơi nhạc. Chạy trong Main Theard. Nó không có giao diện người dùng (user interface).
- IntentService: là 1 Android Service. Tự dừng lại sau khi trả về kết quả, hay hàm **“onHandleIntent”** xử lý xong.
- Thread: là một luồng thực thi tuần tự trong một chương trình. Thread có thể được coi là một mini-process chạy ở trong main process.
- AsyncTask: Thực hiện các công việc bất đồng bộ. Chạy trong background thread và publish kết quả lên trên UI thread. Mà Không yêu cầu bạn phải xử lý cách các thread hay handler hoạt động.

- Service: Là 1 Android Component, có thể Chạy Ngầm, ngay cả khi người dùng không tương tác. Chạy trong Main Thread.
- AsyncTask: Chạy trong Background Thread, chỉ chạy trong khi người dùng còn tương tác ứng dụng.

### Service Android 8.0

- Background Service: Chạy độc lập, không cần giao diện. Giới hạn tác vụ chạy nền, chỉ chạy vài phút 
- Foreground Service: chạy khi có Activity đang chạy, hay kèm Notification

### Foreground và Background Service là gì, Bound service là gì

- Foreground Service: thực hiện hoạt động mà người dùng chú ý. (vd: nghe nhạc)
- Background Service: thực hiện hoạt động chạy ngầm. không cần báo người dùng. Cần có notification
- Bound Service: Component ràng buộc Service để lấy kết quả liên tục (như Client-Server)

### có mấy cách để start service

- bằng class name
- bằng text, dùng tên package + service

### ThreadPool (thuộc java)

Quản lý, điều tiết nhiều Thread

## Intent

### Phân biệt Implicit và Explicit Intent

- Explicit Intent: tường minh, gọi trực tiếp tên ứng dụng
- Implicit Intent: ẩn ý, gọi chung chung, ứng dụng nào chạy thì chạy

## Giải thích về 4 launchmode: standard, singleTop, singleTask, singleInstance

- Standard: nhiều Activity tồn tại (khởi tạo nhiều lần).
- SingleTop: nhiều Activity tồn tại (khởi tạo nhiều lần). Nếu Activity đã khởi tạo ở trên cùng, chỉ gọi hàm onNewIntent. Nếu không trên cùng thì khởi tạo lại..
- SingleTask: Chỉ 1 Activity tồn tại. Nếu Activity đã khởi tạo, destroy các Activity sau nó..
- singleInstance: Chỉ 1 Activity tồn tại, Activity chạy Task khác. Nếu Activity đã khởi tạo, sẽ nhảy lên trên.

## Phân biệt Serializable và Parcelable, cái nào tốt hơn

- Serializable: một interface trong Java. Biến đổi một object thành byte stream để có thể lưu trữ hoặc truyền đi.
- Parcelable: một interface của Android. Giúp biến đổi object thành Parcel để truyền giữa các thành phần của hệ thống. Nhanh hơn.

## ANR là gì, khi nào nó xảy ra: Application not responding

- ANR: Ứng dụng đóng băng, không phải hồi cử chỉ người dùng.

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

## Làm thế nào để upload 1 file ảnh trong máy Android lên server

- Tạo 1 Restfull Api upload ảnh
- Upload ảnh bằng thư viện Retrofit

## Application là gì

- Application là lớp cơ sở trg Android App.
- Chứa tất cả Component khác (activity, service...)
- Khởi tạo đầu tiên, khi ứng dụng được chạy.

## Context là gì

- Context: là 1 thành phần trong android. Cung cấp thông tin môi trường ứng dụng, truy cập tài nguyên, khởi chạy Activity, Service

- ApplicationContext: ngữ cảnh của Toàn ứng dụng
- BaseContext: lấy ngữ cảnh có thể sử dụng
- getContext trong View: lấy ngữ cảnh tạo View

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

- Khi click 4 button thì chọn hình và upload, 4 hình upload chạy song song, khi nhấn nút Save thì làm sao để đợi 4 hình upload xong thì mới gọi API của nút Save

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

- Tạo Google Player Service Project, lấy API_KEY
- Đăng kí key trong Manifest
- Cài Map Dependencies trong Gradle
- Khởi tạo Map trên View, và kolin file
- Khi Map Ready thì gọi hàm Vẽ

## Các bước Push Notification Firebase

- Tạo project, lấy key trên Firebase Console
- Đăng kí key trong Manifest
- Cài Dependencies trong Gradle
- Tạo file FirebaseMessagingService để hiện thông báo
- Xin quyền hiện Notification trong app trước khi hiện thông báo

## Các bước thanh toán google billing

- Tạo project, lấy key trên Google Cloud Console
- Tạo danh sách sản phẩm
- Đăng kí key trong Manifest
- Cài Dependencies trong Gradle
- Khi User nhấn thanh toán: 
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

- FragA->add FragB a qua trạng thái nào-> replace B with C B qua trạng thái nào->popC thì C qua trạng thái nào và A như thế nào
- nếu a bằng null gọi m a khác null gọi n ko dùng if
- viết When có trường hợp loại trừ

---

## Reference

<https://viblo.asia/p/mot-so-cau-hoi-phong-van-android-ban-nen-luu-y-phan-1-3Q75wkLQ5Wb>

---
