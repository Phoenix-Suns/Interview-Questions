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



- Singleton dùng để làm gì
- Khi nào dùng Interface hoặc Abstract Class
- Immutable và mutable là gì
- Tại sao Class String trong Java lại immutable
- Daemon Thread là gì
- Android Garbage collection hoạt động ntn
- Khi nào 1 object sẵn sàng for Garbage collection hốt
- StringBuilder vs String
- StringBuilder vs StringBuffer
- Liệt kê những trường hợp mà finally ko đc gọi
- Java dùng pass-by-value hay pass-by-reference
- Trình bày cách để break bên trong vòng lặp lòng nhau

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

---
