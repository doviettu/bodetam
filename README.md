# Bồ đề tâm — Lên Chùa Cầu An

Game web 3D "Lên Chùa Cầu An" (một file `public/index.html`, Three.js) cùng máy chủ **phòng chùa** để nhiều người lễ chùa chung, chạy trên **Cloudflare Workers** (gói miễn phí).

- `public/index.html`: game. Chơi tại `https://bodetam.<subdomain>.workers.dev`
- `src/index.js`: Worker phục vụ game và phòng chùa (`/room/<tên>`, WebSocket). Mỗi phòng là một Durable Object, tối đa 30 người, không có chat tự do (chỉ cử chỉ, câu soạn sẵn, tặng hoa sen; tên chỉ hiện khi hai người cùng tặng nhau)
- `wrangler.toml`: cấu hình Worker

## Triển khai
Repo đã nối với Cloudflare Workers Builds: **mỗi commit lên nhánh `main` tự build & triển khai**. Xem trạng thái ở Cloudflare → Workers & Pages → `bodetam` → Deployments/Builds.

Chạy thử trên máy: `npm install` rồi `npm run dev` → mở http://localhost:8787

Kiểm tra máy chủ: mở `https://bodetam.<subdomain>.workers.dev/health`.

## Giới hạn gói miễn phí
Durable Objects: 100.000 request mỗi ngày (đặt lại lúc 7 giờ sáng giờ Việt Nam). Vượt mức thì game tự quay về chơi một mình với khách hành hương AI.

Mã nguồn phát triển & lịch sử: https://github.com/doviettu/like

## Cấu hình Cloudflare (Workers Builds)
| Mục | Giá trị |
|---|---|
| Git repository | `doviettu/bodetam` |
| Production branch | `main` |
| Build command | *(để trống)* |
| Deploy command | `npx wrangler deploy` |
| Root directory | `/` |

Tên Worker trên Cloudflare phải là `bodetam` (trùng `name` trong `wrangler.toml`).
