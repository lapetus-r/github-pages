며칠 전 오랜 동료들과 함께 온라인 회식을 하다 우연히 들은 문제가 있는데 재밌을 것 같아 Codility 형식애 맞춰 풀어봤다.

## Snake Problem

* N*N 행렬(matrix)이 주어졌을 때, `matrix[0][0]`로부터 반시계 방향으로 회전하며 중복 없이 행렬의 모든 성분을 출력하라.

```kotlin
fun solution(matrix: List<List<String>>) {
    var m = matrix
    while (m.isNotEmpty()) {
        m.dropLast(1).map { it.first() }.forEach(::println)
        m.last().dropLast(1).forEach(::println)
        m.reversed().dropLast(1).map { it.last() }.forEach(::println)
        m.first().reversed().dropLast(1).forEach(::println)
        m = m.drop(1).dropLast(1).map { it.drop(1).dropLast(1) }
    }
}
```

풀고 나니 `var`로 선언해 둔 변수 `m`이 마음에 들지 않는데 이런 문제들을 최근에 몇차례 경험해본 바, 상수를 쓰겠다고 재귀까지 써가며(그것도 꼬리재귀 조건까지 맞춰가며...) 구현하는게
알고리즘 테스트에는 그다지 도움이 되지 않는다는걸 알았다.

예전과 달리 고수준 언어 차원에서 Collection 을 다루는 Operator 들이 다양하게 지원되기 때문에 문제의 의도만 정확히 파악하면 구현 자체는 금방 끝낼것 같다.
