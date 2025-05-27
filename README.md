# GIỚI THIỆU VỀ GIT
## Mục lục
- 1.[Một số câu lệnh git cơ bản](#một-số-câu-lệnh-git-cơ-bản)
- 2.[Một số tính năng cần thiết](#một-số-tính-năng-cần-thiết)
  - [pull data without lose changes](#pull-data-without-lose-changes)
- 3.[Xử lý lỗi](#xử-lý-lỗi)
  - [Lỗi liên quan đến xung đột history](#để-quản-lý-lịch-sử-và-nội-dung-giữa-hai-thư-mục-git-khác-nhau-bạn-có-một-số-tùy-chọn-tuỳ-theo-nhu-cầu-cụ-thể-dưới-đây-là-các-trường-hợp-và-các-bước-thực-hiện-tương-ứng)
- 4.[hướng dẫn tạo và đẩy git](#hướng-dẫn-tạo-và-đẩy-dự-án-lên-git)
- 5.[Các lệnh cần nhớ](#Các-lệnh-bạn-cần-nhớ)
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
git rebase

git rebase là một lệnh dùng để thay đổi lịch sử commit của nhánh hiện tại bằng cách áp dụng lại các commit của nhánh đó lên một nhánh khác (thường là nhánh chính như main hoặc master). Khi bạn rebase, Git sẽ “di chuyển” toàn bộ các commit của bạn từ vị trí hiện tại lên đầu của nhánh đích mà bạn chỉ định, giúp lịch sử commit trở nên gọn gàng và dễ hiểu hơn.

Cụ thể, lệnh git rebase giúp tái áp dụng các commit từ nhánh hiện tại (ví dụ feature-branch) lên đầu nhánh đích (ví dụ main), thay vì sử dụng merge (gộp các thay đổi lại với nhau).

Ví dụ sử dụng:
Rebase nhánh của bạn lên nhánh main:
```bash
git checkout feature-branch
git fetch origin           # Tải về những thay đổi mới nhất từ kho từ xa
git rebase origin/main      # Rebase nhánh feature-branch lên nhánh main
```
---

## Một số tính năng cần thiết 
### Pull data without lose changes


#### 1. Sử dụng git pull --rebase
- Lệnh này sẽ lấy những thay đổi từ remote và đặt chúng lên trên các thay đổi của bạn. Cách này giúp tránh các commit hợp nhất không cần thiết và giữ các thay đổi của bạn ở vị trí sau cùng.

```bash
git pull --rebase origin <tên-branch>
```
Giải thích: git pull --rebase sẽ cập nhật code từ remote, và nếu có xung đột giữa code remote và code bạn đang làm, Git sẽ yêu cầu bạn giải quyết các xung đột đó.

#### 2. Sử dụng git stash để tạm thời lưu các thay đổi của bạn
- Đây là phương pháp lưu các thay đổi chưa commit của bạn vào stash (một dạng bộ đệm tạm), sau đó bạn có thể kéo code mới từ remote về và lấy lại các thay đổi của mình sau đó.

```bash
# Bước 1: Lưu thay đổi của bạn
git stash

# Bước 2: Kéo code mới nhất từ remote
git pull origin <tên-branch>

# Bước 3: Lấy lại thay đổi của bạn từ stash
git stash pop
```
Giải thích: git stash sẽ lưu các thay đổi của bạn vào một nơi tạm thời mà không cần commit. Sau khi bạn kéo code từ remote về xong, git stash pop sẽ lấy lại các thay đổi của bạn và áp dụng lên code mới.
#### 3. Sử dụng git fetch và git merge thủ công
Nếu bạn muốn kiểm soát tốt hơn quá trình cập nhật, bạn có thể kéo code từ remote mà không kết hợp tự động, sau đó thực hiện hợp nhất (merge) thủ công.

```bash
# Bước 1: Fetch các thay đổi từ remote mà không merge
git fetch origin

# Bước 2: Merge các thay đổi từ remote vào branch hiện tại của bạn
git merge origin/<tên-branch>
```
Giải thích: git fetch chỉ lấy code từ remote về mà không hợp nhất vào branch hiện tại. Sau đó, git merge sẽ kết hợp các thay đổi từ remote vào branch của bạn, cho phép bạn giải quyết xung đột (nếu có) một cách thủ công.
#### 4. Sử dụng git cherry-pick nếu chỉ muốn lấy một số commit từ remote
Nếu remote có một số commit mà bạn muốn áp dụng, bạn có thể dùng git cherry-pick để áp dụng chúng mà không phải cập nhật toàn bộ.

```bash
# Lấy commit cụ thể từ remote
git cherry-pick <commit-hash>
```
Giải thích: git cherry-pick sẽ áp dụng từng commit mà bạn chỉ định từ remote vào branch hiện tại của bạn, giúp bạn giữ lại các thay đổi hiện tại.
#### 5. Khôi phục lại file đã xóa mà không reset toàn bộ code
Nếu bạn chỉ lỡ xóa một file hoặc thư mục và muốn khôi phục lại mà không reset toàn bộ, bạn có thể dùng git checkout để lấy lại file từ remote mà không ảnh hưởng đến các file khác.

```bash
git checkout origin/<tên-branch> -- <đường-dẫn-file-hoặc-folder>
```
Giải thích: Lệnh này sẽ lấy lại file hoặc folder cụ thể từ branch remote mà không làm thay đổi các file khác.

#### 6. Commit thay đổi cục bộ trước khi pull
Nếu các thay đổi hiện tại là cần thiết và bạn muốn lưu lại, bạn có thể commit chúng trước, sau đó thực hiện git pull:
```bash

git add .                       # Thêm tất cả thay đổi
git commit -m "Lưu thay đổi cục bộ"
git pull origin master          # Lấy thay đổi từ remote và merge vào
```
#### 7. Nếu không cần giữ thay đổi cục bộ và muốn khôi phục về trạng thái remote hoàn toàn
Nếu bạn muốn bỏ qua các thay đổi cục bộ chưa commit và đồng bộ hoàn toàn với remote, bạn có thể dùng reset --hard:
```bash
git reset --hard origin/master   # Khôi phục hoàn toàn theo remote, bỏ qua thay đổi cục bộ
```
Lưu ý: Cẩn thận với reset --hard vì lệnh này sẽ xóa các thay đổi cục bộ chưa commit.

---

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


# Hướng dẫn tạo và đẩy dự án lên Git

2. Tạo project với git
- clone 1 project có sẵn
=> git clone link_https

- Tạo 1 project trên github
```bash
Tạo 1 github repository (folder) - nơi chứa code
Clone project này:  git clone link_your_repo
Viết code
git status ( kiểm tra trạng thái files)
git add .  (thêm files)
git commit  -m “your_message”  (tạo nội dung commit)
git push origin main
```

- Tạo project local và đẩy lên github
```bash
Tạo 1 github repo
git init
Viết code
git status
git add .
git commit -m “your message”
git remote add origin https://…..
git push origin master
```
# Các lệnh bạn cần nhớ
- nếu có người sửa trên trùng code của bạn thì bạn cứ add và commit sau đó push và nó hiện thông bao pull nếu muốn an toàn thi dùng
```bash
git pull --no-rebase origin main
```
- => sau khi xử lý phải add . và commit  và push như thường

- nếu bạn muốn reset lại mọi thứ từ lần push cuối cùng lên git
```json
git fetch origin
git reset --hard origin/main
```
