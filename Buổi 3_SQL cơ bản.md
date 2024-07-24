# BUỔI 3: SQL CƠ BẢN

- [BUỔI 3: SQL CƠ BẢN](#buổi-3-sql-cơ-bản)
  - [I. Query cơ bản.](#i-query-cơ-bản)
    - [1. Truy vấn đơn giản.](#1-truy-vấn-đơn-giản)
        - [```select *``` : Hiện tất cả bảng](#select---hiện-tất-cả-bảng)
        - [```select``` : Hiện một số cột](#select--hiện-một-số-cột)
        - [```select..where``` : Hiện một số dòng / bản ghi](#selectwhere--hiện-một-số-dòng--bản-ghi)
        - [```select..order by```: Hiện và sắp xếp theo điểm rồi theo tên](#selectorder-by-hiện-và-sắp-xếp-theo-điểm-rồi-theo-tên)
        - [```select..distinct```: Hiện danh sách giá trị không trùng lặp](#selectdistinct-hiện-danh-sách-giá-trị-không-trùng-lặp)
        - [```select..top```: Hiện các dòng đầu tiên trong bảng](#selecttop-hiện-các-dòng-đầu-tiên-trong-bảng)
    - [2. Truy vấn lồng nhau (nested query).](#2-truy-vấn-lồng-nhau-nested-query)
        - [```select..where (select)``` : Hiện tất cả những người trong bảng nhân viên có lương bằng lương lớn nhất của những người có trong công ty:](#selectwhere-select--hiện-tất-cả-những-người-trong-bảng-nhân-viên-có-lương-bằng-lương-lớn-nhất-của-những-người-có-trong-công-ty)
        - [```select..where (in)``` : Hiện tất cả những người trong bảng nhân viên có lương lớn nhất hoặc lớn nhì của những người có trong công ty:](#selectwhere-in--hiện-tất-cả-những-người-trong-bảng-nhân-viên-có-lương-lớn-nhất-hoặc-lớn-nhì-của-những-người-có-trong-công-ty)
    - [3. Truy vấn tổng nhóm (subtotal query / grouping query).](#3-truy-vấn-tổng-nhóm-subtotal-query--grouping-query)
        - [```select..group by``` : Thống kê theo tiêu chí.](#selectgroup-by--thống-kê-theo-tiêu-chí)
        - [```select..having``` : Hiện ra một số nhóm phù hợp.](#selecthaving--hiện-ra-một-số-nhóm-phù-hợp)
    - [4. Truy vấn liên bảng (cross table query / joining query).](#4-truy-vấn-liên-bảng-cross-table-query--joining-query)
        - [```select..inner join``` : ghép các cặp bản ghi thỏa mãn điều kiện.](#selectinner-join--ghép-các-cặp-bản-ghi-thỏa-mãn-điều-kiện)
        - [```select..left outer join``` : lấy tất cả phía trái và ghép (nếu có) với phải.](#selectleft-outer-join--lấy-tất-cả-phía-trái-và-ghép-nếu-có-với-phải)
        - [```select..right outer join``` : lấy tất cả phía phải và ghép (nếu có) với phía trái.](#selectright-outer-join--lấy-tất-cả-phía-phải-và-ghép-nếu-có-với-phía-trái)
        - [```select..full outer join``` : lấy từ hai phía và ghép (nếu có).](#selectfull-outer-join--lấy-từ-hai-phía-và-ghép-nếu-có)
        - [```select..cross join``` : trả về tất cả các cặp có thể ghép.](#selectcross-join--trả-về-tất-cả-các-cặp-có-thể-ghép)
  - [II. SubQuery.](#ii-subquery)
    - [1. SubQuery là gì?](#1-subquery-là-gì)
    - [2. Một vài quy tắc mà SubQuery phải tuân theo.](#2-một-vài-quy-tắc-mà-subquery-phải-tuân-theo)


## I. Query cơ bản.

- Hỗ trợ truy vấn: distinct, top, as, identity.

- Phép toán tập hợp: in, like, between.

- Các hàm tổng nhóm: sum, max, min, avg.

### 1. Truy vấn đơn giản.

##### ```select *``` : Hiện tất cả bảng

- VD: ```select *from SinhVien```

##### ```select``` : Hiện một số cột

- VD: ```select TenSV, DiemTBfrom SinhVien```

##### ```select..where``` : Hiện một số dòng / bản ghi

- VD:
```
select TenSV, DiemTBfrom SinhVien
where DiemTB > 6.0
```

##### ```select..order by```: Hiện và sắp xếp theo điểm rồi theo tên

- VD: 
```
select TenSV, DiemTBfrom SinhVien
order by DiemTB desc, TenSV asc // asc sắp sếp tăng dần, desc là giảm dần
```

##### ```select..distinct```: Hiện danh sách giá trị không trùng lặp

- VD: ```select distinct QueQuanfrom SinhVien```

##### ```select..top```: Hiện các dòng đầu tiên trong bảng

- VD: 
```
select top 3 TenSV, DiemTBfrom SinhVien
order by DiemTB desc, TenSV asc
```

### 2. Truy vấn lồng nhau (nested query).

##### ```select..where (select)``` : Hiện tất cả những người trong bảng nhân viên có lương bằng lương lớn nhất của những người có trong công ty:

- VD: 
```
select TenNV, Luongfrom NhanVien
where Luong = (select max(Luong) from NhanVien)
```

##### ```select..where (in)``` : Hiện tất cả những người trong bảng nhân viên có lương lớn nhất hoặc lớn nhì của những người có trong công ty:

- VD: 
```
select TenNV, Luongfrom NhanVien
where Luong in (select top 2 Luong from NhanVien order by Luong)
```

Câu lệnh select trong sẽ tạo ra một tập hai giá trị (top 2) đó là lương lớn nhất và lương lớn nhì. Và câu lệnh select thứ nhất sẽ chọn ra những người mà lương nằm trong tập lớn nhất và lớn nhì.

```select..where (in sub)``` : Hiện ra tất cả những người có lương lớn nhất phòng của anh ta (không phải lớn nhất trong công ty mà lớn nhất trong phòng hoặc đơn vị mà anh ta thuộc về)

- VD:
```
select nv1.TenNV, nv1.Luongfrom NhanVien as nv1
where nv1.Luong = (select max(Luong) from NhanVien where Phong=nv1.Phong)
```

Câu lệnh select trong sẽ trả về giá trị lương lớn nhất nhưng không phải lớn nhất trong toàn công ty mà lớn nhất trong phòng của nv1. Sau đó câu lệnh select ngoài cùng sẽ xác định xem nv1 có được chọn không bằng cách kiểm tra lương anh ta với lương lớn nhất của phòng anh ta.

### 3. Truy vấn tổng nhóm (subtotal query / grouping query).

##### ```select..group by``` : Thống kê theo tiêu chí.

- VD1: Hiện ra số lượng các nhân viên ứng với từng quê.

```
select QueQuan, count(*)from NhanVien
group by QueQuan
```

- VD2: Đếm số nam và số nữ trong công ty.

```
select GioiTinh, count(*)from NhanVien
group by GioiTinh
```

- VD3: Tính tổng thu nhập theo từng phòng.

```
select Phong, sum(Luong)from NhanVien
group by Phong
```

##### ```select..having``` : Hiện ra một số nhóm phù hợp.

- VD1: Chỉ đếm số lượng người ở Hải Phòng và số lượng người ở Hà Nội.

```
select QueQuan, count(*)from NhanVien
group by QueQuan
having (QueQuan = ‘HP’, QueQuan = ‘HN’)
```

- VD2: Chỉ hiện ra những phòng nào có tổng thu nhập lớn hơn 500000.

```
select Phong, sum(Luong)from NhanVien
group by Phong
having sum(Luong) > 5000000
```

- VD3: Chỉ hiện ra những tỉnh nào có số lượng người lớn hơn 10.

```
select QueQuan, count(*)from NhanVien
group by QueQuan
having count(*) > 10
```

### 4. Truy vấn liên bảng (cross table query / joining query).

##### ```select..inner join``` : ghép các cặp bản ghi thỏa mãn điều kiện.

- VD: Ghép bảng nhân viên và hiện ra tên nhân viên và tên địa phương.

```
select NhanVien.TenNV, DiaPhuong.TenDP
from NhanVien 
inner join DiaPhuong on NhanVien.QueQuan = DiaPhuong.MaDP
```

##### ```select..left outer join``` : lấy tất cả phía trái và ghép (nếu có) với phải.

- VD: Lấy tất cả những nhân viên kể cả những nhân viên có quê quán không hợp lệ (nghĩa là mã quê quán không có trong bảng địa phương).

```
select NhanVien.TenNV, DiaPhuong.TenDP
from NhanVien 
left outer join DiaPhuong on NhanVien.QueQuan = DiaPhuong.MaDP
```

##### ```select..right outer join``` : lấy tất cả phía phải và ghép (nếu có) với phía trái.

- VD: Lấy tất cả những địa phương ghép với nhân viên, các địa phương không hợp lệ sẽ được ghép với bộ dữ liệu rỗng. Không hiện ra các nhân viên không có mã quê quán phù hợp.

```
select NhanVien.TenNV, DiaPhuong.TenDP
from NhanVien 
right outer join DiaPhuong on NhanVien.QueQuan = DiaPhuong.MaDP
```

##### ```select..full outer join``` : lấy từ hai phía và ghép (nếu có).

- VD: Lấy tất cả những nhân viên (nếu không có quê quán phù hợp thì ghép với bộ dữ liệu rỗng) và tất cả những địa phương kể cả không có nhân viên.

```
select NhanVien.TenNV, DiaPhuong.TenDP
from NhanVien 
right outer join DiaPhuong on NhanVien.QueQuan = DiaPhuong.MaDP
```

##### ```select..cross join``` : trả về tất cả các cặp có thể ghép.

- VD: Ghép từng nhân viên với tất cả các địa phương. Như vậy nếu có m nhân viên và có n địa phương thì bảng đích sẽ có m*n dòng. n dòng đầu cho nhân viên thứ nhất ghép với các địa phương. n dòng sau cho nhân viên thứ hai ghép với các địa phương. và tiếp tục như thế tới nhân viên thứ m.

```
select NhanVien.TenNV, DiaPhuong.TenDP
from NhanVien 
cross join DiaPhuong
```

## II. SubQuery.

### 1. SubQuery là gì?

Truy vấn con hay Subquery là một cách viết câu lệnh trong SQL mà bạn có thể lồng thêm 1 hay nhiều các truy vấn nhỏ khác. Các lệnh thường được sử dụng khi viết là Insert, Select, Delete và Update. Cùng với đó là các toán tử ví dụ như =, <, >, >=, <=, IN, BETWEEN…

Ngoài ra truy vấn con cũng được gọi là INNER QUERY hay INNER SELECT. Các truy vấn chính mà chứa các truy vấn con thì được gọi là OUTER SELECT hoặc OUTER QUERY.

### 2. Một vài quy tắc mà SubQuery phải tuân theo.

- Truy vấn con thường thực thi trước khi truy vấn con không có bất kỳ mối quan hệ đồng quan hệ nào với truy vấn chính , khi có mối quan hệ đồng quan hệ, trình phân tích cú pháp sẽ quyết định nhanh chóng truy vấn nào sẽ thực thi theo thứ tự ưu tiên và sử dụng đầu ra của truy vấn con cho phù hợp.

- Truy vấn con phải được đặt trong dấu ngoặc đơn.

- Các truy vấn con nằm ở phía bên phải của toán tử so sánh.

- Lệnh ORDER BY không thể được sử dụng trong Truy vấn con. Lệnh GROUPBY có thể được sử dụng để thực hiện chức năng tương tự như lệnh ORDER BY.

- Sử dụng các toán tử hàng đơn với Truy vấn con hàng đơn. Sử dụng toán tử nhiều hàng với Truy vấn con nhiều hàng.