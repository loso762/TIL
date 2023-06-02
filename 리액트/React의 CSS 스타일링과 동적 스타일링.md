## 🤔 React에서 CSS를 어떻게 적용할 수 있을까?
React에서 CSS를 이용해 컴포넌트를 스타일링하는 방법은 여러가지가 있다. 
그 중 가장 일반적인 3가지 방법, 즉 인라인 스타일링, Styled Components, 그리고 CSS Modules에 대해 설명하고, 각각의 방법을 언제 사용하면 좋을지에 대해 알아보도록 하자.

<br><br>

## Inline Style
인라인 스타일링은 CSS를 직접 컴포넌트에 적용하는 가장 간단한 방법이다. 
이를 위해 style 속성을 사용하며, 이 속성의 값은 JavaScript 객체이므로 중괄호를 두 번 사용한다. 
첫 번째 중괄호는 JSX 내에 JavaScript 표현식을 포함하기 위한 것이고, 두 번째 중괄호는 JavaScript 객체를 생성하는 데 사용되는 것이다.

### 📌 인라인 스타일 적용하기

```
import React from 'react';

function App() {
  return (
    <div style={{ color: 'blue', fontSize: '20px' }}>
      Hello, world!
    </div>
  );
}

export default App;
```

위 방식은 스타일 규칙이 간단하고 조건에 따라 동적으로 스타일을 변경해야 할 때 유용할 수 있다. 
하지만 이 방식의 단점은 스타일 규칙이 복잡해지거나 여러 요소에 동일한 스타일을 적용해야 할 때 관리가 어렵다는 것이다.


```
import React from 'react';

// 스타일 함수를 선언하여 적용
function CustomButton() {
  const buttonStyle = {
    color: 'white',
    backgroundColor: 'blue',
    padding: '10px',
    borderRadius: '5px',
  };

  return <button style={buttonStyle}>Click me!</button>;
}

export default CustomButton;
```

위 코드와 같이 스타일 함수를 선언하여, style 속성에 적용하는 방법도 가능하지만 일반 HTML에 CSS를 적용할 때 처럼 inline style을 사용하여 스타일을 적용하는 방식은 지양하도록 하자.

<br><br>

## className 방식
React에서는 각 html 요소에 css 클래스를 적용할 때 일반적인 HTML과는 다른 속성을 사용하는데, 바로 'className' 속성이다. 
이 속성은 일반 HTML의 'class' 속성에 해당하는 속성이다. CSS 파일에서 정의한 스타일을 JSX 요소에 적용하기 위해 'className' 속성을 사용할 수 있다.

### 📌 'className' 속성 사용하기

```
/* App.css */
.title {
  color: blue;
  font-size: 20px;
}
```

```
// App.jsx
import React from 'react';
import './App.css'; // css 파일 import

function App() {
  return (
    // className 속성에 css 파일에서 선언된 'title' 클래스 지정
    <div className="title">
      Hello, world!
    </div>
  );
}

export default App;
```

위와 같은 className 방식은 CSS 규칙을 별도의 CSS 파일로 분리하여 관리할 수 있으며, HTML과 비슷한 방식으로 스타일을 적용할 수 있다는 장점이 있다. 
하지만, 이는 CSS 클래스가 전역적으로 적용되기 때문에, 다른 컴포넌트에서 'title' 이라는 값을 가진 class가 있다면 충돌이 발생할 수 있다. 
이와 같은 CSS 클래스 이름 충돌 문제를 해결하기 위해서는 추가적인 방법이 필요하다.


### 🤔 그럼, CSS 클래스가 충돌하지 않게 하려면 어떻게 해야할까?
React에서 CSS 클래스 이름 충돌 문제 해결을 위한 대표적인 두 가지 방식이 있는데, 바로 'styled components'를 사용하는 방식과, '모듈 css'를 사용하는 방식이다.

<br><br>

## Styled Components
'styled-components'는 CSS-in-JS 라이브러리 중 하나로서, JavaScript 파일 내에 CSS를 작성하고, 이를 독립적인 컴포넌트로 활용할 수 있도록 한다. 이 라이브러리를 사용하면 CSS 클래스 이름 충돌을 걱정할 필요 없이 컴포넌트 스코프의 스타일을 생성할 수 있다. 'styled-components'를 사용하기 위해서는 몇 가지의 단계를 거쳐야 한다.

### 📌 'styled-components' 사용하기

#### 1. 라이브러리 설치하기
'styled-components'를 사용하기 위해서는 먼저, 해당 라이브러리를 설치해야 한다. 이는 npm을 사용하여 다음과 같이 수행할 수 있다.

```npm install styled-components```

#### 2. 컴포넌트 작성하기
라이브러리를 설치했다면, JSX 파일 내에 스타일을 정의 해보자. 이를 컴포넌트로 사용할 수 있으며, 이때 주의할 점은 백틱(`)을 사용하여 CSS를 작성한다는 점이다.

```
// StyledTitle.jsx
import styled from 'styled-components'; // 설치한 라이브러리를 import 한다.

// 백틱을 사용하여 css를 작성한다.
const StyledTitle = styled.div`
  color: blue;
  font-size: 20px;
`;

export default StyledTitle;
```

#### 3. 다른 컴포넌트에서 import하여 사용하기

```
// App.jsx
import React from 'react';
import StyledTitle from './StyledTitle'; // 스타일 컴포넌트 import

function App() {
  return (
    // 해당 컴포넌트 사용 (StyledTitle 컴포넌트에 작성한 css가 적용된다.)
    <StyledTitle>
      Hello, world!
    </StyledTitle>
  );
}

export default App;
```

위와 같은 방식으로 React에서 'styled-components'를 사용하여 CSS 스타일을 적용할 수 있다.

### 📌 'styled-components'의 '&'기호
'styled-components'에서는 & 기호를 사용하여 자기 자신을 참조하는 'self-reference'를 만들 수 있다. 
이 기능은 하위 선택자를 생성하거나 hover, active 등의 상태를 지정할 때 유용하게 사용된다.

```
import styled from 'styled-components';

const StyledForm = styled.form`
  width: 300px;
  padding: 20px;
  border: 1px solid black;
  border-radius: 10px;
  
  & input {
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    border: 1px solid grey;
    border-radius: 5px;
  }
`;

export default StyledForm;
```

여기서 '& input'은 이 'styled-component' 내부의 <input> 요소들을 참조한다. 
따라서 StyledForm 컴포넌트 내부에 있는 모든 <input> 요소들은 지정한 스타일을 적용받게 된다. 
이때, 코드에서 확인할 수 있듯이 input 자신에게는 'input' 과 '{}' 를 생략해서 작성한다.

```
// & 기호를 사용하여 호버효과 적용하기
import styled from 'styled-components';

const StyledButton = styled.button`
  padding: 10px;
  color: white;
  background-color: blue;
  
  &:hover {
    background-color: darkblue;
  }
`;

export default StyledButton;
```

'&'는 위에서 말했듯 hover, active 등의 상태를 지정하는 데에도 사용된다. 
위 코드에서 '&:hover'는 StyledButton 위에 마우스가 올라갔을 때 해당 스타일을 적용하라는 것을 의미한다.

'styled- components'는 복잡한 스타일 규칙이 필요하거나 컴포넌트 수준에서 동적인 스타일을 적용할 때 유용하다.
CSS를 JavaScript 코드와 같은 파일에서 관리할 수 있으므로 스타일과 컴포넌트 로직을 함께 보며 개발할 수 있다는 장점이 있다. 
하지만, JavaScript 코드와 CSS 코드가 섞여 있어 가독성이 떨어질 수 있다.

<br><br>

## 모듈 CSS (CSS Modules) 방식
CSS 클래스 이름 충돌 문제를 해결하기 위한 방법 그 두번째는 바로 '모듈 CSS'이다.

### 📌 '모듈 CSS' 사용하기
모듈 CSS는 CSS-in-JS가 아닌 일반 CSS를 사용하면서도 CSS의 스코프를 각 컴포넌트에 한정시키는 방법이다. 
이를 통해 전역 네임스페이스에 대한 의존성을 줄이고 코드가 충돌하는 것을 방지할 수 있다.

모듈 CSS를 사용하기 위한 방식은 매우 간단하다. CSS 파일을 생성하되, 파일 이름 뒤에 '.module.css'를 붙인다. 예를 들어, 'Button.module.css'와 같이 파일을 생성할 수 있다.

```
/* Button.module.css */

.container {
  width: 200px;
  height: 50px;
  background-color: lightblue;
}

.container:hover {
  background-color: darkblue;
}
```

위와 같이 작성된 CSS 파일을 React 컴포넌트에서 사용하기 위해 아래와 같이 import하여 사용한다.

```
// Button.jsx

import React from 'react';
import styles from './Button.module.css'; // 모듈 import

function Button() {
  return (
    <div className={styles.container}>
      Click me!
    </div>
  );
}

export default Button;
```

이렇게 하면 CSS의 스코프가 Button 컴포넌트로 한정되며, 다른 컴포넌트에서 동일한 클래스 이름을 사용하더라도 스타일이 충돌하는 문제를 방지할 수 있다.

<br><br>

## 동적 스타일링 적용
이제 위의 방법들을 사용하여 컴포넌트에서 동적인 스타일링을 적용하는 방법에 대해 알아보자.


### 📌 인라인 스타일로 동적 스타일 적용하기
인라인 스타일을 이용하여 동적 스타일을 적용하기 위해, style 객체를 컴포넌트의 state에 연결하는 방법을 사용할 수 있다.

```
// Button.jsx

import React, { useState } from 'react';

function Button() {
  const [backgroundColor, setBackgroundColor] = useState('lightblue');

  const handleClick = () => {
    setBackgroundColor(backgroundColor === 'lightblue' ? 'darkblue' : 'lightblue');
  };

  return (
    <div 
      style={{backgroundColor: backgroundColor}} 
      onClick={handleClick}
    >
      Click me!
    </div>
  );
}

export default Button;
```


### 📌 'styled-components'로 동적 스타일 적용하기
'styled-components'를 사용할 경우 Props를 통해 동적인 스타일을 적용할 수 있다.

```
// Button.jsx

import React, { useState } from 'react';
import styled from 'styled-components';

// 버튼 스타일 컴포넌트
const StyledButton = styled.div`
  width: 200px;
  height: 50px;
  background-color: ${props => props.clicked ? 'darkblue' : 'lightblue'};
`;

// 버튼 컴포넌트
function Button() {
  const [clicked, setClicked] = useState(false);

  return (
    <StyledButton 
      clicked={clicked} 
      onClick={() => setClicked(!clicked)}
    >
      Click me!
    </StyledButton>
  );
}

export default Button;
```

위 예제 코드에서는 StyledButton이라는 styled component를 생성하고, 이 컴포넌트에 clicked라는 prop을 전달한다. 
이 prop에 따라 배경색이 변경되는 로직을 CSS 코드 내부에 삽입함으로서 동적 스타일을 적용하고 있다.


### 📌 '모듈 CSS'로 동적 스타일 적용하기
CSS 모듈을 사용하면 클래스의 이름을 동적으로 변경하여 스타일을 변경할 수 있다.

```
/* Button.module.css */

.normal {
  width: 200px;
  height: 50px;
  background-color: lightblue;
}

.clicked {
  background-color: darkblue;
}
```

```
// Button.jsx

import React, { useState } from 'react';
import styles from './Button.module.css';

function Button() {
  const [clicked, setClicked] = useState(false);

  return (
    <div 
      className={clicked ? styles.clicked : styles.normal}
      onClick={() => setClicked((clicked)=>!clicked)}
    >
      Click me!
    </div>
  );
}

export default Button;
```

위 예제 코드에서는 useState를 사용하여 clicked 라는 상태를 관리하고, 상태에 따라 클래스의 이름을 변경한다. 
이를 통해 버튼이 클릭될 때 마다 스타일이 동적으로 변화한다.
