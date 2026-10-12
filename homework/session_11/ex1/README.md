# Hướng Dẫn Nộp Bài 1 (`homework/session_11/ex1/`)

## 1. Sản phẩm trong thư mục nộp bài
- Tệp kịch bản [`.github/workflows/ci.yml`](./.github/workflows/ci.yml) được cấu hình đầy đủ theo đúng yêu cầu đề bài:
  - Kích hoạt khi `push` lên nhánh `main`.
  - Job `test` (`name: Run Unit Tests`) chạy trên `ubuntu-latest`.
  - Sử dụng `actions/checkout@v5` để checkout mã nguồn.
  - Sử dụng `actions/setup-java@v5` với `java-version: '17'` và `distribution: 'temurin'`.
  - Cấp quyền thực thi `chmod +x gradlew` và chạy kiểm thử `./gradlew test`.

## 2. Hướng dẫn chụp ảnh màn hình GitHub Actions
1. Đẩy toàn bộ dự án lên nhánh `main` của GitHub Repository:
   ```bash
   git init
   git add .
   git commit -m "feat(ex1): setup GitHub Actions workflow for Spring Boot Gradle unit tests"
   git branch -M main
   git remote add origin <URL_GITHUB_REPO_CUA_BAN>
   git push -u origin main
   ```
2. Mở tab **Actions** trên GitHub Repository -> Chọn lần chạy của workflow **Java Spring Boot CI (Gradle)**.
3. Nhấn vào Job **Run Unit Tests** để hiển thị chi tiết các step tích xanh.
4. Chụp ảnh màn hình và lưu vào thư mục `homework/session_11/ex1/` (ví dụ: `homework/session_11/ex1/github-actions-success.png`).
