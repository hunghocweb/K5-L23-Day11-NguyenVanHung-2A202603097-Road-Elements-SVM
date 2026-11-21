# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): hthuong        Người kiểm (học viên): nguyenvanhung
Ngày: 2026-11-21                        Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): hthuong-front.zip, hthuong-fisheye.zip, revision 1
(sha256 front 39858ec3…d645, fisheye ad667870…c7a5; đã đối chiếu khớp với manifest)
Số ảnh kiểm: 6 (A04, A06, A07, A09, B02, B06; + 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 71 (47 shape + 24 tag)

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 5 | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 7 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 7 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 7 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 7 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 14 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 2 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 16 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 8 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 10 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Cách tính "số mục kiểm": QC1-01 = 6 tag camera; QC1-02 = 4 ảnh front + B02 (fisheye_front); QC1-03 đến 06 = 7 polyline lane
(A04 3, A06 1, A07 1, A09 2); QC1-07 = 8 drivable + 6 crosswalk; QC1-08 = 8 đèn (A04 1, A06 6, A09 1); QC1-09 = 8 đèn + 8 biển;
QC1-10 = 8 biển; QC1-11 = 10 nhãn của B02 và B06; QC1-12 = 2 file.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A04 | lane, L2 (vàng, double) | nặng | Một vạch vàng đôi bên trái bị vẽ thành hai polyline (L1 và L2 chạy sát nhau theo hai nét). Phải là một polyline L1, kind = double. L2 là vạch thừa |
| 2 | QC1-02 | A06 | lane | nặng | Chỉ có L1 (đoạn ngắn 3 điểm). Chưa có R1 dù có vạch trắng liền ở góc phải dưới ảnh (khoảng x 1130–1280, y 548–585) |
| 3 | QC1-07 | A04 | drivable (vùng bên phải vạch đứt) | chính | Có hai vùng drivable cùng area_type = direct. Vùng làn bên phải vạch đứt phải là alternative |
| 4 | QC1-07 | A07 | drivable (direct) | chính | Vùng lái dừng phẳng ở đuôi xe phía trước (y ≈ 400) trong khi đường còn kéo dài. Guideline: gán theo "đi được nếu đường trống", không khoét hay cắt quanh xe khác |
| 5 | QC1-08 | B02 | traffic_light (bên trái ảnh) | chính | Thiếu hộp cho cụm đèn trên cột bên trái (khoảng x 70–160, y 115–215). Tâm hộp ngoài 80 % bán kính, phải có edge_zone |
| 6 | QC1-08 | B02 | traffic_light (bên phải ảnh) | chính | Thiếu hộp cho cụm đèn lớn trên cột bên phải (khoảng x 1075–1190, y 25–190). Cũng ở vùng edge_zone |
| 7 | QC1-04 | B06 | lane (thiếu) | chính | Ảnh thấy rõ vạch trắng đứt ở phần trên bên trái (khoảng x 200–430, y 100–280) nhưng lô không có lane nào. Trọng tâm B06 có lane position = other |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A04 | Lỗi 1: coi là QC1-03 (thừa, nặng) hay QC1-05 (vạch bị tách, chính)? Mình chọn mức cao hơn theo thang lỗi | |
| A06 | Lỗi 2: vạch trắng ở góc phải dưới có tính là R1 của làn đang đi không, hay là R2? | |
| A07 | Thiếu L1: bên trái là rào bê tông, chỉ có vạch rất mờ sát chân rào. Có tính "vạch thấy được" không? Nếu không thì miễn lỗi QC1-02 và nhãn đúng là road_curb dọc chân rào | |
| A07 | road_curb của lô nằm ở đoạn xa bên phải (khoảng x 750–845, y 272–292), mình không thấy vỉa ở đó. Có sai vị trí không? | |
| A09 | Thiếu R1: bên phải làn đang đi chỉ thấy vỉa (đã có road_curb), không thấy vạch sơn. Có miễn lỗi QC1-02 không? | |
| B02 | drivable chỉ phủ phần đường phía xa, không phủ phần dưới vạch ngựa vạn. Có cần phủ qua crosswalk không? | |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 5 / 71 nhãn = 7,0 %   Lỗi nhẹ: 0   Ca chờ lead: 6
Quyết định (Release / Hold / Rework): **Rework**
Lý do (theo luật của phiếu): có ít nhất một lỗi nặng (lỗi 1 ở A04) nên Rework. Lỗi chính cũng vượt 5 % số nhãn đã kiểm (5 / 71 = 7,0 %).
Kết luận vẫn là Rework kể cả khi lead đáp ca mơ hồ theo hướng bỏ lỗi 2 (A06): còn lỗi 1 nặng và 5 lỗi chính.

## Ghi chú kiểm tra khách quan (file nhãn)
28/28 ảnh có đủ 4 tag; tag camera khớp hậu tố tên file ở mọi ảnh; camera trái, phải (B05 đến B08) có lane đều position = other;
manifest ghi contains_images = false, sha256 khớp file. Lint của lô: 6 nặng (đều QC1-02: A05, A06, A07, A09, A14), 0 chính, 6 nhẹ (box < 8 px, không tính vào luật).

Ảnh "không lỗi" cho coach kiểm lại: chưa chọn. Cần một ảnh bạn đã xem kỹ và thấy đúng hoàn toàn (6 ảnh trên đều có lỗi hoặc ca mơ hồ).

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng.
