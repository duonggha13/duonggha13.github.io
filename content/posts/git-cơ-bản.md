+++
date = '2025-05-21T01:22:32+07:00'
draft = true
title = 'Git Cơ Bản'
+++

**Nội dung bài viết**
- [Version control là gì? Tại sao chúng ta cần quan tâm?](#version-control-là-gì-tại-sao-chúng-ta-cần-quan-tâm)
- [Git là gì?](#git-là-gì)
- [Khi nào nên sử dụng Git?](#khi-nào-nên-sử-dụng-git)
- [Tại sao bạn nên chọn Git thay vì các DVCSs khác?](#tại-sao-bạn-nên-chọn-git-thay-vì-các-dvcss-khác)
- [Các tính năng nổi bật của Git](#các-tính-năng-nổi-bật-của-git)
- [Các khái niệm cơ bản trong Git](#các-khái-niệm-cơ-bản-trong-git)
- [Cài đặt Git](#cài-đặt-git)
- [Các câu lệnh Git cơ bản](#các-câu-lệnh-git-cơ-bản)
  - [Khởi tạo và nhận kho lưu trữ (Getting, Creating Repository)](#khởi-tạo-và-nhận-kho-lưu-trữ-getting-creating-repository)
  - [Chụp hình cơ bản (Snapshotting)](#chụp-hình-cơ-bản-snapshotting)
  - [Chia nhánh và hợp nhất (Branching, Merging)](#chia-nhánh-và-hợp-nhất-branching-merging)
  - [Chia sẻ và cập nhật dự án (Sharing, Updating Project)](#chia-sẻ-và-cập-nhật-dự-án-sharing-updating-project)
  - [Kiểm tra và so sánh (Inspection, Comparison)](#kiểm-tra-và-so-sánh-inspection-comparison)
  - [Gỡ lỗi - tìm nguyên nhân (Debugging)](#gỡ-lỗi---tìm-nguyên-nhân-debugging)
  - [Vá lỗi (Patching)](#vá-lỗi-patching)
- [Best Practices với Git](#best-practices-với-git)
- [Tổng kết](#tổng-kết)

<br>
Bài biết sẽ giới thiệu những kiến thức và các câu lệnh cơ bản của Git
<br>
Trước khi đi đến khái niệm của Git, chúng ta cần biết về kiểm soát phiên bản - version control

## Version control là gì? Tại sao chúng ta cần quan tâm?
Version control là một hệ thống ghi lại thay đổi một tệp hoặc một tập hợp các tệp theo thời gian, giúp chúng ta có thể quay lại phiên bản cụ thể sau này.<br><br>
Các loại Version Control System (VCS): <br>
* Hệ thống kiểm soát cục bộ (Local Version Control Systems):
  - Đặc điểm: Lưu trữ tất cả thay đổi trên máy tính cá nhân người dùng, các phiên bản được quản lý bằng cách tạo các bản sao
  - Ưu điểm: Đơn gỉản, dễ sử dụng, không cần mạng
  - Nhược điểm: Dễ bị mất dữ liệu khi máy tính hỏng, khó làm việc nhóm
  - Ví dụ: RCS - Revision Control System
* Hệ thống kiểm soát tập trung (Centralized Version Control Systems - CVCSs)
  - Đặc điểm: Một máy chủ trung tâm lưu trữ toàn bộ các phiên bản, các máy khách sẽ truy cập và chỉnh sửa dữ liệu lên máy chủ
  - Ưu điểm: Dễ quản lý, kiểm soát quyền truy cập tốt
  - Nhược điểm: Dễ bị mất dữ liệu khi máy chủ hỏng, làm việc cần kết nối mạng
  - Ví dụ:
    - SVN - Apache Subversion
    - CVS - Concurrent Versions System
* Hệ thống kiểm soát phiên bản phân tán (Distributed Version Control Systems - DVCSs)
  - Đặc điểm: Mỗi người dùng có đầy đủ bản sao của kho lưu trữ (repository) trên máy tính
  - Ưu điểm: 
    + Linh hoạt, làm việc nhóm tốt
    + Không phụ thuộc vào máy chủ trung tâm
    + Dễ tạo nhánh và hợp nhất
    + Có thể làm việc offline, sau đó đồng bộ dữ liệu với những bản sao khác
  - Nhược điểm
    + Đòi hỏi người dùng có kiến thức sâu với quy trình làm việc của hệ thống
  - Ví dụ:
    + Git
    + Mercurial
    + Darcs
    + Bazaar

**Giờ chúng ta hãy cùng tìm hiểu về Git nhé**

## Git là gì?
Git là một hệ thống kiểm soát phiên bản phân tán (Distributed Version Control System - DVCSs). Git ra đời năm 2005 bởi Linus Torvalds, ban đầu Git được tạo ra phục vụ nhu quản lý mã nguồn phát triển nhân Linux sau khi bị mất quyền truy cập vào công cụ BitKeeper.

## Khi nào nên sử dụng Git?
Git là một hệ thống kiểm soát phiên bản phân tán, với những tính chất của DVCSs, Git thích hợp sử dụng khi:
* Làm việc nhóm hay dự án có nhiều người tham gia: Cho phép mỗi cá nhân chỉnh sửa đồng thời mà không lo xung đột
* Quản lý lịch sử thay đổi và phục hồi phiên bản: Các phiên bản được lưu trữ phục vụ việc khôi phục khi cần thiết
* Phát triển tính năng mới hoặc thử ngiệm: Tạo nhánh riêng để phát triển tính năng mới hoặc thử nghiệm mà không ảnh hưởng đến mã nguồn chính
* Làm việc từ xa hoặc ngoại tuyến: Làm việc ngoại tuyến trên kho lưu trữ cục bộ

## Tại sao bạn nên chọn Git thay vì các DVCSs khác?
Git có những đặc điểm nổi bật mà bạn nên chọn Git
* **Có cộng đồng rộng lớn**: Git có một cộng đồng người dùng rộng lớn và năng động, cung cấp nhiều tài nguyên học tập, hỗ trợ và công cụ bổ trợ. Điều này giúp bạn dễ dàng tìm kiếm sự trợ giúp và giải quyết vấn đề khi gặp khó khăn.
* **Hiệu suất cao**: Git được thiết kế để xử lý nhanh chóng các thao tác như commit, merge và checkout, ngay cả với các dự án lớn
* **Hỗ trợ branching và merging mạnh mẽ**: Việc tạo nhánh (branch) và hợp nhất (merge) trong Git rất nhẹ nhàng và hiệu quả, giúp quản lý các luồng phát triển song song một cách dễ dàng.
* **Bảo toàn toàn vẹn dữ liệu**: Git sử dụng thuật toán SHA-1 để đảm bảo rằng mọi thay đổi đều được theo dõi và không bị mất mát dữ liệu
* **Mã nguồn mở và miễn phí**: Git là phần mềm mã nguồn mở, cho phép cộng đồng đóng góp và phát triển liên tục

Bạn có thể tham khảo thêm tài liệu so sánh các hệ thống DVCSs tại: [comparision of version control software](https://en.wikipedia.org/wiki/Comparison_of_version-control_software)

## Các tính năng nổi bật của Git
* Cách lưu trữ dữ liệu: snapshot
  Thay vì lưu trữ dưới dạng "delta" - các thay đổi của các tệp theo thời gian (sự khác biệt giữa các phiên bản)
  ![alt text](/images/git/image.png)
  *Image Credit: Pro Git book*
  <br>
  <br>
  Thì thì lưu trữ dữ liệu như một chuỗi các ảnh chụp (snapshot) của toàn bộ dự án tại thời điểm commit. Nếu không có gì thay đổi Git chỉ tạo liên kết đến phiên bản trước đó giúp tiết kiệm dung lượng và tăng hiệu suất
  ![alt text](/images/git/image-1.png)
  *Image Credit: Pro Git book*
* Hầu hết các thao tác là cục bộ: Git thực hiện các thao tác như xem lịch sử, so sánh thay đổi, commit ngay trên máy cục bộ mà không cần kết nối mạng.
* Tính toàn vẹn dữ liệu: Mỗi tệp trong Git đều được kiểm tra bằng mã băm SHA-1 đảm bảo không có dữ liệu nào thay đổi mà không bị phát hiện, giúp bảo vệ dữ liệu khỏi sự cố hay bị thay đổi không mong muốn
* Git chủ yếu chỉ thêm dữ liệu: Git được thiết kế để tránh mất mát dữ liệu, hầu hết chỉ thực hiện thêm dữ liệu vào cơ sở dữ liệu Git, giúp lấy lại dữ liệu dễ dàng khi bị xoá nhầm hay thay đổi sai.
* Ba trạng thái chính trong Git:
  - Git theo dõi các tệp thông qua ba trạng thái
    + Modified (đã chỉnh sửa): Tệp được thay đổi nhưng chư đưa vào khu vực staging
    + Staged (đã đưa vào staging): Tệp đã được đánh dấu để đưa vào commit
    + Commited (đã commit): Tệp đã được lưu trữ an toàn trong cơ sở dữ liệu của Git
  - Ba thành phần chính tương ứng là
    + Working Directory (thư mục làm việc): Nơi bạn chỉnh sửa tệp
    + Staging Area (khu vực staging): Nơi bạn chuẩn bị các thay đổi cho commit
    + Git Directory (thư mục Git): Nơi Git lưu trữ dữ liệu và lịch sử của dự án 

## Các khái niệm cơ bản trong Git
Để sử dụng Git hiệu quả, trước tiên các bạn cần hiểu một số khái niệm cốt lõi của Git

1. Repository (Repo)
  Repository là nơi lưu trữ toàn bộ mã nguồn và lịch sử thay đổi của một dự án. Có 2 loại repository:
    - Local Repository: Dữ liệu trên máy cá nhân của bạn
    - Remote Repository: Dữ liệu nằm trên máy chủ Git như GitHub, GitLab, Bitbucket
  Một dự án thường có 2 Git thường bao gồm cả 2 loại, bạn sẽ làm việc với local và sau đó đồng bộ lên remote repository

2. Commit
  Commit được hiểu là một ảnh chụp (snapshot) các thay đổi tại một thời điểm. Một commit sẽ lưu nội dung:
    - Nội dung thay đổi
    - Thời gian commit
    - Người thực hiện commit
    - Lời nhắn (commit message)
  Commit giúp quay lại phiên bản cũ và theo dõi quá trình phát triển của dự án
3. Branch
  Nhánh, là dòng phát triển độc lập của dự án. Mặc định Git có một nhánh chính gọi là `main` hoặc `master`. Bạn có thể tạo nhánh để thực hiện việc thêm tính năng, sửa lỗi, thử nghiệm,.. mà không ảnh hưởng đến mã chính của dự án
4. Merge
   Merge là hành độnh hợp nhất 2 nhánh lại với nhau, việc merge có thể tạo ra xung đột, Git sẽ báo để bạn xử lý
5. Rebase
   Rebase là một cách khác để hợp nhất thay đổi giữa các nhánh, nhưng thay vì hợp nhất như merge thì rebase di chuyển lịch sử thay đổi của một nhánh lên đầu nhánh đích, rebase giúp lịch sử commit đơn giản nhưng cũng có thể xảy ra xung đột
6. HEAD
   HEAD là con trỏ trỏ tới commit hiện tại bạn đang làm việc, nếu HEAD không gắn với nhánh nào, bạn đang ở trạng thái detached HEAD

## Cài đặt Git
Cài đặt Git cho Linux:<br>
  - Nếu bạn sử dụng Fedora, hay những hệ điều hành RPM-based như RHEL hay CentOS, sử dụng dnf
    ```bash
    sudo dnf install git
    ```
  - Nếu bạn sử dụng Debian-base như Ubuntu, sử dụng apt
    ```bash
    sudo apt install git
    ```
Chi tiết cài đặt cho từng hệ điều hành xem tại trang chính thức git: [download git](https://git-scm.com/downloads)

## Các câu lệnh Git cơ bản

### Khởi tạo và nhận kho lưu trữ (Getting, Creating Repository)

- [init](https://git-scm.com/docs/git-init)
Tạo một kho chứa rỗng hoặc khởi tạo lại kho lưu trữ hiện có
  ```bash
  cd /path/to/my/codebase
  git init      #Tạo thư mục /path/to/my/codebase/.git
  ```
- [clone](https://git-scm.com/docs/git-clone)
Tải dữ liệu bản sao của kho chứ remote về máy cá nhân
  ```bash
  git clone https://github.com/user/project.git
  ```

### Chụp hình cơ bản (Snapshotting)

- [add](https://git-scm.com/docs/git-add)
Thêm tệp vào khu vực staging để chuẩn bị commit.
  ```bash
  git add file.txt      # Thêm một tệp cụ thể
  git add .             # Thêm tất cả thay đổi
  ```
- [status](https://git-scm.com/docs/git-status)
Kiểm tra trạng thái các tệp: đã thay đổi, đã staged hay chưa
  ```bash
  git status
  ```
- [diff](https://git-scm.com/docs/git-diff)
Hiển thị sự khác biệt giữa các thay đổi. Hữu ích để xem chi tiết trước khi add hay commit.
  ```bash
  git diff
  ```
- [commit](https://git-scm.com/docs/git-commit)
Lưu snapshot hiện tại vào lịch sử Git.
  ```bash
  git commit -m "lời nhắn commit"
  ```
- [notes](https://git-scm.com/docs/git-notes)
Ghi chú thêm vào commit mà không thay đổi nội dung commit
  ```bash
  git notes add -m "Thêm ghi chú cho commit này"
  git notes show <commit>
  ```

- [restore](https://git-scm.com/docs/git-restore)
Khôi phục tệp về trạng thái trước đó
  ```bash
  git restore file.txt                      # Khôi phục file.txt từ index
  git restore --source=HEAD~1 file.txt      # Khôi phục file từ commit cụ thể
  ```
- [reset](https://git-scm.com/docs/git-reset)
Reset lại index hoặc HEAD
  ```bash
  git reset --soft HEAD~1   # Quay lại commit trước, giữ lại thay đổi trong staging
  git reset --hard HEAD~1   # Xóa hoàn toàn thay đổi, quay về commit trước
  ```
- [rm](https://git-scm.com/docs/git-rm)
Xoá tệp khỏi Git (và có thể khỏi thư mục làm việc)
  ```bash
  git rm file.txt            # Xoá file khỏi repo và thư mục làm việc
  git rm --cached file.txt   # Chỉ xoá khỏi Git (không xoá trên ổ đĩa)
  ```
- [mv](https://git-scm.com/docs/git-mv)
Đổi tên hoặc di chuyển file trong Git
  ```bash
  git mv old_name.txt new_name.txt
  ```

### Chia nhánh và hợp nhất (Branching, Merging)

- [branch](https://git-scm.com/docs/git-branch)
Tạo và quản lý nhánh
  ```bash
  git branch                  # Liệt kê các nhánh
  git branch new-feature      # Tạo nhánh mới
  ```
- [checkout](https://git-scm.com/docs/git-checkout)
Chuyển nhánh hoặc khôi phục file
  ```bash
  git checkout main
  git checkout -- file.txt   # Khôi phục file từ index
  ```
- [switch](https://git-scm.com/docs/git-switch)
Thay thế checkout để chuyển nhánh (dễ hiểu hơn)
  ```bash
  git switch main
  git switch -c new-branch   # Tạo và chuyển sang nhánh mới
  ```
- [merge](https://git-scm.com/docs/git-merge)
  Gộp nhánh
  ```bash
  git merge feature-branch   # Gộp nhánh vào nhánh hiện tại
  ```
- [mergetool](https://git-scm.com/docs/git-mergetool)
Mở giao diện resolve conflict
  ```bash
  git mergetool              # Dùng tool GUI để xử lý xung đột merge
  ```
- [log](https://git-scm.com/docs/git-log)
Xem lịch sử commit
  ```bash
  git log --oneline --graph  # Dạng cây ngắn gọn
  ```
- [stash](https://git-scm.com/docs/git-stash)
Lưu tạm thay đổi chưa commit
  ```bash
  git stash                  # Lưu thay đổi tạm thời
  git stash pop              # Khôi phục và xoá stash
  ```
- [tag](https://git-scm.com/docs/git-tag)
Gắn thẻ cho commit (ví dụ: release)
  ```bash
  git tag v1.0               # Gắn tag nhẹ
  git tag -a v1.1 -m "release v1.1"  # Gắn tag có mô tả
  ```
- [worktree](https://git-scm.com/docs/git-worktree)
Làm việc với nhiều thư mục cùng một repo
  ```bash
  git worktree add ../feature feature-branch
  ```

### Chia sẻ và cập nhật dự án (Sharing, Updating Project)
- [fetch](https://git-scm.com/docs/git-fetch)
Lấy dữ liệu từ remote nhưng không merge
  ```bash
  git fetch origin
  ```
- [pull](https://git-scm.com/docs/git-pull)
Fetch + Merge hoặc Rebase
  ```bash
  git pull origin main
  ```
- [push](https://git-scm.com/docs/git-push)
Đẩy commit lên remote
    ```bash
    git push origin main
    ```
- [remote](https://git-scm.com/docs/git-remote)
Quản lý remote
  ```bash
  git remote -v              # Liệt kê remote
  git remote add origin <url>
  ```
- [submodule](https://git-scm.com/docs/git-submodule)
Nhúng repo bên ngoài vào project
  ```bash
  git submodule add <url> path/
  git submodule update --init --recursive
  ```

### Kiểm tra và so sánh (Inspection, Comparison)

- [show](https://git-scm.com/docs/git-show)
Hiển thị chi tiết commit
  ```bash
  git show HEAD
  ```
- [log](https://git-scm.com/docs/git-log)
Xem nhật ký commit
  ```bash
  git log
  ```
- [diff](https://git-scm.com/docs/git-diff)
So sánh sự khác biệt
  ```bash
  git diff                   # So sánh working tree và index
  git diff HEAD              # So sánh working tree với HEAD
  ```
- [difftool](https://git-scm.com/docs/git-difftool)
Dùng GUI tool để xem diff
  ```bash
  git difftool
  ```
- [range-diff](https://git-scm.com/docs/git-range-diff)
So sánh 2 dải commit
  ```bash
  git range-diff origin/main...HEAD
  ```
- [shortlog](https://git-scm.com/docs/git-shortlog)
Tổng hợp commit theo tác giả
  ```bash
  git shortlog -sne
  ```
- [describe](https://git-scm.com/docs/git-describe)
Gán tên cho commit theo tag gần nhất
  ```bash
  git describe --tags
  ```

### Gỡ lỗi - tìm nguyên nhân (Debugging)

- [apply](https://git-scm.com/docs/git-apply)
Áp dụng file patch
  ```bash
  git apply fix.patch
  ```
- [cherry-pick](https://git-scm.com/docs/git-cherry-pick)
Áp dụng commit cụ thể từ nhánh khác
  ```bash
  git cherry-pick <commit-hash>
  ```
- [diff](https://git-scm.com/docs/git-diff)
So sánh sự khác biệt
  ```bash
  git diff                   # So sánh working tree và index
  git diff HEAD              # So sánh working tree với HEAD
  ```
- [rebase](https://git-scm.com/docs/git-rebase)
Chuyển base commit
  ```bash
  git rebase main
  ```
- [revert](https://git-scm.com/docs/git-revert)
Tạo commit đảo ngược (tạo một commit mới có nội dung ngược lại với một commit đã tồn tại, nhằm hủy bỏ tác động của commit đó, nhưng vẫn giữ nguyên lịch sử commit)
  ```bash
  git revert <commit-hash>
  ```

### Vá lỗi (Patching)

- [bisect](https://git-scm.com/docs/git-bisect)
Tìm commit gây lỗi theo nhị phân
  ```bash
  git bisect start
  git bisect bad             # Commit hiện tại bị lỗi
  git bisect good <commit>   # Commit ổn định
  ```
- [blame](https://git-scm.com/docs/git-blame)
Tìm ai đã thay đổi dòng code nào
  ```bash
  git blame file.txt
  ```
- [grep](https://git-scm.com/docs/git-grep)
Tìm chuỗi trong toàn bộ repo
  ```bash
  git grep "function main"
  ```

## Best Practices với Git
Đây một số best practices được tổng hợp dựa trên lý thuyết nền tảng, những kinh nghiệm làm việc của cá nhân tôi và những chia sẻ của cộng đồng sử dụng Git

1. **Kiểm tra thay đổi trước khi commit**
 <br>Luôn xem lại thay đổi kỹ lưỡng trước khi commit
     ```bash
     git diff
      ```
2. **Commit rõ ràng, ngắn gọn, có ý nghĩa**
   * Không nên:
     - `Update`
     - `Fix bug`
   * Nên:
     - `Fix login form validation`
     - `Refactor user authentication logic`

3. **Commit nhỏ, rõ ràng về mặt logic**
   * Nên:
     - `Add password confirmation field`
     - `Fix typo in README`
   * Không nên:
     - `Add feature + fix 2 unrelated bugs`
   * Ví dụ theo [Conventional Commits](https://www.conventionalcommits.org/):
     - `feat: add search bar to header`
     - `fix: handle empty input in login form`
     - `docs: update API usage in README`
4. **Dùng git stash khi đang dở dang**
   * Khi bạn đang làm dang dở nhưng cần chuyển sang một nhánh khác (ví dụ để fix bug khẩn cấp), git stash cho phép bạn:
     - Lưu lại những thay đổi tạm thời.
     - Trả lại repo về trạng thái sạch sẽ (working directory clean) mà không mất công việc đang làm.
5. **Sử dụng nhánh (branch) hợp lý**
   * `main`: Mã ổn định, có thể deploy
   * `feature-<tên>`: Phát triển tính năng
   * `bugfix-<tên>`: Sửa lỗi
   * `hotfix-<tên>`: Sửa lỗi khẩn cấp
   * `release-<version>`: Chuẩn bị phát hành

6. **Không commit file cấu hình cá nhân, commit sercet (mật khẩu, API key)**
   * Tránh commit .env, config.local.json, v.v.
   * Nên tạo file mẫu như .env.example

## Tổng kết
Bài viết đã giới thiệu những kiến thức cơ bản của Git cũng như các câu lệnh cơ bản mà các lập trình viên thường hay sử dụng, cùng với một số best practices về Git. Hy vọng bài viết giúp các bạn làm quen và sử dụng Git một cách dễ dàng.



**Tài liệu tham khảo**:
* [Git Documents](https://git-scm.com/docs)
* [Pro Git Book](https://git-scm.com/book/en/v2)