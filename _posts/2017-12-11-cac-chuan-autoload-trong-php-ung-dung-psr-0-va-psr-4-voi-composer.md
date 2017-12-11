---
layout: post
title: Các chuẩn autoload trong PHP, ứng dụng PSR-0 và PSR-4 với Composer
categories: [PHP, Composer, PSR]
tags: [PHP, Composer, PSR]
fullview: true
comments: true
---

Như chúng ta đã biết, PSR (PHP Standards Recommendation) là chuẩn coding cho PHP được phát triển bởi FIG (Framework Interoperability Group), mặc dù không phải là chuẩn chính thức của PHP nhưng nó đã và đang được khuyến khích sử dụng bởi nhiều thư viện, framework và các sản phẩm PHP lớn.

Ở thời điểm hiện tại (cuối năm 2017) thì các PSR sau đây đã được ban hành và đang dùng:

- PSR-1: Basic Coding Standard (Tiêu chuẩn cơ bản khi viết code PHP)
- PSR-2: Coding Style Guide (Tiêu chuẩn trình bày code PHP)
- PSR-3: Logger Interface (Giao diện logger)
- ***PSR-4: Autoloading Standard***
- PSR-6: Caching Interface (Giao diện về Caching)
- PSR-7: HTTP Message Interface (Tiêu chuẩn Giao diện thông điệp HTTP)
- PSR-11: Container Interface (Giao diện về trình chứa DIC)
- PSR-13: Hypermedia Links (Tiêu chuẩn về biểu diễn liên kết)
- PSR-16: Simple Cache (Tạo Cache đơn giản từ PSR-6)

Ngoài ra, còn có ***PSR-0 là Autoloading Standard đã bị loại bỏ***.

Trong bài này, sẽ nói về 2 chuẩn autoload là PSR-0 (đã bỏ) và PSR-4 (đang dùng).

PSR-0: chuẩn Autoload cũ
------------------------

PSR-0 là tiêu chuẩn autoload kiểu cũ được dùng cho tới 21-10-2014. Hiện nay, chuẩn PSR-0 đã không còn được chấp nhận rộng rãi, chỉ còn tồn tại trong một số framework sử dụng từ trước đó và khó có thể thay đổi. Chuẩn PSR-0 vì không còn phổ dụng nên chuẩn PSR-4 được đề nghị sử dụng như là một chuẩn thay thế - mạnh mẽ hơn.

Chuẩn PSR-0 yêu cầu bắt buộc phải tuân thủ các điều kiện để tương tác Autoloader như sau: 

**Bắt buộc**

+ Một namespace và một Class phải có cấu trúc sau:

	**``\<Vendor Name>\(<Namespace>\)*<Class Name>``**

+ Với mỗi namespace thì đều phải chứa namespace cấp cao nhất: *('Vendor Name')*.
+ Các namespace có thể có nhiều sub-namespace tùy ý.
+ Mỗi dấu ngăn cách namespace (dấu ``\``) đều được convert thành *DIRECTORY_SEPARATOR* khi tương tác với file system.
+ Kí tự ``_`` trong tên class (CLASS NAME) đều được convert thành *DIRECTORY_SEPARATOR*, và dấu ``_`` không có nghĩa trong tên namespace (namespace không được có kí tự ``_ ``).
+ Một fully-qualified namespace kèm theo tên class phía sau sẽ được thêm đuôi (hậu tố) ``.php`` khi tương tác với file system.
+ Một tên namespace hoặc tên class chỉ được chứa các kí tự alphabetic, bao gồm viết hoa và viết thường.

**Ví dụ:**
``
\Doctrine\Common\IsolatedClassLoader => **/path/to/project/lib/**vendor/Doctrine/Common/IsolatedClassLoader.php

\Symfony\Core\Request => /path/to/project/lib/vendor/Symfony/Core/Request.php

\Zend\Acl => /path/to/project/lib/vendor/Zend/Acl.php
``

Dấu gạch dưới trong tên Namespace và Class sẽ biến thành dấu phân tách thư mục
```
\namespace\package\Class_Name => /path/to/project/lib/vendor/namespace/package/Class/Name.php

\namespace\package_name\Class_Name => /path/to/project/lib/vendor/namespace/package_name/Class/Name.php
```
