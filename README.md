# wanted-movie-app
원티드 프리온보딩 2주차 개인과제 이후 리팩토링 및 추가 기능 구현한 레포지토리입니다.

영화를 검색하고 즐겨찾기 등록/수정이 가능한 서비스입니다.
---

# [🚀 데모](https://hyeongseoku.github.io/wanted-movie-app/) (현재 제대로 동작하지 않음)


### 파일 구조
```
.
├── App.tsx
├── assets
├── components
│   ├── bookMarkCard
│   │   ├── bookMarkCard.module.scss
│   │   └── index.tsx
│   ├── bookMarkListContainer
│   │   ├── bookMarkListContainer.module.scss
│   │   └── index.tsx
│   ├── darkMode
│   │   ├── darkMode.module.scss
│   │   └── index.tsx
│   ├── loader
│   │   ├── index.tsx
│   │   └── loader.module.scss
│   ├── modal
│   │   ├── index.tsx
│   │   └── modal.module.scss
│   ├── movieCard
│   │   ├── index.tsx
│   │   └── movieCard.module.scss
│   ├── navBar
│   │   ├── index.tsx
│   │   └── navBar.module.scss
│   └── searchInput
│       ├── index.tsx
│       └── searchInput.module.scss
├── images
│   └── notfound.png
├── index.tsx
├── logo.svg
├── react-app-env.d.ts
├── reportWebVitals.ts
├── routes
│   ├── BookMark
│   │   ├── BookMark.module.scss
│   │   └── index.tsx
│   ├── NotFound404
│   │   ├── NotFound404.module.scss
│   │   └── index.tsx
│   ├── Route.module.scss
│   ├── Search
│   │   ├── Search.module.scss
│   │   ├── index.tsx
│   │   └── searchMethod.tsx
│   └── index.tsx
├── setupTests.ts
├── styles
│   ├── base
│   │   ├── _fonts.scss
│   │   ├── _more.scss
│   │   └── _reset.scss
│   ├── constants
│   │   ├── _colors.scss
│   │   ├── _levels.scss
│   │   └── _sizes.scss
│   ├── index.js
│   ├── index.scss
│   └── mixins
│       ├── _animation.scss
│       ├── _flexbox.scss
│       ├── _position.scss
│       ├── _responsive.scss
│       └── _visual.scss
├── types
│   └── types.d.ts
└── utils
    ├── apis
    │   └── api.tsx
    ├── atoms
    │   └── atom.ts
    └── constants
        ├── componentsData.tsx
        └── standard.tsx

24 directories, 51 files

```

## 기본 구현
- [x] 하단 메뉴
- [x] 영화 검색
- [x] 검색 결과 표시
- [x] Infinite scroll
- [x] 즐겨찾기 등록/삭제 기능


## 세부 설명

### 검색
![search_mini_demo](https://user-images.githubusercontent.com/48541850/168460854-b0721d1b-d54b-4091-92e5-094e1e15cbad.gif)

**💁 구현 설명**
    
    검색을 담당하는 searchInput 컴포넌트에서 검색어가 입력되면 api가 실행되고 
    recoil로 관리되는 데이터에 검색 데이터를 set해주도록 구현했습니다.
    간단한 예외 처리를 진행해주었으며, sticky속성을 이용해 검색창이 항상 떠있도록 구현하였습니다.


**❗️ 어려웠던 점**

    크게 어려운 점은 없었으나, 예외처리가 api status 값에 따라 처리할 수 없어서
    살짝 헤맸습니다.

**⭐️ 자랑할 점**

    예외 처리를 진행한 점
    로딩중임을 알 수 있도록 처리한 것

---

### 검색 스크롤
![search_scroll_mini_demo](https://user-images.githubusercontent.com/48541850/168460887-3cf1656b-fb5e-4bbf-84ba-ec195ae9d91d.gif)

**💁 구현 설명**

    react-intersection-observer의 useInview를 사용하여 
    가장 최하단의 요소가 화면에 보일때 inView가 true로 변경되고 페이지 번호를 증가 시켜주었고, 
    페이지 번호가 변경될때마다 해당 페이지 번호의 추가 데이터를 불러오도록 구현하였습니다.


**❗️ 어려웠던 점**

    기존의 onScroll 방식이 아닌 react-intersection-observer를 처음 사용하게 되어
    조금 헤맸지만, 어려운 사용 방식이 아니라 금방 이해할 수 있었습니다


**⭐️ 자랑할 점**



---
### 모달
![modal_mini_demo](https://user-images.githubusercontent.com/48541850/168460947-63c1ded3-f2bf-4078-815f-9190fc59b967.gif)

**💁 구현 설명**

    모달을 직접 구현해서 사용하였습니다.
    애니메이션을 위해 modalOpen 상태값에 따라 랜더링이 아닌, 
    visibility 속성의 값이 바뀌도록 설정해주었습니다.

**❗️ 어려웠던 점**

    스타일링 작업에서 너무 과하게 시간을 썼고,(색상 설정..등 쓸데 없는 시간)
    모달에서 즐겨찾기에 추가된 데이터인지 감지를 제대로 못해서 애를 먹었습니다.
    

---

### 즐겨찾기

![bookMark_mini_demo](https://user-images.githubusercontent.com/48541850/168460892-0a674651-5bf0-42f4-94a0-2b3fc09f7aad.gif)
**💁 구현 설명**

    가장 바깥의 Router 페이지가 로드시 bookMarkList라는 이름의 localStorage데이터가 있는지 확인하고 없으면 빈 배열로 localStorage에 생성

    이후 App 페이지에서 useEffect를 이용해 localStorage데이터가 변경될때마다 recoil로 관리되는 데이터인 bookMarkList를 변경시켜주었습니다


**❗️ 어려웠던 점**

    검색 결과에서의 즐겨찾기에 추가됐는지 여부와, 모달에서의 즐겨찾기에 추가됐는지 여부가 
    서로 제대로 추적되지 않아서 굉장히 애를 먹었습니다

---

### 드래그 앤 드롭
![dnd_mini_demo](https://user-images.githubusercontent.com/48541850/168460895-ad351372-f8c1-45a7-b5d7-b4f2eaf78cfa.gif)
**💁 구현 설명**

    react-intersection-observer의 useInview를 사용하여 
    가장 최하단의 요소가 화면에 보일때 inView가 true로 변경되고 페이지 번호를 증가 시켜주었고, 
    페이지 번호가 변경될때마다 해당 페이지 번호의 추가 데이터를 불러오도록 구현하였습니다.


**❗️ 어려웠던 점**

    기존의 onScroll 방식이 아닌 react-intersection-observer를 처음 사용하게 되어
    조금 헤맸지만, 어려운 사용 방식이 아니라 금방 이해할 수 있었습니다


---

## 선택 구현
- [x] 즐겨찾기 목록 순서 조정 (드래그 & 드롭)


## 기술 스택
- React
- TypeScript
- recoil
- react-intersection-observer
- react-beautiful-dnd
- fontawesome


## 보완 사항
- 세부 디테일 디자인 수정
- 디렉토리 구조 수정
- 중복 타입 선언 제거
- 검색 로직 및 즐겨찾기 로직 최적화
- 추가 데이터를 통한 좀 더 다양한 정보 랜더링 (https://imdb-api.com/) [imdbID 활용]

## 회고
크게 어려울 점은 없었던 프로젝트인데도 100% 맘에 든다고 할 순 없을것 같습니다.

초반 스타일링에 허송세월을 보냈던 점이 너무 아쉽고 그로 인해 프로젝트 후반부에서 시간이 부족해서 주먹구구식으로 개발해서 로직이 비효율적인 부분이 존재합니다.

react-beautiful-dnd와 react-intersection-observer를 이용해서 각각 dnd,

infinite-scroll을 구현해 볼 수 있는 경험이 되어서 좋았던 프로젝트입니다.

한가지 더 아쉬운 점을 말하자면, 기존에 필자가 사용하던 폴더구성 방식을 사용하지 않아서 좀 더 헤맸던 것 같습니다. 

디렉토리 구조를 짜는 방식에 있어서도 기존의 방식과 새로운 방식 두가지의 장점을 합쳐서 더 가독성 있는 구조를 짜야할 것 같습니다.
