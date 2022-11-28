---
published: true
layout : single
title : "[우아한 프리코스] 4주차 미션 회고 - 다리 건너기"

categories:
  - precourse
tags:
  - 우아한 프리코스 4주차

toc: true
toc_sticky: true
toc_label: "4주차 미션 회고"
---

드디어 4주차까지 모든 미션이 끝이났다.

3주 후에는 최종 코딩테스트가 있다. 혹시나 주어질 기회를 놓치지 않기 위해 치열하게 공부하고, 그동안 미션 진행에 힘을 쓰느라 하지 못했던 피어리뷰, 스터디에도 참여해보려고 한다.

그런데 한 가지 두려운 것은 최종 코딩 테스트를 치르지도 못하는 상황이 왔을 때의 내 멘탈이다.

멘탈 회복은 3주 뒤의 나에게 맡기고.. 그래도 후회는 없어야 하니까, 그리고 성장해야하니까 !!

최종 코딩테스트까지 남은 3주도 열심히 달려 🏃🏻‍♀️

---

[다리 건너기 미션 PR링크](https://github.com/woowacourse-precourse/javascript-bridge/pull/220/files)

[다리 건너기 미션 요구사항 링크](https://github.com/woowacourse-precourse/javascript-bridge)

이번 주 미션은 오징어 게임에서 나왔던 게임이랑 유사했다! 그래서 문제를 이해하는 시간이 얼마 안걸렸던 것 같다.

![Untitled](/assets/images/precourse-10.png)

추가된 요구사항이 많아 꼼꼼히 읽어봐야했고, 이미 주어진 파일 내의 객체를 활용해야 했기에 고민해야할 부분이 많았다.

이번 회고에서는 겪었던 문제 상황들과 어떻게 학습하여 해결해 나갔는지 적어보려한다.

## 에러가 발생하면 재입력받기

![Untitled](/assets/images/precourse-11.png)

![Untitled](/assets/images/precourse-12.png)

이렇게 비교하고 보니까 안보일만 했구나 싶기도 하다 ..

원래 이전에는 에러 메시지 출력후 “종료”였는데 이번 주차에서는 “그 부분부터 입력을 다시 받는다”로 변경되었다.

이 요구사항을 보자마자 얼마전에 딥다이브 스터디 시간에 다뤘던 try …catch문이 떠올랐다. 그런데 문제는 이론만 알고 있었지 실제 사용은 해본적이 없다는 거였다.

이 요구사항 덕분에 실제로 try ...catch문을 사용해보기도 하고 또 한 단계 성장했다 😇

아래는 내가 작성한 입력을 처리하는 클래스의 코드이다.

```jsx
class InputHandling {
  #answerBridgeArray;
  #bridgeGame;

  play() {
    readBridgeSize(this.handleBridgeSize.bind(this));
  }

  handleBridgeSize(size) {
    try {
      checkBridgeSize(size);
      this.generateAnswerBridge(size);
    } catch (error) {
      Console.print(error);
      readBridgeSize(this.handleBridgeSize.bind(this));
    }
  }

  generateAnswerBridge(size) {
    this.#answerBridgeArray = makeBridge(size, generate);
    this.#bridgeGame = new BridgeGame(this.#answerBridgeArray);
    readMoving(this.handleMovingValue.bind(this));
  }

  handleMovingValue(direction) {
    try {
      checkMovingValue(direction);
      this.decideNextConsolePrint(direction);
    } catch (error) {
      Console.print(error);
      readMoving(this.handleMovingValue.bind(this));
    }
  }

  decideNextConsolePrint(direction) {
    const gameOutcome = this.#bridgeGame.decideMoveOrStop(direction);
    if (gameOutcome === GAME_OUTCOME.FAIL)
      readGameCommand(this.handleGameCommand.bind(this));
    if (gameOutcome === GAME_OUTCOME.FINAL_SUCCESS) Console.close();
    if (gameOutcome === GAME_OUTCOME.SUCCESS)
      readMoving(this.handleMovingValue.bind(this));
  }

  handleGameCommand(command) {
    try {
      checkRestartOrDone(command);
      this.decideRetryOrDone(command);
    } catch (error) {
      Console.print(error);
      readGameCommand(this.handleGameCommand.bind(this));
    }
  }

  decideRetryOrDone(command) {
    if (command === GAME_COMMAND.RESTART) {
      this.#bridgeGame.retry();
      readMoving(this.handleMovingValue.bind(this));
    }
    if (command === GAME_COMMAND.QUIT) {
      this.#bridgeGame.quit();
      Console.close();
    }
  }
}
```

코드를 작성할 때는 미처 생각지 못했다가 다른 분들의 코드를 보면서 깨달은 부분인데, 3번의 입력동안 try …catch문이 반복되니 재사용할 수 있도록 했다면 코드가 훨씬 간결해졌을 것 같다. InputHandling 클래스만 유독 길어서 어떻게 줄일 수 있을까 고민을 많이 했었는데 이 점을 생각치 못한 것이 너무 아쉬웠다.

남은 3주간 더 공부해서 이 클래스의 코드를 디벨롭 시켜봐야겠다 !!

## 파일 구조와 MVC 패턴

![Untitled](/assets/images/precourse-13.png)

이번에는 저번 주차에서 못지켰던 UI 로직과 비즈니스 로직을 분리했다.

콘솔에 나타나는 부분은 모두 View 폴더에 있고 게임 진행과 관련된 파일은 BridgeGame에 두었다.

이번주차는 사실 우테코에서 파일을 나누어 준 바람에 어떻게 파일을 분리할지 조금 더 감이 잡혔던 것 같다.

![Untitled](/assets/images/precourse-14.png)

이번 주차에는 위와 같이 파일을 설명하는 부분도 README 파일에 넣어보았다.

그리고 우테코 프리코스 이전에 MVC 패턴에 대해 공부했기도 했고 많은 분들이 사용하시는 것을 보고 이번 주차 미션에서 적용해볼까 고민을 했었다.

[MVC 창시자가 말하는, MVC의 본질](https://velog.io/@eddy_song/mvc)

[프론트엔드에서 MV_ 아키텍쳐란 무엇인가요?](https://velog.io/@teo/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-MV-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

그런데 위 두 글을 보고 생각이 바뀌었다.

요즘에는 MVC 패턴 이후에 MVVM, MVI 패턴 등 여러가지 패턴이 등장했고 아키텍처의 패러다임이 빠르게 변하고 있다고 한다.

결국 MVC 패턴이 도입된 본질은 피드백 문서에도 있듯이 비즈니스 로직과 UI 로직을 나누기 위함이니 이것만 잘 지키면 되지 않을까 싶었다.

그래서 UI로직은 모두 View 폴더에 넣었고 나머지는 객체가 하는 기능에 따라 파일을 분리했다.

## 객체지향 프로그래밍에 대해 ..

아래는 지난 주차의 피드백 문서 내용의 일부이다.

### 📝 3주차 피드백 문서 내용

- 객체는 객체스럽게 사용한다 - 데이터를 꺼내지(get) 말고 메시지를 던지도록 구조를 바꿔 데이터를 가지는 객체가 일하도록 한다.
- 비즈니스 로직과 UI 로직을 분리한다 - 비즈니스 로직과 UI 로직을 한 클래스가 담당하지 않도록 한다. 단일 책임의 원칙에도 위배된다.

---

그리고 피드백 문서를 유심히 읽어봤을 때, 객체 지향적으로 프로그램을 설계하도록 유도하는 것 같아 객체 지향 원칙을 열심히 공부했다.

[객체지향 프로그래밍과 javascript (약간의 역사를 곁들인...)]([https://velog.io/@teo/oop](https://velog.io/@teo/oop))

[Javascript에서도 SOLID 원칙이 통할까?](https://velog.io/@teo/Javascript%EC%97%90%EC%84%9C%EB%8F%84-SOLID-%EC%9B%90%EC%B9%99%EC%9D%B4-%ED%86%B5%ED%95%A0%EA%B9%8C)

위 두 문서를 읽고 코드에 적용해보려 했지만 이론 공부만으로 객체 지향을 코드에 적용해보기는 매우 어려웠다. 남은 주차동안 객체지향에 대해 더 학습하고 코드를 더 객체스럽게 리팩토링 해봐야할 것 같다.

## 함수를 인자로 전달하기

아래 makeBridge 함수의 인자로 다리의 길이와(size) 랜덤 숫자 0이나 1을 반환하는 함수인 generate()를 전달해주어야 했다.

![Untitled](/assets/images/precourse-15.png)

처음에는 generateRandomNumber라는 함수를 넘겨줄 때 순간 아무 생각 없이 괄호를 넣었었다.

```jsx
makeBridge(size, generate());
```

위와 같이 했다가 “generateRandomNumber is undefined”라는 에러가 발생했다.

그래서 괄호를 삭제하고 함수 이름만 넣었더니 정상적으로 잘 작동이 되었다.

사실 이것도 공부했던 내용인데 함수를 인자로 넘겨준 적이 많이 없어서 순간 헷갈렸던 개념이었던 것 같다.

Deepdive 책의 “18장 - 함수와 일급 객체” 챕터를 리마인드 해보자.

✏ **일급 객체의 조건**

- 변수나 객체 배열에 저장할 수 있다.
- 함수의 매개변수에 전달할 수 있다.
- 함수의 반환값으로 사용될 수 있다.

함수는 위 조건을 모두 만족하여 값으로 취급되는 일급 객체이다. 그리고 함수 객체는 일반 객체와 달리 괄호와 함께 호출 가능하다.

인자로 넘겨줄 때나 객체에 함수를 저장할 때는 괄호 없이 함수의 이름만 입력해주어야 한다 !!

---

## 리팩토링

이번 미션의 추가 중점 사항은 리팩토링이었다.

기존의 15줄 제한과는 달리 10줄 제한이 있는 만큼 더욱 코드와 눈싸움하는 시간이 길었다.

아래는 다리를 만드는 makeBridge 파일에서 리팩토링 전 코드이다.

```jsx
//리팩토링 전
makeBridge(size, generateRandomNumber) {
    let bridgeArray = Array(Number(size)).fill('');
    bridgeArray = bridgeArray.map((item) => item + generateRandomNumber());

    return bridgeArray.map((zeroOrOne) =>
      zeroOrOne.replace(zeroOrOne, replaceString(zeroOrOne))
    );
  },

const replaceString = (zeroOrOne) => {
    if (zeroOrOne === '1') return 'U';
    if (zeroOrOne === '0') return 'D';
}
```

사실 이 makeBridge 파일은 객체의 프로퍼티 추가가 불가능했기 때문에 makeBridge 함수에서 10줄이내로 모든 작업을 수행해야 했다.

그럼에도 불구하고 리팩토링 전 코드에 있던 replaceString 함수를 따로 뺀 이유는 return 문의 depth가 3이 넘어갔기 때문이었다.

이 파일의 코드가 유독 마음에 들지 않아서 정리해두었던 클린코드 강의 내용을 다시 훓어보고 왔는데 삼항연산자가 문득 떠올랐다.

```jsx
//리팩토링 후
makeBridge(size, generateRandomNumber) {
    let bridgeArray = Array(Number(size))
      .fill('')
      .map((item) => item + generateRandomNumber());
    return bridgeArray.map((zeroOrOne) =>
      zeroOrOne.replace(zeroOrOne, zeroOrOne === '1' ? 'U' : 'D')
    );
  }
```

아직은 초보라 그런지 메서드 체이닝과 삼항연산자를 사용하는 습관이 안들어있는 것 같다.

그래도 집요히 리팩토링을 포기하지 않아서 이렇게나 깔끔히 줄일 수 있었던 것에 다행이라고 생각한다.

삼항연산자가 또 유용하게 쓰인 곳이 있다.

```jsx
printResult(upperMapArray, lowerMapArray, attemptNumber) {
    const totalMapArray = [...upperMapArray, ...lowerMapArray];
    const outcome = totalMapArray.includes(LETTER_SIGN.WRONG) ? GAME_OUTCOME.FAIL : GAME_OUTCOME.SUCCESS;

		Console.print(OUTPUT.FINAL_GAME_RESULT);
    this.printMap(upperMapArray, lowerMapArray);
    Console.print(OUTPUT.GAME_SUCCESS_OR_NOT(outcome));
    Console.print(OUTPUT.TOTAL_ATTEMPT_NUMBER(attemptNumber));
  }
```

마지막에 최종 결과가 성공인지 실패인지 판단하여 알맞은 단어를 출력할 때에도 배열에 x가 있으면 실패, 없으면 성공을 출력하도록 하였다.

리팩토링의 필요성을 깨달았으니 이전 주차들도 복습하면서 피드백 문서에 맞춰 리팩토링도 진행해보아야겠다.

## 우아한 프리코스를 마치며🥺

사실 프리코스 이전에 미리 연습한답시고 2주차 미션이었던 숫자 야구 게임을 미리 구현해보았었다.

그때는 불과 2달전인데 어떻게 구현할지 감이 안잡혀 이전 기수분들의 코드를 따라 치는 정도의 실력밖에는 되지 않았었다.

그런데 프리코스 중반 무렵, 내가 스스로 기능 목록을 작성하고 기능 구현도 빠르게 해낼 수 있게 된 것만 봐도 정말 많이 성장한 것 같다.

24살에 본 사주에서 지금까지는 사실 대충 공부했고 25살에 진짜 하고싶은 걸 찾아 공부한다고 한다고 했는데 진짜였다. 참으로 신기하다.

우아한 프리코스를 하면서 공부가 지겹지 않은 적은 처음이었다. 또 한번 느꼈다. 나는 코딩을 좋아한다는 것을 !

물론 잘해내야한다는 부담감에 끝날 즈음엔 지치기도 했었지만 끝나고 나니 아쉬움이 너무 컸다.

스터디에서 지난 과정을 복습하고 새로운 것들을 배우면서 이 아쉬움을 채워나가야겠다.

프리코스를 참여할 수 있게 해주신 우테코 코치님들께 정말 감사드린다💌
