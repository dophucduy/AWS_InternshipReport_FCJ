---
title: " Humane World for Animals uses AWS to scale global animal welfare programs"
weight: 3.2
pre: " <b> 3.2. </b> "

---
### **Humane World for Animals sử dụng AWS để mở rộng quy mô các chương trình phúc lợi động vật toàn cầu**

bởi Stacy Stonich and Jules Marenghi | on 24 SEP 2025 | in [Customer Solutions](https://aws.amazon.com/blogs/publicsector/category/post-types/customer-solutions/), [Nonprofit](https://aws.amazon.com/blogs/publicsector/category/public-sector/nonprofit/), [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/)  | [Permalink](https://aws.amazon.com/blogs/publicsector/humane-world-for-animals-uses-aws-to-scale-global-animal-welfare-programs/) 

Trong hơn 70 năm qua, [Humane World for Animals](https://www.humaneworld.org/en)—trước đây là Humane Society of the United States (Xã hội nhân đạo của nước Mĩ) và Humane Society International (Xã hội nhân đạo quốc tế)—đã là tổ chức tiên phong trong phong trào bảo vệ động vật, giải quyết tận gốc các nguyên nhân gây ra tội ác cho động vật nhằm thúc đẩy sự thay đổi lâu dài và tạo ra một thế giới tốt đẹp hơn cho tất cả các loài động vật trên toàn cầu. Tổ chức đã góp phần xây dựng một thế giới nhân đạo hơn cho động vật, giúp thông qua hàng ngàn đạo luật mang tính bước ngoặt, cứu hộ hàng trăm ngàn cá thể động vật, và chăm sóc, bảo vệ hàng triệu cá thể khác.

Để giải quyết thách thức toàn cầu trong việc quản lý số lượng động vật sống ngoài đường, Humane World for Animals đã phát triển Humane World Apps—một công cụ quản lý dữ liệu toàn cầu toàn diện được thiết kế nhằm cải thiện các chương trình phúc lợi cho chó và mèo thông qua quản lý hoạt động triệt sản (spay and neuter), tiêm chủng hàng loạt (mass vaccination), và tiếp cận dịch vụ chăm sóc (access to care). Với sự hỗ trợ từ [AWS Imagine Grant](https://aws.amazon.com/government-education/nonprofits/aws-imagine-grant-program/)—chương trình tài trợ công cung cấp cả tiền mặt và tín dụng [Amazon Web Services (AWS)](https://aws.amazon.com/) cho các tổ chức phi lợi nhuận đã đăng ký sử dụng công nghệ đám mây để thúc đẩy sứ mệnh—Humane World Apps đang thay đổi cách các chương trình phúc lợi động vật quy mô lớn vận hành trên toàn thế giới.

Trong giai đoạn beta tại Vadodara, Ấn Độ, Humane World Apps đã đạt tỷ lệ triệt sản chó lên đến 86% và số lượng khiếu nại liên quan đến chó giảm 60% sau khi triển khai ứng dụng. Công nghệ này hướng đến việc chấm dứt sự đau khổ của động vật đồng hành bằng cách nâng cao hiệu quả chương trình, hỗ trợ sức khỏe cộng đồng, và thúc đẩy các giải pháp đổi mới bền vững nhằm giảm xung đột giữa người và chó.

Trong bài viết này, chúng tôi sẽ trình bày cách Humane World Apps đang cách mạng hóa công tác quản lý phúc lợi động vật thông qua công nghệ đám mây và các giải pháp dựa trên dữ liệu.

### **Thu thập dữ liệu phân mảnh trong phúc lợi động vật toàn cầu**

Quy mô của thách thức trong việc quản lý số lượng động vật sống ngoài đường là rất lớn. Ước tính có từ 700 triệu đến 1 tỷ con chó trên toàn thế giới, bao gồm cả chó có chủ và không có chủ sống trong các trại cứu hộ, gia đình hoặc tự do trong môi trường đô thị và nông thôn. Theo một [nghiên cứu của MARS](https://www.mars.com/news-and-stories/press-releases-statements/pet-homelessness), có gần 362 triệu chó và mèo sống ngoài đường tại 20 quốc gia. Các cộng đồng và cơ quan chính phủ—đặc biệt ở các quốc gia có nền kinh tế đang phát triển—gặp khó khăn trong việc tìm kiếm các giải pháp hợp lý, nhân đạo và dễ tiếp cận để quản lý số lượng chó mèo, thúc đẩy phúc lợi động vật, và xây dựng sự chung sống hòa bình giữa động vật đồng hành và con người.

Chính phủ chịu trách nhiệm về sức khỏe và an toàn cộng đồng, nhưng nhiều nơi vẫn thiếu các giải pháp cụ thể và chương trình dựa trên bằng chứng vững chắc. Ngoài ra, nhiều nơi vẫn áp dụng biện pháp tiêu hủy động vật sống ngoài đường. Các giải pháp lâu dài bao gồm triệt sản nhân đạo và hiệu quả, tiêm chủng, và tiếp cận dịch vụ thú y giá cả phải chăng là chìa khóa để cải thiện phúc lợi động vật và giảm xung đột giữa người và động vật đồng hành ở những nơi có vấn đề về động vật hoang.

Lịch sử cho thấy các chương trình phúc lợi chó mèo quy mô lớn thường gặp khó khăn do quản lý và thu thập dữ liệu kém hiệu quả, phân mảnh. Hệ quả là kết quả không tối ưu trong việc kiểm soát số lượng chó mèo đi lang thang và giải quyết các vấn đề sức khỏe cộng đồng.

### **Xây dựng giải pháp toàn diện trên AWS**

Mục tiêu của Humane World Apps là cung cấp một nền tảng công nghệ cao thống nhất, tích hợp hệ thống quản lý dữ liệu cho các hoạt động như triệt sản (spay and neuter), tiêm chủng hàng loạt (mass vaccination), và vận hành phòng khám thú y. Ứng dụng bao gồm cả ứng dụng di động và giao diện web, cung cấp các chức năng nâng cao phù hợp với nhu cầu của từng chương trình.

Ứng dụng di động hướng đến việc hỗ trợ đội ngũ hiện trường thu thập dữ liệu theo thời gian thực và ghi lại vị trí bắt để đảm bảo chó được thả về đúng nơi ban đầu. Hệ thống dự kiến sẽ theo dõi toàn bộ chu kỳ chăm sóc, bao gồm chăm sóc trước và sau phẫu thuật, dữ liệu phẫu thuật, và nhận dạng bằng hình ảnh để giám sát từng cá thể động vật cũng như kết quả của chương trình. Người dùng có thể kỳ vọng ứng dụng sẽ quản lý chương trình tiêm phòng bệnh dại thông qua geo-fencing (khoanh vùng địa lý bằng công nghệ số), định vị GPS, và tính năng báo cáo tự động.

Vì Humane World for Animals là một tổ chức phi lợi nhuận, phiên bản beta ban đầu của ứng dụng được xây dựng với ngân sách hạn chế. Một số nhà phát triển là tình nguyện viên, và họ đã thiết kế và xây dựng kiến trúc ứng dụng bằng cách sử dụng các dịch vụ miễn phí hoặc chi phí thấp. Với sự hỗ trợ từ AWS Imagine Grant (chương trình tài trợ của Amazon Web Services dành cho tổ chức phi lợi nhuận), tổ chức hiện đang trong quá trình chuyển đổi ứng dụng beta sang các dịch vụ AWS nhằm thống nhất và đơn giản hóa hệ thống công nghệ.

Hiện tại, ứng dụng được thiết kế sử dụng một máy chủ [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (Amazon EC2 – dịch vụ máy chủ ảo của AWS) duy nhất để lưu trữ cả môi trường sản xuất và thử nghiệm. Ngoài ra, các máy chủ cơ sở dữ liệu cho môi trường sản xuất và thử nghiệm sử dụng [Amazon Relational Database Service](https://aws.amazon.com/rds/) (Amazon RDS – dịch vụ cơ sở dữ liệu quan hệ của AWS). Ứng dụng sử dụng [Amazon Simple Storage Service](https://aws.amazon.com/s3/) (Amazon S3 – dịch vụ lưu trữ đối tượng của AWS) để lưu trữ hình ảnh động vật. Trong quá trình chuyển đổi, tổ chức đã bắt đầu sử dụng [Amazon Simple Email Service](https://aws.amazon.com/ses/) (Amazon SES – dịch vụ gửi email của AWS), và có kế hoạch tận dụng thêm các công cụ AWS khác trong tương lai.

Để đảm bảo khả năng dự phòng, tổ chức duy trì một instance AWS tại Ohio dùng cho cold standby (dự phòng lạnh – hệ thống sao lưu không hoạt động thường xuyên nhưng có thể kích hoạt khi cần). Các môi trường sản xuất và thử nghiệm tại Northern Virginia hiện đang sử dụng Cloudflare CDN (mạng phân phối nội dung của Cloudflare), và sẽ được chuyển sang [Amazon CloudFront](https://aws.amazon.com/cloudfront/) (dịch vụ CDN của AWS) trong tương lai. LucidScale (công cụ trực quan hóa hạ tầng đám mây) được sử dụng để sơ đồ hóa toàn bộ kiến trúc AWS nhằm giúp nhân viên hiểu rõ hệ thống và hỗ trợ vận hành về sau.

### **Mở rộng tác động thông qua công nghệ đám mây**

Sự hỗ trợ từ AWS Imagine Grant đang giúp Humane World for Animals chuyển từ hệ thống công nghệ phân tán sang hệ thống thống nhất trên AWS. Việc chuyển đổi từ kiến trúc beta sang các dịch vụ AWS được thiết kế để thúc đẩy khả năng triển khai toàn cầu và tăng khả năng mở rộng khi nhóm tiến tới đưa ứng dụng vào sản xuất. Dự án sẽ tiếp tục thúc đẩy sứ mệnh của tổ chức thông qua các kết quả dựa trên hiệu quả thực tế.

Humane World Apps hiện đang trong giai đoạn đầu triển khai tại nhiều quốc gia, xây dựng trên thành công của giai đoạn beta tại Ấn Độ. Giai đoạn beta đã cung cấp phản hồi mạnh mẽ về hiệu quả của ứng dụng, chứng minh rằng công nghệ có thể thay đổi kết quả phúc lợi động vật khi được triển khai và mở rộng đúng cách.

Ứng dụng web đóng vai trò là trung tâm quản trị nơi các quản lý chương trình thiết kế và giám sát hoạt động, cung cấp phản hồi cho đội tiêm chủng, tạo báo cáo, và quản lý dữ liệu trên nhiều khu vực. Cách tiếp cận tập trung này cho phép phối hợp tốt hơn và phân bổ nguồn lực hiệu quả hơn trên các chương trình toàn cầu.

### **Lời khuyên cho việc triển khai công nghệ phi lợi nhuận**

Humane World for Animals đưa ra lời khuyên hữu ích cho các tổ chức phi lợi nhuận bắt đầu dự án công nghệ. Thứ nhất, họ khuyến nghị mạnh mẽ việc tận dụng tài nguyên từ Amazon, đặc biệt là sự hướng dẫn từ kiến trúc sư giải pháp kỹ thuật của họ. Thứ hai, họ nhấn mạnh việc giữ vững mục tiêu cuối cùng—khi gặp khó khăn, hãy nhớ đến tác động của dự án đối với cuộc sống của những chú chó ngoài đường. Cuối cùng, họ nhấn mạnh tầm quan trọng của việc triển khai các quy trình vòng đời phát triển phần mềm từ sớm. Việc thiết lập kiểm soát mã nguồn và hệ thống ưu tiên lỗi và yêu cầu trước khi bắt đầu là rất quan trọng, vì thực hiện giữa chừng đã tiêu tốn thời gian quý giá từ khoản tài trợ. Dù khó khăn là điều không thể tránh khỏi, nhóm nhấn mạnh rằng sứ mệnh khiến việc vượt qua chúng trở nên xứng đáng.

Thông qua AWS Imagine Grant, Humane World for Animals đang thay đổi cách các chương trình phúc lợi động vật vận hành trên toàn cầu—tạo ra một thế giới nhân đạo hơn cho hàng triệu động vật đồng thời

**Cách bạn có thể hỗ trợ Humane World for Animals**    
Để tìm hiểu thêm về cách bạn có thể hỗ trợ Humane World for Animals, hãy [truy cập trang web chính thức của tổ chức.](https://www.humaneworld.org/)

TAGS: [AWS Imagine Grant](https://aws.amazon.com/blogs/publicsector/tag/aws-imagine-grant/), [AWS Public Sector](https://aws.amazon.com/blogs/publicsector/tag/aws-public-sector/), [customer story](https://aws.amazon.com/blogs/publicsector/tag/customer-story/), [nonprofit](https://aws.amazon.com/blogs/publicsector/tag/nonprofit/)

**Stacy Stonich**    
Stacy là Phó Chủ tịch cấp cao phụ trách Công nghệ & Giải pháp Thông tin tại Humane World for Animals. Bà lãnh đạo các nhóm phụ trách toàn bộ hạ tầng, bảo mật, ứng dụng và dữ liệu vận hành trơn tru. Với hơn 20 năm kinh nghiệm dẫn dắt các nhóm công nghệ cấp quốc gia và toàn cầu, Stacy đam mê xây dựng tổ chức vững mạnh, thúc đẩy hiệu quả vận hành và đảm bảo khách hàng có trải nghiệm tốt nhất.

**Jules Marenghi**    
Jules là Quản lý phát triển kinh doanh tại AWS. Cô tham gia vào nhóm phụ trách chương trình Imagine Grant và hội nghị liên quan, hỗ trợ các tổ chức phi lợi nhuận trên toàn thế giới trong việc ứng dụng công nghệ đám mây.  
