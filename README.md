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
9. React Router 설치 : 페이지를 전환해주는 기능 제공 ( 버전 : "react-router-dom": "^6.23.1" )
    ```
    seongjaeyong-ui-MacBookAir:react-study seongjaeyong$ npm install react-router-dom@latest
    ```
10. Publishing : GitHub Pages에 업로드할 수 있게 해주는 패키지 다운
    ```
    seongjaeyong-ui-MacBookAir:react-study seongjaeyong$ npm install gh-pages
    ```
    10-1. package.json 파일 수정 -> 맨 마지막 } 바로 위에 작성
       ```
          }, // 마지막에서 두번째 괄호에 콤마 추가
        "homepage": "https://jysung1122.github.io/react-movie"
        //"homepage": "https://{YOUR_GITHUB_ID}.github.io/{YOUR_SAVE_REPOSITORY}"
      }   //-> 맨 마지막 괄호
       ```
    10-2. package.json 파일 수정 -> scripts 코드 추가
       ```
       "scripts": {
          "start": "react-scripts start",
          "build": "react-scripts build",
          "test": "react-scripts test",
          "eject": "react-scripts eject",
          //밑에 두 줄 추가
          "deploy": "gh-pages -d build",
          "predeploy": "npm run build"
        },
       ```
    10-3. 아래 코드 실행하면 build폴더를 생성 후 deploy 실행
       ```
       seongjaeyong-ui-MacBookAir:react-study seongjaeyong$ npm run deploy
       ```
    10-4. 에러 뜰 경우 깃허브에 같은 이름의 repository 생성 (나의 경우 react-movie)
    
    10-5. git remote -v 했을때 아무것도 나오지 않는 상태라면 아래 코드로 repository를 추가
       ```
       git remote add origin https://github.com/jysung1122/react-movie
       // git remote add origin https://github.com/{YOUR_ID}/{YOUR_SAVE_REPOSITORY}
       ```
    10-5. 10-3 재실행


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
   - App.js
      ```
      import { useEffect, useState } from 'react';
   
      function App() {
      
        const [loading, setLoading] = useState(true);
        const [coins, setCoins] = useState([]);
      
        useEffect(() => {
          // Coinpaprika API에서 코인 정보를 가져오는 함수
          fetch("https://api.coinpaprika.com/v1/tickers?limit=10 ") // ?limit=10 -> 이용하여 최대 2000개 까지 가능
            .then((response) => response.json())    // 응답 본문을 JSON 데이터로 파싱
            .then((json) => {
              setCoins(json);      // JSON 데이터를 coins 상태 변수에 저장
              setLoading(false);   // 로딩 상태를 false로 설정 (데이터 로딩 완료)
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
