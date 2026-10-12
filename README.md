# Bài 1: Khởi tạo Workflow chạy Unit Test tự động cho Java Spring Boot với Gradle

## 1. Mục tiêu
- Khởi tạo tệp kịch bản **GitHub Actions Workflow** cho dự án **Java Spring Boot** sử dụng **Gradle**.
- Cấu hình môi trường **Java JDK 17 (Temurin)** và tự động chạy bài kiểm thử **JUnit Test** bằng **Gradle Wrapper** (`./gradlew test`).

---

## 2. Cấu trúc thư mục dự án

```text
SESSION11_BAI1/
├── .github/
│   └── workflows/
│       └── ci.yml                  # Kịch bản GitHub Actions CI chạy Unit Test tự động
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── homework/
│   └── session_11/
│       └── ex1/                    # Thư mục sản phẩm nộp bài theo đường dẫn gợi ý
│           ├── .github/
│           │   └── workflows/
│           │       └── ci.yml
│           └── README.md           # Hướng dẫn kiểm tra & chụp ảnh nộp bài
├── src/
│   ├── main/java/com/example/
│   │   ├── Application.java
│   │   └── Calculator.java
│   └── test/java/com/example/
│       └── CalculatorTest.java     # Bộ kiểm thử JUnit 5 cho Spring Boot
├── .gitattributes                  # Đảm bảo gradlew giữ chuẩn LF trên Linux runner
├── .gitignore
├── build.gradle
├── gradlew
├── gradlew.bat
├── settings.gradle
└── README.md
```

---

## 3. Nội dung tệp kịch bản `.github/workflows/ci.yml`

```yaml
name: Java Spring Boot CI (Gradle)

on:
  push:
    branches: [ "main" ]

jobs:
  test:
    name: Run Unit Tests
    runs-on: ubuntu-latest

    steps:
      - name: Checkout mã nguồn
        uses: actions/checkout@v5

      - name: Thiết lập môi trường Java JDK 17
        uses: actions/setup-java@v5
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Cấp quyền cho Gradle Wrapper
        run: chmod +x gradlew

      - name: Thực thi JUnit Test với Gradle
        run: ./gradlew test
```

---

## 4. Giải thích các thành phần trong Workflow

| Thành phần | Ý nghĩa |
| :--- | :--- |
| `name: Java Spring Boot CI (Gradle)` | Tên hiển thị của Workflow trong tab **Actions** trên GitHub. |
| `on.push.branches: [ "main" ]` | Tự động kích hoạt Workflow khi có sự kiện `push` lên nhánh `main`. |
| `jobs.test` (`name: Run Unit Tests`) | Định nghĩa Job có ID `test` và tên hiển thị **Run Unit Tests**. |
| `runs-on: ubuntu-latest` | Khởi chạy Job trên máy ảo GitHub-hosted runner hệ điều hành Ubuntu mới nhất. |
| `uses: actions/checkout@v5` | Tải mã nguồn từ GitHub Repository về máy ảo runner. |
| `uses: actions/setup-java@v5` | Cài đặt môi trường **Java JDK 17** thuộc bản phân phối **Eclipse Temurin** (`temurin`). |
| `run: chmod +x gradlew` | Cấp quyền thực thi (`execute`) cho tệp script `gradlew` trên môi trường Linux. |
| `run: ./gradlew test` | Thực thi bộ kiểm thử JUnit 5 của dự án Spring Boot thông qua Gradle Wrapper. |

---

## 5. Hướng dẫn kiểm tra & nộp bài trên GitHub Actions

### Bước 1: Đẩy mã nguồn lên GitHub (nhánh `main`)
Chạy các lệnh sau tại thư mục gốc `SESSION11_BAI1`:

```bash
git init
git add .
git commit -m "feat(ex1): add GitHub Actions workflow to run Gradle JUnit tests"
git branch -M main
git remote add origin <URL_GITHUB_REPO_CUA_BAN>
git push -u origin main
```

### Bước 2: Kiểm tra trên GitHub Actions
1. Truy cập vào **GitHub Repository** vừa đẩy code lên -> Chọn tab **Actions**.
2. Nhấn vào workflow **Java Spring Boot CI (Gradle)** đang chạy hoặc vừa hoàn tất.
3. Kiểm tra Job **Run Unit Tests** hiển thị trạng thái **tích xanh (Success)** cùng các bước:
   - `Checkout mã nguồn`
   - `Thiết lập môi trường Java JDK 17`
   - `Cấp quyền cho Gradle Wrapper`
   - `Thực thi JUnit Test với Gradle`
4. **Chụp ảnh màn hình** tab GitHub Actions hiển thị Job **Run Unit Tests** tích xanh và lưu vào thư mục `homework/session_11/ex1/` để hoàn tất sản phẩm nộp bài.
