# LMSm 문서

### 비밀번호 초기화
---

```plantuml

@startuml
autonumber
모바일 --> 서버: 비밀번호 초기화 메일을 요청한다.
note right: GET api/v1/user/send_reset_pwd_email
서버 --> 모바일: 성공적으로 이메일을 보내면 다음과 같은 반환값을 보낸다.
note left: {"success": "true"}

서버 --> 모바일 !!: 이메일이 존재하지 않을 경우, 다음과 같은 형식의 에러메시지를 반환한다.
note left: "Please check your e-mail."
@enduml
```

### 로그인

```plantuml

@startuml
autonumber
모바일 --> 서버: 로그인 요청을 한다. 
note right: POST /api/v1/auth/login
서버 --> 모바일: 성공적으로 로그인을 하면, 액세스 토큰을 반환한다. 

서버 --> 모바일 !!: 로그인에 실패하면, 에러 메시지를 반환한다.
@enduml
```

### 회사 목록

```plantuml
@startuml
autonumber
모바일 --> 서버: 유저에게 속한 회사 목록을 요청한다.
note right: GET api/v1/company/my-companies 
서버 --> 모바일: 유저에게 속한 회사 목록 리스트를 반환한다.
@enduml
```

### 회사 선택

```plantuml
@startuml
autonumber
모바일 --> 서버: 목록에서 특정한 회사를 선택한다.
note right: GET api/v1/company/companies/{company_key}/check-select-company

서버 --> 모바일: 정상동작의 경우 성공값을 리턴한다.
@enduml
```

### 노티스 목록

```plantuml
@startuml
autonumber
모바일 --> 서버: 노티스 목록을 요청한다.
note right: GET api/v1/notice/notices

서버 --> 모바일: 노티스 목록을 반환한다.
@enduml
```

### 알림(NOTICE) 아이템

```plantuml
@startuml
autonumber
모바일 --> 서버: 알림(NOTICE) 목록에서 특정 아이템 조회 요청
note right: GET /api/v1/notice/notices/{notice_key}

서버 --> 모바일: 특정 아이템(NOTICE)의 정보를 반환
@enduml
```

### 투두 리스트(TODO LIST)

```plantuml
@startuml
autonumber
모바일 --> 서버: 투두 리스트(TODO LIST) 목록을 요청
note right: GET /api/v1/contents/my-lecture/to-do-list

서버 --> 모바일: 투두 리스트 목록을 반환
@enduml
```

### 옵셔널 렉처 리스트 (OPTIONAL LIST)

```plantuml
@startuml
autonumber
모바일 --> 서버: 옵셔널 렉처 리스트를 요청한다. (옵셔널 렉처만 가져오는 필터를 설정한다.)
note right
GET api/v1/contents/lectures

end note

서버 --> 모바일: 옵셔널 렉처 목록을 반환
@enduml
```

### 모든 렉처 리스트 (ALL LECTURE LIST)

```plantuml
@startuml
autonumber
모바일 --> 서버: 모든 렉처 리스트를 요청한다.
note right 
GET api/v1/contents/my-lecture/to-do-list
?show_deleted=0
&offset=0
&count=20
&category_list=238,336,627,239,500,268,345,267,319,320,507,508,240,242,
302,303,304,648,444,624,321,337,647,339,455,457,623,649,650,446,646,517,
519,518,520,301,445,645,545,547,564,586,625,626,628,644,651,652,653,654,
655,656,657,658,659,660,661,662,675 <= (모든 카테고리 키를 나타낸다.)
&validity=1
&company_key=26
end note

서버 --> 모바일: 모든 렉처 리스트를 반환한다.
@enduml
```

### 코스 디테일

```plantuml
@startuml
autonumber
모바일 --> 서버: 코스 아이템의 정보를 요청한다.
note right 
api/v1/contents/my-courses/{user_lecture_key}?offset=0&count=20
end note
서버 --> 모바일: 코스 정보를 반환한다.

모바일 --> 서버: 코스에 할당된 렉처 리스트 요청한다.
note right 
api/v1/contents/courses/{course_key}
end note
서버 --> 모바일: 코스에 할당된 렉처 리스트를 반환한다.

@enduml
```

### 렉처 디테일

```plantuml
@startuml
autonumber
모바일 --> 서버: 렉처 아이템의 정보를 요청한다.
note right 
api/v1/contents/lectures/{lecture_key}
end note
서버 --> 모바일: 렉처 정보를 반환한다.
@enduml
```

### 렉처 콘텐츠

```plantuml
@startuml
autonumber
모바일 --> 서버: 콘텐츠 시청 기록 요청을 1분마다 요청한다. 
note right 
PUT api/v1/contents/my-lecture/to-do-list/{user_lecture_key}/contents/completion-period
end note
서버 --> 모바일: 정상적으로 기록이 된 경우, 아래 값을 반환한다.
note left
{
    "success": true
}
end note
@enduml
```
### 렉처 수강 완료
```plantuml
@startuml
autonumber
모바일 --> 서버: 렉처 수강 완료 요청을 보낸다. 
note right 
PUT api/v1/contents/my-lecture/to-do-list/71022/contents/complete
end note
서버 --> 모바일: 정상적으로 기록이 된 경우, 아래 값을 반환한다.
note left
{
"success": true
}
end note
@enduml
```

### 퀴즈와 관련된 정보를 불러 온다.

```plantuml
@startuml
autonumber
모바일 --> 서버: 유저에게 할당된 렉처 정보를 요청한다.
note right 
GET api/v1/contents/my-lecture/to-do-list/{user_lecture_key} 
end note

서버 --> 모바일: 유저 렉처 정보를 반환한다.

모바일 --> 서버: 렉처 정보를 요청한다.
note right 
GET api/v1/contents/lectures/{lecture_key}
end note

서버 --> 모바일: 렉처 정보를 반환한다.

모바일 --> 서버: 퀴즈 이력을 요청한다.
note right 
GET api/v1/contents/my-lecture/to-do-list/{user_lecture_key}/quizzes/history 
end note

서버 --> 모바일: 퀴즈 히스토리를 반환한다.

@enduml
```

### 퀴즈 시작 버튼을 눌렀을 때

```plantuml
@startuml
autonumber
모바일 --> 서버: 퀴즈 시작, 요청을 한다.
note right
POST api/v1/contents/my-lecture/to-do-list/{user_lecture}/quizzes
end note

서버 --> 모바일 : 문제 및 정답 목록을 반환한다.

@enduml
```

### 다음 버튼을 눌렀을 때

```plantuml
@startuml
autonumber
모바일 --> 서버: 퀴즈 다음 버튼을 누른다. 
note right
GET api/v1/contents/my-lecture/to-do-list/71023/quizzes/4514/results?quiz_history_popup=0
end note

서버 --> 모바일 : 다음 문제와 퀴즈 리스트를 반환한다.

@enduml
```

### 퀴즈가 자동으로 채점 될 때

```plantuml
@startuml
autonumber
모바일 --> 서버: 퀴즈 완료 버튼을 누른다.
note right
GET api/v1/contents/my-lecture/to-do-list/71023/quizzes/4514/results?quiz_history_popup=1
end note

서버 --> 모바일 : 퀴즈 결과를 반환한다.

@enduml
```
