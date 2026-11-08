## 📌 STEP 1. Open Source Project 선택

22101046 신태현 


### 베포URL) : https://taehyeon-weather.vercel.app/


### 1) 프로젝트 선택 이유
- React와 Vite 기반의 간단한 구조로 되어 있어, React의 핵심 개념인 컴포넌트 생명주기와 React Hooks(`useState`, `useEffect`)를 분석하고 학습하기에 매우 적합하여 선택했습니다.
- 백엔드 서버나 데이터베이스 구축 없이 공개 오픈 API(Open-Meteo)를 직접 호출하므로, Vercel 배포 및 독립적인 구동이 용이합니다.
- MIT 라이선스가 적용되어 있어 오픈소스 수정 및 재배포가 자유롭습니다.

### 2) 주요 기능 (3가지)
1. **도시명 기반 실시간 날씨 검색**: 사용자가 입력한 도시의 실시간 기온 및 날씨 정보 조회
2. **최저/최고 기온 표시**: 당일 예보 데이터를 바탕으로 최저 및 최고 기온 출력
3. **위치 및 날짜 포맷팅**: 검색된 도시·국가 정보와 현재 날짜를 포맷팅하여 화면에 렌더링



## STEP 2. Clone & Run

프로젝트 설치 및 로컬 실행 방법:

bash
# 1. 저장소 클론
git clone https://github.com/2026-2-OSS/assign10-c02-22101046.git
# 2. 의존성 패키지 설치
npm install
# 3. 개발 서버 실행
npm run dev

## STEP 3. Source code Exploration

1) project Structure

src/main.jsx: React 애플리케이션의 진입점(Entry Point)으로, HTML의 #root 엘리먼트에 최상위 <App /> 컴포넌트를 마운트합니다.

src/App.jsx: 애플리케이션의 최상위 루트 컴포넌트로, 메인 날씨 화면을 렌더링하는 Weaterapp 컴포넌트를 호출합니다.
  
src/component/Weaterapp.jsx: 날씨 검색, API 데이터 호출, 상태 관리, 화면 렌더링을 모두 담당하는 핵심 메인 컴포넌트입니다.

data.jsx: 요일, 날짜, 월, 연도를 사람이 읽기 쉬운 문자열로 포맷팅해 주는 showDate() 유틸리티 함수를 제공합니다.



2) React Component 역할
App 컴포넌트 (src/App.jsx): 애플리케이션의 최상위 루트 컨테이너 역할을 하며, 하위의 Weaterapp 컴포넌트를 화면에 마운트합니다.
Weaterapp 컴포넌트 (src/component/Weaterapp.jsx):
상태 관리(useState): 사용자의 입력 도시(inputCity, city), 날씨 데이터(posts), 에러 상태(error)를 총괄 관리합니다.
비동기 통신(useEffect): 검색 도시가 변경될 때마다 Open-Meteo API를 호출하여 최신 날씨 데이터를 가져옵니다.
조건부 렌더링: 날씨 데이터가 정상일 때는 날씨 카드를 렌더링하고, 도시를 찾지 못하면 에러 UI를 렌더링합니다.




=======================================================================


# React Weather App 🌤️

A modern and responsive weather application built with React.js and Vite.

The application allows users to search for cities and view real-time weather information using the Open-Meteo API.

## 🚀 Features

- Search weather by city name
- Display current temperature
- Show city and country information
- Display minimum and maximum temperature
- Real-time weather data
- Responsive design for desktop and mobile
- Fast and lightweight application

## 🛠️ Technologies

- React.js
- JavaScript (ES6+)
- HTML5
- CSS3
- Vite
- Open-Meteo API
- React Hooks

## 📦 Installation

Clone the repository:

```bash
git clone https://github.com/fshoja/React-Weather-App.git