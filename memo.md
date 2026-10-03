# Memo Teardown — NOTION (Notion AI)

**Họ tên:** Lưu Xuân Dũng
**MSV:** 2A202602746
**Ngày:** 03/10/2026

**Vì sao chọn sản phẩm này:** Notion là case hiếm của nhóm "truyền thống hóa AI" mà AI đã đi trọn một vòng: từ một nút "viết hộ" (wrapper mỏng) đến agent tự chạy workflow trên chính dữ liệu của công ty. Mỗi bước đều có release note chính thức, nên dựng được chuỗi quyết định thay vì đoán mò.

---

## §1. Timeline các cập nhật lớn

| # | Thời điểm | Cập nhật | Context lúc đó | Nguyên lý |
|---|---|---|---|---|
| 1 | **16/11/2022** | **Notion AI private alpha**: trợ lý viết (draft, tóm tắt, sửa văn, dịch) ngay trong trang Notion. [Nguồn](https://www.notion.com/blog/introducing-notion-ai) | Ra mắt **2 tuần trước ChatGPT** (30/11/2022). Jasper, Copy.ai đang bán "AI viết content" thành sản phẩm riêng. Notion đã có hàng chục triệu user nhưng chưa có lớp AI. | **Wrapper mỏng đặt đúng chỗ (distribution > model)**: tính năng thuần gọi LLM, model làm được thì ChatGPT cũng làm được → giá trị *không* nằm ở output mà ở chỗ AI xuất hiện ngay nơi user đang viết, không phải copy-paste sang tab khác. Đây là nước đi chiếm vị trí, chưa phải moat. |
| 2 | **22/02/2023** | **Notion AI GA cho mọi user, bán add-on \$10/member/tháng** tách khỏi gói chính. [Nguồn](https://www.notion.com/releases/2023-02-22) · [Blog giá](https://www.notion.com/blog/notion-ai-is-here-for-everyone) | ChatGPT bùng nổ, chi phí inference cao. Microsoft chuẩn bị công bố 365 Copilot (03/2023). | **Đo willingness-to-pay / AI có chi phí biên**: khác SaaS truyền thống, mỗi lần gọi AI tốn tiền → không thể gộp miễn phí. Tách add-on để biết ai trả tiền thật cho AI và giữ margin của gói lõi. |
| 3 | **31/05/2023** | **AI Autofill trong database** (Notion 2.30): AI tự điền cột tóm tắt, action item, tag cho hàng nghìn dòng. [Nguồn](https://www.notion.com/releases/2023-05-31) | ChatGPT chỉ làm việc với một khung chat, không hiểu "dòng/cột". Notion đang đẩy mảng project management. | **Embedded AI vào cấu trúc dữ liệu có sẵn (thoát khỏi wrapper)**: AI không còn là ô chat mà chạy *trên schema* của user. Model thế hệ sau không hấp thụ được vì nó không sở hữu database đó → bắt đầu có lớp moat từ workflow. |
| 4 | **14/11/2023** | **Q&A by Notion AI** (beta, Notion 2.35): hỏi bằng ngôn ngữ tự nhiên, AI trả lời từ *toàn bộ workspace*, có trích dẫn trang gốc. [Nguồn](https://www.notion.com/releases/2023-11-14) | OpenAI vừa ra GPTs + upload file (DevDay 11/2023); Glean đang bán enterprise search cho công ty lớn. | **Data moat / System of Record + quy tắc x10**: ChatGPT giỏi hơn về model nhưng *không có* wiki, spec, meeting note của công ty. Tìm thông tin nội bộ từ "lục 10 phút / hỏi đồng nghiệp" → "hỏi 1 câu, có link nguồn" là cải thiện x10 cho đúng một job. |
| 5 | **25/09/2024** | **"New Notion AI"** (2.45): gộp search–generate–analyze–chat vào một chỗ, **AI Connectors** đọc Slack, Google Drive; phân tích PDF/ảnh. [Nguồn](https://www.notion.com/releases/2024-09-25) | Claude/GPT-4o làm tốt multimodal; dữ liệu công ty nằm rải rác ở nhiều tool, Notion chỉ chứa một phần. | **Mở rộng biên moat: từ "data trong Notion" sang "context của cả công ty"**: nếu moat là dữ liệu, thì càng gom nhiều nguồn context thì AI càng khó thay. Chấp nhận đọc dữ liệu tool khác để trở thành *điểm hỏi duy nhất*. |
| 6 | **13/05/2025** | **Notion 2.51 / "Notion AI for Work"**: AI Meeting Notes, Enterprise Search, Research Mode; **bỏ add-on, AI không giới hạn chỉ có trong gói Business & Enterprise**. [Nguồn](https://www.notion.com/releases/2025-05-13) | Granola, Otter làm AI meeting note rất mạnh; Glean làm enterprise search; Microsoft/Google bundle Copilot/Gemini vào gói Workspace. | **Bundling + đổi người trả tiền (cá nhân → công ty)**: AI chuyển từ "add-on cho ai thích" thành *lý do nâng gói* lên Business. Đồng thời **meeting notes là cửa nạp dữ liệu mới**: mỗi cuộc họp tự tạo thêm context cho search/Q&A → vòng lặp dữ liệu (data flywheel). |
| 7 | **18/09/2025** | **Notion 3.0: Agents** — agent tự làm việc nhiều bước (tạo trang, dựng database, cập nhật hàng loạt), có trang "instructions" làm bộ nhớ. [Nguồn](https://www.notion.com/releases/2025-09-18) | Cả ngành chuyển từ "chat" sang "agent" (Claude, ChatGPT agent mode, MCP phổ biến). | **Định nghĩa lại "tốt": từ trả lời đúng → làm xong việc**. Agent của Notion mạnh hơn agent chung vì *đã có sẵn* nơi lưu kết quả (page/database) và context (workspace + connectors). Moat workflow được dùng làm nền cho agent. |
| 8 | **24/02/2026** | **Notion 3.3: Custom Agents** — agent chạy nền theo lịch hoặc trigger (triage task, trả lời Q&A nội bộ, viết status report), chia sẻ cho cả team. [Nguồn](https://www.notion.com/releases/2026-02-24) | Doanh nghiệp bắt đầu đòi "AI teammate" thay vì "AI assistant"; cạnh tranh với automation (Zapier) và agent builder. | **Vòng lặp học ở cấp tổ chức + Vertical theo workflow**: mỗi team tự đóng gói *domain expertise* của mình (quy trình, tiêu chuẩn) vào instructions của agent → giá trị nằm ở tri thức quy trình mà model nền không có. Từ đây Notion bán *lao động số*, không chỉ bán chỗ ghi chú. |

**Vì sao chọn những mốc này:** Tôi chọn mốc theo tiêu chí "có đổi *vị trí của AI* hoặc *người trả tiền* không": 8 mốc trên vẽ ra một đường đi rõ — viết hộ (1) → kiếm tiền (2) → AI trên dữ liệu có cấu trúc (3) → AI hiểu cả workspace (4–5) → AI là lý do mua gói công ty (6) → AI tự làm việc (7–8). Tôi **loại** các mốc: *AI prompt yêu thích (08/2023)* và *chat history / GPT-4 trong Notion (2024)* vì chỉ là cải thiện UX, không đổi moat hay segment; *Notion Calendar (01/2024)* và *Notion Mail / Forms (10/2024)* vì là mở rộng sản phẩm không lấy AI làm trung tâm — chúng quan trọng với chiến lược "all-in-one" nhưng không phải quyết định về AI.

---

## §2. Tệp user & JTBD

| | Early adopters (11/2022 – 2023) | Tệp hiện tại (2025 – 2026) |
|---|---|---|
| **Đặc điểm** | Người dùng Notion cá nhân sẵn có: creator/blogger viết newsletter, freelancer, sinh viên quản lý note, "productivity nerd" theo dõi Twitter tech và Product Hunt; gói Free/Plus, tự trả tiền bằng thẻ cá nhân. *Ví dụ người thật:* một content writer freelance viết 3 bài blog/tuần, đã dùng Notion làm content calendar. | Team 20–500 người ở startup/scale-up công nghệ dùng Notion làm wiki + project tracker: Product Manager, Ops/HR lead, Engineering manager. Người trả tiền là **công ty** (gói Business/Enterprise), người quyết định là IT/Ops. *Ví dụ người thật:* PM ở một startup SaaS 80 người, mỗi tuần phải tổng hợp tiến độ từ 5 team và trả lời câu hỏi lặp lại của nhân viên mới. |
| **JTBD chính** | "Khi phải viết bài mà đang bí ý, tôi muốn có bản nháp đầu tiên ngay trong chỗ tôi đang viết, để không mất 30 phút nhìn trang trắng." | "Khi sếp/nhân viên mới hỏi 'dự án X đang ở đâu, quy định Y thế nào', tôi muốn có câu trả lời đúng kèm link nguồn trong vài giây, để không phải lục 5 tool hay làm phiền đồng nghiệp." · "Sau mỗi cuộc họp, tôi muốn biên bản và việc cần làm tự nằm đúng chỗ, để không ai quên follow-up." |
| **Trước đó họ làm bằng cách nào** | Tự viết từ đầu; hoặc mở ChatGPT/Jasper ở tab khác rồi copy-paste qua lại. | Search thủ công trong Notion/Slack/Drive; nhắn hỏi trên Slack; ghi biên bản tay hoặc dùng bot riêng (Otter, Granola); trả tiền thêm cho Glean để search toàn công ty. |

**Dịch chuyển tệp:** Hai mốc gây dịch chuyển rõ nhất là **Q&A (mốc 4, 11/2023)** và **bundling vào gói Business (mốc 6, 05/2025)**. Mốc 4 đổi *job*: giá trị của AI không còn là "viết hộ một người" mà là "hiểu tri thức của cả nhóm" — và giá trị này tăng theo số người cùng ghi vào workspace, nên tự nhiên nghiêng về team. Mốc 6 đổi *người trả tiền*: khi AI đầy đủ chỉ có ở gói Business, user cá nhân bị đẩy xuống mức dùng thử, còn công ty trở thành khách hàng chính. Job "viết nháp" của early adopters bị ChatGPT/Claude hấp thụ gần hết (đúng dự báo "wrapper mỏng là feature chờ bị hấp thụ"), nên Notion phải dịch sang chỗ mà chatbot chung không với tới: dữ liệu nội bộ.

**Switching cost (map 4 forces)** — nhìn từ góc một công ty đang cân nhắc *rời Notion* sang Microsoft 365 Copilot / Google Workspace + Gemini:

| Lực | Nội dung | Mạnh/yếu |
|---|---|---|
| **Push** (vấn đề với cái hiện tại) | Gói Business đắt hơn khi AI bị bundle bắt buộc; Notion chậm với workspace lớn; công ty đã trả tiền M365/Google nên Notion AI thành "trả hai lần". | Trung bình, đang tăng |
| **Pull** (sức hút cái mới) | Copilot/Gemini đã có sẵn trong email, lịch, file Office mà công ty đang dùng; IT chỉ quản một nhà cung cấp. | Trung bình |
| **Habit** (thói quen giữ lại) | Toàn bộ wiki, spec, database dự án, template, liên kết giữa các trang nằm trong Notion; nhân viên quen cấu trúc block/database; agent và instructions đã được cấu hình theo quy trình team. | **Mạnh nhất** |
| **Anxiety** (nỗi lo khi chuyển) | Migrate mất định dạng database/relation; mất lịch sử; agent phải dựng lại từ đầu; lo đứt quy trình trong thời gian chuyển. | Mạnh |

**Lực giữ mạnh nhất là Habit gắn với dữ liệu** (data gravity): user không ở lại vì AI của Notion giỏi hơn, mà vì AI của Notion *là AI duy nhất đọc được dữ liệu đó trong đúng cấu trúc đó*. **Nếu lực này biến mất** — ví dụ chuẩn MCP/connector khiến Copilot hoặc Claude đọc được workspace Notion tốt như chính Notion AI — thì Notion AI quay về vị trí wrapper, và user sẽ giữ Notion làm "kho dữ liệu" nhưng dùng AI của bên khác. Đây là rủi ro lớn nhất của chiến lược hiện tại.

---

## §3. Ba dự đoán hướng đi (10/2026 – 10/2027)

**Dự đoán 1** *(loại: mở rộng tính năng)*
- **Dự đoán:** Notion sẽ ra **thư viện agent dựng sẵn theo phòng ban** (HR onboarding, triage support ticket, sprint report cho engineering) và cho phép chia sẻ/bán agent trên Marketplace giống cách đang làm với template.
- **Lập luận:** Mốc 7–8 đã có hạ tầng agent nhưng mỗi team phải tự viết instructions — rào cản lớn với PM/Ops không rành prompt (tệp hiện tại ở §2). Notion từng giải đúng bài toán này cho template bằng Marketplace; đóng gói *domain expertise* thành agent dựng sẵn là bước Vertical AI tự nhiên của mốc 8.

**Dự đoán 2** *(loại: thay đổi mô hình kiếm tiền)*
- **Dự đoán:** Notion sẽ chuyển dần sang **giá tính theo mức dùng/kết quả cho agent** (credits theo số lần chạy hoặc số tác vụ hoàn thành), tách khỏi giá theo đầu người (per seat).
- **Lập luận:** Mốc 2 cho thấy Notion luôn tách AI ra khi chi phí biên cao; agent chạy nền theo lịch (mốc 8) tốn inference *không phụ thuộc số người*, nên giá per seat của mốc 6 không còn khớp chi phí. Người trả tiền đã là công ty (§2), mà công ty quen mua "lao động số" theo sản lượng. *(Ghi chú: kết quả search cho thấy Custom Agents đã có tín hiệu tính phí theo "Notion Credits" từ 05/2026 — tôi chưa mở được trang gốc để kiểm chứng, nên coi đây là dữ kiện củng cố, không phải căn cứ chính.)*

**Dự đoán 3** *(loại: đe dọa Big Tech)*
- **Dự đoán:** Trước sức ép từ Copilot/Gemini, Notion sẽ **mở workspace thành "context server" cho AI bên ngoài** (đẩy mạnh MCP, cho Claude/ChatGPT đọc–ghi Notion) đồng thời giữ lại các tính năng chỉ chạy trong Notion như agent nền, phân quyền theo dòng, audit log — tức chấp nhận "AI nào cũng dùng Notion làm bộ nhớ" thay vì cố thắng ở model.
- **Lập luận:** §2 chỉ ra moat thật là dữ liệu + cấu trúc (Habit), không phải model; mốc 5 và mốc 7 cho thấy Notion đã chọn mở connector ra ngoài. Nếu đóng lại, user sẽ bị Push sang Big Tech vì "trả hai lần"; nếu mở, Notion biến rủi ro lớn nhất (AI bên ngoài đọc được dữ liệu) thành lợi thế: mọi AI đều phải đi qua Notion.

**Dự đoán tự tin nhất:** Dự đoán 1 — vì nó là phần nối trực tiếp của mốc 8 và một pattern Notion đã từng làm thành công (Marketplace template). **Giả định có thể làm nó gãy:** user doanh nghiệp thật sự *tin* giao việc cho agent chạy nền. Nếu agent hay sai và lực Anxiety (sợ AI làm hỏng dữ liệu) tăng lên, Notion sẽ phải lùi về hướng "AI gợi ý, người duyệt" thay vì mở rộng agent tự động.

---

## §4. AI Log

| Việc | AI làm hay bạn làm? | Bạn kiểm chứng/phán đoán lại thế nào? |
|---|---|---|
| Tìm danh sách mốc ứng viên từ changelog Notion (2022–2026) | AI (trợ lý AI trong IDE Antigravity, dùng web search) | Mở từng link `notion.com/releases/...` để đối chiếu ngày tháng và tên bản release. Phát hiện AI gán nhầm một tính năng (Credits pricing) cho trang 04/05/2026, thực tế trang đó là "A new home on mobile" → không dùng làm mốc, chỉ ghi chú trong Dự đoán 2. |
| Kiểm tra chi tiết thực tế (giá add-on \$10, bundling AI vào gói Business, Autofill ở bản 2.30) | AI trích nội dung trang gốc | Đọc lại câu gốc trên trang release/blog; chỉ giữ chi tiết nào có trong trang gốc. Bỏ con số "1 triệu waitlist" vì chỉ thấy trong kết quả search, chưa thấy ở nguồn gốc. |
| Chọn 8 mốc và loại các mốc khác | Bạn, có AI đề xuất | Áp tiêu chí "có đổi vị trí của AI hoặc người trả tiền không"; loại prompt yêu thích, chat history, Calendar, Mail/Forms (lý do ở §1). |
| Gắn nguyên lý cho từng mốc | AI viết nháp, bạn sửa | So với framework Day 16 (x10, wrapper/moat, Vertical AI, vòng lặp học); sửa mốc 1 từ "moat từ workflow" thành "wrapper mỏng đặt đúng chỗ", vì lúc đó chưa có moat thật. |
| Persona early adopters vs hiện tại, JTBD | AI viết nháp, bạn sửa | Dùng thử Notion free tier; đọc review G2/Reddit (gồm review 1–2 sao) để kiểm tra JTBD có đúng việc user nói không. *(Cần tự điền: bạn đã đọc nguồn nào.)* |
| Phân tích 4 forces | Bạn, có AI hỗ trợ trình bày | Tự xác định Habit/data gravity là lực mạnh nhất và kịch bản "nếu lực này biến mất". |
| 3 dự đoán | Bạn, có AI gợi ý | Kiểm tra mỗi dự đoán có trỏ về ít nhất 1 mốc ở §1 và 1 nhận định ở §2; xác định giả định có thể làm gãy Dự đoán 1. |
| Định dạng memo, văn phong | AI | Đọc lại toàn bài, sửa chỗ diễn đạt chưa đúng ý mình. |

**Chỗ AI làm nhiều nhất:** tổng hợp timeline và viết nháp cột nguyên lý. Nếu bỏ phần đó ra, tôi vẫn giải thích được logic cả bài: Notion đi từ wrapper mỏng → AI trên dữ liệu có cấu trúc → AI là lý do mua gói công ty → agent; moat thật là dữ liệu chứ không phải model.
