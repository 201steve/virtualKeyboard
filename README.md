# 가상키보드

### 1. 클래스 사용하여 응집도 높이기

* 클래스 구조를 사용하여 관련 기능과 데이터를 한 곳에 모아 코드의 응집도를 높인다.

### 2. 특정 요소에서부터 DOM 요소 탐색하기

* document가 아닌, body 하위의 특정 요소에서부터 DOM 요소를 탐색한다.
* 페이지 크기가 크거나 DOM 요소가 많은 경우 유리하다.

### 3. Private 변수 사용하여 접근 제한

* private 변수를 사용해 외부에서 직접 접근할 수 없도록 한다.

### 4. 세마포어를 활용한 이벤트 동기화

* 운영체제의 세마포어 개념을 자바스크립트에서도 활용하여 키보드 이벤트와 마우스 이벤트가 동시에 작동하지 않도록 한다.
* 임계영역을 설정하여 하나의 이벤트가 실행될 때 다른 이벤트가 실행되지 못하도록 한다.

#### 4-1. 세부 구현 방법:

1. Private 변수 설정
    * 키보드 이벤트와 마우스 이벤트의 시작점에서 #keyPress = false, #mouseDown = false로 뮤텍스를 설정한다.
2. 키보드 이벤트 진입 영역 (onKeyDown)
    * #mouseDown이 true이면 얼리 리턴하고, #mouseDown이 false일 때만 #keyPress를 true로 바꿔주고 정의된 이벤트 실행.
3. 키보드 이벤트 해제 영역 (onKeyUp)
    * #mouseDown이 true이면 얼리 리턴하고, #mouseDown이 false일 때만 #keyPress를 false로 바꿔준다.
4. 마우스 이벤트 진입 영역 (onMouseDown)
    * #keyPress가 true이면 얼리 리턴하고, #keyPress가 false일 때만 #mouseDown을 true로 바꿔준고 정의된 이벤트 실행.
5. 마우스 이벤트 해제 영역 (onMouseUp)
    * #keyPress가 true이면 얼리 리턴하고, #keyPress가 false일 때만 #mouseDown을 false로 바꿔준다.

### 5. 다크모드는 html 태그를 활용

* css 속성중에 filter 속성을 활용해서 다크모드를 구현할 수 있다.
* filter: invert(100%) hue-rotate(180deg);

### 6. 이벤트가 발생했을때에 가장 가까운 요소를 찾는 법

* event.target.closest('요소명')을 사용하면 이벤트가 발생한 요소로부터 가장 가까운 요소를 찾을 수 있다.

### html속성으로 data-* 사용하기

* data-* 속성을 사용하면 html 요소에 사용자가 원하는 임의의 데이터를 저장할 수 있다.

### 분리된 이벤트 핸들러에서 private 프로퍼티에 접근했다면

* 분리된 이벤트 핸들러에서 this는 전역을 바라보기때문에 private 프로퍼티에 접근할 수 없다.
* 이벤트 핸들러에 bind로 this를 전달해 클래스 인스턴스를 바라보게 해야 한다.