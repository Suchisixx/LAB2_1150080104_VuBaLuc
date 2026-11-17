
# LAB 2 - MÃ HÓA ĐỐI XỨNG HIỆN ĐẠI

- **Họ và tên:** Vũ Bá Lực
- **MSSV:** 1150080104
- **Lớp:** 11-ĐH-THMT
- **Học phần:** An toàn và Bảo mật thông tin

---

## 1. Cấu trúc thư mục

- `pom.xml`: Cấu hình Maven (JDK 17, Oracle JDBC `ojdbc11`, BouncyCastle `bcprov-jdk18on`, lớp chính `week_02.frm_Menu`).
- `sql/`:
  - `01_Tao_User_Oracle.sql`: Tạo tài khoản `lab2_user` trong Oracle PDB `FREEPDB1`.
  - `02_Tao_Bang_Oracle.sql`: Tạo 2 bảng `app_users` và `crypto_history`.
  - `03_Kiem_Tra_Du_Lieu_Oracle.sql`: Kiểm tra dữ liệu đã lưu trong Oracle.
- `src/main/java/week_02/`:
  - Dùng chung & CSDL: `CipherUtil.java`, `FileTextIO.java`, `DbConfig.java`, `HistoryDao.java`, `UserDao.java`.
  - Thuật toán: `DESCipher.java`, `TripleDESCipher.java`, `AESCipher.java`, `RC4Cipher.java`, `TwofishCipher.java`, `AESCTRCipher.java`.
  - Giao diện Swing: `frm_Menu.java`, `frm_KetNoiSQL.java`, `frm_LichSu.java`, `frm_DES.java`, `frm_TripleDES.java`, `frm_AES.java`, `frm_RC4.java`, `frm_Twofish.java`, `frm_AES_CTR.java`.
- `LAB2_Python/aes_cbc_gui.py`: Bài nâng cao 02 (AES-256-CBC bằng Python Tkinter).

---

## 2. Yêu cầu môi trường

- **JDK 17** trở lên
- **Apache NetBeans** (bản 20 trở lên)
- **Oracle Database** (đang chạy PDB `FREEPDB1`, cổng `1521`) + SQL Developer hoặc SQL*Plus
- **Python 3.10+** và thư viện `cryptography` (cho bài nâng cao 02)

---

## 3. Hướng dẫn chuẩn bị cơ sở dữ liệu Oracle

1. Mở SQL Developer (hoặc SQL*Plus), kết nối vào PDB `FREEPDB1` bằng tài khoản quản trị (`SYS` / `SYSTEM`).
2. Mở và chạy script `sql/01_Tao_User_Oracle.sql` (bấm **F5 - Run Script**) để tạo user `lab2_user` với mật khẩu `LabUser@2026`.
3. Tạo kết nối mới bằng tài khoản `lab2_user` (Hostname: `127.0.0.1`, Port: `1521`, Service Name: `FREEPDB1`, Password: `LabUser@2026`).
4. Mở và chạy script `sql/02_Tao_Bang_Oracle.sql` (bấm **F5**) để tạo 2 bảng `app_users` và `crypto_history`.

---

## 4. Hướng dẫn chạy chương trình Java (NetBeans)

1. Mở NetBeans → **File → Open Project...** → chọn thư mục `LAB2_MaHoaHienDai`.
2. Nhấp phải tên project → **Clean and Build (`Shift + F11`)** để Maven tải thư viện `ojdbc11` và `bcprov-jdk18on` rồi biên dịch.
3. Nhấp phải tên project → **Run (`F6`)** để mở cửa sổ chính `frm_Menu`.
4. Trên `frm_Menu`:
   - Bấm **Kết nối Oracle** → nhập Password `LabUser@2026` → **Test Connection** (thông báo thành công là có thể lưu lịch sử và đăng ký/đăng nhập).
   - Chọn lần lượt các bài **2.1 DES**, **2.2 TripleDES**, **2.3 AES + Login**, **2.4 RC4**, **2.5 Twofish**, **2.6 Nâng cao - AES-CTR** để thực hiện mã hóa/giải mã.
   - Bấm **Xem lịch sử** (hoặc chạy `sql/03_Kiem_Tra_Du_Lieu_Oracle.sql`) để kiểm tra dữ liệu lưu trong Oracle.

---

## 5. Hướng dẫn chạy bài nâng cao Python (AES-CBC)

Mở Command Prompt hoặc PowerShell tại thư mục `LAB2_Python`:

1. Cài đặt thư viện (nếu chưa có):
   ```powershell
   py -m pip install cryptography
   ```
2. Chạy tự kiểm thử:
   ```powershell
   py aes_cbc_gui.py --self-test
   ```
   *(Kết quả đúng sẽ in: `SELF-TEST OK: 4 thông điệp mã hóa/giải mã đúng, sai khóa bị phát hiện.`)*
3. Chạy giao diện Tkinter:
   ```powershell
   py aes_cbc_gui.py
   ```
