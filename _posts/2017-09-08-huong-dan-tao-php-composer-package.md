---
layout: post
title: Hướng dẫn tạo PHP Composer Package
categories: [PHP, Composer]
tags: [GitHub, Packagist, PHP, Composer]
fullview: true
comments: true
---

Đề tạo một PHP Composer Package làm thư viện nhúng vào các dự án khác, chúng ta cần thực hiện các bước như sau:

**Bước 1**: Tạo một repository trên *GitHub* và clone về máy local


- Để clone 1 repository có sẵn ở trên máy cục bộ, bạn hãy sử dụng dòng lệnh: `git clone /đường-dẫn-đến/repository/` (đường dẫn có thể copy từ giao diện ***Clone and download***. Ví dụ: `https://github.com/webhoanhao/ggsignin.git`).
- Nếu repository đó ở máy chủ khác thì bạn hãy gõ dòng lệnh: `git clone tênusername@địachỉmáychủ:/đường-dẫn-đến/repository`


**Bước 2**: Trong thư mục vừa clone về, chạy `composer init` để tạo ra file `composer.json` cho package

**Bước 3**: Chỉnh sửa file `composer.json` để có nội dung phù hợp cho package

**Bước 4**: Viết code cho package

**Bước 5**: Đưa code lên lại *GitHub*

**Bước 6**: Tạo tag phiên bản phát hành cho package

**Bước 7**: Submit package lên *Packagist*
