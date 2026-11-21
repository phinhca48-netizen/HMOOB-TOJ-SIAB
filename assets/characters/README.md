# Character assets

Thư mục chứa các mô hình nhân vật 3D của HMOOB TOJ SIAB.

## Tên file quy ước

- `player_hmong_girl.glb` — nhân vật nữ người Mông điều khiển được.
- `player_hmong_boy.glb` — nhân vật nam người Mông.
- `villagers.glb` — bộ nhân vật dân làng.
- `elder_child.glb` — người cao tuổi và trẻ em.
- `chicken.glb` — gà.
- `pig.glb` — lợn.

## Asset đầu tiên

Tạo `player_hmong_girl.glb` theo hướng dẫn tại [docs/3d-character-pipeline.md](../../docs/3d-character-pipeline.md).

Yêu cầu kỹ thuật:
- glTF Binary (.glb), đơn vị mét, đứng thẳng, mặt hướng +Z.
- Có Armature/skin weights và animation clips tên `Idle`, `Walk`, `Run`, `Jump`.
- Chân đặt tại mặt phẳng Z-up? **Không**: game Three.js dùng trục Y là chiều cao; mô hình phải xuất theo chuẩn glTF Y-up.
- Tâm/root nằm giữa hai bàn chân; không có animation root-motion bắt buộc.
- Texture gói trong GLB; ưu tiên file dưới 15 MB.
- Không đổi tên các animation sau khi đã nối vào code.

Chưa đặt mô hình giả hoặc file rỗng ở đây. Chỉ thêm GLB sau khi đã tạo và kiểm tra thật.
