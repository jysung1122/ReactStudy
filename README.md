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
     import ReactDOM from 'react-dom';
     import App from './App';
     
     ReactDOM.render(
       <React.StrictMode>
         <App />
       </React.StrictMode>,
       document.getElementById('root')
     );
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
