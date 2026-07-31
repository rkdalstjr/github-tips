# 마크다운 문서 사용법

## 제목
#의 개수로 제목의 크기를 표현한다. 하위 제목으로 갈수록 #의 개수가 많아진다.

## 문단
빈 줄(줄바꿈) 하나가 문단을 구분한다. 즉, 엔터키를 두 번 쳐야 줄바꿈이 된다.

## 글꼴 처리
굵게 : `**굵게**`

기울임 : `*기울임*`

강조 : `***강조***`

취소선 : `~~삭제~~`

## 인라인 코드
`pip install pandas`

`을 텍스트 양 옆에 넣어 사용한다. 명령어, 함수명, 변수명 표시에 적합하다. 위의 글꼴 처리 방법을 그대로 보여주면서 사용했다.

## 코드 블록
```python
for int in ints:
    print(int)
```

`을 3번 붙여서 코드 위 아래에 넣어 사용한다. 언어를 지정하고 코드를 사용하기 적합하다.

## 목록
- a
- b
- c
    - 1
    - 2
- d
    1. ㄱ
    2. ㄴ
    3. ㄷ

위와 같이 들여쓰기, -, 번호로 사용한다.

## 체크리스트

- [ ] 구현
- [ ] 테스트
- [x] 완료

깃허브같은 사이트에서 렌더러를 지원해준다면, 체크박스 기능을 사용할 수 있다.

## 인용문
> 중요 내용
>> 세부 내용

`>`을 사용해서 인용문을 작성한다.

## 수평선
1234567890
---
1234567890
***
1234567890
___
```
---

***
___
```
문서를 구분할 때 사용한다.

## 링크
- 일반 링크
[GitHub](https://github.com)
- 자동 링크
<https://github.com>
```
[GitHub](https://github.com)
<https://github.com>
```
링크 대신에 텍스트를 넣을 때 일반 링크를 사용한다.

## 이미지
```
![설명](image.png)
```
이미지를 넣을 때 같은 폴더에 이미지가 있어야 한다. 다른 폴더에 있는 경우, 아래 상대경로 예시를 참고한다.
```
하위폴더에 있을 때
![설명](images/photo.jpg)

상위폴더에 있을 때
![설명](../logo.png) << ../../../의 방식으로 상위 단계를 구분
```

아니면 인터넷에 올라가 있는 이미지 주소를 그대로 넣을 수 있다.
```
![구글 로고](https://www.google.com/images/branding/googlelogo/light/googlelogo.png)
```

## 표
| 이름 | 역할 |
|------|------|
| 김철수 | 개발 |
| 홍길동 | 기획 |

| 왼쪽 | 가운데 | 오른쪽 |
|:-----|:------:|------:|

```
| 이름 | 역할 |
|------|------|
| 김철수 | 개발 |
| 홍길동 | 기획 |

| 왼쪽 | 가운데 | 오른쪽 |
|:-----|:------:|------:|
```

## 이스케이프 문자
```
\*
\`
\#
\[
```
위와 같이 사용하면 `를 사용하지 않고도 문자 그대로 출력한다.

## 접기
<details>
<summary>클릭해서 보기</summary>

숨겨질 내용

</details>

```
<details>
<summary>클릭해서 보기</summary>

숨겨질 내용

</details>
```
위와 같이 사용한다.

## Mermaid 다이어그램
지원 종류
- Flowchart
```mermaid
flowchart TD
    A[시작] --> B{조건 확인}
    B -->|Yes| C[실행]
    B -->|No| D[종료]
```
- Sequence Diagram
```mermaid
sequenceDiagram
    participant A as 사용자
    participant B as 서버
    A->>B: 요청 전송
    B-->>A: 응답 반환
```
- Class Diagram
```mermaid
classDiagram
    Animal <|-- Dog
    Animal <|-- Cat
    class Animal {
        +String name
        +eat()
    }
    class Dog {
        +bark()
    }
```
- State Diagram
```mermaid
stateDiagram-v2
    [*] --> 대기중
    대기중 --> 실행중: 시작
    실행중 --> 완료: 성공
    실행중 --> 오류: 실패
    오류 --> [*]
```
- ER Diagram
```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : "주문한다"
    ORDER ||--|{ LINE-ITEM : "포함한다"
    CUSTOMER {
        int id PK
        string name
    }
    ORDER {
        int id PK
        date order_date
    }
```
- Gantt Chart
```mermaid
gantt
    title 프로젝트 일정
    dateFormat YYYY-MM-DD
    section 기획
    요구사항 분석 :a1, 2024-01-01, 7d
    설계 :after a1, 5d
    section 개발
    구현 :active, 2024-01-10, 10d
    테스트 :2024-01-20, 5d
```
- Pie Chart
```mermaid
pie
    title 기술 스택 비율
    "JavaScript" : 40
    "Python" : 30
    "Java" : 20
    "기타" : 10
```
- Git Graph
```mermaid
gitGraph
    commit id: "초기 커밋"
    branch develop
    checkout develop
    commit id: "기능 추가"
    checkout main
    merge develop
```
- XY Chart
```mermaid
xychart-beta
    title "월별 누적 수익률 (%)"
    x-axis ["1월", "2월", "3월", "4월", "5월", "6월"]
    y-axis "수익률" 0 --> 25
    bar [5, 8, 12, 15, 18, 22]
    line [5, 8, 12, 15, 18, 22]
```
- User Journey
```mermaid
journey
    title 퀀트 전략 리스크 점검
    section 매매 사이클
      데이터 수집: 3: 시스템
      신호 생성: 4: 시스템, 트레이더
      주문 실행: 2: 시스템, 브로커
      리스크 관리: 5: 시스템
```
- Kanban
```mermaid
kanban
    Todo[할 일]
        task1[전략 리팩토링]@{ assigned: '나', priority: 'High' }
        task2[데이터 클렌징]@{ assigned: '팀A', priority: 'Low' }
    In Progress[진행 중]
        task3[백테스팅 고도화]@{ assigned: '나', priority: 'High' }
        task4[실시간 모니터링 구축]@{ assigned: '팀B', priority: 'High' }
    Review[검토 중]
        task5[수익률 분석 리포트]@{ assigned: '팀A' }
    Done[완료]
        task6[데이터 파이프라인 구축]
        task7[전략 v1.0 개발]
```
- Quadrant Chart
```mermaid
quadrantChart
    title 전략 성과 평가 (수익률 vs. 변동성)
    x-axis 낮은 변동성 --> 높은 변동성
    y-axis 낮은 수익률 --> 높은 수익률
    quadrant-1 고수익-저변동
    quadrant-2 고수익-고변동
    quadrant-3 저수익-저변동
    quadrant-4 저수익-고변동
    전략 A: [0.3, 0.7]
    전략 B: [0.6, 0.4]
    전략 C: [0.8, 0.9]
    전략 D: [0.2, 0.3]
```
- C4 Diagram
```mermaid
C4Container
    title 퀀트 시스템 아키텍처

    Container(api, "API Gateway", "REST API", "외부 요청 처리")
    Container(engine, "백테스팅 엔진", "Python", "전략 검증")
    Container(live, "실매매 엔진", "Python", "실시간 주문 실행")
    Container(db, "데이터베이스", "PostgreSQL", "시세/체결 데이터 저장")
    Container(queue, "메시지 큐", "RabbitMQ", "이벤트 브로커")

    Rel(api, engine, "백테스트 요청")
    Rel(api, live, "실매매 명령")
    Rel(engine, db, "데이터 조회")
    Rel(live, db, "체결 저장")
    Rel(live, queue, "이벤트 발행")
    Rel(queue, engine, "이벤트 구독")
```

모든 다이어그램은 %%로 주석을 추가할 수 있다.

## 앵커 링크
[목록으로 이동](#목록)
```
[(챕터명)으로 이동](#챕터명)
```
위와 같이 사용하여 긴 문서에서 빠르게 챕터를 이동할 수 있다.

## VS 코드 단축키
| 단축키              | 기능     |
| ---------------- | ------ |
| Ctrl + Shift + V | 미리보기   |
| Ctrl + K → V     | 옆 미리보기 |
| Ctrl + Space     | 자동완성   |
| Alt + Shift + F  | 문서 정렬  |
| Ctrl + /         | 주석     |