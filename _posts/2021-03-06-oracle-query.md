##### Table 생성

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 create_table.sql %}

##### Column 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 add_column.sql %}

##### Column 삭제

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 drop_column.sql %}

##### Column 이름 변경

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 rename_column.sql %}

##### Column 타입 변경

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 modify_column.sql %}

##### Table 주석 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 comment_column.sql %}

##### Constraint 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 add_constraint.sql %}

##### Constraint 삭제

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 drop_constraint.sql %}

##### Sequence 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 create_sequence.sql %}

##### Sequence 삭제

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 drop_sequence.sql %}

##### Table 정보 확인

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 select_table_info.sql %}

##### 복수 데이터 한번에 추가

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 insert_multiple_data.sql %}

##### 엑셀을 활용해 복수 데이터 한번에 추가하는 쿼리 작성

{% gist lapetus-r/d73a816d3fa2452aa6fe0f5e65d63ec0 insert_multiple_data.xlsx %}

##### Mybatis 리턴값

| Method | Success | Fail |
|:---:|:---:|:---:|
| `select()` | select 결과 | null |
| `insert()` | null|에러 |
| `update()` | 1 | 0 |
| `delete()` | 삭제한 row count | 삭제한 row count |
