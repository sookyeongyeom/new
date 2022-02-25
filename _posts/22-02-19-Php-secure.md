---
title: PHP Prepared Statement (SQL Injection Secure Coding)
category: [Back-End, PHP]
---

> PHP Prepared Statement

- 바인딩 데이터는 SQL 문법이 아닌 내부의 인터프리터나 컴파일 언어로 처리하므로 문법적인 의미를 가질 수 없다. 따라서 파라미터 바인딩 과정을 거치면 대부분의 SQL Injection 공격을 방지할 수 있다.

```php
$sql = "INSERT INTO apply(id, name, student_id, department, community_id, phone, semester, tool, intro, file) VALUES (0, ?, ?, ?, ?, ?, ?, ?, ?, ?);";

$stmt = mysqli_prepare($conn, $sql);
if($stmt === false) { echo('Statement 생성 실패 : ' . mysqli_error($conn)); exit(); }

$bind = mysqli_stmt_bind_param($stmt, "sssssssss", $name, $student_id, $department, $snulife_id, $phone, $semester, $tool, $intro, $files);
if($bind === false) { echo('파라미터 바인드 실패 : ' . mysqli_error($conn)); exit(); }

$exec = mysqli_stmt_execute($stmt);
```