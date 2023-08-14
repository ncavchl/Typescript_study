# learn-typescript

인프런의 [타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner) 온라인 강의 리포지토리입니다.

[![typescript-beginner](https://joshua1988.github.io/images/posts/web/inflearn/typescript-beginner-kor.png)](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner)

## 개발 환경

- [Chrome](https://www.google.com/intl/ko/chrome/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Node.js LTS 버전(v10.x 이상)](https://nodejs.org/ko/)
- [Git](https://git-scm.com/downloads)

💡 참고 사항 : 수업에서는 VSCode를 기준으로 설명합니다. 별도로 선호하시는 IDE가 있다면 그걸 쓰셔도 괜찮습니다 😄

## VSCode 플러그인 목록

- 색 테마 : [Night Owl](https://marketplace.visualstudio.com/items?itemName=sdras.night-owl)
- 파일 아이콘 테마 : [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
- 문법 검사 : ESLint, [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
- 실습 환경 보조 : [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- 기타
  - [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode), [Project Manager](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager), [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag), [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens), [Atom Keymap](https://marketplace.visualstudio.com/items?itemName=ms-vscode.atom-keybindings), [Jetbrains IDE Keymap](https://marketplace.visualstudio.com/items?itemName=isudox.vscode-jetbrains-keybindings) 등

## License & Copyright

**Copyright © 2020 Captain Pangyo**
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivs 4.0 Unported License</a>.


## 강의 메모
### interface, type 차이
- type 별칭 사용시 타입의 모습(내부 요소)을 프리뷰로 바로 확인 가능함
- type 별칭 : 새로운 타입 값을 하나 생성하는 것이 아닌, 정의한 타입에 나중에 쉽게 참고할 수 있게 이름을 부여하는 것
- **타입의 확장 가능/불가능 여부**
- 인터페이스는 확장이 가능함(extends), 타입 별칭이 불가능하므로 `type` 보다 `interface` 사용 권장
- [좋은 소프트웨어는 언제나 확장이 용이해야한다는 원칙](https://ko.wikipedia.org/wiki/%EA%B0%9C%EB%B0%A9-%ED%8F%90%EC%87%84_%EC%9B%90%EC%B9%9/)


## 타입 가드
- 특정 타입으로 타입의 범위를 좁현나가는(필터링 하는) 과정


```ts
// 유니온 타입
function askSomeone(someone: Developer | Person) {
  someone.name; // O
  someone.age; // X - 공통된 속성에 대해서만 정의 가능(타입 가드)
}

// 인터섹션 타입
function askSomeone(someone: Developer & Person) {
  someone.name; // O
  someone.age; // O 
}
```


## Enums
- 특정 값들의 집합을 의미하는 자료
```ts
// 숫자형 이넘
enum Shoes {
  Nike,
  Adidas,
}

const myShoes = Shoes.Nike;
console.log(myShoes); // 0

// 문자형 이넘
enum Shoes {
  Nike = '나이키',
  Adidas = '아디다스',
}

const myShoes = Shoes.Nike;
console.log(myShoes); //  "\uB098\uC774\uD0A4"

// 활용

enum Answer {
  yes = 'Y',
  no = 'N',
}
function ask(ans: Answer) {
  if (ans === Answer.yes) {
    console.log('');
  }
  if (ans === Answer.no) {
    console.log('');
  }
}

ask(Answer.yes);
ask(Answer.no);
ask('N'); // error
```

### Class
- class: 인스턴스 생성 `constructor() {}`
```ts
class Person {
  name: string;
  age: number;

  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
const capt = new Person('Steve', 100);
```
- 자바스크립트 prototype 기반 언어다
  - 모든 객체들이 메소드와 속성들을 상속 받기 위한 템플릿으로써 `prototype object`를 가진다.
  - `prototype chain` : 프로토타입 객체도 또 다시 상위 프로토타입 객체로부터 메소드와 속성을 상속 받을 수도 있고, 그 상위 프로토타입 객체도 마찬가지. 다른 객체에 정의된 메소드와 속성을 한 객체에서 사용할 수 있도록 하는 근간
- class 대신 함수형 문법으로도 생성 가능
``` ts
function Person(name: string, age: number) {
  this.name = name;
  this.age = age;
}

const capt = new Person('캡', 100);
```

### 함수 선언 vs 클래스 선언
1. 클래스
   - 리액트 예전 문법
   - 클래스 기반 코드
   - ```ts
     class App extends React.Component { } 
     ```
   - state 및 lifeCycle 메소드 사용하여 컴포넌트 관리 가능
   - 보다 복잡한 로직 구현 가능
   - 코드 길이 증가로 가독성 저하
  
2. 함수 선언
   - 리액트 최신 문법
   - 훅 기반의 함수형 코드
   - ```ts
     // 함수 선언식
     function App() { ... }

     // 함수 표현식(할당식)
     const App = () => { ... } 
     ```
   - 간결하고 가독성이 높음
   - Hooks 사용을 통해 state, lifeCycle 기능 활용 가능
   - 재사용성 증가 - 훅을 통해 로직을 분리, 재사용 가능한 함수 작성 가능
   - 코드 스플리팅 더 쉽게 사용 가능
   - **함수 선언식**
     - 함수 이름과 함께 선언하는 방식
     - hoisting 에 영향 받지 않음
     - 함수 정의 전 호출 가능
     - 전체 블록 내에서 사용 가능
   - **함수 표헌식**
     - 변수에 함수 할당 방식 (익명 함수)
     - hoisting 에 영향 받음
     - 변수 선언된 이후에만 호출 가능
     - 선언된 범위 내에서만 사용 가능
    
### 타입 단언 (type assertion)
- `as` 키워드 사용
- 내가 정의한 타입으로 간주해라
- DOM API 조작시에 많이 사용
```ts
var div = document.querySelector('div'); // querySelector 하위에 들어간 태그에 맞게 div 타입 정의됨

// div 는 null 일 수도 있기 때문에 에러 발생
div.innerText ...

// 일반적인
if (div) {
  div.innerText ... // div 가 있는지 확인 후 사용해야 함
}

// 단언
var div = document.querySelector('div') as HTMLDivElement;
div.innerText .. // 사용가능
```

### 타입 가드 (type quard)
- 특정 범위 안에서 런타입 타입 검사를 수행하는 표현식
```ts
  // 타입 가드
function isDeveloper(target: IDeveloper | IPerson): target is IDeveloper {
  return (target as IDeveloper).skill !== undefined;
}

const tony: IDeveloper = { name: 'ff', skill: 'ff' };

if (isDeveloper(tony)) {
  console.log(tony.skill);
} else {
  console.log(tony);
}
```

### 타입 호환 (type compatibility)
- 특정 타입이 다른 타입에 맞는지를 의미
```ts
interface IIronman {
    name: string;
  }

  let hero: IIronman = { name: 'f' };

  const capt = { name: 'test', location: 'tet' };

  hero = capt;

  console.log(hero);

  class Avengers {
    name: string;
    constructor(name: string) {
      this.name = name;
    }
  }

  let i: IIronman = { name: 'f' };

  i = new Avengers('f');

  class Hulk {
    handSize: number;
    constructor(name: string, handSize: number) {
      this.handSize = handSize;
    }
  }

  class Captain {
    handSize: number;
    constructor(handSize: number) {
      this.handSize = handSize;
    }
  }

  let a: Hulk = { handSize: 1 };
  let s: Captain = { handSize: 1 };

  a = s; // OK
  s = a; // OK
```
