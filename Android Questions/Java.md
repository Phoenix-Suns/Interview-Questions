# Câu hỏi phỏng vấn Java

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

## MVVM, MVP, MVC là gì, khi nào dùng cái nào


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

---
