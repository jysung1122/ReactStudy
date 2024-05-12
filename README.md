# ReactStudy

## ReactEX
- React.useState()에 대해 다뤄보고 학습한 파일

-------------------------------

## react-study
- ReactEX와 별개로 따로 폴더를 만들어 학습 중..

### 개발 환경 구축
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

### 학습 시작
1. useState에 이어서 useEffect 사용법
   - App.js
     ```
      // src/App.js
      import Button from "./Button.js";         //파일 따로 생성해야함
      import styles from "./App.module.css";    //파일 따로 생성해야함
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
   - App.module.css
   - .css와 .module.css의 차이점은 .css는 모든 컴포넌트가 적용되는 반면 .module.css는 원하는 컴포넌트만 css스타일 적용 가능
     ```
     .title {
       font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, 
           Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
       font-size: 18;
      }
     ```
   - Button.js
     ```
      import PropTypes from 'prop-types';
      import styles from './Button.module.css';
      
      function Button( {text} ) {
          return <button className={styles.title}>{text}</button>
      }
      
      Button.propTypes = {
          text: PropTypes.string.isRequired,
      }
      
      export default Button;
     ```
   - Button.module.css
     ```
      import PropTypes from 'prop-types';
      import styles from './Button.module.css';
      
      function Button( {text} ) {
          return <button className={styles.title}>{text}</button>
      }
      
      Button.propTypes = {
          text: PropTypes.string.isRequired,
      }
      
      export default Button;
     ```
2. 컴포넌트의 Create와 Destroyed
   - App.js
     ```
      // src/App.js
      import { useState, useEffect } from "react";
   
      function Hello() {
      
        function byFn() {
          console.log("bye :(");
        }
      
        function hiFn() {
          console.log("created :)");
          return byFn;
        }
      
        useEffect(hiFn, []);
      
        // 위 hiFn()과 같음
        // useEffect(() => {
        //   console.log("created :)");
        //   return () => console.log("destroyed :(");
        // }, []);
      
        return <h1>Hello</h1>;
      }
      
      
      function App() {
      
        const [showing, setShowing] = useState(false);
        const onClick = () => setShowing((prev) => !prev);
        return (
          <div>
            {showing ? <Hello/> : null}
            <button onClick={onClick}>{showing ? "Hide" : "Show"}</button>
          </div>
        );
      }
      
      export default App;
   
     ```
3. To Do List
   - App.js
     ```
      import { useState } from 'react';

      function App() {
      
        const [todo, setTodo] = useState('');
        const [todos, setTodos] = useState([]);
      
        const onChange = (e) => setTodo(e.target.value);
      
        const onSubmit = (e) => {
          e.preventDefault();
          if(todo === "") {
            return;
          }
      
          // 비어있는 todos 배열에 todo 값 추가 : todos[3, 2, 1] -> 4 입력 -> todos[4, 3, 2, 1]
          setTodos((currentArray) => [todo, ...currentArray]);
          setTodo("");
        };
      
        return (
          <div>
            <h1>My To Dos({todos.length})</h1>
            <form onSubmit={onSubmit}>
              <input 
                onChange={onChange} 
                value={todo} 
                type="text" 
                placeholder="Write your to do..."
              />
              <button>Add To Do</button>
            </form>
            <hr/>
            <ul>
              {todos.map((item, index) => (
                <li key={index}>{item}</li>
              ))}
            </ul>
          </div>
        );
      }
      
      export default App;

     ```
4. 코인 API 받아와서 달러를 입력하면 몇개의 코인을 얻을 수 있는 지 환전하는 코드
   ```
   import { useEffect, useState } from 'react';

   function App() {
   
     const [loading, setLoading] = useState(true);
     const [coins, setCoins] = useState([]);
   
     useEffect(() => {
       fetch("https://api.coinpaprika.com/v1/tickers?limit=10 ") // ?limit=10 -> 이용하여 최대 2000개 까지 가능
         .then((response) => response.json())
         .then((json) => {
           setCoins(json);
           setLoading(false);
         });
     }, []);
   
     function USDToCoin() {
       const [amount, setAmount] = useState(0);
       const [selectedCoinId, setSelectedCoinId] = useState(0); // 선택된 코인의 id를 관리하는 상태
     
       const reset = () => {
         setAmount(0);
         setSelectedCoinId(0); // 리셋 시 선택된 코인 id도 초기화
       };
     
       const onChange = (event) => {
         setAmount(event.target.value);
       };
     
       const selectedCoin = coins.find((coin) => coin.id === selectedCoinId); // 선택된 코인 객체 찾기
   
       return (
         <div>
           <div>
             <select value={selectedCoinId} onChange={(e) => setSelectedCoinId(e.target.value)}>
               <option value="0">Select a coin</option>
               {coins.map((coin) => (
                 <option key={coin.id} value={coin.id}>
                   {coin.name} ({coin.symbol}): ${coin.quotes.USD.price} USD
                 </option>
               ))}
             </select>
           </div>
           <hr />
           <div>
             <label>If You have </label>
             <input
               value={amount}
               id="usd"
               placeholder="USD"
               type="number"
               onChange={onChange}
             />
             <label> USD</label>
           </div>
           <div>
             <label>So You have </label>
             <input
               value={selectedCoin ? (amount / selectedCoin.quotes.USD.price) : ""}
               id="coin"
               placeholder="COINS"
               type="number"
               onChange={onChange}
               disabled
             />
             <label> {selectedCoin ? selectedCoin.symbol : ''}</label>
           </div>
           <button onClick={reset}>Reset</button>
         </div>
       );
     }
   
     return (
       <div>
         <h1>The {loading ? "" : `${coins.length}`} Coins</h1>
         {loading ? (<strong>Loading...</strong>) : 
           <USDToCoin/>
         }
         
       </div>
     );
   }
   
   export default App;

   ```
