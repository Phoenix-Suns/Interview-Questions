# Clear Architecture Note

- Presentation : Chịu trách nghiệm việc hiển thị thông tin cho người dùng
  - Gồm: 
    - UI (Activities & Fragments)
    - Presenters/ViewModels (gọi User case, mapper)
- Domain : Thể hiện các khái niệm về business logic của ứng dụng
  - Gồm:
    - Use case
    - Entities (Model)
    - Repository Interfaces
- Application (có thể Chung Domain layer) : Định nghĩa các công việc mà phần mềm được cho là thực hiện bằng cách phối hợp luồng dữ liệu từ và đến các domain model
  - Usecase gọi đến Data Layer
- Data : Chứa các domain model
  - Gồm:
    - Reponsitory Implementations
    - Data Source
    - Mapper (Network, Room to Model)

![](images/clear_architecture_contain.png)

## Data Flow

![](images/clear_architecture_data_flow.png)

UI (View) ↔ ViewModel ↔ UseCase ↔ Repository ↔ Data Source (API/DB)

1. UI: Nhận dữ liệu từ ViewModel, hiển thị trên giao diện. gọi phương thức từ ViewModel.
2. ViewModel: Xử lý sự kiện UI, gọi UseCase để lấy dữ liệu.
3. UseCase: thu thập dữ liệu từ User và gởi Repositories.
4. Repository: trả về dữ liệu từ Data Source (Local hay Remote).
5. Data trả về UI để hiển thị

🚀 Dữ liệu luân chuyển theo một hướng rõ ràng từ Data → Domain → Presentation.



## Dependency Rule

![](images/clear_architecture_dependency.png)

## Reference

- <https://proandroiddev.com/clean-architecture-data-flow-dependency-rule-615ffdd79e29>
