Dưới đây là hướng dẫn chi tiết để cấu hình **Spotless với Gradle** nhằm tự động format mã nguồn Java theo chuẩn **Google Java Format** — rất phù hợp để tích hợp với Husky hoặc CI/CD pipelines.

---

## 🧰 1. Thêm plugin Spotless vào `build.gradle`

Nếu bạn dùng **Gradle Groovy DSL** (`build.gradle`):

```groovy
plugins {
    id 'java'
    id 'com.diffplug.spotless' version '6.22.0'
}

spotless {
    java {
        googleJavaFormat() // dùng chuẩn Google Java Format
        target 'src/**/*.java' // chỉ định file cần format
    }
}
```

Nếu bạn dùng **Gradle Kotlin DSL** (`build.gradle.kts`):

```kotlin
plugins {
    java
    id("com.diffplug.spotless") version "6.22.0"
}

spotless {
    java {
        googleJavaFormat()
        target("src/**/*.java")
    }
}
```

---

## 🧪 2. Cách sử dụng Spotless

| Lệnh | Mục đích |
|------|----------|
| `./gradlew spotlessApply` | Format mã nguồn |
| `./gradlew spotlessCheck` | Kiểm tra xem mã nguồn đã được format chưa |

👉 Bạn có thể tích hợp `spotlessCheck` vào pipeline CI để đảm bảo mã nguồn luôn tuân thủ convention.

---

## 🧩 3. Tích hợp với Husky

Trong `package.json`:

```json
"scripts": {
  "format:java": "./gradlew spotlessApply",
  "check:java": "./gradlew spotlessCheck"
}
```

Trong `.husky/pre-commit`:

```bash
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npm run check:java
```

---

## 🧠 Gợi ý nâng cao

- Bạn có thể thêm định dạng cho các file khác như `xml`, `json`, `md`, `yaml` bằng Spotless.
- Có thể cấu hình để bỏ qua một số file bằng `exclude`.

---
