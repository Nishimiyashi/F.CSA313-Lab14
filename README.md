# Calculator - Maven Java Төсөл

Энэ нь Maven-д суурилсан энгийн тооны машины Java аппликейшн юм.

## Төслийн Бүтэц

```
calculator/
├── pom.xml
├── checkstyle.xml
├── README.md
├── .gitignore
├── src/
│   ├── main/
│   │   └── java/
│   │       └── lab14/
│   │           └── sict/
│   │               └── must/
│   │                   └── edu/
│   │                       └── mn/
│   └── test/
│       └── java/
│           └── lab14/
│               └── sict/
│                   └── must/
│                       └── edu/
│                           └── mn/
└── .github/
    └── workflows/
        └── ci.yml
```

## Хэрхэн Угсрах болон Ажиллуулах

### Шаардлага
- Java 17
- Maven 3.6+

### Командууд

#### Төслийг угсрах:
```bash
mvn clean compile
```

#### JUnit тест ажиллуулах:
```bash
mvn test
```

#### Checkstyle кодын загварын шалгалт:
```bash
mvn checkstyle:check
```

#### JaCoCo code coverage тайлан үүсгэх:
```bash
mvn jacoco:report
```

Coverage тайланг `target/site/jacoco/index.html` файлд харна.

#### Бүх шалгалтууд (Checkstyle, Test, Coverage):
```bash
mvn clean test
```

Энэ нь Checkstyle (validate phase-д), JUnit тестүүд, болон JaCoCo 100% branch coverage шалгалтыг автоматаар гүйцэтгэнэ.

## Git Workflow

### Салбарууд
- `main`: Үндсэн салбар (production-ready код)
- `develop`: Хөгжүүлэлтийн салбар
- `feature/*`: Онцлог хөгжүүлэлтийн салбарууд
- `release/*`: Хувилбар гаргах салбарууд
- `hotfix/*`: Яаралтай засварын салбарууд

### CI/CD
GitHub Actions нь дараах шалгалтуудыг автоматаар гүйцэтгэнэ:
- Checkstyle кодын загварын шалгалт
- JUnit тестүүд
- JaCoCo 100% branch coverage шалгалт

## Хувилбарууд
- v1.0.0: Эхний хувилбар
- v1.0.1: Тэгээр хуваах зохицуулалттай hotfix

