# chuyen-doi-erdCHUYỂN ĐỔI ERD SANG MÔ HÌNH QUAN HỆ
Bước 1: Xác định các thực thể có trong mô hình ERD
Dựa trên sơ đồ ERD cho trước, ta xác định được các thực thể (Entity) chính bao gồm:
•	PHIEUXUAT (Phiếu xuất)
•	VATTU (Vật tư)
•	PHIEUNHAP (Phiếu nhập)
•	DONDH (Đơn đặt hàng)
•	NHACC (Nhà cung cấp)
Bước 2: Xác định các mối quan hệ 1 - 1, 1 - n, n - m giữa các thực thể
•	Mối quan hệ 1 - n (Một - Nhiều):
o	Giữa NHACC (1) và DONDH (N) qua quan hệ Cung cấp (4). Chuyển khóa chính MaNCC từ bảng NHACC sang bảng DONDH làm khóa ngoại.
•	Mối quan hệ n - m (Nhiều - Nhiều):
o	Giữa PHIEUXUAT và VATTU qua quan hệ Chi tiết phiếu xuất (1), sinh ra bảng trung gian kèm các thuộc tính riêng: DGXuat, SLXuat.
o	Giữa VATTU và PHIEUNHAP qua quan hệ Chi tiết phiếu nhập (2), sinh ra bảng trung gian kèm các thuộc tính riêng: DGNhap, SLNhap.
o	Giữa VATTU và DONDH qua quan hệ Chi tiết đơn đặt hàng (3), sinh ra bảng trung gian tương ứng.
Bước 3: Xác định các thuộc tính đa trị và tạo thành 1 bảng mới
•	Thực thể NHACC chứa thuộc tính SDT (Số điện thoại) được thể hiện bằng vòng tròn kép $\rightarrow$ Đây là thuộc tính đa trị.
•	Tách thuộc tính này thành một bảng riêng biệt gồm: Khóa chính của nhà cung cấp (MaNCC) kết hợp với SDT để tạo thành khóa chính tổ hợp, đảm bảo cơ sở dữ liệu đạt chuẩn 1NF.
Bước 4: Liệt kê lại danh sách các bảng sau khi chuyển đổi xong
1.	Bảng PHIEUXUAT: SoPX (PK), NgayXuat
2.	Bảng VATTU: MaVTU (PK), TenVTU
3.	Bảng PHIEUNHAP: SoPN (PK), NgayNhap
4.	Bảng NHACC: MaNCC (PK), TenNCC, DiaChi
5.	Bảng DIENTHOAI_NCC (Thuộc tính đa trị SDT): MaNCC (FK), SDT (Khóa chính tổ hợp: MaNCC, SDT)
6.	Bảng DONDH: SoDH (PK), NgayDH, MaNCC (FK)
7.	Bảng CHITIET_PHIEUXUAT: SoPX (FK), MaVTU (FK), DGXuat, SLXuat (Khóa chính tổ hợp: SoPX, MaVTU)
8.	Bảng CHITIET_PHIEUNHAP: SoPN (FK), MaVTU (FK), DGNhap, SLNhap (Khóa chính tổ hợp: SoPN, MaVTU)
9.	Bảng CHITIET_DONDH: SoDH (FK), MaVTU (FK) (Khóa chính tổ hợp: SoDH, MaVTU)

