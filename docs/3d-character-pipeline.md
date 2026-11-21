# Quy trình nâng cấp nhân vật 3D — HMOOB TOJ SIAB

## Mục tiêu

Tạo nhân vật nữ người Mông phong cách realistic bằng Blender miễn phí, xuất `player_hmong_girl.glb`, sau đó tích hợp vào game mà không thay đổi gameplay.

## Trạng thái hiện tại đã kiểm tra

- Game đang nằm trong file `HMOOB_TOJ_SIAB_ALL_CHARACTERS_RIGGED_3D.html`.
- Game dùng Three.js 0.170.0.
- Nhân vật chính được tạo trong module `game/models` bằng `createPlayerCharacter(materials, kind)`, gọi `buildHmongCharacter(...)`.
- Nhân vật hiện tại có `root`, `bodyGroup`, skeleton và các chuyển động được game điều khiển.
- Chưa có GLTFLoader hoặc mô hình GLB bên ngoài trong bản hiện tại.

**Vì vậy:** không xóa nhân vật procedural và không sửa điều khiển. Bản GLB mới sẽ được thêm như lớp hiển thị thay thế có kiểm soát; nhân vật cũ luôn là phương án dự phòng. Chỉ bật thay thế sau khi kiểm tra được kích thước, hướng mặt, điểm đặt chân và animation.

## 1. Cài Blender miễn phí trên Windows

Khuyến nghị Blender 5.2 LTS cho dự án ổn định. Tải từ trang chính thức: https://www.blender.org/download/

1. Mở trang tải Blender.
2. Chọn Windows Installer ở mục Blender 5.2 LTS.
3. Tải file cài đặt `.msi`, mở file và chọn Next → Install.
4. Mở Blender từ Start Menu.
5. Ở màn hình đầu tiên, chọn giao diện mặc định; không cần mua tài khoản hay kích hoạt bản quyền.

Không tải bộ cài từ trang không rõ nguồn gốc.

## 2. Chuẩn bị dự án nhân vật

1. Mở Blender → File → New → General.
2. Xóa khối lập phương mặc định bằng cách chọn nó và nhấn X → Enter.
3. Lưu dự án ngay: File → Save As.
4. Đặt tên `player_hmong_girl.blend`.
5. Lưu bản làm việc trong thư mục riêng trên máy; không lưu đè file game HTML.

## 3. Tiêu chuẩn thiết kế nhân vật

Thiết kế một cô gái người Mông trưởng thành trẻ tuổi, vóc dáng tự nhiên, tỷ lệ người thực tế; trang phục truyền thống cần nghiên cứu theo vùng/văn hóa cụ thể, tránh tự ý trộn hoa văn của nhiều nhóm.

Các phần cần có:
- Đầu, mặt, mắt, mũi, miệng, tai và tóc.
- Thân, hai tay, bàn tay, hai chân và bàn chân.
- Trang phục nhiều lớp: áo, váy/quần theo thiết kế đã chọn, thắt lưng, khăn/đồ đội đầu nếu phù hợp.
- Họa tiết thêu vải được làm bằng texture hoặc normal map; không tạo quá nhiều vật thể nhỏ gây nặng game.
- Màu da và vật liệu vải tự nhiên, không bóng nhựa.

Giữ silhouette rõ ràng để nhân vật vẫn dễ nhìn khi camera ở xa.

## 4. Rig (xương) và chuyển động

Tạo một Armature cho nhân vật. Tên xương nên rõ ràng, ví dụ:
- `root`, `hips`, `spine`, `chest`, `neck`, `head`
- `upper_arm.L`, `forearm.L`, `hand.L` và các xương bên phải
- `thigh.L`, `shin.L`, `foot.L` và các xương bên phải

Gắn mesh vào Armature bằng Automatic Weights, sau đó kiểm tra ở Pose Mode. Sửa Weight Paint ở vai, khuỷu tay, hông và đầu gối để tránh méo.

Tạo các Action tối thiểu:
- `Idle`: đứng thở nhẹ.
- `Walk`: đi bộ.
- `Run`: chạy.
- `Jump`: nhảy.
- `Wave`: vẫy tay (không bắt buộc).

Để game điều khiển được, mỗi animation phải là Action/NLA track có tên ổn định. Game hiện tại chưa nối các clip GLB này vào bộ điều khiển, nên chưa được coi là tích hợp xong chỉ vì file GLB có animation.

## 5. Xuất GLB

1. Chọn mesh, Armature và các phụ kiện thuộc nhân vật.
2. File → Export → glTF 2.0.
3. Chọn định dạng `glTF Binary (.glb)`.
4. Bật Selected Objects.
5. Bật Mesh, Materials, Skinning và Animations.
6. Animation Mode chọn Actions (hoặc NLA Tracks nếu đã tổ chức clip bằng NLA).
7. Đảm bảo các Action được gắn/đưa vào NLA để exporter nhận diện.
8. Đặt tên file chính xác: `player_hmong_girl.glb`.
9. Xuất vào `assets/characters/`.

Tài liệu Blender giải thích việc xuất skinning và animation: https://docs.blender.org/manual/en/latest/addons/scene_gltf2.html

## 6. Tự kiểm tra trước khi đưa lên GitHub

- Mở lại file GLB trong Blender hoặc một trình xem glTF.
- Kiểm tra nhân vật đứng thẳng, chân chạm mặt đất, mặt hướng về trục +Z.
- Thử từng clip Idle/Walk/Run/Jump.
- Kiểm tra không thiếu texture.
- Giữ file GLB tối ưu, mục tiêu ban đầu dưới 15 MB.
- Không đưa file .blend backup lớn hoặc texture nguồn không dùng vào bản game.

## 7. Đưa GLB lên GitHub miễn phí

1. Mở repository: https://github.com/phinhca48-netizen/HMOOB-TOJ-SIAB
2. Mở thư mục `assets/characters`.
3. Chọn Add file → Upload files.
4. Kéo `player_hmong_girl.glb` vào.
5. Commit message: `Add realistic Hmong girl character model`.
6. Chọn Commit changes.

GitHub giới hạn kích thước file thường tải lên qua trình duyệt; nếu GLB vượt 100 MB, cần giảm dung lượng hoặc dùng Git LFS (có hạn mức miễn phí và giới hạn riêng). Không cần Git LFS nếu GLB đã tối ưu dưới 15 MB.

## 8. Quy tắc tích hợp vào game

Không thay file game bằng một bản viết lại. Khi GLB đã có trong repository, bước lập trình tiếp theo sẽ:

1. Thêm tải GLB bất đồng bộ bằng GLTFLoader tương thích Three.js 0.170.0.
2. Giữ nhân vật procedural làm fallback nếu mạng lỗi hoặc GLB lỗi.
3. Giữ nguyên `playerAvatarRoot`, vị trí, góc quay, camera, collider, input, save/load và logic nhiệm vụ.
4. Gắn mô hình GLB vào đúng transform của player; chuẩn hóa scale, hướng +Z và chân tại mặt đất.
5. Nối AnimationMixer với vòng lặp cập nhật của game; ánh xạ Idle/Walk/Run/Jump.
6. Kiểm tra đổi nhân vật girl/boy, tải save, di chuyển, va chạm, nhảy và chuyển cảnh.
7. Chỉ sau khi tất cả kiểm tra đạt mới tắt mesh procedural cho nhân vật girl.

**Lưu ý:** chưa có file GLB thực tế trong repository, vì vậy chưa thể kiểm tra kích thước, rig, clip hoặc bật mô hình mới trong game. Không đánh dấu công việc tích hợp hoàn tất trước các kiểm tra trên.
