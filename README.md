# 게임 관리 프로그램

## 1. Service Topic

* **주제**: 게임 관리 프로그램 

* **설명**: 등록된 비디오 게임의 목록을 확인하고, 새로운 게임 정보를 등록, 수정, 삭제할 수 있는 관리자용 프론트엔드 페이지입니다.

## 2. Data Fields

게임 정보 관리를 위해 총 7개의 데이터 필드를 사용합니다. 

1. **ID**: 게임 데이터의 고유 식별 번호 

2. **게임명 (Title)**: 게임의 공식 제목 \[Text\]

3. **장르 (Genre)**: 게임의 장르 (RPG, Action, FPS, Simulation 등) \[Select\]

4. **출시일 (Release Date)**: 게임이 공식 출시된 연/월/일 \[Date\]

5. **가격 (Price)**: 게임의 판매 가격(원화) \[Number\]

6. **개발사 이메일 (Developer Email)**: 개발사 또는 퍼블리셔의 고객지원 연락처 \[Email\]

7. **상세 설명 (Description)**: 게임의 줄거리나 특징에 대한 부가 설명 \[Textarea\]

## 3. List Page (`index.html`)

메인 화면인 게임 목록 페이지에서는 사용자가 한눈에 정보를 파악할 수 있도록 핵심 필드 5가지를 테이블 형태로 표시합니다.

* ID

* 게임명

* 장르

* 플랫폼 (PC / Console 등)

* 출시일

## 4. Validation

데이터를 등록(`add.html`)하거나 수정(`edit.html`)할 때, 잘못된 값이 입력되는 것을 방지하기 위해 JavaScript를 이용한 유효성 검사 5가지를 적용했습니다.

1. **필수값 입력 여부 및 문자열 길이**: 게임명은 최소 2글자 이상 입력하도록 강제했습니다.

2. **Select 선택 여부**: 장르 선택 항목 중 하나를 반드시 선택하도록 검사했습니다.

3. **날짜 입력 여부**: 출시일 필드가 비어있지 않은지 검사했습니다.

4. **숫자 범위**: 가격은 음수가 될 수 없으므로 0 이상의 숫자인지 검사했습니다.

5. **이메일 형식**: 정규 표현식(`/^[^\s@]+@[^\s@]+\.[^\s@]+$/`)을 사용하여 올바른 이메일 형식(예: `a@b.com`)인지 검사했습니다.

## 5. RWD (Responsive Web Design)

사용자가 데스크탑과 모바일 환경 모두에서 불편함 없이 사용할 수 있도록 반응형으로 구성했습니다.

* **Desktop**: Bootstrap Grid(`col-lg-8`, `col-md-6`)를 활용하여 입력 폼을 중앙에 배치하고, 2단으로 나누어 화면 공간을 효율적으로 사용했습니다.

* **Mobile**:

  * CSS Media Query(`@media (max-width: 768px)`)를 사용하여 모바일 화면에서는 컨테이너의 좌우 여백을 줄였습니다.

  * 모바일에서 터치하기 쉽도록 하단의 버튼(Button)들이 화면 너비의 100%(`width: 100%`)를 차지하도록 변경했습니다.

  * 데이터 목록을 감싸는 div에 `table-responsive` 클래스를 적용하여, 테이블 내용이 길어질 경우 화면이 깨지지 않고 가로 스크롤이 생기도록 처리했습니다.

## 6. Bootstrap

빠르고 일관된 디자인을 위해 Bootstrap 5.3 프레임워크의 클래스와 컴포넌트를 적극 활용했습니다.

* **Layout**: `container`, `row`, `col`, `col-md-6`, `col-lg-8`, `mt-5`, `mb-3` (그리드 및 여백)

* **Component**:

  * `navbar`, `navbar-expand-lg`, `navbar-dark`, `bg-dark` (상단 네비게이션 바)

  * `card`, `card-header`, `card-body` (폼과 데이터를 깔끔하게 담는 박스)

  * `table`, `table-hover`, `table-bordered` (데이터 목록 및 상세 정보 테이블)

  * `badge bg-success` (상태 표시)

* **Form & Button**: `form-control`, `form-select`, `form-label`, `btn`, `btn-primary`, `btn-warning`, `btn-danger`, `btn-outline-secondary`

## 7. Problem & Solution

* **Problem (문제)**: 정적 HTML/JS로만 구현하다 보니 폼에서 데이터를 수정하거나 추가한 뒤 페이지가 이동하면, 입력했던 데이터가 목록 페이지에 반영되지 않는 문제가 있었습니다.

* **Solution (해결)**: 현재 환경이 백엔드/DB가 없는 프론트엔드 UI 중심의 과제임을 인지하고, JS에서 폼의 기본 제출 동작을 `event.preventDefault()`로 막았습니다. 대신 유효성 검사가 통과되면 `alert()`나 `confirm()`을 띄워 사용자에게 피드백을 주고 `window.location.href`로 자연스럽게 다음 페이지로 이동하도록 했습니다.

## 8. Reflection

* **새롭게 알게 된 점**: Bootstrap의 Grid 시스템(`row`, `col`)과 Utility 클래스(`mt-3`, `d-flex` 등)를 조합하면 CSS를 거의 작성하지 않고도 훌륭한 반응형 레이아웃을 만들 수 있다는 것을 체감했습니다. 또한 자바스크립트 정규식을 활용한 이메일 유효성 검사 로직을 이해하게 되었습니다.

* **궁금한 점 / 향후 과제**: 페이지 이동 시에도 데이터가 유지되게 하려면 어떻게 해야 하는지 더 알고 싶습니다.