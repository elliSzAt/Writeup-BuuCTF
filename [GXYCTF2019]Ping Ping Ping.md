Truy cập vào web ta thấy challenge này đã gợi ý cho chúng ta rằng ?/ip=, do đó ta thử nhập vào đó 1 địa chỉ IP như 192.168.1.1.  

<img width="694" alt="image" src="https://user-images.githubusercontent.com/125866921/224555209-96491fcd-3bbd-4765-b435-3cb65ec3ea94.png">

Ta thấy rằng trong địa chỉ IP này có chứa gì đó, thử list nó ra bằng lệnh |ls.  

<img width="270" alt="image" src="https://user-images.githubusercontent.com/125866921/224555242-3c0c3413-537f-4eac-a8f5-1cd1a3feae31.png">

Thử truy cập vào file flag bằng lệnh cat.

<img width="164" alt="image" src="https://user-images.githubusercontent.com/125866921/224555335-6a1fa387-d49c-49dc-902c-9d151732fce5.png">

Ta thấy trang web này đã cấm những thứ như khoảng trống, sau đó tôi đã thử với các kí tự và nó vẫn vậy.  

Ta có thể sử dụng $IFS$9 để thay thế cho những khoảng trống.  

Ta thử với lệnh sau: /?ip=;cat$IFS$9`ls`, ta nhận thấy giao diện web đã thay đổi, ta vào xem source code và nhận cờ.  

flag{----------}
