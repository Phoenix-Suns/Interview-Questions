# Câu hỏi phỏng vấn Java

- [Câu hỏi phỏng vấn Java](#câu-hỏi-phỏng-vấn-java)
  - [Liệt kê, giải thích 4 tính chất OOP](#liệt-kê-giải-thích-4-tính-chất-oop)
  - [MVVM, MVP, MVC, MVI là gì, khi nào dùng cái nào](#mvvm-mvp-mvc-mvi-là-gì-khi-nào-dùng-cái-nào)
    - [MVC (Model View Control)](#mvc-model-view-control)
    - [MVP (Model View Presenter)](#mvp-model-view-presenter)
    - [MVVM (ModelView View Model)](#mvvm-modelview-view-model)
    - [MVI: (Model View Intent)](#mvi-model-view-intent)
  - [Singleton dùng để làm gì](#singleton-dùng-để-làm-gì)
  - [Khi nào dùng Interface hoặc Abstract Class](#khi-nào-dùng-interface-hoặc-abstract-class)
  - [Liệt kê những trường hợp mà finally ko đc gọi](#liệt-kê-những-trường-hợp-mà-finally-ko-đc-gọi)
  - [Java dùng pass-by-value hay pass-by-reference](#java-dùng-pass-by-value-hay-pass-by-reference)
  - [Trình bày cách để break bên trong vòng lặp lòng nhau](#trình-bày-cách-để-break-bên-trong-vòng-lặp-lòng-nhau)
  - [Cách hoán đổi 2 số a và b mà ko cần tạo thêm biến thứ 3](#cách-hoán-đổi-2-số-a-và-b-mà-ko-cần-tạo-thêm-biến-thứ-3)
  - [Android Garbage collection hoạt động ntn](#android-garbage-collection-hoạt-động-ntn)
  - [Khi nào 1 object sẵn sàng for Garbage collection hốt](#khi-nào-1-object-sẵn-sàng-for-garbage-collection-hốt)
  - [Daemon Thread là gì](#daemon-thread-là-gì)
  - [Sealed class, data class](#sealed-class-data-class)
  - [S.O.L.I.D](#solid)
  - [let, also, apply, with](#let-also-apply-with)
  - [val, var, const, const val, lazy, lateinit](#val-var-const-const-val-lazy-lateinit)
  - [Rx](#rx)

## Liệt kê, giải thích 4 tính chất OOP

- Tính đóng gói (encapsulation)
  - Cho phép chỉnh sửa phạm vi truy cập của biến, phương thức
  - Cho phép gom các lớp thành Pakage

- Tính kế thừa (Inheritance)
  - Cho phép xây dựng 1 lớp mới, dựa trên lớp đã có.
  - Cho phép lớp con kế thừa các thành phần của Cha
  
- Tính đa hình (polymorphism)
  - Đối tượng có thể thay đổi kiểu (biến hình)
  - Lớp con có thể Ghi Đè lại phương thức lớp cha

- Tính trừu tượng (abstraction)
  - Cho phép loại bỏ tính chất phức tạp của đối tượng, 
  - bằng cách chỉ đưa ra các thuộc tính và phương thức cần thiết của đối tượng,
  - ẩn đi cách thức mà nó thực hiện.

## MVVM, MVP, MVC, MVI là gì, khi nào dùng cái nào

MVC: 1 Controler xử lý nhiều View
MVP: 1 Presenter xử lý 1 View, View giao tiếp trực tiếp vào Presenter
MVVM: 1 View Model xử lý 1 View, View giao tiếp ViewModel thông qua giao thức hỗ trợ
MVI: View giao tiếp ViewModel thông qua Intent và nhận State trả về

### MVC (Model View Control)

Controller get Event from User
1 Controller relate, control to multi View
Controller control View + Model

### MVP (Model View Presenter)

### MVVM (ModelView View Model)

View: interactive with user, show infomation, gét user input.
Model: handle with data, sqlite, file
3 Layer.
ViêwModel: connect View& ViewModel, handle demand from view.

View get Event from User
Multiple View mapping 1 ModelView
View contain relation properties to ViewModel
belong support technology, Need a libary to use

### MVI: (Model View Intent)

- View -> Intent -> ViewModel -> State -> View
- ![mvc mvp mvvm](images/mvc_mvp_mvvm.jpg)
- ![mvi](images/mvi.png)

## Singleton dùng để làm gì

- Một class chỉ có duy nhất một instance (khởi tạo)
- Cung cấp toàn cầu để truy cập tới instance đó
- Dùng khi ứng dụng chỉ cần duy 1 instance để quản lý (vd: Trình nghe nhạc, chỉ cần 1 Singleton Music) 

## Khi nào dùng Interface hoặc Abstract Class

- Abstract class: là một class cha cho tất cả các class có cùng bản chất.
- Interface: là một chức năng mà bạn có thể thêm và bất kì class nào.

## Liệt kê những trường hợp mà finally ko đc gọi

- Finally: biến không thay đổi giá trị sau khi khởi tạo

## Java dùng pass-by-value hay pass-by-reference

- Pass-by-value: (trong != ngoài) thay đổi biến trong hàm => ngoài hàm sẽ không bị ảnh hưởng. Nó giống như bạn copy giá trị của biến vào biến khác rồi truyền vào hàm.
- Pass-by-reference: (trong == ngoài) là khi bạn thay đổi biến trong hàm => ngoài hàm bị ảnh hưởng. Nó giống như bạn truyền đúng địa chỉ của biến đó vào hàm.

```java
public static void changeStuff(int a, Test b, Test c, int[] d)
{
    a = a * 10;     // méo đổi
    b = new Test(); // méo đổi
    c.item = "changed"; // đổi //reference
    d[0] = 3;   // đổi //reference
}
```

## Trình bày cách để break bên trong vòng lặp lòng nhau

```java
for(int i = 0; i < 1000; i++) {
   for(int j = 0; j < 1000; j++) {
       if(condition) {
            // both of the loops need to break and control will go to stmt2
            i = j = 1000; break;
       }
   }
}

// Dùng goto:
for(int i = 0; i < 1000; i++) {
    for(int j = 0; j < 1000; i++) {
        if (condition) {
            goto end;
        }
    }
}

end:
stmt2
```

## Cách hoán đổi 2 số a và b mà ko cần tạo thêm biến thứ 3

- Dùng cộng trừ

```java
a = a + b;
b = a - b;
a = a - b;
```

- Dùng Nhân chia

```java
a = a * b;
b = a / b;
a = a / b;
```

## Android Garbage collection hoạt động ntn

Khi object không sử dụng => Garbage Collector đánh dấu

Khi có Garbage Collector, chúng ta có thể cấp phát bộ nhớ cho một đối tượng sau đó sử dụng nó và khi không còn bất kì một tham chiếu nào tới đối tượng đó, đối tượng sẽ được đánh dấu để Garbage Collector giải phóng các bộ nhớ đã được phân bổ. Và Garbage collector cũng đảm bảo rằng mọi đối tượng có tham chiếu trực tiếp sẽ không bị xóa khỏi bộ nhớ.

## Khi nào 1 object sẵn sàng for Garbage collection hốt

- Object không còn được sử dụng, hay tham chiếu

## Daemon Thread là gì

là những luồng của java chạy song song với luồng của ứng dụng. (vd: Garbage collection)
Tự hủy cùng với ứng dụng.

- Immutable và mutable là gì
- Tại sao Class String trong Java lại immutable

- StringBuilder vs String
- StringBuilder vs StringBuffer

## Sealed class, data class

- Sealed class: là lớp trừu tượng (Abstract class - SubClass phải cùng file), mở rộng của Enum class (có thể sử dụng when)
- Data Class: Lớp lưu trữ dữ liệu, khi khởi tạo phải có Properties

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


---
