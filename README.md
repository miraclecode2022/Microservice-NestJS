# TRIỂN KHAI CẤU TRÚC DỰ ÁN

Triển khai cấu trúc dự án với ***NodeJS - Typescript - Nestjs Framework*** hướng tới cấu trúc ***Microservice*** - Giải thích các điểm lợi và hại ( kèm cách giải quyết ).


## NodeJS

- Node.js là một nền tảng chạy trên môi trường V8 JavaScript runtime - một trình thông dịch JavaScript cực nhanh chạy trên trình duyệt.
- Single Thread nhưng nhờ cơ chế Non-blocking I/O nên server có thể xử lý nhiều request cùng một lúc và trở nên nhanh hơn.
- Sử dụng JavaScript Event Loop.
- Hệ sinh thái ***npm*** đa dạng và được có rất nhiều cộng đồng hỗ trợ.

## Typescript
####  - Tại sao nên sử dụng TypeScript ?

- Là ngôn ngữ bậc cao của Javascript nhưng đồng thời vẫn hỗ trợ tốt JS thuần.
- Là ngôn ngữ dynamic type và hỗ trợ hầu hết các tính chất của các ngôn ngữ thuần hướng đối tượng như C/C++,Java... và các kĩ thuật của JS như ES6. Vì vậy khiến cho việc lập trình trở nên dễ dàng cũng nhưng là dễ maintain và mở rộng.
- Cha đẻ là ông lớn Google và được đông đảo người dùng sử dụng nên TS hỗ trợ được hầu hết các Framework của JS.
***
####  - Vậy TS có hại không ?

- Là ngôn ngữ bậc cao của JS nhưng TS không trực tiếp chạy trên browser và phải thông qua trình biên dịch trong core để chuyển đổi thành JS thuần khi runtime.
- TS yêu cầu tính rõ ràng và quy định chặt chẽ khi runtime nếu áp dụng TSlint hay ESlint vào sẽ đảm bảo tính tường minh của code, nhưng sẽ tốn nhiều thời gian hơn để code.
- Có thể nói TS là một mã nguồn mở nhưng vẫn phụ thuộc vào Google để có sự hỗ trợ lớn nhưng trong tương chưa biết sao. Google thường có vụ đem con bỏ chợ lắm, nhưng cũng may là TS đc đông đảo người dùng sử dụng.

## NestJS Framework

- Link github: https://github.com/nestjs/nest
> NestJS là một framework dùng để build NodeJS server-side applications một cách hiệu quả, dễ mở rộng. Được xây dựng và hỗ trợ đầy đủ với Typescript.
- Lấy cảm hứng từ cấu trúc **Microservice** nên cấu trúc khi build rất rõ ràng và dễ mở rộng hơn, NestJS cũng hỗ trợ để các lập trình viên build cấu trúc **Microservice** rất tốt.
-  Sử dụng CLI dễ dàng auto generate ra các module, service, middleware, controller... và tự kết nối chúng với nhau trong module.
- Mặc định sử dụng Jest framework làm Unit Test, khi generate các service, controller, middleware thì CLI tự động tạo file spec để tạo khung test cho file đó luôn.
- Ra đời sau một số framework khác nhưng được trọng dụng nhiều, hiện tại (2020) số star trên Github chỉ đứng thứ 3 sau Express và Meteor.
- NestJS có rất nhiều module hỗ trợ bạn, từ việc hot reload, logger cho đến GraphQL, Websocket rồi cqrs pattern, microservices,... Bạn chỉ cần NestJS để làm tất cả mọi thứ.
- Module microservices của NestJS hỗ trợ đủ loại kết nối: RabbitMQ, gRPC, Kafka, Redis,...
- Có thể sử dụng dễ dàng các package cài thêm giống như Express/Fastify.

## Cấu trúc Microservice

> Nền tảng cả kiến trúc microservices là xây dựng một ứng dụng mà ứng dụng này là tổng hợp của nhiều services nhỏ và độc lập có thể chạy riêng biệt, phát triển và triển khai độc lập.

#### Ưu điểm:

-   Cải thiện khả năng bảo trì - mỗi service tương đối nhỏ do đó dễ hiểu và thay đổi hơn.
-   Khả năng testing dễ dàng hơn - các services nhỏ hơn và nhanh hơn để test.
-   Khả năng triển khai tốt hơn - các services có thể được triển khai độc lập
-   Cho phép các services được phát triển bởi những team khác nhau. Mỗi team có thể phát triển, thử nghiệm, triển khai và mở rộng quy mô dịch vụ của mình một cách độc lập với tất cả các team khác.
-  Giảm thiểu rủi ro: Nếu có lỗi trong một service thì chỉ có service đó bị ảnh hưởng. Các services khác sẽ tiếp tục xử lý các yêu cầu. Trong khi đó, một thành phần hoạt động sai của kiến trúc một khối có thể làm ảnh hưởng toàn bộ hệ thống.
-  Dễ dàng thay đổi sử dụng các công nghệ mới: Khi triển khai các services bạn có thể lựa chọn nhiều công nghệ mới. Tương tự khi có thay đổi lớn đối với các services hiện có bạn có thể dễ dàng thay đổi công nghệ.

#### Nhược điểm:

-   Cần implement việc communication giữa các inter-services
-  Handle lỗi khó và phức tạp hơn vì một luồng sử lí có thể chạy qua nhiều service.
-  Việc thực hiện các requests trải rộng trên nhiều services khó khăn hơn, điều này cũng đòi hỏi sự phối hợp cẩn thận giữa các teams.
-   Khó khăn trong việc đảm bảo toàn vẹn CSDL nếu triển khai theo kiến trúc cơ sở dữ liệu phân vùng.
- Triển khai và quản lý microservices nếu làm thủ công theo cách đã làm với ứng dụng một khối phức tạp hơn rất nhiều. ( Cần áp dụng nhiều tool hỗ trợ để việc triển khai dễ dàng và chạy smooth. vd: RabitMQ, Docker, Kubernetes..).
-  Phải xử lý sự cố khi kết nối chậm, lỗi khi thông điệp không gửi được hoặc thông điệp gửi đến nhiều đích đến vào các thời điểm khác nhau.

## Giao thức liên hệ giữa các services.

#### TCP/IP Protocol

- **TCP/IP** là tập hợp nói chung của các giao thức như: **HTTP** - **HTTPS** - **FTP**
-  Thường dùng nhất là cho việc giao tiếp giữa client ( Web Service ) và backend ( Core Service ).
 -  TCP là giao thức hướng kết nối (connection-oriented), có nghĩa là buộc phải thiết lập kết nối trước sau đó mới đến tiến trình truyền dữ liệu.
 -   Cung cấp cơ chế đánh số thứ tự gói tin (sequencing): sử dụng để ráp các gói tin chính xác ở điểm nhận, loại bỏ gói tin trùng lặp.
 -  TCP có khả năng truyền và nhận dữ liệu cùng một lúc — song công (full-duplex).
 -   Cơ chế báo nhận (Acknowledgement): tức là khi A gửi gói tin cho B, nếu B nhận được thì sẽ gửi thông báo cho A, trường hợp A không nhận được thông báo thì sẽ gửi lại gói tin tới khi nào B báo nhận thì thôi.
 -   Tính năng phục hồi dữ liệu bị mất trên đường truyền.
 
 #### gRPC Protocol
 - gRPC là một RPC framework gíup bạn kết nối giữa các service trong hệ thống, nó hỗ trợ load balancing, tracing, health checking và authentication, hỗ trợ từ ứng dụng mobile, trình duyệt cho tới back-end service.
 - gRPC sử dụng Protocol Buffer để transfer data thay vì JSON/XML truyền thống nên tốc độ được gia tăng đáng kế, ngoài ra nó cũng dùng RPC thay cho REST API, trong việc thiết kế API, sự khác biệt giữa REST API vs RPC là REST được thiết kế để tập trung vào Resource còn RPC thì tập trung vào action, hành động.
 
## RabitMQ/Apache Kafka - MESSAGE QUEUE

## Kubernetes
