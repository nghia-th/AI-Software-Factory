# Multi-Agent AI Orchestration Platform

Nền tảng điều phối đa Agent AI (Multi-Agent AI Orchestration) chuyên biệt hóa cho toàn bộ quy trình phát triển phần mềm (SDLC 10 bước). Hệ thống tích hợp các AI Agent đảm nhận từng vai trò cụ thể (BA, Architect, UI/UX, Detail Designer, Backend Coder, Frontend Coder, Tester, Reviewer) cùng cơ chế cổng duyệt có con người can thiệp (Human-in-the-loop Gate & Acceptance).

---

## 1. Hai Cách Chạy Hệ Thống (Architecture & Deployment Modes)

Từ phiên bản **v0.3.0**, nền tảng hỗ trợ 2 mô hình vận hành:

### Cách A: Máy Chủ Dùng Chung (Production Docker + Caddy) — Khuyến nghị
- Mô hình chính thức cho nhóm làm việc chung: Product Owner dựng **MỘT máy chủ duy nhất**, đồng đội truy cập trực tiếp qua trình duyệt web trên mạng LAN hoặc Internet bảo mật bằng HTTPS tự động.
- Triển khai trọn gói 6 dịch vụ qua Docker Compose: `caddy`, `frontend`, `backend`, `worker`, `postgres`, `redis`.
- Tự động di trú CSDL, nạp công cụ và 9 mẫu prompt chuẩn v1.0, cấp chứng chỉ SSL và hỗ trợ chế độ bảo trì HTTP 503 tức thời.
- **Xem hướng dẫn chi tiết tại:** [`docs/deployment.md`](docs/deployment.md).

### Cách B: Môi Trường Phát Triển Cục Bộ (Local Dev Native)
- Dành cho Developer / PO chạy và debug trực tiếp trên macOS mà không cần qua container.
- Yêu cầu: macOS, Python 3.12, Node.js 18/20 LTS, PostgreSQL 16 và Redis 7 (chạy native qua Homebrew).
- Các bước thiết lập như hướng dẫn ở Mục 2 bên dưới.

---

## 2. Cài Đặt Lần Đầu (Initial Setup cho Local Dev)

### Bước 2.1: Clone repository
```bash
git clone <repository_url> orchestration-agent
cd orchestration-agent
```

### Bước 2.2: Thiết lập môi trường Python Backend
```bash
cd backend
python3.12 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip poetry
poetry install --no-root   # installs into the active .venv
cd ..
```

### Bước 2.3: Thiết lập môi trường Frontend Next.js
```bash
cd frontend
npm ci
cp .env.local.example .env.local
cd ..
```

### Bước 2.4: Khởi tạo hệ thống tự động qua Script
Chạy script thiết lập chính thức:
```bash
./scripts/local/setup.sh
```
Script sẽ tự động:
1. Tạo file cấu hình `backend/.env` từ `.env.example` nếu chưa có.
2. Kiểm tra và tự động sinh khóa bí mật an toàn `LLM_SECRET_KEY` (Fernet) và `JWT_SECRET_KEY` (`secrets.token_urlsafe(48)`). Khóa đã hợp lệ được bảo toàn nguyên vẹn.
3. Kiểm tra kết nối PostgreSQL và Redis, tự động tạo cơ sở dữ liệu `orchestration_agent` nếu thiếu.
4. Chạy migration cơ sở dữ liệu qua Alembic (`alembic upgrade head`).
5. Nạp danh mục 5 công cụ chuẩn hệ thống (`seed_tools.py`).
6. Tạo tài khoản Quản trị viên nền tảng (Platform Admin) đầu tiên (hỏi nhập email và mật khẩu an toàn).

---

## 3. Vận Hành Hàng Ngày (Running Local Dev)

Mở 3 cửa sổ terminal riêng biệt từ thư mục gốc dự án:

### Terminal 1: Backend API (FastAPI)
```bash
./scripts/local/start-api.sh
```
- API chạy tại: **http://localhost:8000**
- OpenAPI Swagger UI: **http://localhost:8000/docs**
- Health check: `curl http://localhost:8000/health` (trả về `"version": "0.2.0"`)

### Terminal 2: Background Worker (ARQ)
```bash
./scripts/local/start-worker.sh
```
- Xử lý hàng đợi tác vụ nền, điều phối workflow của các Agent và ghi nhận kiểm toán (audit).

### Terminal 3: Frontend Web Dashboard (Next.js)
```bash
./scripts/local/start-frontend.sh
```
- Giao diện web chạy tại: **http://localhost:3000**
- Đăng nhập bằng tài khoản Platform Admin đã tạo ở bước thiết lập. Hệ thống sẽ tự động chuyển hướng vào Trang chủ Dashboard (`/`).

---

## 4. Quản Lý Người Dùng & Phân Quyền (User Management)

Từ phiên bản **v0.2.0**, việc quản trị người dùng được hỗ trợ toàn diện cả trên giao diện web và dòng lệnh:

### 4.1. Quản lý trực quan trên Giao diện Web (Khuyến nghị)
1. Đăng nhập bằng tài khoản **Platform Admin**.
2. Truy cập menu **"Quản lý người dùng"** (`/settings/users`).
3. Các chức năng có sẵn:
   - **Tạo người dùng mới / Mời thành viên:** Nhập email, họ tên, vai trò và sinh liên kết mời một lần (Invite Link) bảo mật để gửi cho người dùng.
   - **Đặt lại mật khẩu:** Tạo liên kết đặt lại mật khẩu một lần (Reset Password Link) an toàn.
   - **Khóa / Mở khóa tài khoản:** Khóa tài khoản sẽ ngay lập tức thu hồi mọi phiên đăng nhập của người dùng trong vòng ≤ 30 giây (ADR-10, ADR-11) và đóng kết nối WebSocket.
   - **Thăng / Hạ quyền Platform Admin:** Phân quyền quản trị viên nền tảng với cơ chế tự bảo vệ chống tước quyền admin cuối cùng.
4. Người dùng kích hoạt tài khoản qua trang công khai `/activate?token=...` và đặt lại mật khẩu qua trang `/reset-password?token=...`.
5. Người dùng tự quản lý thông tin cá nhân và đổi mật khẩu tại trang Hồ sơ (`/profile`).

### 4.2. Quản lý qua Script CLI (Dành cho Quản trị viên máy chủ)
Vẫn duy trì đầy đủ các công cụ dòng lệnh hỗ trợ tự động hóa và cứu hộ:
```bash
# Thao tác nhanh qua script shell:
./scripts/local/add-user.sh --email dev@local.dev --name "Developer" --admin

# Sử dụng Python CLI (yêu cầu kích hoạt virtualenv backend):
source backend/.venv/bin/activate
python backend/scripts/manage_users.py list
python backend/scripts/manage_users.py create --email user@local.dev --full-name "User Name"
python backend/scripts/manage_users.py reset-password --email user@local.dev
python backend/scripts/manage_users.py set-platform-admin --email user@local.dev on
python backend/scripts/manage_users.py deactivate --email user@local.dev
python backend/scripts/manage_users.py reactivate --email user@local.dev
```

---

## 5. Đa Ngôn Ngữ & Thêm Ngôn Ngữ Mới (i18n)

Hệ thống hỗ trợ song ngữ Tiếng Việt và Tiếng Anh (`messages/vi.json`, `messages/en.json`):
- **Đổi ngôn ngữ trên giao diện:** Sử dụng bộ chọn ngôn ngữ (Locale Switcher) trên thanh tiêu đề ứng dụng (Header) để chuyển đổi tức thời.
- **Thêm một ngôn ngữ mới vào hệ thống:**
  1. Sao chép tệp mẫu tiếng Anh sang mã ngôn ngữ mới:
     ```bash
     cp frontend/messages/en.json frontend/messages/<locale>.json
     ```
     *(Ví dụ: `frontend/messages/ja.json` cho tiếng Nhật)*.
  2. Mở tệp mới và cập nhật trường metadata ở đầu tệp:
     ```json
     "_meta": {
       "locale": "ja",
       "name": "日本語"
     }
     ```
  3. Dịch các giá trị chuỗi tương ứng.
  4. Chạy kiểm tra tính toàn vẹn và khớp khóa dịch 100%:
     ```bash
     npm --prefix frontend run i18n:check
     ```
  5. Bộ chọn ngôn ngữ trên Header sẽ tự động phát hiện và hiển thị ngôn ngữ mới.

---

## 6. Cấu Hình Kết Nối LLM & Bảng Đơn Giá (Model Pricing)

### 6.1. Kết Nối LLM Cấp Nền Tảng & Kết Nối Riêng Của Dự Án
- **Kết nối Nền tảng (Platform LLM):** Platform Admin cấu hình tại `/settings/llm-connections` dùng chung cho toàn bộ dự án.
- **Kết nối Riêng Dự án (Project LLM - v0.3.0):** Quản trị viên dự án có thể cấu hình API Key và nhà cung cấp riêng tại tab **Kết nối LLM** trong cài đặt dự án (`/projects/{id}/settings?tab=llm-connections`). Khóa được mã hóa độc lập và chỉ thành viên trong dự án mới có quyền truy cập.
- **Danh mục Preset hỗ trợ:** Ollama Cloud/Local, DeepSeek, BytePlus Ark, OpenRouter, Google Gemini, OpenAI-compatible.
- **Kiểm tra kết nối trực tiếp:** Kiểm tra qua nút "Kiểm tra kết nối" trên giao diện hoặc qua script CLI:
  ```bash
  ./scripts/local/test-llm.sh
  ```

### 6.2. Cấu Hình Bảng Đơn Giá Mô Hình AI & Báo Cáo Nguồn Chi Phí
- Platform Admin quản lý bảng đơn giá tại **"Bảng đơn giá"** (`/settings/model-pricing`) (USD / 1 triệu tokens).
- Giao diện **Báo cáo Chi phí Token** (`/projects/{id}/reports`) từ v0.3.0 hỗ trợ lọc theo nguồn kết nối (Nền tảng / Dự án) và từng kết nối cụ thể (SCR-AO-07).

---

## 7. Cấu Hình Email SMTP Nền Tảng & Đổi Mật Khẩu Thu Hồi Phiên (v0.3.0)

### 7.1. Cấu hình Email SMTP & Hàng Đợi Gửi Ngầm
1. Đăng nhập với quyền **Platform Admin**, truy cập **"Cấu hình SMTP"** (`/settings/smtp`).
2. Nhập thông tin máy chủ SMTP (Host, Port, Username, Password, Sender Email, TLS/STARTTLS).
3. Sử dụng tính năng **"Gửi thư thử nghiệm"** để kiểm tra tính thông suốt kết nối.
4. Sau khi cấu hình, các liên kết mời thành viên mới (`/activate`) và đặt lại mật khẩu (`/reset-password`) sẽ được tự động gửi qua email cho người nhận thông qua hàng đợi ARQ Worker. Trạng thái gửi (`PENDING`, `SENT`, `FAILED`) được theo dõi trực quan trên danh sách người dùng.

### 7.2. Đổi Mật Khẩu Thu Hồi Phiên Chọn Lọc (Selective Session Revocation)
- Người dùng thực hiện đổi mật khẩu tại trang Hồ sơ (`/profile`). Hệ thống tự động thu hồi toàn bộ các phiên đăng nhập khác của chính người dùng đó mà không làm ngắt quãng phiên hiện tại đang thao tác (ADR-23).

---

## 8. Sao Lưu & Khôi Phục Thảm Họa (Disaster Recovery CLI)

Nền tảng cung cấp bộ công cụ quản trị máy chủ `scripts/ops/orchestration-cli` (ADR-14):

```bash
# 1. Tạo bản sao lưu toàn diện (CSDL PostgreSQL + Artifacts WORM):
./scripts/ops/orchestration-cli backup

# 2. Liệt kê các bản sao lưu hiện có:
./scripts/ops/orchestration-cli list

# 3. Khôi phục hệ thống từ một bản sao lưu (kèm cờ bảo trì HTTP 503):
./scripts/ops/orchestration-cli restore <TÊN-BẢN-SAO-LƯU>

# 4. Dọn dẹp bản sao lưu cũ (giữ lại 7 bản gần nhất):
./scripts/ops/orchestration-cli prune

# 5. Cài đặt lịch Cron tự động sao lưu lúc 02:00 AM hàng ngày:
./scripts/ops/orchestration-cli install-cron --dry-run   # Xem trước cấu hình
./scripts/ops/orchestration-cli install-cron             # Cài đặt thật
```

---

## 9. Rà Soát & Dọn Dẹp Dữ Liệu Kiểm Thử

Để kiểm tra các dự án test sinh ra từ quá trình chạy E2E hoặc các tài khoản thử nghiệm:
```bash
# Chế độ xem trước (Dry-run mặc định, an toàn tuyệt đối):
./scripts/local/cleanup-test-data.sh

# Chế độ thực thi (yêu cầu gõ 'yes' để xác nhận):
./scripts/local/cleanup-test-data.sh --apply
```

---

## 10. Hướng Dẫn Chạy Kiểm Thử (Automated Tests)

### 10.1. Backend Unit & Integration Tests (pytest)
```bash
cd backend
source .venv/bin/activate

# Chạy toàn bộ test suite (nhanh ~36-80s nhờ cơ chế Redis/ARQ stub):
pytest -n 4

# Chạy linter kiểm tra chuẩn mã nguồn:
ruff check app tests alembic
cd ..
```

### 10.2. Frontend Tests & E2E Playwright
Bộ kiểm thử E2E Playwright được tổ chức làm 2 tầng rõ rệt:
- **Tầng Smoke (`npm run test:e2e`):** Kiểm thử nhanh (< 1 phút) toàn bộ các chức năng cốt lõi và giao diện mới của v0.3.0 (xem Agent trực tiếp, cấu hình chế độ tự quyết, quản lý kết nối LLM, cấu hình SMTP với Fake SMTP server cục bộ `smtp-server`).
- **Tầng Full (`npm run test:e2e:full`):** Kiểm thử luồng thực thi 10 bước trọn vẹn kết hợp mô hình AI cục bộ qua Ollama (`@llm`).

```bash
cd frontend

# Kiểm tra tính toàn vẹn đa ngôn ngữ (100% khớp khóa):
npm run i18n:check

# Kiểm tra kiểu TypeScript & Linter:
npx tsc --noEmit
npm run lint

# Chạy bộ Smoke Test nhanh (tích hợp Fake SMTP Server tự động):
npm run test:e2e

# Chạy bộ Full E2E toàn luồng (yêu cầu Ollama khởi chạy):
npm run test:e2e:full
cd ..
```

---

## 11. Xử Lý Sự Cố Thường Gặp (Troubleshooting)

1. **Frontend Dev Server báo lỗi 503 sau khi vô tình chạy `npm run build`**:
   - *Nguyên nhân*: Lệnh `build` ghi đè thư mục `.next` của tiến trình phát triển.
   - *Khắc phục*: Tắt tiến trình frontend, xóa thư mục `.next` (`rm -rf frontend/.next`), sau đó khởi động lại bằng `./scripts/local/start-frontend.sh`.
2. **Trang chủ Dashboard báo trạng thái Background Worker là "stale" hoặc "mất kết nối"**:
   - *Nguyên nhân*: Tiến trình ARQ Worker chưa được bật hoặc Redis bị ngắt kết nối.
   - *Khắc phục*: Kiểm tra Redis (`redis-cli ping`), sau đó chạy `./scripts/local/start-worker.sh`.
3. **Người dùng nhận thông báo "Tài khoản bị khóa" hoặc mã lỗi 403**:
   - *Nguyên nhân*: Tài khoản đã bị khóa bởi Platform Admin hoặc phiên làm việc đã bị thu hồi.
   - *Khắc phục*: Liên hệ Platform Admin kiểm tra trạng thái tài khoản tại màn hình `/settings/users`.
4. **Email thư mời hoặc đặt lại mật khẩu không tới người nhận**:
   - *Nguyên nhân*: Cấu hình SMTP chưa được thiết lập tại `/settings/smtp` hoặc tiến trình ARQ Worker chưa chạy.
   - *Khắc phục*: Quản trị viên lấy liên kết kích hoạt / đặt lại mật khẩu trực tiếp trên giao diện để gửi thủ công, đồng thời kiểm tra log của ARQ Worker.

---

## 12. Giới Hạn Phiên Bản v0.3.0

- **Sandbox Docker tạm tắt (`SANDBOX_ENABLED=false`)**: Agent Tester trong phiên bản này tập trung vào phân tích tĩnh (Static Analysis) và kiểm tra logic thay vì khởi chạy container cô lập để thực thi mã nguồn.
- **Hàng đợi Email chưa tự động gửi lại khi lỗi (No Auto-retry)**: Email gửi thất bại do sự cố máy chủ SMTP được đánh dấu `FAILED`; quản trị viên sử dụng liên kết dự phòng trên giao diện để bàn giao thủ công cho người dùng.
- **Thống kê phiên thu hồi khi đổi mật khẩu**: Số lượng phiên hiển thị (`revoked_sessions_count`) có thể đếm dư các phiên đã hết hạn nhưng người dùng chưa bấm đăng xuất do khóa tập phiên Redis được quản lý theo TTL.
- **Kiểm thử E2E Smoke còn một số kịch bản dùng `?mock=`**: Có 7 điểm kiểm thử smoke đặc thù sử dụng tham số giả lập trạng thái chỉ có thể phát sinh thông qua tương tác LLM phức tạp (đã được ghi chú rõ ràng mã miễn trừ `mock-exception` theo T-156).
- **Kế hoạch phiên bản tiếp theo**: Tích hợp các nhà cung cấp đám mây lớn (Azure OpenAI, AWS Bedrock, GCP Vertex AI), phê duyệt cổng duyệt qua Slack/Telegram, và hỗ trợ giao thức MCP Server được hoạch định phát triển trong phiên bản v0.4.0 và v0.5.0.

