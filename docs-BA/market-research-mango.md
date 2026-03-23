# Market Research: Mango — Khám phá quán ăn gần tôi (MVP: ăn uống)

**Date:** 23/03/2026  
**Author:** Yuki  
**Related PRD:** `docs-BA/PRD/ba-prd-mango-restaurant-discovery.md`  

---

## 1. Executive Summary

**Insight 1 (Trust & decision):** Người dùng hiện dựa nhiều vào review rời rạc (đặc biệt từ Google Maps) nên khó so sánh nhanh theo tiêu chí mong muốn. Vì vậy, “chuẩn hoá review + ranking rõ ràng theo nhu cầu” là đòn bẩy trực tiếp giảm thời gian ra quyết định.

**Insight 2 (Community signals):** Các tín hiệu như “vote hữu ích”, vote up/down, và moderation khi có báo xấu là các yếu tố quyết định chất lượng nội dung và mức tin tưởng.

**Insight 3 (Table booking — Phase3):** Nhu cầu đặt bàn sẽ xuất hiện rõ hơn sau khi đã có tệp users browsing/review. Thách thức chính nằm ở “tính sẵn có dữ liệu trạng thái bàn/khả năng đặt” và độ tin cậy của luồng đặt chỗ.

**Top recommendation:** Tập trung validate mạnh nhất cho vòng lặp “browsing -> xem review chuẩn hoá -> ra quyết định nhanh” trong MVP; song song chuẩn bị research riêng cho tính năng đặt bàn (dự kiến Phase 3) để tránh xây sai dữ liệu & UX.

**Next steps (sau desk research — để chốt quyết định):**
- Chọn 3 luồng MVP cần validate sớm nhất: `list -> detail -> review breakdown`, `review -> vote/helpful`, và `subscription gating`.
- Lên danh sách requirement tối thiểu cho Phase 3 booking (availability confidence, timeout/cancel policy, deposit/no-show logic).
- Làm primary research “nhanh gọn” theo dạng usability/short interviews để hiệu chỉnh assumption (không bắt buộc trong report này).

---

## 2. Research Methodology

### Research Questions (Draft 8 câu hỏi ưu tiên)
**Market questions**
- Quy mô/độ tăng trưởng của nhu cầu “tìm quán ăn gần tôi” tại Hà Nội (online discovery vs offline)?
- Xu hướng người dùng chuyển từ review rời rạc sang “nền tảng tổng hợp có xếp hạng” như thế nào?

**User questions**
- Người dùng hiện đang ra quyết định bằng những bước nào (Google Maps / group / hỏi bạn bè / website quán)?
- Pain điểm lớn nhất là gì: thiếu chuẩn hoá review, thiếu cá nhân hoá, hay thiếu “độ tin”?
- Người dùng sẵn sàng trả bao nhiêu (hoặc chấp nhận subscription gating) để xem danh sách/browsing không?

**Competitive questions**
- Đối thủ giải bài toán discovery bằng UX/tín hiệu trust như thế nào (điểm tổng hợp, helpful vote, moderation)?
- Chỗ trống (gap) nào thị trường đang bỏ ngỏ: chuẩn hoá tiêu chí, tốc độ ra quyết định, hay cơ chế community?

### Methods (desk research only)
- Thu thập và tổng hợp thông tin công khai từ: website/app store listing, trang tính năng/FAQ, bài viết chính thức/PR, và báo cáo/điểm tổng hợp công khai.
- Đọc và đối chiếu với PRD: xác định điểm “table stakes” (discovery, review, trust) và khoảng trống (structured scoring, vote helpful, booking availability confidence).
- Dùng nguồn nghiên cứu/phân tích công khai để hỗ trợ insight (ví dụ: ảnh hưởng của online reviews và rủi ro fake reviews).

### Limitations
- Do chỉ desk research, các kết luận về “willingness to pay” và “booking acceptance” là giả thuyết dựa trên hành vi thị trường (subscription gating, vouchers, booking pilots), cần xác nhận bằng primary research sau đó.

---

## 3. Market Overview

### Market scope (Draft)
- **Geography:** Toàn Việt Nam (ban đầu ưu tiên các đô thị lớn, nhưng báo cáo này xét scope VN).
- **Category:** Discovery quán ăn theo vị trí + review có cấu trúc (bao gồm vote/helpful và moderation) + gating subscription 6 tháng.
- **Adjacency (Phase 3):** đặt bàn/đặt chỗ khi có bàn trống (availability confidence).

### Market sizing (TAM/SAM/SOM) — placeholder
> Lưu ý: Với desk research, phần “tính tiền” cho discovery/review là không trực tiếp đo được. Vì vậy, TAM dùng **proxy** từ thị trường online F&B (đặt món/đặt bàn) để phản ánh mức độ sẵn sàng dùng kênh online.

- **TAM (proxy):** Thị trường **online food delivery** tại Việt Nam được báo cáo đạt khoảng **$968M (2024)** và có ước tính lên **$2.1B (2025)**; dự báo có thể đạt **$3.22B vào 2033** (CAGR ~13.58%). Nền tảng: sự dịch chuyển sang kênh online cho “quyết định ăn gì/ở đâu” đang tăng nhanh.
- **SAM (discovery + dine-in/booking):** Các đô thị nơi người dùng sẵn sàng đặt/duyệt nhà hàng qua app: **Hà Nội, TP.HCM, Đà Nẵng và các TP lớn**. Nhóm này có khả năng áp dụng nhanh vote/helpful, subscription và tích hợp booking.
- **SOM (MVP 12–18 tháng):** Mục tiêu thực tế cho Mango nên là chiếm **một phần nhỏ của traffic discovery chất lượng** (users browsing quán -> mở detail -> đọc review breakdown) trước, sau đó mới mở rộng conversion sang booking. Con số cụ thể cần primary/analytics để chốt (desk research chỉ đưa khung).

### Key trends (Draft)
- **Online F&B tăng trưởng và chuẩn hoá discovery qua app:** các nền tảng lớn đang mở rộng danh mục và “dine out/đặt bàn” để chiếm trọn hành trình quyết định.
- **Trust layer là lợi thế cạnh tranh:** rủi ro fake reviews và “quảng cáo trá hình” khiến người dùng ngày càng cần tín hiệu tin cậy (vote/report/moderation) thay vì chỉ sao.
- **Review dần chuyển từ text/photo không cấu trúc sang decision support:** người dùng tìm cơ chế “so sánh nhanh” theo tiêu chí (món/giá/phục vụ/không gian/vệ sinh), dù nhiều đối thủ hiện vẫn thiên về cảm nhận.
- **Booking bắt đầu hội tụ vào discovery:** ví dụ Grab Dine Out có pilot đặt bàn tại VN; Foody và các platform đặt bàn/voucher cũng thúc đẩy “đặt ngay để tránh hết bàn”.

### PESTLE highlights (Draft)
- **Political/Legal:** ràng buộc dữ liệu/nguồn (scraping), trách nhiệm moderation nội dung và policy xử lý review sai lệch.
- **Economic:** người dùng nhạy với ưu đãi (vouchers/discounts) khi chuyển sang booking; subscription 6 tháng cần “value rõ ràng” (preview, quota, ROI).
- **Social:** thói quen xem review + ảnh/visual mạnh; community ảnh hưởng mạnh nhưng cũng tạo rủi ro thao túng (đặc biệt ở nhóm).
- **Technological:** personalization theo hành vi (affinity) cần data sạch; Phase 3 booking cần tích hợp availability + chính sách cancel/no-show để giảm fail.

---

## 4. User Insights

### Personas (dựa trên PRD, desk assumptions)

**Persona A: Người quyết định nhanh**
- **Goals:** chọn quán trong thời gian ngắn trong bán kính 5km, có điểm tổng hợp rõ ràng.
- **Pain points:** review rời rạc, khó so sánh tiêu chí; cá nhân hoá yếu.
- **Behavior:** mở app, scan list, mở 1–3 quán, đọc breakdown, vote/helpful ngẫu nhiên tuỳ trải nghiệm.
- **Technology comfort:** cao (mobile-first).
- **Quote (placeholder):** “Tôi chỉ cần biết quán nào hợp tiêu chí của tôi ngay lập tức…”

**Persona B: Reviewer/Cộng tác viên**
- **Goals:** viết review có tác động, được ghi nhận/payout theo tương tác.
- **Pain points:** thiếu động lực/không tin payout; sợ bị thao túng; quy tắc comment/vote chưa rõ.
- **Behavior:** viết review sau khi đi ăn; vote helpful; điều chỉnh nội dung theo feedback/moderation.
- **Quote (placeholder):** “Nếu thấy hệ thống công bằng, tôi sẽ đóng góp thường xuyên hơn.”

**Persona C (Adjacency cho booking — sẽ validate sau): Người cần đặt bàn**
- **Goals:** đảm bảo chỗ đúng thời điểm, giảm rủi ro “đến nơi mới biết hết”.
- **Pain points:** không biết bàn trống thật sự; đặt xong vẫn bị fail.
- **Quote (placeholder):** “Đặt được mà không chắc còn bàn thì vẫn không yên tâm.”

### JTBD statements (Draft)
- Khi tôi muốn ăn ngoài vào tối nay (situation), tôi muốn chọn nhanh quán hợp tiêu chí (motivation) để tránh mất thời gian và thất vọng (expected outcome).
- Khi tôi đã đi ăn ở một quán (situation), tôi muốn đóng góp review hữu ích và được ghi nhận/payout (expected) để cảm thấy công bằng và có tác động.
- Khi tôi cần đặt bàn cho nhóm (situation), tôi muốn biết tình trạng chỗ trống một cách đáng tin cậy (expected) để giảm rủi ro và chủ động kế hoạch.

---

## 5. Competitive Landscape

### 5.1 Competitive set (đối thủ giải cùng “job”: tìm nơi ăn + giảm rủi ro chọn sai)

| Đối thủ | Điểm mạnh (desk research) | Điểm yếu (desk research) | Bài học cho Mango |
|---|---|---|---|
| `Google Maps` | Quy mô phủ cực rộng, UGC dày (rating, ảnh, review), dễ tìm qua search/SEO, trải nghiệm discovery nhanh. | Review/tiêu chí chưa được chuẩn hoá để “so sánh nhanh theo nhu cầu”; khó filter theo breakdown 5 thang; độ nhiễu/fake/misleading tồn tại theo thời gian; booking phụ thuộc từng nơi. | Mango cần “decision support layer”: review có cấu trúc + ranking giải thích được theo tiêu chí người dùng. Trust phải rõ ràng, không chỉ dựa vào số sao. |
| `Foody` | Có discovery local và **đặt bàn** qua nền tảng: hotline hoặc tab “Đặt chỗ/Đặt bàn” trên trang nhà hàng, Foody xác nhận/liên hệ, kèm ưu đãi. | Cơ chế booking thường thiên về “liên hệ/xác nhận” hơn là availability tức thì; review có thể thiên về cảm nhận/ảnh, chưa tối ưu để so sánh theo thang mục tiêu như MVP Mango. | Khi vào Phase 3, cần thiết kế booking theo hướng “availability confidence” và SLA/logic cancel/no-show rõ ngay trong UX. Với MVP, giữ chuẩn review breakdown để khác biệt cốt lõi. |
| `Lozi` | Image-first discovery, “quanh đây”/gợi ý theo món & trải nghiệm, cộng đồng chia sẻ mạnh. | Không phải nền tảng đặt bàn; decision support theo tiêu chí (giá/không gian/vệ sinh...) chưa “chuẩn hóa để ra quyết định nhanh”. | Mango có thể học “visual browsing” từ Lozi nhưng vẫn ép tối thiểu cấu trúc review để biến ảnh thành thông tin so sánh. |
| `Grab Dine Out` | Nâng dine-in lên app lớn: có pilot đặt bàn ở VN, người dùng có menu + xem review và voucher trước khi đến. | Là hệ sinh thái giao đồ ăn/delivery; booking phụ thuộc nhà hàng/đối tác; tín hiệu trust có thể không được tối ưu riêng cho “chọn quán để ăn tại chỗ”. | Mango nên tách rõ 2 layer: (1) review breakdown + trust riêng cho ăn tại chỗ, (2) booking chỉ là “conversion layer” sau khi người dùng đã tin vào quyết định. |
| `Mytour (table.mytour.vn)` | Là kênh đặt bàn có search/filter theo rating, khoảng cách, danh mục; có voucher/ưu đãi rõ ràng, phủ toàn quốc. | Tính “community review chuẩn hoá” để so sánh theo tiêu chí có thể không sâu như marketplace review; availability confidence/cơ chế xác nhận có thể không minh bạch theo mức độ realtime. | Mango cần thể hiện rõ trạng thái chỗ trống (hoặc độ tin cậy) + chính sách huỷ/không đến để giảm “fail booking”. Review structured phải là thứ dẫn người dùng tới booking. |
| `Tripadvisor` | Có cơ chế moderation/report minh bạch hơn; có chính sách loại bỏ review giả/AI và chống review rác. | Discovery “gần tôi” và personalization theo tiêu chí địa phương có thể không mạnh bằng app bản địa; ở VN vẫn có vấn đề fake review (đòi hỏi trust layer mạnh). | Mango nên đầu tư moderation + transparency như một phần sản phẩm, không chỉ “admin xử lý”; có chính sách rõ với AI/fake và cơ chế báo cáo/điều tra nhất quán. |
| `Facebook/Zalo groups` | Cộng đồng thật, khuyến nghị theo tình huống, tốc độ lan truyền cao. | Khó scale theo chuẩn; rủi ro thao túng/bịa đặt (đặc biệt ở nhóm có admin can thiệp); nội dung thường không có cấu trúc để ra quyết định nhanh. | Mango phải “productize community”: verification/anti-manipulation + review structured + tín hiệu trust có thể kiểm chứng. |

### 5.2 Strategic gap analysis (Mango nên thắng ở đâu)
- **Gap 1: Standardized review as decision support**: biến UGC thành hệ thống so sánh theo thang mục tiêu (MVP review breakdown 5 thang) thay vì chỉ rating/text.
- **Gap 2: Trust signals that are user-actionable**: “vote helpful” + moderation report/policy phải nhìn thấy được (và có tác dụng), để giảm rủi ro fake/quảng cáo trá hình.
- **Gap 3: Booking with availability confidence**: thay vì chỉ “gửi yêu cầu/đợi xác nhận”, Phase 3 cần hiển thị rõ mức độ còn bàn và chính sách cancel/no-show để giảm fail.

---

## 6. Synthesis & Opportunities

### Key findings (Draft format)
1. **[INSIGHT]** Review online (đặc biệt có thông tin/ảnh chi tiết) có tác động trực tiếp đến ý định chọn nhà hàng tại Việt Nam.  
   **[EVIDENCE]** Nghiên cứu với 466 người dùng online VN cho thấy “perceived importance” của online reviews ảnh hưởng đến ý định sử dụng review khi chọn nơi ăn; chất lượng nội dung và cue trực quan (ảnh) làm tăng độ tin.  
   **[IMPLICATION]** Mango nên tối ưu “decision support”: review phải có cấu trúc, có tiêu chí so sánh được; ảnh nên được dùng như evidence chứ không chỉ trang trí.  
   **[RECOMMENDATION]** Ưu tiên `FR-001/FR-002/FR-004/FR-005` để giảm time-to-decision bằng ranking + breakdown rõ ràng.

2. **[INSIGHT]** Rủi ro fake review/quảng cáo trá hình làm trust trở thành biến số sống còn; platform càng “cởi mở” UGC càng cần trust layer có cơ chế và minh bạch.  
   **[EVIDENCE]** Tripadvisor công bố transparency report về moderation (tỉ lệ bị reject trước khi lên public, và cơ chế chống review giả/AI). Các bài tổng hợp cũng cho thấy Vietnam nằm trong nhóm quốc gia bị phát hiện nhiều review giả. Ngoài ra, có ghi nhận thao túng trong community nhóm review (admin can thiệp/bịa đặt).  
   **[IMPLICATION]** `vote helpful` + `report/moderation` phải là tính năng “để người dùng hành động”, không chỉ là admin backoffice.  
   **[RECOMMENDATION]** Ưu tiên `FR-008/FR-009/FR-016` (tối thiểu: report rõ ràng + policy + audit trail) từ MVP.

3. **[INSIGHT]** Dine-in/đặt bàn đang “được app hoá” (booking trở thành một bước trong hành trình khám phá), nhưng availability confidence vẫn là điểm thất bại nếu không có policy/ops rõ.  
   **[EVIDENCE]** Grab Dine Out đã chạy pilot tính năng đặt bàn tại các city lớn; Foody và Mytour đều thúc đẩy booking qua app và kèm voucher/ưu đãi để tăng conversion.  
   **[IMPLICATION]** Phase 3 “đặt bàn khi thấy bàn trống” cần cơ chế đảm bảo/giảm rủi ro (ví dụ: thời hạn xác nhận, cancel/no-show, có thể dùng deposit ở mức phù hợp).  
   **[RECOMMENDATION]** MVP tập trung discovery+trust; Phase 3 pilot theo năng lực availability, không mở rộng khi dữ liệu chưa đủ tin cậy.

4. **[INSIGHT]** Tailwind tăng trưởng của kênh online trong F&B ở VN đủ mạnh để Mango có “market pull”, nhưng người dùng sẽ kỳ vọng app phải làm được phần việc trust và quyết định nhanh.  
   **[EVIDENCE]** Thị trường online food delivery VN tăng nhanh (báo cáo năm 2025 tăng mạnh và dự báo dài hạn).  
   **[IMPLICATION]** Mango nên cạnh tranh bằng “lý do khác” với delivery (structured review + trust + decision logic cho ăn tại chỗ) thay vì chỉ chạy danh mục/ưu đãi.  
   **[RECOMMENDATION]** Tối ưu UX cho list-first -> detail -> review breakdown -> vote trước khi nghĩ tới booking scale.

### Opportunity list (ICE — placeholder)
| Opportunity | Impact (1-10) | Confidence (1-10) | Ease (1-10) | ICE Score |
|---|---:|---:|---:|---:|
| Structured review breakdown + ranking theo tiêu chí (decision support) | 9 | 7 | 6 | 7.56 |
| Trust layer user-actionable: vote helpful + report + moderation policy | 8 | 6 | 5 | 4.8 |
| Subscription gating với value hook (preview/quota rõ ràng) | 6 | 4 | 6 | 4.0 |
| Phase 3 booking có availability confidence + cancel/no-show logic | 7 | 4 | 3 | 2.8 |

### Prioritized recommendations (Draft)
- Priority 1: MVP làm tốt “time-to-decision” bằng review breakdown + ranking rõ ràng.
- Priority 2: Trust layer phải thể hiện cơ chế hành động của user (helpful/report) và policy xử lý sai lệch.
- Priority 3: Booking (đặt bàn khi bàn trống) chỉ mở rộng theo mức độ availability confidence và chính sách giảm rủi ro fail.

---

## 7. Appendix

### Open items / Data gaps
- Cần xác nhận: định lượng willingness-to-pay và cách subscription gating tạo “value perception” (preview limit/quota) cho từng persona.
- Cần xác nhận: khả năng lấy dữ liệu availability (realtime hay near-realtime), SLA vận hành và chính sách cancel/no-show để Phase 3 “bàn trống” không gây fail.
- Cần xác nhận: thiết kế moderation UX (minh bạch đến đâu, phản hồi report tới user ra sao) để đạt niềm tin và giảm “report fatigue”.

### Sources
- Online F&B market proxy (online food delivery VN): https://www.globenewswire.com/news-release/2025/09/12/3149130/28124/en/Vietnam-Online-Food-Delivery-Market-Trends-and-Forecast-Report-2025-2033-Competitive-Analysis-of-Vietnammm-com-Foody-vn-Now-vn-Eat-vn-and-Grab-Food.html
- Foody đặt bàn: https://www.foody.vn/bai-viet/dat-ban-qua-foody-that-tien-loi-voi-nhieu-uu-dai-hap-dan-687
- Lozi là nền tảng chia sẻ review (không tập trung đặt bàn): https://reatimes.vn/print/lozi-va-foody-dau-la-lua-chon-cua-nguoi-yeu-am-thuc-20214219.htm
- Grab Dine Out (dine-in/đặt bàn): https://www.grab.com/vn/en/food/dine-out/
- Grab Dine Out pilot tại VN (thông tin pilot): https://www.vietnam.vn/en/grabfood-thu-nghiem-tinh-nang-an-tai-nha-hang
- Mytour table booking: https://table.mytour.vn/
- Tripadvisor moderation transparency & chống fake/AI: https://ir.tripadvisor.com/news-releases/news-release-details/tripadvisor-content-moderation-transparency-report-reveals-new
- Vietnam fake reviews (tổng hợp): https://www.vietnam.vn/en/bao-cao-minh-bach-cua-tripadvisor-danh-gia-bang-ai-van-chua-duoc-chap-nhan
- Online reviews ảnh hưởng ý định chọn nhà hàng VN: https://tamucc-ir.tdl.org/items/2f439f7e-1091-4ff0-9941-a7031986fbd5
- Bịa đặt/thao túng trong nhóm review: https://znews.vn/lo-tin-nhan-admin-nhom-review-do-an-dung-canh-boi-xau-nha-hang-post947104.html
- Bài học booking policy/mitigation no-show (deposit reference): https://www.opentable.com/restaurant-solutions/resources/nowserving-deposits/

