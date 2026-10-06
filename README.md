# Báo cáo Bài 1: Khôi phục commit đã mất bằng Git Reflog

## 1. Mục tiêu
- Sử dụng lệnh `git reflog` để truy vết các tham chiếu commit cũ.
- Khôi phục một commit đã bị xóa khỏi nhánh làm việc do sử dụng lệnh `reset --hard`.

## 2. Quá trình thực hiện
Trong quá trình làm việc, em đã lỡ tay sử dụng lệnh `git reset --hard HEAD~1` khiến cho commit chứa file `feature.txt` bị biến mất hoàn toàn khỏi thư mục làm việc và không còn hiển thị khi gọi lệnh `git log`.

### Bước 1: Tra cứu Reflog
Để tìm lại commit đã bị mất, em dùng lệnh:
```bash
git reflog
```
Kết quả hiển thị trên terminal:
```
4eda03f (HEAD -> main) HEAD@{0}: reset: moving to HEAD~1
0aa1411 HEAD@{1}: commit: Them tinh nang quan trong
4eda03f (HEAD -> main) HEAD@{2}: commit (initial): Init
```
Dựa vào lịch sử này, em xác định được commit chứa tính năng quan trọng có mã hash là `0aa1411`.

### Bước 2: Khôi phục commit
Sau khi đã có mã hash, em dùng lệnh `reset --hard` để đưa con trỏ HEAD về lại trạng thái của commit đó:
```bash
git reset --hard 0aa1411
```
Kết quả trả về:
```
HEAD is now at 0aa1411 Them tinh nang quan trong
```

### Bước 3: Kiểm tra lại
Chạy lệnh `git log --oneline` để xác nhận commit đã quay trở lại:
```
0aa1411 (HEAD -> main) Them tinh nang quan trong
4eda03f Init
```
File `feature.txt` cùng đoạn code quan trọng bên trong cũng đã xuất hiện lại trong thư mục làm việc thành công.
