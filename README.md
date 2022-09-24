# Blog-SVATTT-2022
Hey đây là blog lần đầu chơi giải sinh viên an toàn thông tin, với những cay đắng.
## Vòng khởi động
### AscisStore1(web)
![image](https://user-images.githubusercontent.com/82523299/192097181-280a9532-54b8-49c2-81f7-4aae8d8d120a.png)
Tôi bắt đầu giải bài này trong tâm thế đây là 1 bài rất khó vì đã nghe danh tiếng của giải này từ lâu.
Tôi bắt đầu fuzzing và có nhiều hướng, tôi đã suy nghĩ đầu tiên đến sql injection nhưng sau khi test 1 vài payload và tôi đã bỏ qua lỗi này (1 sai lầm).
Sau đó hơn 2 tiếng sau ngồi fuzz tiếp và có ngó sang những mảng khác và cả bài web thứ 2 nhưng vẫn bất lực với bài này. Tôi nghĩ giải này out trình mình rồi nhưng rồi tôi đã 
thử lại sqli và lần này lại được. Nhưng sai lầm tiếp theo là tôi ko thấy nó in select ở đâu cả và tôi nghĩ đây là blind sql injection và với trình độ hiện tại
tôi không có khả năng code dạng này.
Tôi lại bất lực và 30p tiếp theo tôi đã thấy cái chỗ nó in cái select
![image](https://user-images.githubusercontent.com/82523299/192096976-09de9b60-fe69-415f-b11d-31097755d322.png)
![image](https://user-images.githubusercontent.com/82523299/192097010-8b66abc2-7d0f-415b-8ff4-432077b20d39.png)
Tới đây thì mọi thứ coi như end. 
##### payload: `-1' union select 1,group_concat(password),3,4,5,6,7 from users-- -`
##### flag: ASCIS{SQ11-I5-t0o-EA$Y}


### AscisStore2 (web)
![image](https://user-images.githubusercontent.com/82523299/192097141-cc6e36c3-9aa9-41d8-84da-70f6a8f03c8d.png)

Sau khi rút kinh nghiệm ở bài 1, giải này ko quá đó chỉ cần nghĩ đơn giản thôi và suy nghĩ đó đã đúng 
Bài này web y hệt chỉ thêm cái page profile, và tôi chắc chắn bug nó nằm ở trong đó rồi
Tôi đã thử qua vài tính năng và cái tính năng có khả năng lỗi cao nhất là cái phần upload ảnh
Sau khi upload ảnh thì sẽ có 1 đường dẫn dẫn tới tấm ảnh đó
![image](https://user-images.githubusercontent.com/82523299/192097282-10713869-3d18-40d4-a2ce-c527abd13d4f.png)

Tôi đã thử hàng loạt bug liên quan đến upload như upload shell, LFI, SSRF nhưng tất cả đều ko được có vẻ cái hàm lấy ảnh nó ko dùng mấy cái hàm như file_get_content hay include
Cuối cùng tôi đã thử cái lỗi ez nhất Path Traversal và cuối cùng được :(( (đúng là vòng khởi động, mọi thứ đều basic nhất có thể)
![image](https://user-images.githubusercontent.com/82523299/192097426-2e7cb89e-aeb5-4f75-8561-3199b3bdcdaf.png)
Nếu mọi người thắc mắc sao cái payload lại thế kia thì bài này nó replace '../' thành ''
##### ASCIS{P4Th-TrAV3rSA1-bAby}

### Sau vòng này tôi đã rút kinh nghiệm nên làm mọi thử từ đơn giản nhất, vì nghĩ là 1 giải lớn mà tôi đã ko test những payload basic nhất và điều đó đã khiến tôi trả giá
