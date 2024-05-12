# ReactStudy

## ReactEX
- React.useState()에 대해 다뤄보고 학습한 파일

-------------------------------

## react-study
- ReactEX와 별개로 따로 폴더를 만들어 학습 중..

### 학습 시작
1. node.js 다운
2. 터미널 열어서 아래 확인
   ```
   (base) seongjaeyong@seongjaeyong-ui-MacBookAir Documents % node -v
   v17.4.0
   (base) seongjaeyong@seongjaeyong-ui-MacBookAir Documents % npx
   
   Entering npm script environment at location:
   /Users/seongjaeyong/Documents
   Type 'exit' or ^D when finished

   sh-3.2$ exit
   exit
   (base) seongjaeyong@seongjaeyong-ui-MacBookAir Documents % 
   ```
3. 확인되었으면 Reactapp 생성
   ```
   (base) seongjaeyong@seongjaeyong-ui-MacBookAir Documents % npx create-react-app react-study
   ```
4. vscode로 해당 폴더로 열어서 ctrl + shift + ~ 를 눌러 터미널을 연 후 아래 코드 입력
   ```
   seongjaeyong-ui-MacBookAir:react-study seongjaeyong$ npm start
   ```
5. 그러면 디폴트로 localhost:3000 로 React App 웹페이지 생성됨
6. src 폴더 안에 index.js와 App.js 빼고 모두 삭제
7. 두 파일을 아래 코드로 변경 (맨 기본으로 초기화)
   - index.js
     ```
     import React from 'react';
     import ReactDOM from 'react-dom/client'; // 임포트 경로 변경에 주목하세요
     import App from './App';
     
     const container = document.getElementById('root');
     const root = ReactDOM.createRoot(container); // 루트 인스턴스를 생성합니다.
     root.render(<App />); // 루트 인스턴스를 사용하여 렌더링합니다.
     ```
   - App.js
     ```
     function App() {
       return (
         <div>
             <h1>Welcome back!</h1>
         </div>
       );
     }
     
     export default App;
     ```
8. vscode에서 새로운 터미널을 하나 더 열어서 아래 코드 입력 (ReactEX 파일에서 학습한 PropTypes 다운)
   ```
   seongjaeyong-ui-MacBookAir:react-study seongjaeyong$ npm install prop-types
   ```

### 코딩 시작
- useState에 이어서 useEffect 사용법
  ```
   // src/App.js
   import Button from "./Button";
   import styles from "./App.module.css";
   import { useState, useEffect } from "react";
   
   function App() {
   
     const [counter, setCounter] = useState(0);
     const onClick = () => setCounter((prev) => prev + 1);
   
     const [keyword, setKeyword] = useState("");
     const onChange = (event) => setKeyword(event.target.value);
   
     //처음 실행될 때 한번만 실행되는 코드
     useEffect(() => {
       console.log("i run only once");
     }, []);
   
     //keyword가 변화할때 마다 실행되는 코드
     useEffect(() => {
       console.log("i run when keyword changes");
     },[keyword]);
   
     //counter가 변화할때 마다 실행되는 코드
     useEffect(() => {
       console.log("i run when counter changes");
     },[counter]);
   
     //keyword & counter가 변화할때 마다 실행되는 코드
     useEffect(() => {
       console.log("i run when keyword & counter changes");
     }, [keyword, counter]);
   
     return (
       <div>
           <input value={keyword} onChange={onChange} type="text" placeholder="Search here..."/>
           <h1 className={styles.title}>{counter}</h1>
           <button onClick={onClick}>Click me</button>
           <Button text="Continue"/>
       </div>
     );
   }
   
   export default App;
  ```
