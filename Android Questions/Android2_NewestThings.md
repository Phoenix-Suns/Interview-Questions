# Những cái mới nhất

## Lập lịch, quản lý tác vụ ngầm

### Work Manager (Jetpack)

Work Manager là một thư viện được thiết kế cho việc lập lịch và quản lý các tác vụ ngầm (giống JobScheduler)
Dể sử dụng, dể truy cập, dể huỷ, hỗ trợ mọi android 14 trở lên

### JobScheduler (android 5)

Lên lịch, hẹn giờ để thực hiện tác vụ: (như: AlarmManager(không khuyến khích sử lý network))
- Task khi kết nối nguồn điện, khi kết nối Internet
- Task chạy mỗi ngày 1 lần

### Alarm manager

Lên lịch, hẹn giờ để thực hiện tác vụ. Kết nối với Alarm Service của hệ thống

## Android Jetpack

Architecture: Help design Robust, tesable apps
- Data Binding, LiveData: Tương tác View
- Lifecycles: Quản lý vòng đời Activity, Fragment
- Navigation: Điều hướng
- Paging
- Room: Lưu dữ liệu
- ViewModel: Phân chia sử lý logic
- Work Manager: lập lịch và quản lý các tác vụ ngầm.
(giống JobScheduler, Alarm manager)
- Compose: Xây dựng layout với kotlin

