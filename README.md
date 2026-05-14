<img width="210"  alt="cb028101-de71-4be2-8264-7cbe3c22c04c" src="https://github.com/user-attachments/assets/de4e35a3-031f-487d-802a-a91c55bcd005" />
<img width="210" alt="af7e01ef-771a-452a-b6f0-538fb42e7f6f" src="https://github.com/user-attachments/assets/9fbf39c3-9a1d-456d-afa0-a0b1f9969169" />
<img width="210"  alt="78554ea6-e64e-47a2-9709-643f3cea2371" src="https://github.com/user-attachments/assets/ac921cd7-d856-4fdc-a7a3-638e5b3e4a65" />


# 📱 UserAPIApp — SwiftUI REST API Integration

**UserAPIApp** là ứng dụng iOS mẫu minh họa cách tích hợp REST API chuyên nghiệp sử dụng **SwiftUI** và **Networking Foundation** nguyên bản của Apple. Dự án được xây dựng theo chuẩn kiến trúc **MVVM** (Model-View-ViewModel), tập trung vào việc quản lý luồng dữ liệu bất đồng bộ và xử lý triệt để các trạng thái của giao diện (UI States).

---

## ✨ Tính năng nổi bật

* **Tải dữ liệu bất đồng bộ:** Tích hợp `URLSession` kết hợp với cú pháp `async/await` hiện đại.
* **Kiến trúc MVVM sạch:** Phân tách rõ ràng giữa giao diện (View), xử lý logic (ViewModel) và tác vụ mạng (Service).
* **Quản lý trạng thái giao diện (UI States):**
  * ⏳ **Loading State:** Hiển thị màn hình chờ khi đang tải dữ liệu.
  * ❌ **Error State:** Bắt và hiển thị lỗi thân thiện với người dùng kèm cơ chế **Retry** (thử lại).
  * 📭 **Empty State:** Giao diện tối ưu khi không có dữ liệu hoặc không tìm thấy kết quả.
* **Tìm kiếm trực tiếp (Searchable):** Lọc người dùng theo tên mượt mà ngay trên danh sách.
* **Làm mới dữ liệu (Pull-to-Refresh):** Hỗ trợ thao tác kéo để cập nhật dữ liệu mới nhất.
* **Tải ảnh bất đồng bộ (AsyncImage):** Hiển thị avatar ngẫu nhiên từ *Pravatar* kèm hiệu ứng placeholder.

---

## 🛠 Công nghệ & Thư viện sử dụng

* **Nền tảng:** iOS 16.0+
* **Ngôn ngữ:** Swift 5.9+
* **Giao diện:** SwiftUI
* **Networking:** URLSession nguyên bản (Không sử dụng thư viện bên thứ 3)
* **Phân tích dữ liệu:** Codable (JSON Parsing)

---

## 📂 Cấu trúc dự án

```text
UserAPIApp/
│
├── Models/
│   ├── User.swift          # Data model map với JSON
│   └── APIError.swift      # Định nghĩa các lỗi có thể xảy ra
│
├── Services/
│   └── UserService.swift   # Đảm nhiệm việc gọi API bằng async/await
│
├── ViewModels/
│   └── UserViewModel.swift # Điều phối dữ liệu, xử lý logic tìm kiếm & trạng thái
│
├── Components/
│   ├── LoadingView.swift   # Giao diện tải trang dùng chung
│   └── ErrorView.swift     # Giao diện thông báo lỗi & nút Retry
│
├── Views/
│   ├── UserRowView.swift   # Component hiển thị từng dòng user
│   ├── UserDetailView.swift# Màn hình thông tin chi tiết
│   └── UserListView.swift  # Màn hình danh sách chính
│
└── UserAPIApp.swift        # Entry point của ứng dụng

## Luồng dữ liệu (MVVM Flow)
┌───────────────┐      User Input       ┌───────────────────┐
│               ├──────────────────────>│                   │
│   SwiftUI     │                       │   UserViewModel   │
│    Views      │<──────────────────────┤                   │
└──────┬────────┘    Update UI (@Published)└─────────┬─────────┘
       │                                             │
       │ Navigation                                  │ fetchUsers()
       ▼                                             ▼
┌───────────────┐                       ┌───────────────────┐
│UserDetailView │                       │    UserService    │
└───────────────┘                       └─────────┬─────────┘
                                                     │
                                                     │ HTTP Request
                                                     ▼
                                        ┌───────────────────┐
                                        │     REST API      │
                                        └───────────────────┘
