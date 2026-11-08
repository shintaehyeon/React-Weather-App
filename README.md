## 📌 STEP 1. Open Source Project 선택

작성자: 22101046 신태현
배포 URL: https://taehyeon-weather.vercel.app/
과제 저장소: https://github.com/2026-2-OSS/assign10-c02-22101046.git
원본 프로젝트 출처: fshoja/React-Weather-App
 (MIT License)

### 1) 프로젝트 선택 이유
- React와 Vite 기반의 간단한 구조로 되어 있어, React의 핵심 개념인 컴포넌트 생명주기와 React Hooks(`useState`, `useEffect`)를 분석하고 학습하기에 매우 적합하여 선택했습니다.
- 백엔드 서버나 데이터베이스 구축 없이 공개 오픈 API(Open-Meteo)를 직접 호출하므로, Vercel 배포 및 독립적인 구동이 용이합니다.
- MIT 라이선스가 적용되어 있어 오픈소스 수정 및 재배포가 자유롭습니다.

### 2) 주요 기능 (3가지)
1. 도시명 기반 실시간 날씨 검색: 사용자가 입력한 도시의 실시간 기온 및 날씨 정보 조회
2. 최저/최고 기온 표시: 당일 예보 데이터를 바탕으로 최저 및 최고 기온 출력
3. 위치 및 날짜 포맷팅: 검색된 도시·국가 정보와 현재 날짜를 포맷팅하여 화면에 렌더링



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

1) project Structure (주요 파일의 역할)

- src/main.jsx: React 애플리케이션의 진입점(Entry Point)으로, HTML의 #root 엘리먼트에 최상위 <App /> 컴포넌트를 마운트합니다.

-src/App.jsx: 애플리케이션의 최상위 루트 컴포넌트로, 메인 날씨 화면을 렌더링하는 Weaterapp 컴포넌트를 호출합니다.
  
- src/component/Weaterapp.jsx: 날씨 검색, API 데이터 호출, 상태 관리, 화면 렌더링을 모두 담당하는 핵심 메인 컴포넌트입니다.

- data.jsx: 요일, 날짜, 월, 연도를 사람이 읽기 쉬운 문자열로 포맷팅해 주는 showDate() 유틸리티 함수를 제공합니다.



2) React Component 역할
App 컴포넌트 (src/App.jsx): 애플리케이션의 최상위 루트 컨테이너 역할을 하며, 하위의 Weaterapp 컴포넌트를 화면에 마운트합니다.
Weaterapp 컴포넌트 (src/component/Weaterapp.jsx):

    상태 관리(useState): 사용자의 입력 도시(inputCity, city), 날씨 데이터(posts), 에러 상태(error)를 총괄 관리합니다.
    비동기 통신(useEffect): 검색 도시가 변경될 때마다 Open-Meteo API를 호출하여 최신 날씨 데이터를 가져옵니다.
    조건부 렌더링: 날씨 데이터가 정상일 때는 날씨 카드를 렌더링하고, 도시를 찾지 못하면 에러 UI를 렌더링합니다.



3) Code Analysis (코드 분석 및 동작 원리)
jsx
// src/component/Weaterapp.jsx 내 날씨 조회 비동기 로직
const geo = await fetch(
  `https://geocoding-api.open-meteo.com/v1/search?name=${city}&count=1&language=ko`
);
const geoData = await geo.json();
if (!geoData.results) {
  setError(true);
  return;
}
const { latitude, longitude, name, country } = geoData.results[0];
const weather = await fetch(
  `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,weather_code&daily=temperature_2m_max,temperature_2m_min&timezone=auto`
);
const weatherData = await weather.json();

동작 원리 설명:
1. 사용자가 입력한 도시 이름(city)을 가지고 Open-Meteo Geocoding API를 호출하여 해당 도시의 위도(latitude)와 경도(longitude) 좌표를 먼저 구합니다.
2. 검색 결과가 없으면 setError(true)를 호출하여 'City not found' 에러 화면을 띄웁니다.
3. 좌표를 정상적으로 받아오면 해당 위도·경도 값을 넘겨 Forecast API를 호출하여 현재 기온, 최저/최고 기온을 받아와 상태(posts)에 저장하고 화면을 갱신합니다.



### STEP 4. Customizing
 기존 오픈소스 프로젝트에서 Text, Style, UI/Data 3가지 유형을 각각 다음과 같이 커스터마이징하였습니다.

1) Text 커스터마이징 (src/component/Weaterapp.jsx)
상단 제목 추가: 기존 프로젝트에는 상단 타이틀이 없었으나, 본인의 이름을 반영하여 <h1 className="app-title">신태현의 날씨 예보</h1>라는 제목을 화면 최상단에 새롭게 추가하였습니다.
검색창 문구 한글화: 영문 입력 안내 문구(placeholder="Search for a city...")를 국내 사용자가 직관적으로 이해할 수 있도록 placeholder="도시 입력 후 Enter"로 변경하였습니다.

2) Style 커스터마이징 (src/component/Weaterapp.css)
타이틀 전용 CSS 스타일 정의: 새로 추가한 상단 제목이 배경과 잘 어울리도록 .app-title 스타일 클래스를 추가하였습니다.
폰트 크기를 26px로 키우고 굵게(bold) 처리하였으며, 가독성을 위해 글자색을 흰색(white)으로 지정하고 하단 여백(margin-bottom: 24px)을 부여하였습니다.

3) UI / Data 커스터마이징 (src/component/Weaterapp.jsx)
기본 검색 도시 변경: 기존에 외국의 'iran'으로 고정되어 있던 기본 조회 도시를 국내 사용자에 맞추어 'Pohang'(포항)으로 변경하였습니다.
검색 폼 제출 방식 개선: 키 입력 시마다 API를 호출하는 비효율을 방지하기 위해 <form onSubmit> 이벤트를 적용하여 Enter 키를 눌렀을 때만 검색되도록 개선하였습니다.
한글 도시명 검색 지원 (데이터 매핑): '서울', '포항', '부산', '대구', '제주' 등 한국어 도시명을 입력해도 영문 도시명으로 자동 변환해 검색을 수행하는 cityNames 매핑 객체 데이터를 추가하였습니다.
주요 도시 빠른 선택 버튼 UI 추가: 검색창 하단에 클릭 한 번으로 도시 기온을 즉시 조회할 수 있는 [서울] [포항] [부산] [제주] 4개의 퀵 버튼을 새롭게 추가하였습니다.


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