---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
**Session Manager** là một chức năng nằm trong dịch vụ System Manager của AWS, SSM cung cấp khả năng quản lý phiên bản an toàn và có thể kiểm tra được mà **không cần mở cổng đến, không cần Bastion Host hoặc quản lý khóa SSH**. Session Manager cũng giúp dễ dàng tuân thủ các chính sách của công ty yêu cầu quyền truy cập có kiểm soát vào các phiên bản, thực hành bảo mật nghiêm ngặt và nhật ký có thể kiểm tra đầy đủ với các chi tiết truy cập phiên bản, trong khi vẫn cung cấp cho người dùng cuối quyền truy cập đa nền tảng bằng một cú nhấp chuột vào các phiên bản được quản lý của bạn.

Với việc sử dụng Session Manager, bạn sẽ có được những ưu điểm sau đây mà các cách làm truyền thống không có:

- Không cần phải mở cổng 22 cho giao thức SSH nên bảo mật hơn.
- Có thể cấu hình để kết nối không cần đi ra ngoài internet nên bảo mật hơn.
- Không cần quản lý private key của server để kết nối SSH.
- Quản lý tập trung được user bằng việc sử dụng AWS IAM.
- Truy cập tới server một cách dễ dàng và đơn giản bằng một click chuột.
- Thời gian truy cập nhanh chóng hơn các phương thức truyền thống như SSH
- Hỗ trợ nhiều hệ điều hành khác nhau như Linux, Windows, MacOS
- Log lại được các phiên kết nối và các câu lệnh đã thực thi trong lúc kết nối tới server.

Với những ưu điểm trên, bạn có thể sử dụng Session Manager thay vì sử dụng kỹ thuật Bastion host giúp chúng ta tiết kiệm được thời gian và tiền bạc khi quản lý server Bastion.