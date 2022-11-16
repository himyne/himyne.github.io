---
published: true
layout : single
title : "[우아한 프리코스] 3주차 미션 회고 - 로또"

categories:
  - precourse
tags:
  - 우아한 프리코스 3주차

toc: true
toc_sticky: true
toc_label: "3주차 미션 회고"
---

3주차 미션을 하면서 로또의 룰을 새삼 깨달았다.  보너스 번호는 1등이랑 2등 결정 지을때만 필요한거 나만 처음 알았는지 ..?! 😮

로또 프로그램을 만들고 로또를 한도없이 사면서 깨달은 점.. 백만원을 사던 오천원을 사던 당첨 확률은 비슷하고 심지어 더 많은 돈을 쓸수록 잃는 돈이 훨~씬 많았다 ㅋㅋㅋㅋ 그래도 현실에서는 할 수 없는 로또 flex도 해보고 나름 재밌었다. 

그리고 3주차가 되니 점점 잃어가는 허리와 목건강 .. 마지막 남은 4주차를 불태우고 헬스장으로 건강을 되찾으러 가야겠다 ✊🏻

## 시작하며

아래는 내가 제출한 PR 주소와 미션 링크이다.

[https://github.com/woowacourse-precourse/javascript-lotto/pull/483](https://github.com/woowacourse-precourse/javascript-lotto/pull/483)

[https://github.com/woowacourse-precourse/javascript-lotto](https://github.com/woowacourse-precourse/javascript-lotto)

이번 주차에서는 클래스 분리와 도메인 로직에 대한 테스트 작성에 중점을 두어야 하는 주차였다.

불과 2달 전, 클래스 문법을 딥다이브 책에서 열심히 공부하고 정리했던 기억도 있는데 직접 클래스를 다루려고 하니 어렵게만 느껴졌다.

[https://himyne.github.io/deepdive/deepdive-25/](https://himyne.github.io/deepdive/deepdive-25/)

사전적 정의와 예제 코드를 통해 이론을 익히는 것, 실제 코드를 작성하면서 부딪혀보는 것 둘 다 병행이 되어야 진짜 내가 안다고 할 수 있는 것 같다.

앞으로 우테코 프리코스가 끝나더라도 딥다이브 스터디원들과 함께 계속 자바스크립트 과제를 구현하는 연습을 통해 실용적인 공부를 해봐야겠다 !

## 클래스 분리

내가 했던 클래스 분리 방법은 이렇다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8bbab8f6-c429-4c0f-bfe1-5eba5e2b031b/Untitled.png)

처음에는 클래스를 기능별로 나눌까? 라고 생각해서 많은 클래스 파일을 만들었었다. 로또를 발행하는 클래스, 로또를 추첨하는 클래스, 결과를 출력하는 클래스 등등.. 그런데 오히려 기능별로 파일을 만드니 가독성이 떨어지는 것 같았고 파일이 너무 많아지는 바람에 정리된 느낌이 들지 않았다.

이렇게 클래스 분리에 대해 고민을 하던 중 다시 요구사항을 유심히 읽어보고 힌트를 얻었다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac99c75e-2d87-47e6-b95f-a0f4d361b694/Untitled.png)

Lotto 클래스에서 당첨 번호를 인자 numbers 넘겨받고 유효성 검사를 한 뒤에 값이 유효하면 private 변수로 재할당하는 방식으로 클래스가 짜여있었다.

Lotto 클래스가 당첨 번호를 입력받고 그 입력값을 처리하는 것처럼 총 3번의 입력에 대한 클래스를 만들면 되겠다라고 생각했다.

그래서 결국 LottoAmount(구입금액), Lotto(당첨 번호), Bonus(보너스 번호) 총 3개의 클래스로 분리하여 코드를 작성해 나갔다.

그리고 3번의 입력을 받는 부분은 UserInput 클래스에 게임 순서대로 코드를 작성했다.

아직까지 클래스 분리에 대한 부분은 어떻게 하는게 맞는지 확신이 서진 않지만 지난 주차에서는 하지 못했던 클래스 분리를 해냈다는 것부터 내가 성장하였다는 증거가 아닐까 ! 

다음주차 미션에서는 어떤 성장을 이뤄낼지 벌써 기대가 된다 🤗

## private 접근 제한자

이전 요구사항에서는 없던 로또 클래스 내의 `#number` 가 눈에 띄었다. 왠지 요구사항으로 그냥 지나가면 안될 것 같았고 private 접근 제한자에 대해 공부를 해보았다.

우선 private 접근 제한자는 2021년 1월에 나온 친구이다. 캡슐화와 정보 은닉이 완전하게 되지 않는 자바스크립트의 단점을 보완하고자 나왔다고 한다.

나온지 얼마 안된 문법이라 그런가 구글링을 해봐도 많은 정보가 나오지는 않아서 더욱 어떻게 사용해야 할지 어려웠다.

어쨌든 private의 사용 목적이 정보 은닉이기 때문에 은닉되어야 하는 변수들을 외부에서 접근했을 때 수정 가능할까?라는 의문을 가지고 내 코드를 계속 살펴보며 코드를 작성했다.

아직은 private을 적재적소에 잘 활용하지 못하는 것 같아 아쉬움이 남았다. 다른 분들의 코드도 보고 더  자세히 공부하여 다음 주차 미션에서는 좀 더 내 코드에 확신을 가지고 싶다.

## 숨어있는 자바스크립트의 허점 발견

이 주제는 사실 그냥 코드를 작성하다가 재밌는 것을 발견해서 나중에 회고글에 써야지라고 생각해두었던 내용이다.

```jsx
// 금액 amount가 1000원 이하인지 검사하는 코드
if (amount < 1000) {
    error(ERROR.UNDER_THOUSAND);
  }
```

readLine의 특성상 콘솔의 입력은 모두 문자열로 들어온다. 그렇다는 것은 amount가 문자열 `'1000'` 으로 들어왔다는 것이다. 

근데 왜 숫자 `1000`보다 작은지 검사했을 때 제대로 검사가 되는걸까??

처음에는 문자열을 숫자타입으로 바꿔준 후에 유효성 검사를 해야하나 싶었는데 굳이 그럴 필요가 없겠구나를 깨달았다. 

논리 연산자로 이루어진 표현식을 평가하기 위해 문자열이 숫자로 암묵적 타입 변환이 일어나기 때문이다 !

역시 자바스크립트는 다른 문법과는 달리 신기한 점이 많다. 그래서 더 재밌는걸지도 ..?

## ESLint와 Prittier 적용

지난 주차들에는 이미 vscode에 깔려있는 코드 포맷터 prittier만 적용시켰었다.

그런데 혹시나 하여 우테코의 요구사항을 찬찬히 읽던 중 airbnb style guide를 따른다는 말이 눈에 밟혔다.

그래서 이번 주차부터는 ESLint에 Airbnb style guide를 적용시키고 Prittier와 충돌이 일어날 수 있는 상황을 방지하는 코드도  추가해보았다.

[도움이 되었던 블로그 글]([https://it-eldorado.tistory.com/175](https://it-eldorado.tistory.com/175))

## 도메인 로직과 비즈니스 로직 ??

이번 주차 공통 피드백으로 도메인 로직에 대한 테스트 코드를 작성하라고 하셨다.

그런데 도메인 로직이 뭔지도 모르는 나는 구글링으로 또 새로운 개념을 배웠다 ✏

[[비즈니스 로직, 도메인 로직이 대체 뭐야?](https://velog.io/@eddy_song/domain-logic)

참고했던 블로그인데 (글 제목 === 내심정) 이었고, 도움이 많이 되었다.

도메인 로직은 현실 문제에 대한 의사결정을 하는 코드라고 한다.

그렇다면 로또 프로그램에서 의사결정을 담당하는 도메인 로직은 무엇일까 생각해보았다.

로또를 발행하는 클래스는 다음과 같은 순서로 코드가 이루어져있을 것이다.

1. **입력받은 로또 구입 금액이 유효한 값인지 확인한다.** 
2. 유효하다면 금액을 1000으로 나누어 콘솔에 수량을 출력하고, 유효하지 않다면 에러를 띄운다.
3. **수량만큼 랜덤한 숫자 6개를 만든다.**
4. 사용자에게 발행한 로또 번호들을 콘솔에 출력하여 보여준다.

위 네가지 중에서는 굵게 표시된 번호가 의사결정에 해당하는 부분이고, 나머지는 UI(User Interface)에 해당하지 않나라고 생각하여 두 가지 사항에 대해서만 테스트 코드를 작성하였다.

그런데 또 내가 정답인지는 확실하지 않다. 역시 성장에는 나보다 잘하는 사람의 피드백이 필요하다는 것을 느낀다 😥 

## 다음 주차는 !!

회고 글을 쓰는 와중에 4주차 미션과 공통 피드백을 받았다.심지어 내 코드의 허점들이 보이기 시작했다. 비즈니스 로직과 UI 로직을 분리하라는 피드백을 보자마자 생각난 나의 미천한 코드들 😂

```jsx
class LottoAmount {
  #lottoAmount;

  constructor(money) {
    checkLottoAmount(money);
    this.#lottoAmount = money / NUMBER.THOUSAND_WON;
    print(OUTPUT.PURCHASED_AMONUT(this.#lottoAmount)); // print 야.. 너 왜 거깄니 .. 
  }

  publishUserLotto() {
    const publishedUserLotto = [];

    for (let index = 0; index < this.#lottoAmount; index++) {
      let eachUserLottoNumber = random();
      publishedUserLotto.push(eachUserLottoNumber);
      print(`[${eachUserLottoNumber.join(', ')}]`); // 여기도 있네 ? ..
    }
    return publishedUserLotto;
  }
```

황급히 피드백을 수용한 코드를 짜보았다.

UserInput에서 print를 하고 LottoAmount에는 print 문을 없앴다. 

```jsx
// UserInput.js 
class UserInput {
  play() {
    readLine(INPUT_QUERY.LOTTO_AMOUNT, this.handleInputMoney.bind(this));
  }
	// handleInputMoney : 금액 입력 받는 메서드
  handleInputMoney(money) {
    this.lottoAmount = new LottoAmount(money);
    print(OUTPUT.PURCHASED_AMONUT(this.lottoAmount.getLottoAmount()));
    this.publishedLotto = this.lottoAmount.publishUserLotto();
    this.publishedLotto.forEach((eachUserLottoNumber) =>{
      print(`[${eachUserLottoNumber.join(', ')}]`);
    })
    readLine(INPUT_QUERY.WINNING_NUMBER, this.handleWinningNumber.bind(this));
  }
}
```

이렇게 하니 UserInput.js 의 메서드 내부가 또 너무 복잡해보인다.

다음 번에는 출력 부분도 다른 파일에 나누는 것이 좋겠다.

```jsx
// LottoAmount.js
class LottoAmount {
  #lottoAmount;

  constructor(money) {
    checkLottoAmount(money);
    this.#lottoAmount = money / NUMBER.THOUSAND_WON;
  }

  getLottoAmount() {
    return this.#lottoAmount;
  }

  publishUserLotto() {
    const publishedUserLotto = [];

    for (let index = 0; index < this.#lottoAmount; index++) {
      let eachUserLottoNumber = random();
      publishedUserLotto.push(eachUserLottoNumber);
    }
    return publishedUserLotto;
  }
}
```

클린해진 LottoAmount 클래스 내부이다. 확실히 더 좋아보인다.

이번 주차도 아쉬운 점 투성이지만 피드백 내용을 미리 사전에 다 지킨 사람은 천재만재아닐까 ?

다음 주차도 후회되는 마음은 넣어두고 배움에 집중해야겠다.

## 마치며 💨

글을 너무 두서없이 쓴 것 같지만 그만큼 정신이 없었던 주차였다.

정말 새로 알게 된 개념도 너무 많았고 어려워진 문제 난이도에 복습해야 할 개념들도 많았다.

갈 길이 멀었지만 그래도 성장했다는 것은 몸소 느끼고 있으니 그걸로 되었다 😇

다음 주차도 건강 챙겨가며 미션을 잘 마무리해보고 싶다.