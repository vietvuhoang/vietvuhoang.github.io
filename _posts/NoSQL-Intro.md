---
layout: post
title: Giới thiệu về NoSQL
---

**_NoSQL_**, được viết tắt bởi **_"Not Only SQL"_** là phương pháp thiết kế Database thay thế cho Cơ Sở Dữ liệu truyền thống (**_RDBMS_**). 

Với các hệ thống cơ sở dữ liệu truyền thống ( _RDBMS_ ), hệ thống các bảng, các mối quan hệ, cấu trúc dữ liệu thường được thiết kế cẩn thận trước khi triển khai, điều này cũng có nghĩa rằng việc thay đổi cấu trúc dữ liệu sẽ trở bên khó khăn và hiếm khi xảy ra trong các phiên bản phần mềm. 
Ngày nay, với nhu cầu sử dụng dữ liệu lớn, các hệ thống cơ sở dữ liệu truyền thống, được thiết kế để chạy trên một server mạnh, thường gặp khó khăn trong việc nâng cấp, mở rộng (large scale-out) với chi phí đắt đỏ. 

![SQL]({{ site.baseurl }}/images/NoSQL/sql.png "Hard to scale-out with SQL")

_NoSQL_ là giải pháp hữu dụng cho các vấn đề mà cơ sở dữ liệu truyền thống gặp phải với các đặc tính phổ biến:

- Không sử dụng mô hình quan hệ (rational model)
- Thường là Open Source
- Không xác định rõ cấu trúc dữ liệu (Schemaless)
- Hoạt động tốt với mô hình Clusters, dễ mở rộng (large scale-out)

Các các hệ thống cơ sở dữ liệu _NoSQL_ thường được chia thành 4 loại căn cứ vào mô hình thiết kế của chúng:

- Key-Value Stores
- Document Stores
- Column Family Databases
- Graph Databases

![No SQL Familly](https://cdn.ttgtmedia.com/rms/onlineImages/data_management-nosql.png "No SQL Familly")

## Key-Value Stores

Kiểu NoSQL này sử dụng hash-table để lưu các unique-key trỏ đến các value tương ứng. Value có thể là bất cứ dạng dữ liệu nào: giá trị dạng number, text, JSON, BSON... 

Đây là dạng thiết kế đơn giản nhất của NoSQL. Client có thể sử dụng 3 method cơ bản: GET, PUT, DELETE để ghi và đọc dữ liệu. Và vì Key-Value NoSQL luôn truy cập Primary Key, nên rất dễ mở rộng vào có hiệu suất cao.

![Key-Value No SQL](https://d3an9kf42ylj3p.cloudfront.net/uploads/2018/02/021518-pic1.png?x38402 "Key-Value No SQL")

Key-Value Stores là giải pháp cho những ứng dụng yêu cầu tốc độ đọc ghi nhanh:
- Quản lý Session
- Data Caching 

Tuy nhiên, Key-value không phù hợp với các hệ thống đòi hỏi truy vẫn phức tạp. Điển hình của mô hình Key-Value chính là [Redis Cache](https://redis.io/ "Redis").

## Document Stores

Document Stores cũng gần giống Key-Value Stores, với mô hình quản lý theo Key trỏ đến Value tương ứng. Điểm khác biệt là Document Stores lưu trữ dữ liệu có cấu trúc dạng JSON, BSON hoặc XML, được gọi là *document*. Mỗi Document  là một đối tượng có cấu trúc mà thành phần (_attributes_) là dạng string, date, binary hoặc là array. Điều này giúp document dễ dàng được index và truy vấn thông qua các _attributes_.

_Document_ có cấu trúc mềm dẻo, dễ thay đổi theo thời gian, mỗi _documents_ có thể có cấu trúc khác nhau. Các _documents_ có thể được nhóm lại trong các _containers_ tùy thuộc vào yêu cầu bài toán. Mặt khác, các _documents_ còn có thể được chứa ngay trong một _document_ với cấu trúc không cần phải được xác định.

![Document Stores]({{ site.baseurl }}/images/NoSQL/documents.png)

Với sự mềm dẻo trong cấu trúc dữ liệu, và khả năng làm việc trên Cluster với lượng dữ liệu lớn, dễ scale-out, Document Stores thường được sử dụng trong các bài toán:

- Content Management System 
- E-commerce system 

Các cơ sở dữ liệu dạng Document: MongoDB, Couchbase.

## Column Family Databases

Column Family database sử dụng concept gọi là keyspace. Keyspace tương đương với Schema trong Rational Database. Keyspace chứa tất cả các Column Family. 

![Keyspace]({{ site.baseurl }}/images/NoSQL/keyspace.png)

Vậy Column Family là gì? Hãy xem một ví dụ về Column Family lưu thông tin User Profile như sau:

![Column Family]({{ site.baseurl }}/images/NoSQL/column_family.png)

Như vậy, mỗi _**Column Family**_ chứa các _**Rows**_, mỗi _**Row**_ chứa các _**Columns**_, Mỗi _**Column**_ có tên chính là từng attribute của _Object_ và _Value_, cùng _timestamp_.

![Row]({{ site.baseurl }}/images/NoSQL/row.png)

Như vậy nếu so sánh với Rational Database ta thấy rõ sự khác biệt: Mỗi _Table_ có nhiều rows, mỗi rows là một _object_ với các _column_ là các _attributes_, điều này cũng có nghĩa tất cả các _object_ thuộc một table sẽ được lưu vào cùng một nơi.

Với cách tiếp cận của Column Family, mỗi _object_ được lưu vào 1 _row_ trong Column Family, và dễ dàng phân tán ở nhiều nơi. 

_**Column Family**_ mang lại các lợi ích như sau:
- Hiệu quả khi nén (Compression) hoặc phân vùng dữ liệu
- Dễ mở rộng
- Truy vấn và load dữ liệu nhanh

Các hệ cơ sở dữ liệu loại Column Family: BigTable, Cassandra, HBase...


## Graph Databases

**Graph Database** chú trọng vào mối quan hệ giữa các đối tượng trong hệ thống. Ví dụ điển hình là trong mạng xã hội Facebook, bạn có bài viết nào, được tag vào ở bài viết nào, có mối quan hệ với ai... điều đó được thể hiện trong các _Nodes_ và _Relationships_ của _**Graph Database**_.

![Graph Databases]({{ site.baseurl }}/images/NoSQL/graphs.png)

**Graph Database** bao gồm các _Nodes_, và _Relationships_ giữa các _Nodes_. cả  _Nodes_ và _Relationships_ đều có các thuộc tính gọi là _properties_. _Nodes_ là các thực thể trong graph và có thể được gắn các _Lable_ cung cấp _context_ và _metadata_. Trong khi đó _Relationships_ cung cấp sự kết nối trực tiếp, đơn phương hay song phương giữa hai _Notes_. Có thể có nhiều hơn 1 mối quan hệ (_relationships_) giữa hai _Nodes_ và mỗi mối quan hệ có hướng, kiểu, điểm đầu (_Start Node_) và điểm cuối (_End Node_). 

Ví dụ cho loại cơ sở dữ liệu này là _Neo4j_.

## Tổng hợp và lược dịch 

[NoSQL (Not Only SQL database)](https://searchdatamanagement.techtarget.com/definition/NoSQL-Not-Only-SQL "NoSQL (Not Only SQL database)")

[NoSQL Data Architecture & Data Governance: Everything You Need to Know](http://www.dataversity.net/nosql-data-architecture-data-governance-everything-need-know/ "NoSQL Data Architecture & Data Governance: Everything You Need to Know")

[What is a Column Store Database?](https://database.guide/what-is-a-column-store-database/)

## Video Blog

[![GOTO 2012 • Introduction to NoSQL • Martin Fowler](https://img.youtube.com/vi/qI_g07C_Q5I/0.jpg) ](https://www.youtube.com/watch?v=qI_g07C_Q5I "GOTO 2012 • Introduction to NoSQL • Martin Fowler")

## Sách tham khảo

[NoSQL Distilled: A Brief Guide to the Emerging World of Polyglot Persistence](https://martinfowler.com/books/nosql.html "NoSQL Distilled")
