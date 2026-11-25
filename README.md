# srs-agmt-functional-matrix

**AG-MT** · Agent Node · phiên bản **1.1.0** · giấy phép MIT

> Vietnamese-language Claude skill — one independent, reusable service of the SRS-SOP agent pipeline. Machine-readable contract: [`skill.json`](skill.json).

Agent Node AG-MT (Bước B5a SOP viết SRS, chỉ dự án khách đã có phần mềm): lập ma trận chức năng hiện trạng — đối chiếu từng yêu cầu nguyên tử và từng mã yêu cầu của khách với phần mềm đang chạy, danh mục chức năng hiện có, chức năng ngoài yêu cầu, chức năng × vai trò, và kết luận đáp ứng theo từng mã yêu cầu của khách (RTM TL-04 tra theo mã KH). Dùng khi mô tả ngược hoặc kê khai đáp ứng cho một hệ thống đã có.

## Hợp đồng giao tiếp

Skill là một dịch vụ độc lập, ghép lỏng: nhận đầu vào và trả đầu ra dưới dạng tài liệu/JSON mô tả trong [`SKILL.md`](SKILL.md), không gọi trực tiếp skill khác và không gắn với dự án cụ thể. Dùng riêng lẻ, hoặc ghép qua bộ điều phối [`srs-sop-pipeline`](https://github.com/HaNguyen1409/srs-sop-pipeline).

| Bước SOP | Việc | Loại | Nhận từ | Chuyển tới |
|---|---|---|---|---|
| 5a | Ma trận chức năng hiện trạng — chỉ dự án đã có phần mềm (mục 11): danh mục chức năng hệ thống × REQ × vai trò, cột đáp ứng | Code + Agent | B2 (SRC hệ thống), B5 | B5 (RTM: cột đáp ứng theo mã KH), B6, B8, B8a, B9, B12 |

**Sản phẩm đầu ra:** Ma trận chức năng hiện trạng (kết luận đáp ứng theo mã yêu cầu dùng cho RTM TL-04)

**Skill phía sau (dùng đầu ra):** [`srs-ag03-gap-analysis`](https://github.com/HaNguyen1409/srs-ag03-gap-analysis) `^2.2.1` · [`srs-ag05-feature-matrix`](https://github.com/HaNguyen1409/srs-ag05-feature-matrix) `^2.0.0` · [`srs-agtq-project-overview`](https://github.com/HaNguyen1409/srs-agtq-project-overview) `^1.1.0` · [`srs-ag06-business-model`](https://github.com/HaNguyen1409/srs-ag06-business-model) `^1.4.2` · [`srs-ag07-screen-flow-design`](https://github.com/HaNguyen1409/srs-ag07-screen-flow-design) `^1.0.0`

## Cài đặt

**Claude Code** — clone đúng phiên bản vào thư mục skill:

```bash
git clone --branch v1.1.0 https://github.com/HaNguyen1409/srs-agmt-functional-matrix.git ~/.claude/skills/srs-agmt-functional-matrix
```

Nâng cấp: `git -C ~/.claude/skills/srs-agmt-functional-matrix fetch --tags && git -C ~/.claude/skills/srs-agmt-functional-matrix checkout v<phiên-bản-mới>`.

**claude.ai / Claude Desktop** — tải `srs-agmt-functional-matrix-v1.1.0.zip` ở trang [Releases](https://github.com/HaNguyen1409/srs-agmt-functional-matrix/releases) rồi tải lên ở phần Skills trong cài đặt.

**Cả bộ** — xem [`srs-sop-skills`](https://github.com/HaNguyen1409/srs-sop-skills) (cài toàn bộ skill theo phiên bản đã khoá).

## Quản lý phiên bản

Theo [SemVer](https://semver.org/lang/vi/), áp cho hợp đồng giao tiếp của skill:

| Tăng | Khi |
|---|---|
| MAJOR | Đổi hợp đồng làm vỡ skill phía sau: đổi/bỏ trường JSON, đổi hệ mã ID, đổi bố cục tài liệu đầu ra |
| MINOR | Thêm khả năng tương thích ngược: trường tuỳ chọn, mục mới, chế độ mới |
| PATCH | Sửa câu chữ, sửa lỗi, làm rõ luật mà không đổi đầu ra |

Phát hành: sửa `SKILL.md` → tăng `version` trong frontmatter, `VERSION`, `skill.json` → thêm mục vào [`CHANGELOG.md`](CHANGELOG.md) → `python tools/check_skill.py` → commit → `git tag -a vX.Y.Z -m "vX.Y.Z"` → `git push --follow-tags`. GitHub Actions kiểm lại, chạy test và đính kèm zip vào Release.

## Giấy phép

MIT — xem [`LICENSE`](LICENSE).
