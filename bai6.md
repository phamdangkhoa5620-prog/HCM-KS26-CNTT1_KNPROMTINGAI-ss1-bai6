BÀI LÀM: QUẢN LÝ CONTEXT WINDOW – MARTX
Phần 1: Giải thích hình tượng Chiếc cốc nước
- Context Window được hiểu như một chiếc cốc nước có dung tích giới hạn, tượng trưng cho bộ nhớ ngữ cảnh ngắn hạn của AI.
- Mỗi tin nhắn của khách hàng và phản hồi của AI đều chiếm một lượng dung lượng trong cốc, được tính bằng Token.
- Khi cuộc hội thoại kéo dài, lượng Token liên tục tăng khiến chiếc cốc dần đầy.
- Khi dung lượng đạt giới hạn, hệ thống có thể thực hiện Truncation (cắt gọt dữ liệu), tức là loại bỏ một phần nội dung cũ để dành chỗ cho thông tin mới.
Áp dụng vào tình huống MartX:
- Ở lượt 1, khách hàng cung cấp tên Trần Văn B và mã đơn hàng #MTX-9988. AI vẫn ghi nhớ được thông tin này.
- Sau 40 lượt tư vấn rau củ với nhiều phản hồi dài, Context Window dần bị lấp đầy.
- Đến lượt 42, hệ thống thực hiện Truncation và loại bỏ thông tin cũ ở lượt 1.
- Vì vậy, AI không còn thấy thông tin tên và mã đơn hàng ban đầu, dẫn đến nhầm khách hàng thành chị Mai và yêu cầu cung cấp lại mã đơn.
Kết luận: AI không thực sự có trí nhớ vô hạn. Khi Context Window bị giới hạn, thông tin cũ có thể bị loại bỏ nếu không được lưu trữ riêng.
Phần 2: Phương án quản lý RAM bộ nhớ
1. Thao tác người dùng
- Tóm tắt hội thoại: Sau mỗi 10–15 lượt chat, yêu cầu AI tổng hợp thông tin quan trọng như tên khách hàng, mã đơn hàng, vấn đề đang gặp phải và hướng xử lý.
- Nhắc lại thông tin quan trọng: Khi chuyển sang chủ đề mới, cung cấp lại những dữ liệu cần thiết để AI không nhầm lẫn.
- Hạn chế câu trả lời dài: Yêu cầu AI trả lời ngắn gọn, đúng trọng tâm để tiết kiệm Token.
- Chia phiên chat: Nếu cuộc tư vấn quá dài, tạo phiên mới và cung cấp bản tóm tắt từ phiên trước.
2. Thiết kế hệ thống
- Sử dụng bộ nhớ ngoài (External Memory): Lưu thông tin khách hàng, mã đơn hàng và lịch sử giao dịch vào cơ sở dữ liệu riêng thay vì chỉ phụ thuộc vào Context Window.
- Áp dụng RAG (Retrieval-Augmented Generation): Khi khách hàng đặt câu hỏi, hệ thống tự động truy xuất thông tin liên quan từ cơ sở dữ liệu và đưa vào Context Window để AI trả lời chính xác.
- Tóm tắt tự động: Hệ thống tự động tổng hợp các nội dung quan trọng sau một số lượt hội thoại, tránh tích lũy quá nhiều Token không cần thiết.
- Ưu tiên dữ liệu quan trọng: Giữ lại tên khách hàng, mã đơn hàng, trạng thái giao dịch và yêu cầu hỗ trợ; loại bỏ những nội dung trao đổi không còn cần thiết.
Kết luận
Để tránh hiện tượng tràn Context Window, MartX cần kết hợp thao tác quản lý hội thoại của nhân viên với thiết kế hệ thống lưu trữ bộ nhớ ngoài và truy xuất dữ liệu bằng RAG.

Nguyên tắc: Không phụ thuộc hoàn toàn vào trí nhớ ngắn hạn của AI; những thông tin quan trọng phải được lưu trữ riêng để có thể truy xuất bất cứ lúc nào.