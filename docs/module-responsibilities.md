# 기능별 책임과 모듈 경계 (초안)

> 이 문서는 기능별 책임을 구분한 초기 설계 문서입니다. 현재 폴더는 하나의 Xcode 프로젝트 내부 디렉터리이며, 독립된 Swift Package를 의미하지 않습니다.

| 모듈 | 담당 기능 | 주요 의존 대상 |
| --- | --- | --- |
| Auth | 로그인, 회원가입, 사용자 인증 | 공통 데이터 모델 |
| User | 사용자 프로필, 사용자 설정 | Auth |
| Chat | AI 대화 및 대화 내역 | Auth, AI 통신 계층 |
| Emotion | 감정 분석 결과 조회, 감정 기록·리포트 | Chat, Auth |
| Community | 모임 생성·검색·가입, 게시글, 댓글 | Auth |
| Challenge | 개인·공동 챌린지, 참여, 인증 | Community, Auth |
| Moment | 순간기록, 사진, 태그, 수집함 | Auth |
| Health | HealthKit 데이터 조회 및 표시 | HealthKit, 필요한 경우 Auth |

## 구조

```text
Rapport/
├── App/
├── Features/
│   ├── Auth/
│   ├── User/
│   ├── Chat/
│   ├── Emotion/
│   ├── Community/
│   ├── Challenge/
│   ├── Moment/
│   └── Health/
├── Core/
│   ├── Models/
│   ├── Networking/
│   └── Storage/
└── Resources/
```

## 구분 원칙

- `Features/`: 화면, ViewModel, 해당 기능의 서비스 및 전용 모델을 배치합니다.
- `Core/Models/`: 여러 기능이 공통으로 사용하는 타입만 배치합니다.
- `Core/Networking/`: API 요청과 네트워크 통신을 위한 공통 코드를 배치합니다.
- `Core/Storage/`: 공통 저장소 어댑터와 영속성 관련 코드를 배치합니다.
- `App/`: 앱 진입점, 앱 전체 의존성 구성 및 라우팅을 담당합니다.
- `Resources/`: 에셋, 로컬라이제이션 등 앱 리소스를 배치합니다.

## 다음 단계

1. 이 저장소를 로컬 Mac에 클론합니다.
2. Xcode 프로젝트를 생성하고 실제 디렉터리와 프로젝트 내 그룹을 연결합니다.
3. 각 기능의 데이터 모델(`struct`, `enum`)을 정의합니다.
4. Repository/Service 프로토콜 및 클래스의 함수 시그니처를 정의합니다.
5. 세부 함수 계약(입력·출력, 오류, 선행조건)을 작성합니다.

> 이 커밋은 폴더 구조만 초기화합니다. Xcode 프로젝트(`.xcodeproj`), Swift 소스 코드 및 실행 가능한 앱은 아직 생성되지 않았습니다.
