# Git Workflow Зааварчилгаа

Энэхүү баримт бичиг нь төсөлд Git workflow-ийг хэрхэн хэрэгжүүлэх талаар зааварчилгаа өгнө.

## 1. GitHub Репозитори Үүсгэх

1. GitHub дээр шинэ репозитори үүсгэ (public)
2. Локал төслийг Git-д эхлүүл:

```bash
git init
git add .
git commit -m "Maven-д суурилсан Java тооцоолуурын төслийг эхлүүлэх"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

## 2. Main Салбарын Хамгаалалт Тохируулах

1. GitHub дээр репозиторийн "Settings" > "Branches" хэсэгт оч
2. "Branch protection rules" дээр "Add rule" дар
3. Main салбарт дараахыг тохируул:
   - "Require a pull request before merging" идэвхжүүл
   - "Require status checks to pass before merging" идэвхжүүлж, "CI Процесс" workflow-ийг сонго
   - "Require branches to be up to date before merging" идэвхжүүл
   - "Do not allow bypassing the above settings" идэвхжүүл

## 3. Develop Салбар Үүсгэх

```bash
git checkout -b develop
git push -u origin develop
```

## 4. Feature Салбарууд Үүсгэх

### Multiplication Feature:

```bash
git checkout develop
git checkout -b feature/add-multiplication
# Multiplication.java болон MultiplicationTest.java файлууд аль хэдийн үүсгэгдсэн
git add src/main/java/lab14/sict/must/edu/mn/Multiplication.java
git add src/test/java/lab14/sict/must/edu/mn/MultiplicationTest.java
git commit -m "Үржүүлэх функц болон JUnit тест нэмсэн"
git push -u origin feature/add-multiplication
```

GitHub дээр PR үүсгэж develop руу нэгтгэ.

### Division Feature:

```bash
git checkout develop
git checkout -b feature/add-division
# Division.java болон DivisionTest.java файлууд аль хэдийн үүсгэгдсэн
git add src/main/java/lab14/sict/must/edu/mn/Division.java
git add src/test/java/lab14/sict/must/edu/mn/DivisionTest.java
git commit -m "Хуваах функц болон JUnit тест нэмсэн"
git push -u origin feature/add-division
```

GitHub дээр PR үүсгэж develop руу нэгтгэ.

## 5. Release Салбар болон Tag Үүсгэх

```bash
git checkout develop
git checkout -b release/v1.0.0
git tag v1.0.0
git push origin release/v1.0.0
git push origin v1.0.0
```

## 6. Hotfix Салбар Үүсгэх

```bash
git checkout release/v1.0.0
git checkout -b hotfix/v1.0.1
# Division.java файлд тэгээр хуваах зохицуулалт аль хэдийн нэмэгдсэн
git add src/main/java/lab14/sict/must/edu/mn/Division.java
git add src/test/java/lab14/sict/must/edu/mn/DivisionTest.java
git commit -m "Тэгээр хуваахыг зохицуулсан division засварласан"
git push -u origin hotfix/v1.0.1
```

GitHub дээр хоёр PR үүсгэ:
1. hotfix/v1.0.1 → release/v1.0.0
2. hotfix/v1.0.1 → develop

Нэгтгэсний дараа:

```bash
git checkout release/v1.0.0
git tag v1.0.1
git push origin v1.0.1
```

## 7. Локал Шалгалт

PR үүсгэхээс өмнө локал дээр дараах командуудыг ажиллуул:

```bash
# Тест ажиллуулах
mvn test

# Checkstyle шалгах
mvn checkstyle:check

# Coverage тайлан үүсгэх
mvn jacoco:report
# target/site/jacoco/index.html файлыг нээж coverage 100% эсэхийг шалга
```

## 8. Merge Conflict Шийдвэрлэх

Хэрэв merge conflict гарвал:

```bash
git checkout feature/add-multiplication
git merge develop
# Conflict-ийг засварла
git add <conflicted-files>
git commit -m "Merge conflict шийдвэрлэсэн"
git push origin feature/add-multiplication
```

Дэлгэрэнгүй мэдээллийг `conflict_resolution.md` файлд харна.

## Тайлбар

- Бүх код нь Checkstyle дүрмийг дагаж байх ёстой
- Бүх тестүүд 100% branch coverage хангах ёстой
- CI шалгалт амжилтгүй бол merge татгалзагдана

