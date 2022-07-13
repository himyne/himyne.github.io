---
layout: single
title:  "리액트 네이티브 -1"

categories:
  - ReactNative
tags:
  - ReactNative
---

***
### 네이티브 애플리케이션

운영체제를 구성하는 언어와 같은 언어로 만들어지는 애플리케이션이다. 그 말은 뭐냐면 IOS 는 Objective-C 나 Swift로 개발하고 안드로이드는 자바나 코틀린으로 따로 개발해야 한다는 뜻이다.

- 장점 : 높은 성능이 보장됨.
- 단점 : 개발에 투입되는 리소스가 많아진다.

***
### 하이브리드 애플리케이션

- 웹뷰를 이용해 보여지는 영역에 html을 보여준다.
- html+css+js를 이용해 화면을 구현한다.
- 네이티브로 맘ㄴ들어진 앱 컨테이너로 네이티브 기능 연동
- 장점 : 웹 기술에 익숙하면 빠른 개발 가능
- 단점 : 뷰 퍼포먼스 최적화가 힘듦
- 하이브리드 앱은 모바일 웹 사이트를 감싼 네이티브 앱으로, apache cordova, ionic, appcelerator titanium등을 사용할 수 있다.

***
### 크로스 플랫폼 네이티브 애플리케이션

- 네이티브가 아닌 언어로 작성하지만 빌드 단계에서 네이티브로 변환됨
- 리액트 네이티브(JS), 유니티(C#), 자마린(C#), 플러터(Dart) 등
- 장점 : 자신에게 익숙한 언어로 빠른 개발 가능
- 단점 : 네이티브 연동 기능이 많을 경우에는 효율성 떨어짐

***
### 주요 크로스 플랫폼 네이티브 애플리케이션의 제작 환경

1. unity 유니티
    
    화면 구성 : unity editor
    
    로직 : C#
    
2. Xamarin
    
    화면 구성 : Xamarin.Forms
    
    로직 : C#
    
3. Flutter 
    
    화면 구성 & 로직 : Dart
    
4. React Native
    
    화면 구성 : JSX(중 XML)
    
    로직 : JSX(중 JS)
    
***
### JSX

- Javascript + XML
- ECMA Script 6 표준의 자바스크립트 사용
- JSX 내에 스타일시트를 포함함 웹의 CSS와 많은 개념을 공유하지만 독자적인 포맷 CSS 파일로 작성 불가

***
### 리액트 / 리액트 네이티브

- 리액트 : JSX → REACT(VIRTUAL DOM) → HTML(VIEW) , JSX를 HTML로 렌더링 한다.
- 리액트 네이티브 : JSX → REACT NATIVE(VIRTUAL DOM) → ANDROID/IOS VIEW , JSX를 네이티브 뷰 형태로 렌더링 한다.

***
### 애플리케이션의 구조

![image](https://user-images.githubusercontent.com/88049162/170433023-44537fef-b564-40aa-8989-9d1665ee4b4e.png)

데이터 처리는 자바스크립트가 수행하고 뷰와 자바스크립트 엔진을 연결하는 브릿지가 존재

***
### 엑스포 스냅 (expo)

- 기본 환경

App.js : 시작점 ( entry point) 가 되는 파일, App() {} 은xml 문법으로 되어있고 styles는 css 문법으로 작성 할 수 있다. 

package.json : 필요한 모듈이 있을 때 [npmjs.com](http://npmjs.com) 에서 다운받기.

컬러와 같은 스타일시트는 텍스트(<text>)에만 적용할 수 있음. 

***
# 리액트 네이티브 시작

## flex 개념 정리

[https://flexboxfroggy.com/#ko](https://flexboxfroggy.com/#ko)

- flex-grow 설정 - flex : 1 이면 전체화면 꽉참.[https://developer.mozilla.org/ko/docs/Web/CSS/flex-grow](https://developer.mozilla.org/ko/docs/Web/CSS/flex-grow)

***
### justify-content

- **`flex-start`**: 요소들을 컨테이너의 왼쪽으로 정렬합니다.
- **`flex-end`**: 요소들을 컨테이너의 오른쪽으로 정렬합니다.
- **`center`**: 요소들을 컨테이너의 가운데로 정렬합니다.
- **`space-between`**: 요소들 사이에 동일한 간격을 둡니다.
- **`space-around`**: 요소들 주위에 동일한 간격을 둡니다.

***
### align-items

- **`flex-start`**: 요소들을 컨테이너의 꼭대기로 정렬합니다.
- **`flex-end`**: 요소들을 컨테이너의 바닥으로 정렬합니다.
- **`center`**: 요소들을 컨테이너의 세로선 상의 가운데로 정렬합니다.
- **`baseline`**: 요소들을 컨테이너의 시작 위치에 정렬합니다.
- **`stretch`**: 요소들을 컨테이너에 맞도록 늘립니다.

***
### flex-direction

- **`row`**: 요소들을 텍스트의 방향과 동일하게 정렬합니다.
- **`row-reverse`**: 요소들을 텍스트의 반대 방향으로 정렬합니다.
- **`column`**: 요소들을 위에서 아래로 정렬합니다.
- **`column-reverse`**: 요소들을 아래에서 위로 정렬합니다.

- 때때로 컨테이너의 row나 column의 순서를 역으로 바꾸는 것만으로는 충분하지 않습니다. 이러한 경우에는 **`order`**속성을 각 요소에 적용할 수 있습니다. order의 기본 값은 0이며, 양수나 음수로 바꿀 수 있습니다.

***
### flex-wrap

- **`nowrap`**: 모든 요소들을 한 줄에 정렬합니다.
- **`wrap`**: 요소들을 여러 줄에 걸쳐 정렬합니다.
- **`wrap-reverse`**: 요소들을 여러 줄에 걸쳐 반대로 정렬합니다.

- **`flex-direction`**과 **`flex-wrap`**이 자주 같이 사용되기 때문에, **`flex-flow`**가 이를 대신할 수 있습니다. 이 속성은 공백문자를 이용하여 두 속성의 값들을 인자로 받습니다. 예를 들어, 요소들을 가로선 상의 여러줄에 걸쳐 정렬하기 위해 **`flex-flow: row wrap`**을 사용할 수 있습니다.

***
### aling-content

**`align-content`**를 사용하여 여러 줄 사이의 간격을 지정할 수 있습니다. 이 속성은 다음의 값들을 인자로 받습니다:

- **`flex-start`**: 여러 줄들을 컨테이너의 꼭대기에 정렬합니다.
- **`flex-end`**: 여러 줄들을 컨테이너의 바닥에 정렬합니다.
- **`center`**: 여러 줄들을 세로선 상의 가운데에 정렬합니다.
- **`space-between`**: 여러 줄들 사이에 동일한 간격을 둡니다.
- **`space-around`**: 여러 줄들 주위에 동일한 간격을 둡니다.
- **`stretch`**: 여러 줄들을 컨테이너에 맞도록 늘립니다.

- 개구리 마지막 문제 답
    
    flex-flow : column-reverse wrap-reverse;
    justify-content : center;
    align-content : space-between;
    
- SafeAreaView

노치 (아이폰 상단바) 없는 화면, VIEW와 다름.

- stylesheet 안에서 borderwidth나 height와 같은 속성을 다룰 때, pixel값이나 퍼센트%값을 지정할 수  있다.
- React.fragment : 실제 렌더링에 반영되지 않는 추상 컨테이너 , 빈태그를 열고 닫으면 된다.

***
### 로또 번호 랜덤 화면 만들기

- lodash
    - package.json에 버전과 함께 추가하면 설치가 되고 App.js에서 import 할 수 있다.
    - 가장 많이 사용되는 라이브러리이다.
- State
    
    [https://ko.reactjs.org/docs/state-and-lifecycle.html](https://ko.reactjs.org/docs/state-and-lifecycle.html)
    
    - 화면의 변경 사항이 있을 때 이전의 상태와 이후의 상태가 달라졌을 때 전체 화면이 다시 그려질 필요가 없다는 장점

***  
### styled-components

- css에서 표현하던 방법 그대로 들어갈 수 있다. string 처리하거나 숫자만 써야하는 단점을 보완해준다.
- **Template literals**
    
    ```jsx
    //Syntax
    `string text`
    
    `string text line 1
     string text line 2`
    
    `string text ${expression} string text`
    
    tag `string text ${expression} string text`
    ```
    
    ${] 를 이용하여 외부 요인으로 변할 수 있는 속성을 적용시킬 수 있다.
    
    조금 더 logical 하게 구현가능하다.
