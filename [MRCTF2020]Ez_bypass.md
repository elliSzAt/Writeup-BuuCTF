```
I put something in F12 for you
include 'flag.php';
$flag='MRCTF{xxxxxxxxxxxxxxxxxxxxxxxxx}';
if(isset($_GET['gg'])&&isset($_GET['id'])) {
    $id=$_GET['id'];
    $gg=$_GET['gg'];
    if (md5($id) === md5($gg) && $id !== $gg) {
        echo 'You got the first step';
        if(isset($_POST['passwd'])) {
            $passwd=$_POST['passwd'];
            if (!is_numeric($passwd))
            {
                 if($passwd==1234567)
                 {
                     echo 'Good Job!';
                     highlight_file('flag.php');
                     die('By Retr_0');
                 }
                 else
                 {
                     echo "can you think twice??";
                 }
            }
            else{
                echo 'You can not get it !';
            }

        }
        else{
            die('only one way to get the flag');
        }
}
    else {
        echo "You are not a real hacker!";
    }
}
else{
    die('Please input first');
}
}Please input first
```

Đây là một đoạn mã PHP. Nó bao gồm một số biến và điều kiện để kiểm tra các giá trị được nhập vào từ URL và biểu mẫu POST.

Cụ thể, khi bạn truy cập vào trang web này, bạn cần nhập thông tin vào URL như sau:

``?gg=value1&id=value2``

nếu giá trị của md5($id) giống với giá trị của md5($gg) và id khác với gg, chương trình sẽ in ra thông báo "You got the first step".

Nếu bạn nhập thông tin vào biểu mẫu POST với ô nhập passwd, chương trình sẽ kiểm tra xem giá trị bạn nhập vào có phải là một số hay không. Nếu không phải, chương trình sẽ kiểm tra xem giá trị của passwd có giống với 1234567 hay không. Nếu giống, chương trình sẽ in ra thông báo "Good Job!" và hiển thị nội dung của tệp flag.php trên trang web.

Nếu không phải là 1234567, chương trình sẽ in ra thông báo "can you think twice??".

Nếu giá trị của passwd là một số, chương trình sẽ in ra thông báo "You can not get it!".

Nếu giá trị của md5($id) không giống với giá trị của md5($gg) hoặc id bằng gg, chương trình sẽ in ra thông báo "You are not a real hacker!".

Nếu bạn không nhập đủ thông tin cần thiết vào URL và biểu mẫu POST, chương trình sẽ in ra thông báo "only one way to get the flag".

Chỉ khi bạn nhập đúng thông tin cần thiết và đạt được điều kiện để hiển thị nội dung tệp flag.php

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/18f3d5ce-5f7e-4e11-9582-35d05ed277b9)

Ở phần tham số mình sử dụng mảng để bypass, do md5() không thể xử lý mảng.

Nhập tham số "gg" có giá trị là "QNKCDZO" trong URL, thì điều kiện md5($id) === md5($gg) sẽ trả về giá trị true trong trường hợp này. Điều này là do "QNKCDZO" được mã hóa bằng MD5 sẽ trả về giá trị là "0e830400451993494058024219903391". Vì "0e830400451993494058024219903391" bắt đầu bằng chữ số 0 và theo sau là một chuỗi các chữ số khác, nên PHP sẽ coi giá trị này là một số thực và giá trị của nó sẽ là 0.

Số 240610708 được mã hóa bằng cách sử dụng hàm băm MD5 sẽ trả về giá trị là "0e462097431906509019562988736854". Điều đặc biệt là giá trị này bắt đầu bằng chữ số 0 và theo sau là một chuỗi các chữ số khác.

Trong PHP, nếu một chuỗi bắt đầu bằng số 0 và theo sau là một chuỗi các chữ số khác, thì PHP sẽ coi chuỗi đó là số thực (floating-point number) và giá trị của nó sẽ bằng 0. 

Còn phần ``passwd`` PHP so sánh loại yếu php== Khi so sánh các loại dữ liệu khác nhau, trước tiên nó sẽ chuyển đổi dữ liệu ở cả hai bên == thành cùng loại, so sánh dữ liệu ký tự với dữ liệu số và chuyển đổi dữ liệu ký tự thành dữ liệu dữ liệu.

 Ví dụ: 1234567a sẽ được chuyển đổi thành 1234567 để so sánh và nó cũng sẽ bỏ qua chức năng is_numeric() post và chuyển vào passwd=1234567a
