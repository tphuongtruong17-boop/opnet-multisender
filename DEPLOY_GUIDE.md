# 🚀 Hướng dẫn Deploy OP_NET MultiSender lên GitHub + Vercel

> Dành cho người chưa biết Git. Làm theo từng bước — khoảng **15 phút** là xong.

---

## 📁 Cấu trúc thư mục cần có

```
opnet-multisender/
├── index.html          ← App chính (file bạn đang có)
├── vercel.json         ← Cấu hình Vercel (file bạn đang có)
├── README.md           ← Mô tả project
└── .github/
    └── workflows/
        └── deploy.yml  ← CI/CD tự động (file bạn đang có)
```

---

## BƯỚC 1 — Tạo tài khoản GitHub

1. Vào **https://github.com** → Sign up (miễn phí)
2. Xác nhận email

---

## BƯỚC 2 — Tạo Repository mới trên GitHub

1. Đăng nhập GitHub → nhấn nút **"+"** (góc trên phải) → **New repository**
2. Điền:
   - **Repository name:** `opnet-multisender`
   - **Description:** `OP_NET MultiSender dApp — Bitcoin L1`
   - Chọn **Public** (để Vercel free tier hoạt động)
   - ☑ Check **"Add a README file"**
3. Nhấn **Create repository**

---

## BƯỚC 3 — Upload file lên GitHub (không cần Git)

Trong trang repo vừa tạo:

### Upload `index.html` và `vercel.json`:
1. Nhấn **"Add file"** → **"Upload files"**
2. Kéo thả 2 file: `index.html` và `vercel.json`
3. Scroll xuống → nhấn **"Commit changes"** (màu xanh)

### Upload `deploy.yml` (cần tạo thư mục):
1. Nhấn **"Add file"** → **"Create new file"**
2. Ở ô tên file, gõ: `.github/workflows/deploy.yml`
   - Gõ `.github/` → GitHub tự tạo thư mục
   - Tiếp tục gõ `workflows/` rồi `deploy.yml`
3. Dán nội dung file `deploy.yml` vào ô editor
4. Nhấn **"Commit changes"**

---

## BƯỚC 4 — Tạo tài khoản Vercel

1. Vào **https://vercel.com** → Sign up
2. Chọn **"Continue with GitHub"** ← quan trọng, dùng GitHub để link
3. Authorize Vercel truy cập GitHub

---

## BƯỚC 5 — Deploy lên Vercel (lần đầu)

1. Trong Vercel Dashboard → nhấn **"Add New Project"**
2. Tìm repo `opnet-multisender` → nhấn **"Import"**
3. Vercel tự detect `vercel.json` → không cần cấu hình gì thêm
4. Nhấn **"Deploy"**
5. Chờ ~30 giây → ✅ Done!

URL sẽ có dạng: **`https://opnet-multisender.vercel.app`**

---

## BƯỚC 6 — Setup CI/CD tự động (GitHub Actions)

Mỗi lần bạn sửa file và push/upload lên GitHub, Vercel sẽ tự động redeploy.

Nhưng để `deploy.yml` hoạt động, cần thêm 3 secrets:

### Lấy Vercel Token:
1. Vào **vercel.com → Settings → Tokens**
2. Nhấn **"Create"** → đặt tên `github-actions` → **Full Access**
3. Copy token (chỉ hiện 1 lần!)

### Lấy Org ID và Project ID:
1. Trong Vercel → vào project `opnet-multisender`
2. Vào **Settings → General**
3. Scroll xuống thấy **"Project ID"** → copy
4. Vào **Settings → General** → "Team ID" (hoặc vào **vercel.com/account** → "Your ID") → copy

### Thêm secrets vào GitHub:
1. Vào repo GitHub → **Settings** (tab trên cùng)
2. Menu trái → **Secrets and variables → Actions**
3. Nhấn **"New repository secret"** và thêm lần lượt:

| Name | Value |
|------|-------|
| `VERCEL_TOKEN` | token vừa copy |
| `VERCEL_ORG_ID` | Your ID / Team ID từ Vercel |
| `VERCEL_PROJECT_ID` | Project ID từ Vercel |

---

## BƯỚC 7 — Test CI/CD

1. Vào GitHub repo → chỉnh sửa bất kỳ file nào (vd: sửa README)
2. Commit changes
3. Vào tab **Actions** → xem workflow chạy
4. Sau ~1 phút → site tự động update trên Vercel ✅

---

## 🔧 Workflow sau này (cập nhật app)

Mỗi lần muốn update:
1. GitHub repo → nhấn file muốn sửa → icon ✏️ Edit
2. Sửa nội dung → Commit changes
3. GitHub Actions tự chạy → Vercel tự redeploy (~1 phút)

---

## ❓ Lỗi thường gặp

**"No output directory named 'public' found"**
→ Xóa trong Vercel Project Settings → Output Directory → để trống

**GitHub Actions fail "VERCEL_TOKEN not found"**
→ Kiểm tra lại tên secrets phải đúng chính xác (case-sensitive)

**Trang trắng sau deploy**
→ Kiểm tra `vercel.json` đã upload chưa

---

## 📱 Kết quả

- Site live: `https://opnet-multisender.vercel.app`
- Mỗi lần push lên `main` → tự động deploy
- HTTPS miễn phí, CDN toàn cầu
- Không cần server, không tốn tiền

---

*Cần hỗ trợ thêm → hỏi trực tiếp trong chat*
