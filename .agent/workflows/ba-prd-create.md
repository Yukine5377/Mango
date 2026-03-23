---
description: "Workflow to generate a Product Requirements Document (PRD) from AS-IS to TO-BE."
---
Version: 1.0.0
Author: M2MBA
Last Updated: 2026-03-06
Description: Workflow tự động tạo Product Requirements Document (PRD) toàn diện từ kết quả khơi gợi yêu cầu.

# Workflow: BA PRD Creation

Workflow này hướng dẫn Agent thực hiện chuỗi các bước liên tiếp để tự động hóa quá trình tạo Product Requirements Document (PRD) cho một dự án/tính năng mới, bắt đầu từ dữ liệu khơi gợi yêu cầu. Việc này kết hợp các skill phân tích BA có sẵn để tạo thành một chuỗi luồng xử lý mượt mà.

## Các bước thực hiện:

1. **Thu thập Kết quả Khơi gợi Yêu cầu**
   - Yêu cầu người dùng cung cấp tài liệu "Kết quả khơi gợi yêu cầu" (Meeting notes, bản ghi âm đã chuyển text, thư điện tử trao đổi, hoặc file thống nhất yêu cầu ban đầu).
   - Nếu người dùng đã cung cấp mô tả ngay từ prompt đầu tiên, tiến hành nạp dữ liệu và tự động sang Bước 2.

// turbo
2. **Phân tích Quy trình Hiện tại (AS-IS)**
   - Input: Kết quả khơi gợi yêu cầu ở Bước 1.
   - Thao tác: Áp dụng Agent skill `ba-process-analysis` để phân tích nghiệp vụ, mô hình hóa và xác định lỗi/vấn đề (pain points) của hệ thống hiện tại.
   - Output: File tài liệu phân tích AS-IS.

// turbo
3. **Đề xuất Quy trình Mới (TO-BE)**
   - Input: File quy trình AS-IS từ Bước 2 và mục tiêu mong đợi của người dùng.
   - Thao tác: Áp dụng Agent skill `ba-process-proposal` để thiết kế quy trình đề xuất (TO-BE), giải quyết các pain points đã xác định.
   - Output: File tài liệu quy trình TO-BE.

// turbo
4. **Mô hình Tổng quan Sản phẩm**
   - Input: Quy trình TO-BE và kết quả khơi gợi yêu cầu.
   - Thao tác: Áp dụng Agent skill `ba-product-overview-gen` để xác định các actor, application, hệ thống tích hợp và mô hình giao tiếp.
   - Output: File tài liệu `Analysis/ba-product-overview-gen.md`.

// turbo
5. **Phân tích Danh sách Epic và Tính năng (Use Case)**
   - Input: File quy trình TO-BE từ Bước 3 và Mô hình tổng quan từ Bước 4.
   - Thao tác: Áp dụng Agent skill `ba-usecase-list-gen` để trích xuất và gom nhóm các Use Case thành từng Epic.
   - Output: File danh sách Epic và Use Cases chi tiết.

// turbo
6. **Tổng hợp và Tạo Product Requirements Document (PRD)**
   - Input: Toàn bộ dữ liệu từ Bước 1 đến Bước 5.
   - Thao tác: Tổng hợp thành file PRD duy nhất. BẮT BUỘC tuân thủ file mẫu: `e:\Training Project\Skill BA gg Antigravity\.agent\workflows\references\ba-prd-template.md`. 
   - *Lưu ý về Infographic:* Bước này không tự động gen ảnh. Nếu cần ảnh minh họa cho mục "4. Mô hình tổng quan sản phẩm", hãy chạy riêng workflow `/ba-infographic-gen` sau khi PRD hoàn tất.
   - Output: File PRD `docs-BA/PRD/ba-prd-[feature-name].md`.

// turbo
7. **Thiết kế ERD (Entity-Relationship Diagram)**
   - Input: File PRD đã hoàn tất từ Bước 6.
   - Thao tác: Kích hoạt skill `ba-erd-gen` để phân tích các thực thể và quan hệ.
   - Output: File ERD lưu vào thư mục `Data model/`.
   - *Lưu ý:* Nếu thông tin trong PRD chưa đủ để xác định attributes/relations, skill `ba-erd-gen` sẽ tự động dừng và hỏi User làm rõ trước khi sinh file.
   - Sau khi tạo file ERD xong → thực hiện **Quy tắc Cập nhật Master ERD** ở mục dưới.

---

## 📁 Quy tắc Quản lý File Output

### Nguyên tắc Update vs Tạo Mới

| Tình huống | Hành động | Kết quả |
|------------|-----------|---------|
| Thêm/bớt tính năng trong cùng nghiệp vụ | **Update file cũ** | Tăng Minor version (v1.0 → v1.1), ghi Change log |
| Scope/nhóm nghiệp vụ mới hoàn toàn | **Tạo file mới** theo tên nghiệp vụ đó | Đồng thời hỏi User cập nhật Master Index |

### Quy tắc Cập nhật Master PRD Index

Sau mỗi lần tạo PRD mới, Agent **BẮT BUỘC** phải kiểm tra và cập nhật file:
`docs-BA/PRD/prd-index.md`

Nếu file chưa tồn tại → Tạo mới. Định dạng file:

```markdown
# PRD Master Index

| Tên file | Nhóm nghiệp vụ | Version | Mô tả ngắn | Ngày tạo |
|----------|----------------|---------|------------|----------|
| [ba-prd-xxx.md](link) | [Nhóm nghiệp vụ] | v1.0 | [Tóm tắt scope] | DD/MM/YYYY |
```

### Quy tắc Cập nhật Master ERD

Khi tạo xong file ERD mới, Agent hỏi User:
> *"File ERD `ba-erd-[tên].md` đã tạo xong. Bạn có muốn cập nhật vào **Master ERD tổng** không?"*

**Nếu User đồng ý:** Cập nhật file `Data model/erd-master.md` với nội dung:
- **Chỉ vẽ các Entities** (không vẽ attributes) và **quan hệ giữa chúng** (Mermaid `erDiagram` tối giản).
- Thêm bảng mapping: Entity nào thuộc ERD file nào, nghiệp vụ nào.

Định dạng file `erd-master.md`:

```markdown
# ERD Master - Tổng quan Thực thể Hệ thống

## Sơ đồ Quan hệ Tổng (Entities Only)
[Mermaid erDiagram chỉ có entity và relationship, KHÔNG có attributes]

## Danh sách File ERD theo Nhóm Nghiệp vụ

| Nhóm nghiệp vụ | File ERD chi tiết | Entities thuộc nhóm |
|----------------|-------------------|---------------------|
| [Ví dụ: Quản lý Đơn hàng] | [ba-erd-order.md](link) | Order, OrderItem, Payment |
| [Ví dụ: Quản lý Người dùng] | [ba-erd-user.md](link) | User, Role, Permission |
```

---

## 📌 INPUT SPEC (Kết quả khơi gợi yêu cầu) — Mango MVP (ăn uống gần tôi)

### 0) Tên tính năng/feature
**Mango — Khám phá quán ăn gần tôi (MVP: ăn uống)**

### 1) Mục tiêu sản phẩm
- **User goal:** Mở app lên là thấy danh sách quán ăn gần vị trí của mình tại Hà Nội, có review chi tiết và điểm đánh giá rõ ràng để quyết định nhanh.
- **Business goal:** Tạo mạng lưới review có chất lượng thông qua cơ chế trả tiền cho cộng tác viên dựa trên mức tương tác và độ hữu ích.
- **Non-goal (MVP):** Không tập trung “chỗ chơi” trong bản đầu; không tạo hệ thống xác thực quán theo quy trình phức tạp (chỉ admin xử lý theo report/khiếu nại).

### 2) Phạm vi MVP (In-scope)
- **Nền tảng:** Web app/ứng dụng client.
- **Danh mục:** Chỉ **ăn uống**.
- **Tìm kiếm theo vị trí:** Bán kính tối đa **5km** quanh người dùng.
- **Vị trí khi mở app:** Lấy GPS ngay khi mở.
- **Fallback khi không cấp quyền GPS:** lọc theo **quận/huyện**, mặc định **Ba Đình, Hà Nội**.
- **Giao diện ưu tiên:** **Danh sách** (list-first), hỗ trợ browsing.
- **Dữ liệu ban đầu:** cào từ **Google Maps công khai**.
- **Review:** bắt buộc **đăng nhập** để review.
  - Không cho ẩn danh; profile không chứa thông tin cá nhân chi tiết.
  - Không giới hạn số review.
- **Review fields (mỗi review):**
  - Điểm tổng hợp (từ nhiều thang).
  - Nội dung chữ review.
  - Giá (tầm giá/khung giá theo dữ liệu review).
  - Giờ mở cửa.
  - Độ đông.
  - Món nên thử.
  - Thang điểm 1-5 cho **5 hạng mục**: `đồ ăn`, `giá`, `phục vụ`, `không gian`, `vệ sinh`.
- **Voting & feedback:**
  - Vote `up/down` cho review.
  - Vote “hữu ích”.
  - Có **bình luận** (comment) để tăng tương tác.
- **Admin backoffice (MVP):**
  - Quản lý **reviewer**.
  - Quản lý **quán**.
  - **Duyệt/điều tra vote** (xử lý hành vi thao túng).
  - Xử lý **khiếu nại/báo xấu**: không duyệt review trước khi public, nhưng admin có thể xử lý khi có báo cáo xấu.
- **Trang quán:**
  - **Tạo trang quán khi có review đầu tiên.**
  - Sau đó quán trả phí đăng tải **1 lần 100k** khi admin **duyệt**.
- **Thu phí người dùng:**
  - Người dùng cần thanh toán để **tiếp tục xem danh sách quán ăn theo chu kỳ 6 tháng**.
  - **Áp dụng từ khi tải app** (nếu chưa có subscription hợp lệ thì gating sẽ kích hoạt ngay).
- **Cá nhân hóa (MVP):**
  - Tập trung cá nhân hóa ngay trong MVP theo tín hiệu hành vi browsing và tương tác (click/visit, vote, helpful, thời điểm).

### 3) Quy trình nghiệp vụ (AS-IS vs TO-BE) — tóm tắt
**AS-IS (hiện tại):**
- Người dùng tìm “quán ăn gần tôi” bằng Google Maps/search, đọc review rải rác, khó so sánh nhanh theo các khía cạnh mong muốn.

**TO-BE (MVP Mango):**
1. Người dùng mở app -> cấp quyền vị trí (hoặc fallback Ba Đình).
2. App hiển thị danh sách quán ăn trong bán kính 5km.
3. Người dùng browsing list -> mở chi tiết quán -> đọc review + score tổng hợp.
4. Đăng nhập -> viết review (điền 5 thang 1-5 + fields: giá/giờ/độ đông/món nên thử).
5. Vote up/down + “hữu ích” + comment.
6. Admin điều tra vote thao túng và xử lý báo xấu/khiếu nại (không duyệt trước khi public).
7. Trang quán tạo từ review đầu tiên; quán nộp 100k khi admin duyệt đăng tải.
8. Người dùng trả phí 6 tháng để tiếp tục browsing.

### 4) Business Rules & tính toán chính

#### 4.1 Quy tắc vị trí
- “Gần tôi” = bán kính tối đa **5km**.
- Không có GPS -> dùng lọc theo **quận/huyện**, mặc định **Ba Đình**.

#### 4.2 Review & điểm
- Điểm review là **trung bình cộng** 5 thang điểm `food/price/service/space/hygiene`, mỗi thang từ **1-5**.

#### 4.3 Ranking & cá nhân hóa (MVP)
- List score kết hợp:
  - cộng đồng: điểm review + số lượng review + vote/helpful,
  - cá nhân: affinity suy từ hành vi user,
  - vị trí: khoảng cách trong bán kính 5km.
- Dạng công thức (PRD sẽ chốt weights):
  - `finalScore = w1 * communityScore + w2 * personalAffinity + w3 * distanceScore` (TBD weights/chuẩn hóa sẽ chốt sau)

#### 4.4 Payout cho cộng tác viên (linear + cap 10k)
- Đầu vào payout:
  - `views` (lượt xem review),
  - `voteUp`, `voteDown`,
  - `helpfulCount` (người bấm hữu ích),
  - `commentCount` (số comment).
- Công thức tuyến tính (trọng số `base/a/b/c/d` sẽ chốt sau):
  - `payout = min(10000, base + a*views + b*(voteUp - voteDown) + c*helpfulCount + d*commentCount)`
- Giới hạn: **trần 10k/review**.

#### 4.5 Quán trả phí 100k (1 lần) và lifecycle trang quán
- Tạo trang quán ngay khi có review đầu tiên.
- Quán trả **100k** **1 lần** khi admin duyệt trạng thái đăng tải.
- Trạng thái trước khi quán trả 100k:
  - Quán **không được trả lời bình luận**.
  - Quán **không được thay ảnh** (chỉ cho xem).

### 5) User Stories (gợi ý)
- Xem danh sách quán trong 5km.
- Xem trang quán và review chi tiết/breakdown 5 thang.
- Đăng nhập viết review (điền đủ fields).
- Vote up/down, vote hữu ích, comment.
- Payout cộng tác viên theo tương tác (linear + cap 10k/review).
- Admin xử lý khiếu nại/báo xấu và điều tra vote thao túng.
- Trang quán tạo từ review đầu tiên; sau đó quán trả 100k khi duyệt.
- Cá nhân hóa list theo tín hiệu hành vi (browsing).
- Thu phí người dùng 6 tháng để tiếp tục xem danh sách.

### 6) Assumptions & Dependencies
- Dữ liệu cào từ Google Maps cần tuân thủ chính sách sử dụng dữ liệu của nguồn.
- Admin là quyền lực cuối để xử lý report xấu/gian lận vote.
- Policy subscription (6 tháng) cần chốt logic gating: free xem bao lâu trước khi phải trả.

### 7) Open Questions (cần chốt thêm trước khi generate PRD chi tiết)
- Trọng số payout `base/a/b/c/d`: **TBD (chốt sau)**.
- Ranking/thuật toán list: **TBD (chốt sau)**.
