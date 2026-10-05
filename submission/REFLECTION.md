# Reflection — Lab 19

**Tên:** _Đàm Quang Sơn_
**Cohort:** _4_
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Exact queries:** BM25 và Hybrid cùng đạt Precision@10 cao nhất (96.7%), vượt Semantic (88.7%). Lý do: Từ khóa đặc thù khớp chính xác theo tần suất thuật ngữ (TF-IDF), không bị nén mờ vector.
- **Paraphrase queries:** BM25/Hybrid giữ vị trí dẫn đầu; RRF giúp phân bổ thứ hạng ổn định khi truy vấn diễn đạt khác từ vựng gốc.
- **Mixed queries:** Hybrid thắng tuyệt đối (100% vs BM25 97.0%, Semantic 98.5%). RRF (k=60) kết hợp hoàn hảo giữa từ khóa chính xác và ngữ nghĩa ngữ cảnh. Chung cuộc toàn bộ 50 queries: Hybrid (78.6%) thắng BM25 (77.8%) và Semantic (73.2%).

**Khi KHÔNG dùng Hybrid:**
- **Pure BM25:** Khi truy vấn là mã SKU, mã lỗi, số hiệu hợp đồng, hoặc hệ thống yêu cầu độ trễ cực thấp (< 2ms) không muốn tốn chi phí/tài nguyên inference mô hình embedding.
- **Pure Vector:** Khi tìm kiếm cross-lingual (đa ngôn ngữ), đa phương thức (multimodal), hoặc câu hỏi mang tính khái niệm trừu tượng không có bất kỳ từ khóa trùng lặp nào với tài liệu.

---

## Điều ngạc nhiên nhất khi làm lab này

Filtered-ANN giúp giữ Recall 100% khi filter chọn lọc cao (<1%), trong khi post-filter bị sập hoàn toàn về 0% do ANN kéo toàn bộ top-K vào các cụm bị filter loại bỏ.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với:
