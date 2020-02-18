### 가장 큰 수
https://programmers.co.kr/learn/courses/30/lessons/42746

#### 문제 요약
* 수를 모두 이어붙여서 만든 수 중에서 가장 큰 수를 구하고, String으로 return하라

#### 문제 풀이 과정
* 1차 - 실패(정확성 테스트 케이스 11개 중 1개 실패)
    * [1차 제출 코드](Solution1.java)
        * 모든 경우의 수를 구하는 게 너무 힘들다고 생각해서 최대한 경우의 수를 줄이려 노력했다
        * sort 시 다음과 같은 규칙을 따르도록 Comparable을 implement한 Num class를 만듦었다
            * 자리 수가 같을 경우, 큰 수가 앞으로 온다
                * 3과 9를 비교한다면 9, 3 순서
            * 자리 수가 다를 경우, 두 String을 순서를 바꾸어 붙였을 때 큰 수가 앞으로 온다
                * 9와 30일 때 9, 30
                * 3과 30일 때 3, 30
                * 3, 30, 34일 때 34, 3, 30
    * 결과
        ```
        테스트 1 〉	통과 (1930.22ms, 366MB)
        테스트 2 〉	통과 (695.70ms, 364MB)
        테스트 3 〉	통과 (3014.60ms, 368MB)
        테스트 4 〉	통과 (63.50ms, 62.2MB)
        테스트 5 〉	통과 (1545.12ms, 365MB)
        테스트 6 〉	통과 (1129.94ms, 365MB)
        테스트 7 〉	통과 (32.46ms, 53.1MB)
        테스트 8 〉	통과 (29.03ms, 53.4MB)
        테스트 9 〉	통과 (29.76ms, 53.6MB)
        테스트 10 〉	통과 (30.08ms, 55.4MB)
        테스트 11 〉	실패 (34.45ms, 55.4MB)

        채점 결과
        정확성: 90.9
        합계: 90.9 / 100.0
        ```
        * 테스트 케이스 11이 뭘까... 내가 뭘 빠뜨렸을까...?
            * [아 [0, 0, 0, 0]일 때 0000이 되는게 문제군...](https://programmers.co.kr/learn/questions/8011)

* 2차 - 통과
    * [2차 제출 코드](Solution2.java)
        * 정렬 기준이 하나이기 때문에 굳이 Comparable을 구현하는 class를 만들 것까지는 없다고 판단해서  
        sort할 때 Comparator를 구현하는 방식으로 변경
            * 비교할 때, 자리 수가 같고 다름에 상관없이 비교해도 된다는 걸 깨닫고 수정함
            * 9, 3이어도 39가 큰지 93이 큰지 확인 -> 93이 크므로 9, 3 순으로 정렬
        * 1차 때 실패했던 '모든 element가 0'인 케이스에 대한 처리를 위해 Integer.parseInt()를 사용했는데,  
        모든 element가 0인 케이스만 성공하고 나머지는 모두 실패했다
            * https://programmers.co.kr/learn/questions/7436
            * Integer의 MAX_VALUE가 2147483647이므로 이를 초과해서 발생하는 문제인 것으로 보인다
            * 그래서 solution()의 return type도 String인 것으로 보임
        * 마지막에 answer의 0번째 char가 0인지 확인하고 return하도록 수정
            * BigInteger.parseInt()를 쓰던가
            * numbers의 모든 원소가 0인지 확인하던가
            * 모든 원소의 합이 0인 걸 확인하던가