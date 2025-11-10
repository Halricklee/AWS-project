GAME DESIGN DOCUMENT – Concept & Core System

1. **Nhân vật chính**  
* Một người ngoài hành tinh trên đĩa bay  
* Gắn avatar của người chơi lên đĩa bay (mặc định hoặc chụp hình đã qua filter)  
* Kích thước: Avt có thể to hơn đĩa bay một chút để thấy được avt 


2. **Avatar**  
* có 2 loại: mặc định (2 cái) và chụp mặt áp filter  
* Sử dụng AI (file python) viết nhận dạng khuôn mặt và áp filter alien \=\> Unity gọi file đó \=\> áp vào


3. **Vật cản:**

   ### ***3.1. Loại không thể Dash (chạm vào \= dừng, mất máu)***

* Xe cẩu

* Xe ben

* Container

* Rào công trình

  ### ***3.2. Loại Dash được (người chơi có thể Dash xuyên qua)***

* Ổ gà

* Cây cỏ

* Nắp cống


  **4\. Item có effect**

  Xuất hiện trong màn chơi giống như obstacle nhưng có hiệu ứng.

  ###  Mystery Box (random buff/debuff)

* Effect tiêu cực (Debuff):

  * Nếu không spam Z trong 3s → nổ, \-1 máu.

  * Đảo ngược trái-phải trong 2s.

  * Màn hình tối/mờ 2–3s.

  * Khóa Dash trong X giây.

* Effect tích cực (Buff):

  * Bánh mì → “Buff bẩn”: vượt mọi chướng ngại vật trong 5s.

  * Cà phê → “Heal bẩn”: hồi 1 mạng.

  * Hút item (magnet).

  * Tăng tốc 5s (ko hỗ trợ vượt được vật cản)


    **5\. Tiền và shop**

    

* Tiền sống qua ngày: Icon 10k VND. (rải trong lúc chơi giống item khác)

* Cách dùng:

  * Nhặt trong game.

  * Dùng để mua item trong shop hoặc mua mạng khi die (giới hạn số lần).

* Shop bán gì?

  * Bánh mì (Buff bẩn) – 100k.

  * Cafe (Heal bẩn) – 50k.

  * Cân nhắc thêm: hút item, tăng tốc

    

  **6\. Task Challenge** 

  Có tổng 15 level, mỗi map có 5 level, mỗi level cần phải hoàn thành bao nhiêu đó task.


  6.1 Map 1: (mỗi level 1 task)

- Lv 0 \-\> 1: ăn và sử dụng item bánh mì  
- 1-\>2: ăn và sử dụng item cafe  
- 2-\>3: đạt được ít nhất x score (sau này chỉnh)  
- 3-\> 4:Dash được 3 vật cản  
- 4-\> 5:Nhặt và mở được hộp mysery box  
- 5-\> 6: đánh thắng boss  
  6.2 Map 2: (mỗi level 2 task)  
- 6-\>7: thay đổi avt áp filter \+ mua 1 món từ shop  
- 7-\> 8: đạt được ít nhất x score \+ nhặt và mở 2 mystery box  
- 8-\>9:  Dash xuyên qua 5 vật cản \+ nhặt và sử dụng 3 item cafe   
- 9-\>10:thu thập được 10k x 5 và ko mất máu nào trong 1 lượt  
- 10-\>11: đánh thắng boss trong x giây  
    
    
  6.3 Map 3: (mỗi level 3 task \- tùy)

  \-11-\> 12:Cấm nhặt bất kì item nào và đạt được ít nhất x score  
  \-12-\> 13:ko rẽ phải ko bao nhiêu đó giây và bị 2 effect tiu cực từ mystery box  
  \-13-\>14: ko va chạm vật cản nào trong 1 lượt và đạt ít nhất x score   
  \-14-\>15: đánh thắng boss trong x giây

    
  **7\. Điều kiện mở khóa**  
  Đánh được boss \+ đạt được level đó  
    
  **8\. Hệ thống score**  
* Cách tính:

  * Dựa theo thời gian sống sót.

  * Lụm item → \+bonus score.

  * Va chạm obstacle → \-score.

* Reset & Leaderboard:

  * Reset score mỗi map.

  * Leaderboard:

    * Local: Xếp theo score từng map.

    * Global: Xếp theo tổng score 3 map (chỉ mở khi player unlock đủ 3 map).

  **9\. Hệ thống máu**

* người chơi có 3 mạng  
* hồi máu bằng Cafe or có thể mua 1 lượt nếu die   
    
  **10\. Đánh boss**   
* Boss xuất hiện ở level 5, 10, 15\.  
* Có cơ chế bắn boss (người chơi tấn công được).  
* Tìm ref design  
    
  **11\. Tính năng Real-time:**  
  **11.1: Gạ đua với bạn bè cùng 1 map**  
* 2 nhân vật (của bạn và đối thủ) chạy **song song trên cùng map**.

* Cùng né obstacle, ăn item, và bắn nhau nếu bạn có chế độ boss/fight.

* Nếu 1 bên chết → người kia vẫn chạy tiếp.

* Khi cả 2 chết → server so sánh score → ai thắng.  
    
  **11.2:** **Real-time Leaderboard update**  
* Người chơi vừa chơi vừa thấy bảng xếp hạng **cập nhật tức thì** (giống như Subway Surfer hiển thị bạn bè vượt mình).

* Dùng: **API Gateway \+ DynamoDB Streams \+ WebSocket API**.

* Nhẹ, không cần nhiều băng thông.  
  **11.3:** **Real-time Events / Live Ops (optional)**  
* Ví dụ: "Trong 10 phút tới, ai nhặt nhiều mystery box nhất được thưởng".

* Game server hoặc Lambda bắn sự kiện qua **SNS/SQS hoặc WebSocket API** đến client.

* Tạo cảm giác “online thật” mà backend vẫn nhẹ.

EXTRA nếu có thời gian:

\-cutscene mở đầu game đoạn đĩa bay bay xuốn

\-sự kiện toàn cầu trong game do mình đề ra random (11.3)

