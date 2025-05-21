+++
date = '2025-05-21T01:22:32+07:00'
draft = true
title = 'Git Cơ Bản'
+++

# Bài biết sẽ giới thiệu những kiến thức và các câu lệnh cơ bản của Git
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
------- Updating -------



