![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/86dccf8f-cbba-4563-8f58-68be1f781082)

Vào challenge thì nó cho chúng ta 2 lựa chọn là gâu gâu và meo meo, thử bấm vào 1 cái xem sao.

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/00a20f69-9a38-41c8-9847-27453d08f8b5)

Khi click vào thì nó sẽ chuyển hướng mình vào 1 file gọi là meo meo, nhìn vào URL thì đây là dấu hiệu rõ ràng của lỗi LFI.

Do đó mình sử dụng payload: ``category=php://filter/read=convert.base64-encode/resource=index`` để xem phần source code của nó, vì là phần trước nó đã có ``index.php`` rồi nên phần mình muốn đọc ở sau chỉ còn có ``index`` thui.

![b](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/09beb752-c188-4bda-b5f8-66ed94baa144)

Tiếp theo nhìn vào phần source code ta thấy có 1 file gì đó trước 2 cái meo meo và gâu gâu này, nên mình thử tiến đến nó để tìm flag xem sao.

``category=meowers/../flag``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/e14f3f02-7551-4d77-9758-4292a3c74ee5)

Ở đây nó thách thức mình đọc flag nè, nên chắc là flag sẽ nằm trong file flag, tiến hành tạo payload thôi.

``category=php://filter/read=convert.base64-encode/resource=meowers/../flag``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/66167cd9-f88d-4b80-9401-dddcf7ad0494)

Ở đây nó sẽ xuất hiện 1 chuỗi kí tự base64, decode nó ra xem.

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/c7141060-e61b-405f-bcde-911ac8456518)
