# Các câu hỏi phỏng vấn công ty cũ

- [Các câu hỏi phỏng vấn công ty cũ](#các-câu-hỏi-phỏng-vấn-công-ty-cũ)
  - [1. activity lifecycle](#1-activity-lifecycle)
  - [2. What’s the difference between onCreate() and onStart()?](#2-whats-the-difference-between-oncreate-and-onstart)
  - [3. When should you use a Fragment, rather than an Activity?](#3-when-should-you-use-a-fragment-rather-than-an-activity)
  - [4. Memory leak xảy ra khi nào?](#4-memory-leak-xảy-ra-khi-nào)
    - [Phòng tránh memory leak](#phòng-tránh-memory-leak)
  - [5. describe mvvm, mvvm vs mvc, why mvvm](#5-describe-mvvm-mvvm-vs-mvc-why-mvvm)
  - [7. unit test: how to write code for easier unit testing](#7-unit-test-how-to-write-code-for-easier-unit-testing)
  - [8. how many ways to send data back from Activity B \> A](#8-how-many-ways-to-send-data-back-from-activity-b--a)
  - [9. constrain layout](#9-constrain-layout)
  - [10. 1 màn hình có 4 button để upload hình, và 1 nút Save](#10-1-màn-hình-có-4-button-để-upload-hình-và-1-nút-save)
  - [S.O.L.I.D](#solid)
  - [6. dependency injection - Tiêm phụ thuộc](#6-dependency-injection---tiêm-phụ-thuộc)
  - [let, also, apply, with](#let-also-apply-with)
  - [val, var, const, const val, lazy, lateinit](#val-var-const-const-val-lazy-lateinit)
  - [Rx](#rx)
  - [Dialog vs Fragment dialog](#dialog-vs-fragment-dialog)
  - [Activity vs Fragment Activity vs AppCompatActivity](#activity-vs-fragment-activity-vs-appcompatactivity)
  - [Context?](#context)
  - [Khác nhau include và merge](#khác-nhau-include-và-merge)
  - [Là gì? dùng trong trường hợp nào](#là-gì-dùng-trong-trường-hợp-nào)

## 1. activity lifecycle

![activity lifecycle](images/activity_lifecycle.png)

OnCreate - onStart (onRestart) - onResume
OnPause - OnStop - onDestroy

- OnCreate: Call on Activity first create.
- OnStart: Activity become visible to user. Screen Rotate.
- OnResume:  After hidden, Visible Again to user.
- OnPause: Activity hidden, below other Activity, but we can see it.
- OnStop: Activity invisible to user. we can not see it.
- OnDestroy: Activity had be kill by User, or System.

## 2. What’s the difference between onCreate() and onStart()?

OnCreate: call on Activity first create, 
OnStart: Activity become visible to user.

When user comeback Activity, call OnRestart then OnResume. 
If app had been gabage memory, call OnCreate  again.

## 3. When should you use a Fragment, rather than an Activity?

Fragment là một phần giao diện người dùng hoặc hành vi của một ứng dụng. Fragment có thể được đặt trong Activity, nó có thể cho phép thiết kế activity với nhiều mô-đun. Có thể nói Fragment là một loại sub-Activity. Fragment cũng có layout của riêng của nó, cũng có các hành vi và vòng đời riêng.

We need a independent ui, to display on activity. 
It a part of Activity.
Modular section of Activity.

Content of a tab, a Dialog, a list, a ui of slider...

## 4. Memory leak xảy ra khi nào?

Since the AsyncTask maintains a reference to the previous instance of the Activity, that Activity won’t be garbage collected, resulting in a memory leak.

### Phòng tránh memory leak

Không giữ reference của view bên trong AsyncTask
Không giữ reference của View ở đối tượng static
Tránh đưa các Views vào trong Collection, bạn có thể sử dụng WeakHashMap
Dùng Leak-Canary để hiển thị biến leak

## 5. describe mvvm, mvvm vs mvc, why mvvm

![mvc mvp mvvm](images/mvc_mvp_mvvm.jpg)

MVVM: design pattern.
View: interactive with user, show infomation, gét user input.
Model: handle with data, sqlite, file
3 Layer.
ViêwModel: connect View& ViewModel, handle demand from view.

View get Event from User
Multiple View mapping 1 ModelView
View contain relation properties to ViewModel
belong support technology, Need a libary to use

MVC:
Controller get Event from User
1 Controller relate, control to multi View
Controller control View + Model
Longger code

## 7. unit test: how to write code for easier unit testing

unit test: kiểm thử method test.

using Dependency injection.
create a method for every fuction.
divice module for every mission. like: model, view, controller, data, helper.

## 8. how many ways to send data back from Activity B > A

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

## 9. constrain layout

ConstraintLayout allows you to create large and complex layouts with a flat view hierarchy (no nested view groups). It's similar to RelativeLayout in that all views are laid out according to relationships between sibling views and the parent layout, but it's more flexible than RelativeLayout and easier to use with Android Studio's Layout Editor.

It is a Container View, 
All Child View have a relationship, constrain together and parent layout.
Similar to RelativeLayout, but more flexible.
Easy to use with Android Studio's Layout Editor.

## 10. 1 màn hình có 4 button để upload hình, và 1 nút Save

- Khi click 4 button thì chọn hình và upload, 4 hình upload chạy song song, khi nhấn nút Save thì làm sao để đợi 4 hình upload xong thì mới gọi API của nút Save

First Way:
We can use a flag variable to count Finish upload.
when every upload finish, we will check it.

Second Way:
we can use AsyncTask to Check. we run upload onDoinBackground, then check it onPostExcute

Third Way:
We use third library like RxAndroid. 
we put all Upload method into Observable Zip method. 
then Check finish on Subscribe method

## S.O.L.I.D

S — Single Responsibility Principle
O — Open Closed Principle
L — Liskov Substitution Principle
I — Interface Segregation Principle
D — Dependency Inversion Principle

S — Single Responsibility Principle (nhiệm vụ)
class/module chỉ thực hiện một chức năng. Model, network, calculate...

O — Open Closed Principle (thích nghi)
code để có thể thích nghi với các yêu cầu mới mà không thay đổi code cũ. Dùng interace để thiết kế.

L — Liskov Substitution (thay thế) Principle
class con phải thay thế được class cha.
Nếu lớp cha không giải quyết được lớp con, thì tạo lớp cha lớn hơn, để cả 2 cùng kế thừa.

I — Interface Segregation (phân biệt) Principle
nhiều interface thực hiện sẽ tốt hơn là ít interface chứa nhiều function. Ko phải implement ko cần thiết

D — Dependency Inversion Principle (phụ thuộc)
Hạn chế Phụ thuộc Module trong Module. Tránh khởi tạo Module trong Module

## 6. dependency injection - Tiêm phụ thuộc

dependency: phụ thuộc.
injected: tiêm, bơm.

It is a method to reduce dependency module in side a other module.
Dont create Module's Instance in side an other Module.
We need provide module by other way, like: constructer, setter, interface...

It will easier for unit test, upgrade, update, module.

annotations thirth library, like: dagger 2

## let, also, apply, with

- with: để gọi nhiều phương thức(method) cùng 1 đối tượng.
- let: để check null
  - là một hàm phạm vi (scoping function):
  - Sử dụng một biến trong một phạm vi cụ thể trong đoạn code.
- apply: để Trả về Object (giống return function)
  - extension function cho tất cả các loại Object.
- also: để trả về Object gọi nó (return this)
- run: kết hợp with & let

## val, var, const, const val, lazy, lateinit

- var: khai báo biến.
- val: Khai báo biến tĩnh. (Khởi tạo lúc chạy)
- const val: Khai báo biến tĩnh. (khởi tạo lúc biên dịch)
- lateinit: biến khởi tạo sau. (dùng cho var)
- lazy: biến khởi tạo sau. (dùng cho val). được cấp lần đầu sử dụng (lazy by {}, giống get nhưng chỉ lấy lần đầu sử dụng)

## Rx

- <http://reactivex.io/documentation/operators.html#creating>
- just: subscribe item
- from: subscribe từng item trong list
- defer: subscribe item cuối cùng (???)
- interval: subscribe item sau mỗi khoảng thời gian

- map: Trả về phần tử độc lập
- fatMap: Trả về các phần tử đồng thời

## Dialog vs Fragment dialog

- Hiện Fragment theo dạng Dialog, dialog phức tạp, tái sử dụng, khuyến khích dùng

## Activity vs Fragment Activity vs AppCompatActivity

- Activity là lớp cơ sở
- Fragment Activity (extend Activity) có kèm quản lý fragment
- AppCompatActivity (extend FragmentActivity) có 1 số hàm tương thích Api Cũ

## Context?

- Cung cấp thông tin, quyền truy cập thông tin, trạng thái ứng dụng
- ApplicationContext: ngữ cảnh của Toàn ứng dụng
- BaseContext: lấy ngữ cảnh có thể sử dụng
- getContext trong View: lấy ngữ cảnh tạo View

## Khác nhau include và merge

- merge: áp dụng lớp Container chứa Include
- <LinearLayout><include></Linearlayout>
- <merge>123...</merge> => <LinearLayout>123...</Linearlayout>

## Là gì? dùng trong trường hợp nào

Generic
Singletone
SOLID
Dagger

Các bước vẽ trên GG Map
Các bước Push Notification
Thuật toán tìm đường đi ngắn nhất, qua nhiều điểm
Thuật toán sắp xếp kho hàng

- FragA->add FragB a qua trạng thái nào-> replace B with C B qua trạng thái nào->popC thì C qua trạng thái nào và A như thế nào
- nếu a bằng null gọi m a khác null gọi n ko dùng if
- khi nào viewmodel bị huỷ
- làm sao biết view nào tiêu tốn nhiều tài nguyên ( dùng cái gì)
- từ api 16-29 có thay đổi gì cần chú ý
- có mấy cách để start service
- làm recycler view giống view pager
- viết When có trường hợp loại trừ
