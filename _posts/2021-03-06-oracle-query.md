###### 테이블 생성

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 create_table.sql %}

### 컬럼 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 add_column.sql %}

### 컬럼 삭제

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 drop_column.sql %}

### 컬럼명 변경

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 rename_column.sql %}

### 컬럼타입 변경

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 modify_column.sql %}

### 테이블 주석

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 comment_column.sql %}

### PK 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 add_constraint.sql %}

### PK 삭제

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 drop_constraint.sql %}

### 시퀀스 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 create_sequence.sql %}

### 시퀀스 삭제

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 drop_sequence.sql %}

### 테이블 정보 확인

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 select_table_info.sql %}

### 테이블 복수 데이터 한번에 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 insert_multiple_data.sql %}

### 엑셀 활용 Query 작성

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 insert_multiple_data.xlsx %}

### Mybatis 리턴

| Method | Success | Fail |
|:---:|:---:|:---:|
| `select()` | select 결과 | null |
| `insert()` | null|에러 |
| `update()` | 1 | 0 |
| `delete()` | 삭제한 row count | 삭제한 row count |
