Lần đầu tiên mở chủ đề, và tìm thấy một hình ảnh khi tìm kiếm index.php trong url, lúc này tôi đã kiểm tra mã nguồn và tìm thấy tệp source.php, và truy cập trực tiếp vào mã nguồn của giao diện.  

![image](https://user-images.githubusercontent.com/125866921/224553148-8b60e744-fcf9-44b5-be5f-65820503668d.png)

Rõ ràng là chúng ta cần tiến hành kiểm tra mã và phân tích mã nguồn.  

<img width="1267" alt="image" src="https://user-images.githubusercontent.com/125866921/224553358-e4d13fc1-adc4-4ff4-a1e4-96c788cd58f4.png">

Toàn bộ lỗ hổng bị khai thác là chức năng bao gồm ở cuối mã, tệp khai thác chứa lỗ hổng , tức là nó cần bao gồm tệp ffffllllaaaagggg và cần sử dụng .../ để bỏ qua.  

Tại thời điểm này , chúng ta cũng có thể kiểm tra nội dung trong hint.php, /index.php?file=hint.php đây là tệp chứa mã nguồn củasource.phpindex.php.  

Bạn có thể nhận được lời nhắc rằng cờ đang ffffllllaaaaggggở trong , nhưng chúng tôi không biết cấp thư mục cụ thể của cờ tại thời điểm này, vì vậy chúng tôi cần chuyển.  
    index.php?file=hint.php?/../../../../../../../../ffffllllaaaagggg
    
<img width="1280" alt="image" src="https://user-images.githubusercontent.com/125866921/224553474-28ba315d-80f7-41bc-aa2b-bfe515892ea2.png">

<img width="1279" alt="image" src="https://user-images.githubusercontent.com/125866921/224553851-cf87a0d4-59f9-4521-b2b1-446c721dc924.png">


flag{-----------}
