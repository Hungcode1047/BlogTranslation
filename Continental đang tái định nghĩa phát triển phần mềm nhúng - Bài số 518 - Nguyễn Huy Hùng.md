# Continental đang tái định nghĩa phát triển phần mềm nhúng.

> **📖 Bài viết gốc**: https://aws.amazon.com/vi/blogs/industries/continental-is-redefining-embedded-software-development/ 
> **👤 Tác giả**: Amir Mahdi Namazi, Daniel Schleicher, Martin Kraus, và Samer Odeh 
> **📅 Ngày xuất bản**: 11 Tháng 4 2025
> **🌐 Nguồn**: AWS for Industries 
> **👨‍💻 Người dịch**: Nguyễn Huy Hùng - FCJ Intern  
> **📅 Ngày dịch**: 06/07/2025 
> **⏱️ Thời gian đọc**: 3-7 phút

---

## 📋 Tóm tắt

Continetal là một trong những công ty trong lĩnh vực ảo hóa phần cứng của xe ô tô. Thay vì thiết kế phần cứng vật lí rồi mới thiết kế phần mềm dành cho phần cứng vật lí đó, một điều sẽ khiến cho việc phát triển phần mềm trở nên giới hạn.
Thì giờ đây, việc ảo hóa các phần cứng này, cụ thể hơn thiết kế một phần cứng vật lí ở môi trường ảo trước. Điều này có thể làm song song với việc phát triển phần mềm. Trong khi trước kia là không thể vì giới hạn phần cứng vật lí.
Ngoài ra công ty còn kết hợp AWS trong lĩnh vực ảo hóa này.

**🎯 Đối tượng đọc**: Dành cho đối tượng quan tâm về lĩnh vực oto, xe máy điện, lĩnh vực tự động hóa.
**📊 Độ khó**: Dễ  
**🏷️ Tags**: SDV, software defined vehicle

---

## 📚 Mục lục

- Phần 1: Giới thiệu
- Phần 2: Bước nhảy tới việ ảo hóa ECU
- Phần 3: Sự hướng đến ưu tiên thiết kế phần mềm ECU
- Kết luận.
- Đôi lời về tác giả.
---

Nội dung bài dịch chính:

Continental đang tái định nghĩa phát triển phần mềm nhúng.

Bởi Amir Mahdi Namazi, Daniel Schleicher, Martin Kraus, and Samer Odeh vào 11 4 2025 tại Amazon EC2, Automotive, Industries

Việc ảo hóa các bộ điều khiển điện tử (Electronic control units - ECUs) và các ứng dụng mà chúng hỗ trợ đã trở thành một nền tảng trọng yếu cho việc đổi mới trong ngành công nghiệp ô tô. Continental đang thay đổi lại định nghĩa của việc phát triển phần mềm nhúng bằng cách tách rời quá trình phát triển và kiểm thử phần mềm ECU khỏi sự phụ thuộc vào các giới hạn của phần cứng vật lý. Sự ảo hóa mở ra khả năng thực hiện song song công việc phát triển phần cứng và phần mềm cho các ECU mới, giúp rút ngắn đáng kể thời gian đưa sản phẩm ra thị trường theo cấp số nhân. Hơn nữa, sự ảo hóa còn cung cấp quyền hạn mạnh mẽ hơn cho các nhà phát triển trên toàn thế giới trong việc thiết kế và kiểm tra các ứng dụng cho ECU. Giờ đây, họ không còn cần đến phần cứng vật lý để tiến hành xác thực tính thực thi của những ứng dụng đang trong quá trình phát triển dành cho ECU.

Continental AG (Continental), một Đối tác của AWS, đang đi đầu trong xu hướng ảo hóa này với sản phẩm Smart Cockpit High-Performance Computer (HPC), Có thể tạm dịch là Buồng Lái Thông Minh sử dụng Điện Toán Hiệu Năng Cao, đây là một ECU có khả năng để đáp ứng việc chạy các ứng dụng đòi hỏi hiệu năng tính toán cao.
Bằng cách sử dụng các dịch vụ của AWS như Amazon Elastic Compute Cloud (Amazon EC2); dịch vụ vừa mang tính bảo mật lại còn có khả năng tùy biến công suất tính toán phù hợp với hầu như mọi tác vụ, Continental đã đưa ra một phương pháp phát triển HPC theo kiểu mô-đun và có khả năng điều chỉnh quy mô một cách linh hoạt. Phương pháp của Continental tận dụng các phân vùng (partitions), là những phần riêng biệt và độc lập của một ECU, để ảo hóa riêng biệt với nhiều loại hệ thống ô tô khác nhau, như là hệ thống giải trí và điều khiển - infotainment (bản đồ GPS, trạng thái xe, camera lùi và nghe nhạc, video, điện thoại, kết nối mạng,...) hoặc là cụm đồng hồ hiển thị ( bảng đồng hồ nằm sau vô-lăng đối với oto truyền thống hoặc màn hình LCD / kỹ thuật số toàn phần với xe hiện đại). Các phân vùng này trao quyền cho các nhóm phát triển phần mềm ô tô khả năng tích hợp nhiều bộ phần mềm khác nhau trong việc phát triển phần mềm, đồng thời vẫn duy trì được tính linh hoạt và khả năng mở rộng của chúng.
Bài viết này phân tích công trình tiên phong của Continental trong lĩnh vực ảo hóa ECU, nhấn mạnh khả năng kết hợp các phân vùng theo bất kỳ cách nào mà kỹ sư muốn, không bị ràng buộc bởi những nguyên tắc cũ. Điều này giúp tạo điều kiện cho việc thử nghiệm các cấu hình ECU trong tương lai và khám phá những đặc tính cụ thể của từng cấu hình riêng biệt.

Sự chuyển đổi sang lĩnh vực ảo hóa ECU

Hành trình của Continental hướng tới việc ảo hóa HPC bắt đầu từ nhu cầu rút ngắn thời gian trong phát triển các HPC mới. Bằng cách sử dụng công nghệ ảo hóa ECU và triển khai nó trên hạ tầng đám mây của AWS, Continental đã tăng tốc độ phát triển của những HPC mới theo cấp số nhân. Phương pháp của Continental không chỉ tăng tốc quy trình phát triển mà còn giúp nâng cao chất lượng và độ tin cậy của sản phẩm cuối cùng - sản phẩm đã trải qua các khâu kiểm tra chất lượng và phát triển, bắt đầu lưu hành trên thị trường. Mỗi một phân vùng có thể chạy trên các máy ảo AWS Graviton sử dụng kiến trúc ARM, vốn mang lại hiệu suất đi đôi với giá thành tối ưu cho các khối lượng công việc trên đám mây Amazon EC2.

Việc sử dụng Graviton giúp tạo ra môi trường phát triển giống hệt phần cứng ECU hiện đại trên xe, cho phép các kỹ sư phần mềm ô tô chạy đúng cùng một chương trình trên cả mô phỏng đám mây lẫn phần cứng thật ở bên trong chiếc xe. Sự đồng nhất giữa môi trường được ảo hóa so với phần cứng vật lí ngoài thực tế này giúp đơn giản hóa và tăng hiệu quả cho quy trình phát triển và kiểm thử phần mềm ô tô, việc mô phỏng trên đám mây tái hiện chính xác cách mà xe hoạt động ngoài đời thật.

Có nhiều yếu tố giúp việc sử dụng ECU ảo thay thế ECU vật lí trở nên khả thi:

Chạy code gần như bắt kịp với thời gian thực tế: Với giải pháp của Continental, tất cả các phân vùng đều hoạt động gần với thời gian thực tế. Điều này đạt được nhờ sự đồng nhất giữa các CPU trên nhiều tài nguyên tính toán hiện nay và AWS đám mây. Nhiều ECU hiện đại sử dụng CPU kiến trúc ARM, vốn cũng có sẵn trên các máy ảo Amazon EC2, cho phép sử dụng cùng chương trình đã biên dịch mà không phải thay đổi gì ở trên cả hai môi trường thực và ảo.

Bộ gia tốc phần cứng cho ô tô:Các hệ thống máy tính hiệu năng cao trên xe tự lái cần GPU để đạt hiệu suất tốt hơn. Sự đồng nhất môi trường giữa ECU mục tiêu và dịch vụ của AWS cũng đạt được nhờ sử dụng GPU tương tự. AWS cung cấp máy ảo EC2 hỗ trợ GPU của Nvidia và Qualcomm.

Giao tiếp giữa các phân vùng (IPC):  Việc ảo hóa giao tiếp cũng quan trọng không kém việc dùng cùng loại CPU trên cả hai môi trường. IPC được ảo hóa sẽ phản chiếu đúng môi trường phần cứng thật, và cho phép chạy chương trình với tốc độ gần bắt kịp thời gian thực và giữ nguyên chương trình đã biên dịch trên mọi phân vùng.

Tích hợp thiết bị ngoại vi: Một ECU ảo cần phải hoạt động và phản ứng, vận hành y hệt những gì một ECU phiên bản vật lí có thể. Các thiết bị ngoại vi như mạng CAN bus, giao thức SOME/IP, Bluetooth, camera và giao diện âm thanh hoặc hình ảnh đều được hỗ trợ đầy đủ trong môi trường ảo, giúp việc kiểm thử và xác nhận tổng thể dễ dàng hơn. Các thiết bị ngoại vi như hệ thống mạng CAN bus, giao thức SOME/IP, Bluetooth, camera, và giao diện âm thanh hoặc hình ảnh đều được hỗ trợ đầy đủ trong môi trường ảo, giúp việc kiểm thử và xác nhận tổng thể trở nên dễ dàng hơn.

Hướng tới phát triển ECU lấy phần mềm làm trung tâm

Trong truyền thống phát triển, các hãng ô tô phát triển ECU theo cách tiếp cận tập trung vào phần cứng trước. Các thông số kỹ thuật phần cứng được tạo ra đầu tiên. Sau đó, các mẫu phần cứng mục tiêu mới được chuyển cho nhóm phát triển phần mềm. Một nhược điểm của cách tiếp cận truyền thống là nhóm phát triển phần mềm phải điều chỉnh và xoay xở với những giới hạn tài nguyên của phần cứng mục tiêu.
Việc ảo hóa ECU kết hợp với khái niệm phân vùng ECU giúp các kỹ sư phần mềm ô tô chủ động tạo ra các cấu hình ECU. Họ có thể đáp ứng xu hướng tích hợp nhiều phân vùng trên duy nhất một máy tính hiệu năng cao (HPC), ví dụ như phân vùng ADAS(hệ thống hỗ trợ lái xe tiên tiến) và phân vùng thông tin & giải trí. Trong môi trường đám mây, nhóm phát triển có thể tự do tạo các cấu hình tùy ý và điều chỉnh tài nguyên bộ nhớ, CPU để đáp ứng những yêu cầu cụ thể của ngành ô tô. Điều này cho phép họ kết hợp các phân vùng hiện có một cách sáng tạo. Nhờ công nghệ này, nhóm phát triển có thể xây dựng phần mềm và kiểm thử cách nó hoạt động trên nhiều cấu hình ECU ảo khác nhau.
Continental đã biến ý tưởng về việc phát triển ECU ưu tiên phần mềm thành hiện thực, một phần nhờ tìm ra cách kết hợp linh hoạt các phân vùng thành những máy tính hiệu năng cao ảo (HPC). Hình minh họa bên dưới cho thấy tất cả các loại phân vùng hiện có: Android Automotive OS, Linux, AUTOSAR Classic Platform, QNX và AUTOSAR Adaptive Platform.
Hãy xem ví dụ về ADAS‑Cockpit HPC (AC HPC), chạy hai phân vùng trên cùng một thiết bị phần cứng. Bắt đầu từ danh mục ứng dụng và phần mềm trung gian, Continental xác định các năng lực cần thiết và phân bổ chúng vào các phân vùng tương ứng. Một AC HPC có thể bao gồm nhiều phân vùng AUTOSAR Classic, một phân vùng ADAS (ví dụ chạy trên QNX), một phân vùng AUTOSAR Adaptive và một phân vùng Android Automotive OS. Các phân vùng độc lập này cho phép Continental tạo ra các phiên bản ảo của phần cứng mục tiêu. Chúng hỗ trợ đa dạng môi trường vận hành ô tô và các trường hợp sử dụng trong tương lai. Mỗi phân vùng được xây dựng theo yêu cầu hệ thống cụ thể, giúp đơn giản hóa việc phát triển và kiểm thử các chức năng ECU khác nhau. Thêm vào đó, năm phân vùng này có thể kết hợp với nhau theo cùng các giao thức đã dùng trên xe thật. Điều này cho phép hỗ trợ thế hệ HPC mới tích hợp các tính năng từ nhiều lĩnh vực khác nhau trên một nền tảng phần cứng duy nhất.
Các phân vùng ảo được tích hợp lại thành một hệ thống con ECU ảo hoặc một máy tính hiệu năng cao ảo (vHPC) đầy đủ tất cả các thiết bị ngoại vi ảo cần thiết. Sau đó, vHPC có thể được kiểm thử bằng cùng bộ công cụ kiểm thử đã dùng cho phần cứng mục tiêu và ECU ảo hóa. Bằng cách đánh giá nhu cầu tài nguyên phần cứng, Continental có thể đề xuất và chọn hệ thống trên chip (SoC, ví dụ NXP hoặc Qualcomm) phù hợp nhất cho phần cứng và khối lượng công việc trong dự án HPC mới, từ đó tối ưu hiệu năng, hiệu quả hoạt động và chức năng cho khách hàng cuối (người tiêu dùng).

Hình 1 dưới đây minh họa một số loại phân vùng khác nhau, mỗi loại được thiết kế để chạy các ứng dụng ô tô trong môi trường đám mây. Hãy hình dung chúng như các bộ phần mềm khác nhau, mỗi bộ tượng trưng cho một hệ điều hành và khung phần mềm riêng. Phía dưới mỗi bộ đó là các tầng chung dành cho việc giao tiếp và kết nối phần cứng.  
Hình 1. Hiện nay có các phân vùng Android, Linux, Autosar, QNX và Adaptive Autosar có sẵn
Các tùy chọn phân vùng khác nhau, từ trái sang phải trong Hình 1 ở trên, như sau:

Android Automotive OS: Dựa trên Android như hệ điều hành trên nhiều điện thoại và máy tính bảng, lý tưởng cho giao diện thân thiện với người dùng khi sử dụng các tính năng trên ô tô như nghe nhạc, dẫn đường và gọi rảnh tay. Phân vùng này chạy trên nền Linux và sử dụng trình quản lý gói để cài đặt, cập nhật ứng dụng.

Linux: Là hệ điều hành mã nguồn mở linh hoạt, được dùng rộng rãi. Phù hợp cho các tác vụ ô tô chung không yêu cầu hiệu năng gần thời gian thực nghiêm ngặt, đồng thời cung cấp trình quản lý gói để dễ dàng thêm hoặc cập nhật phần mềm.

AUTOSAR Classic Platform: Là chuẩn phần mềm ô tô truyền thống, tập trung vào vận hành đáng tin cậy và gần thời gian thực. Phân vùng này hoàn hảo để chạy các chức năng cốt lõi của xe cần phản hồi nhanh và ổn định, đồng thời sử dụng mô phỏng mô hình (ví dụ Synopsys Silver) để kiểm thử các đơn vị runnable (đơn vị phần mềm cơ bản).

QNX: Nổi tiếng với kiến trúc nhân vi mô an toàn, ổn định và gần thời gian thực. Thường được dùng cho các hệ thống an toàn quan trọng và hệ thống giải trí thông tin, nơi độ tin cậy là yếu tố then chốt, và cũng bao gồm trình quản lý gói để quản lý phần mềm một cách đơn giản.

AUTOSAR Adaptive Platform: Là chuẩn mới dành cho công nghệ xe kết nối hiện đại, hỗ trợ các tính năng tiên tiến như V2X (giao tiếp xe–xe và xe–hạ tầng), đồng thời tích hợp trình quản lý gói để đơn giản hóa việc triển khai ứng dụng và dịch vụ.
Dưới tất cả các bộ phần mềm (stacks) là các lớp sau:
●	Giao tiếp: Xử lý chia sẻ dữ liệu và nhắn tin giữa các thành phần khác nhau của hệ thống.

●	Ngoại vi: Quản lý kết nối phần cứng như cảm biến, camera hoặc các thiết bị khác trên ô tô.

Kết luận

 Với hạ tầng đám mây AWS, Continental mang đến giải pháp mô‑đun và có khả năng mở rộng, giúp đẩy nhanh quá trình phát triển phần mềm cho các máy tính hiệu năng cao trên ô tô (HPC). Thông qua việc tạo các phân vùng ảo và tích hợp nhiều lĩnh vực phần mềm ô‑tô trong cùng một nền tảng tính toán hiệu năng cao, cách tiếp cận ảo hóa HPC của Continental đánh dấu một bước tiến trong phát triển phần mềm ô‑tô. Cấu hình này hỗ trợ các nhóm phát triển phần mềm trong việc kiểm thử và xác nhận ứng dụng ô‑tô, phù hợp với xu hướng hợp nhất đa dạng chức năng xe vào môi trường tính toán tập trung.
Công trình ảo hóa ECU của Continental ủng hộ tương lai của các hệ thống ô‑tô kết nối và thông minh, mang lại những giải pháp ngày càng thích nghi tốt hơn, tin cậy hơn và hướng đến người dùng. Hãy cùng chúng tôi định hình thế hệ xe được xác định bằng phần mềm tiếp theo - liên hệ với các chuyên gia của chúng tôi ngay hôm nay để khám phá cách AWS có thể giúp bạn tăng tốc phát triển.

Amir Mahdi Namazi
Amir có bằng Cử nhân Kỹ thuật (Bachelor of Engineering) ngành Khoa học Máy tính và Kỹ thuật Công nghiệp tại TH-Köln, và ngành Cơ khí tại OTH-Regensburg. Anh gia nhập Continental năm 2017 với vai trò Nhà phân tích dữ liệu, làm việc với cảm biến NOx trong bộ phận Powertrain (hệ thống truyền động). Năm 2019, anh trở thành Kỹ sư phần mềm, tập trung vào truyền thông trong xe và các Bộ điều khiển động cơ (ECU). Từ năm 2020, Amir đảm nhiệm vị trí Kiến trúc sư phần mềm cho HPC, và từ năm 2023 đến nay, anh dẫn dắt một nhóm DevOps chuyên về “AI, Đám mây và Ảo hóa” cho các hệ thống HPC trên ô tô.
Daniel Schleicher
Daniel Schleicher là Kiến trúc sư Giải pháp Cấp cao (Senior Solutions Architect) tại AWS, phụ trách hỗ trợ Continental với trọng tâm là xe ô tô được điều khiển bằng phần mềm (software-defined cars). Trong lĩnh vực này, anh quan tâm đến việc áp dụng các nguyên tắc điện toán đám mây cho ứng dụng ô tô và cải tiến quy trình phát triển phần mềm ô tô thông qua phần cứng ảo hóa. Ở các vai trò trước đây, Daniel đã dẫn dắt quá trình chuyển một nền tảng tích hợp doanh nghiệp lên AWS tại Volkswagen và, với tư cách quản lý sản phẩm, đóng góp vào việc xây dựng dịch vụ trung tâm cho Mercedes Intelligent Cloud.
Martin Kraus
Martin Kraus phụ trách mảng DevOps và công nghệ trong mảng Kinh doanh HPC Ô tô của Continental. Sau nhiều năm làm trưởng nhóm phần mềm trong các dự án khách hàng ngành ô tô, hiện tại anh chịu trách nhiệm về DevOps với trọng tâm xây dựng chuỗi công cụ CI/CD/CT cho các dự án HPC. Ngoài ra, anh còn áp dụng các công nghệ mới để quản lý độ phức tạp thông qua triển khai các giải pháp ảo hóa, đồng thời nâng cao hiệu quả bằng cách tích hợp và triển khai các giải pháp AI trong các nhóm phát triển.

Samer Odeh
Samer Odeh là Quản lý Tài khoản Kỹ thuật (Technical Account Manager) tại AWS, chuyên hỗ trợ khách hàng trong ngành công nghiệp ô tô. Với hơn 15 năm kinh nghiệm trong lĩnh vực CNTT và công nghệ đám mây, Samer tập trung vào việc giúp các doanh nghiệp ô tô tối ưu hóa hạ tầng AWS và tận dụng dịch vụ đám mây để thúc đẩy đổi mới trong xe được điều khiển bằng phần mềm (SDV). Anh có chuyên môn sâu về kiến trúc đám mây, thực hành DevOps và hoạch định chiến lược CNTT cho các giải pháp xe kết nối. Samer đam mê hỗ trợ các tổ chức ô tô đạt được hiệu quả vận hành tối ưu và tăng tốc quá trình chuyển đổi số thông qua các dịch vụ AWS, đặc biệt là trong lĩnh vực phát triển và triển khai SDV.


---

## 📖 Glossary - Thuật ngữ

| English | Tiếng Việt | Định nghĩa |
|---------|------------|------------|
| Smart Cockpit High-Performance Computer (HPC) | Buồng Lái Thông Minh sử dụng Điện Toán Hiệu Năng Cao | Smart Cockpit là buồng lái thông minh, Còn HPC - máy tính điện toán hiệu năng cao thì nó như kiểu máy tính xịn dùng để tính toán. Cái thứ này sẽ được tích hợp trong xe để xử lí tốt hơn |
| Infotainment | Thông tin và giải trí | Từ này là từ kết hợp của Information(thông tin) và Entertaiment(giải trí). Nó liên quan đến cái bảng điều khiển nơi có thể hiện thông tin xe lẫn việc coi phim nghe nhạc này kia thì phải. |

## 🔗 Tài liệu tham khảo

### Tài liệu gốc

### Tài liệu tiếng Việt

### Tools và Services

- Third-party Tools: Chat GPT, Google dịch, Google

---

## 💬 Ghi chú của người dịch

Một số từ hơi lạ, cũng không quá khó nhưng để dịch tốt thì cảm thấy khó khăn.

### Challenges trong quá trình dịch
- **Technical Terms**: Thuật ngữ khó dịch là: Smart Cockpit High-Performance Computer (HPC). Cách giải quyết là: đọc khái niệm, ngồi nghĩ ra cách dịch.
- **Cultural Context**: Buồng Lái Thông Minh sử dụng Máy tính Hiệu Năng Cao.
- **Complex Concepts**: Không phức tạp ở cách giải thích, mà khó để dịch sát nghĩa mà không dài dòng.
### Insights gained
- **Technical Learning**: Kĩ năng dịch thuật
- **Language Skills**: Kỹ năng lựa chọn từ ngữ
- **Industry Knowledge**: Dịch tạm hiểu thì còn dễ, dịch để hiểu thì khó hơn. Nhưng dịch hay, sát ngữ nghĩa thì cực kì khó khăn.

---

## 🤝 Đóng góp và Feedback

Bài dịch này được thực hiện trong khuôn khổ **FCJ Internship Program**. 

**📧 Liên hệ**: teamo.my.little.lion@gmail.com  
**💬 Feedback**: Mọi góp ý để cải thiện chất lượng dịch thuật xin gửi về email trên  
**🔄 Updates**: Bài dịch sẽ được cập nhật dựa trên feedback từ cộng đồng

---

*© 2025 - Bản dịch thuộc về Nguyễn Huy Hùng. Vui lòng credit khi sử dụng.*