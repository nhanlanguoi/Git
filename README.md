# GIỚI THIỆU VỀ GIT
## Mục lục
- 1.[Một số câu lệnh git cơ bản](#một-số-câu-lệnh-git-cơ-bản)
- 2.[Xử lý lỗi](#xử-lý-lỗi)
---
## Một số câu lệnh git cơ bản

### 1. Khởi tạo và cấu hình Git
git init: Khởi tạo một repository Git mới trong thư mục hiện tại.
```bash
git init
```

git clone <`repository-url`>: Tạo bản sao của một repository từ URL.


```bash
git clone https://github.com/username/repo.git
```

git config: Thiết lập cấu hình Git như tên người dùng và email.
```bash
git config --global user.name "Tên của bạn"
git config --global user.email "email@example.com"
```
### 2. Kiểm tra trạng thái và log
git status: Kiểm tra trạng thái của các tệp trong thư mục, giúp bạn biết tệp nào đã được chỉnh sửa, tệp nào đang trong khu vực tạm (staging), và tệp nào chưa được theo dõi.

```bash
git status
```
git log: Hiển thị lịch sử commit của repository.

```bash
git log
```
### 3. Thêm và commit thay đổi
git add <`file`>: Thêm một tệp vào khu vực tạm (staging).

```bash
git add <file-name>
```
git add .: Thêm tất cả các tệp đã chỉnh sửa vào khu vực tạm.

```bash
git add .
```
git commit -m "message": Commit các thay đổi trong khu vực tạm với một tin nhắn.

```bash
git commit -m "Mô tả ngắn gọn về thay đổi"
```

### 4. Làm việc với các nhánh (branches)
git branch: Liệt kê tất cả các nhánh trong repository.

```bash
git branch
```
git branch <`branch-name`>: Tạo một nhánh mới.

```bash
git branch new-feature
```
git checkout <`branch-name`>: Chuyển đổi sang nhánh khác.

```bash
git checkout new-feature
```
git checkout -b <`branch-name`>: Tạo và chuyển ngay sang nhánh mới.

```bash
git checkout -b new-feature
```
git merge <`branch-name`>: Hợp nhất nhánh được chỉ định vào nhánh hiện tại.

```bash
git merge new-feature
```
### 5. Đẩy và lấy thay đổi từ remote
git remote add origin <`url`>: Thêm một remote mới với tên origin vào repository của bạn.

```bash
git remote add origin https://github.com/username/repo.git
```
git push origin <branch-name>: Đẩy nhánh hiện tại lên remote origin.

```bash
git push origin master
```
git fetch: Lấy thông tin mới nhất từ remote nhưng không hợp nhất vào nhánh hiện tại.

```bash
git fetch
```
git pull: Lấy thay đổi từ remote và hợp nhất vào nhánh hiện tại.

```bash
git pull origin master
```
### 6. Xử lý các xung đột (conflicts)
Xung đột xảy ra khi có thay đổi xung đột ở cùng một dòng hoặc cùng một tệp giữa các nhánh khác nhau.
Khi gặp xung đột, Git sẽ thông báo và bạn có thể sử dụng các công cụ hỗ trợ (ví dụ như VS Code) để chỉnh sửa và chọn giữ thay đổi nào. Sau khi chỉnh sửa xong, sử dụng:
```bash
git add <file>
git commit -m "Resolve conflict"
```
### 7. Các lệnh khác
git stash: Lưu tạm thời các thay đổi chưa commit để có thể quay lại sau.

```bash
git stash
```
git stash pop: Áp dụng lại các thay đổi đã được lưu trong stash.

```bash
git stash pop
```
git reset --hard <`commit-id`>: Khôi phục toàn bộ repository về một commit cụ thể.

```bash
git reset --hard <commit-id>
```
git rm <`file`>: Xóa tệp khỏi repository và commit thay đổi.

```bash
git rm <file-name>
```
### 8. Xem và xóa nhánh remote
git branch -r: Liệt kê tất cả các nhánh trên remote.

```bash
git branch -r
```
git push origin --delete <branch-name>: Xóa nhánh trên remote.

```bash
git push origin --delete <branch-name>
```






## Xử lý lỗi 

### Để quản lý lịch sử và nội dung giữa hai thư mục Git khác nhau, bạn có một số tùy chọn tuỳ theo nhu cầu cụ thể. Dưới đây là các trường hợp và các bước thực hiện tương ứng:

#### 1. Gộp lịch sử (history) của hai thư mục Git (local và remote)
   
Nếu bạn muốn gộp lịch sử của thư mục mới với thư mục đã có trên remote mà không mất dữ liệu, bạn có thể thực hiện như sau:

- Bước 1: Kéo lịch sử từ remote về (nếu chưa có), đồng thời tạo một nhánh mới từ remote để đảm bảo bạn giữ được lịch sử cũ.

```bash
git pull origin main --allow-unrelated-histories
```

- Bước 2: Nếu có xung đột, hãy sửa các xung đột, sau đó commit lại.

```bash
git add .
git commit -m "Merged histories"
```
- Bước 3: Sau khi gộp xong, bạn có thể đẩy toàn bộ lịch sử mới lên remote.

```bash
git push origin main
```

#### 2. Thay thế nội dung trên remote bằng nội dung từ thư mục hiện tại

Nếu bạn muốn xóa nội dung cũ trên remote và thay thế bằng nội dung của thư mục mới, thì bạn cần dùng force push. Điều này sẽ ghi đè toàn bộ nội dung và lịch sử trên remote.

- Bước 1: Đảm bảo bạn đang ở nhánh muốn đẩy lên (ví dụ: main).

```bash
git checkout main
```
- Bước 2: Thực hiện force push để ghi đè lịch sử trên remote.

```bash
git push -f origin main
```
#### 3. Kéo nội dung từ remote về và xóa nội dung hiện tại (sao chép remote xuống)
Nếu bạn muốn lấy lại thư mục từ remote và thay thế toàn bộ nội dung trong thư mục hiện tại, bạn có thể làm như sau:

- Bước 1: Xóa toàn bộ nội dung hiện tại (đảm bảo không có thay đổi chưa commit).

```bash
rm -rf *
```
- Bước 2: Kéo nội dung từ remote về.

```bash
git pull origin main
```

#### 4. Kéo nội dung từ remote về và gộp với nội dung hiện tại (kết hợp cả hai)
Nếu bạn muốn kết hợp nội dung từ remote với thư mục hiện tại, bạn có thể sử dụng git pull với --allow-unrelated-histories.

- Bước 1: Thực hiện pull với tùy chọn --allow-unrelated-histories.

```bash
git pull origin main --allow-unrelated-histories
```
- Bước 2: Nếu có xung đột, hãy giải quyết xung đột rồi commit.

```bash
git add .
git commit -m "Merged local and remote content"
```
Các lệnh này sẽ giúp bạn quản lý lịch sử và nội dung của hai thư mục Git khác nhau.
