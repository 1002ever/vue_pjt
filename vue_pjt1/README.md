# vue_pjt1

> \*\* **vue 프로젝트 git으로 관리 시 주의사항**
>
> node_modules는 용량이 크므로 기본적으로 git.ignore로 설정되어 있다.
>
> => 프로젝트를 새로이 pull 하는 곳에서는 필요 모듈이 없는 상태
>
> => 해당 프로젝트에 사용된 모듈들은 package.json에 저장되어 있다.
>
> => 모듈들이 없더라도 `npm install`을 터미널에 치면 자동으로 필요한 모듈들을 다운로드 한다.



### - 구현 사항

- Movie 페이지(인덱스 페이지)

  -  '영화 가져오기' 버튼을 클릭하면

    => Card를 나열하는 형태로 영화 이미지 + 제목을 보여줌

  - Card 내 '영화 정보 상세보기' 클릭하면

    => 영화 줄거리 등을 담는 모달창이 뜸



- Video 페이지(영화 예고편 검색 페이지)

  - input에 텍스트 입력 후 엔터를 누르거나 search를 클릭하면

    => 텍스트 + trailer 를 검색한 결과를 리스트로 보여줌





#### - Vue 구조

![image-20200603235240323](C:\Users\175424\AppData\Roaming\Typora\typora-user-images\image-20200603235240323.png)



### - 구현 과정

​	=> 김영원(Movie 페이지), 전석현(Video 페이지)



​	ㄱ. router 추가 및 부트스트랩 cdn 설정

​		\- `vue add router` 로 프로젝트 내 라우터 추가

​		\- public 내 index.html에서 부트스트랩 cdn 설정

 

​	ㄴ. App.vue

​		\- 부트스트랩을 이용하여 어느 페이지에서든 보이는 navbar 설정



​	ㄷ. 여러 페이지를 url로 접근할 수 있도록 url 할당 => router/index.js 에서

​		\- `path 설정 시 장고와는 달리 뒤에 /를 붙이지 않음`

​		

​	ㄹ. Movie 페이지

​		\- view에 해당하는 MovieView에서의 첫 번째 컴포넌트인 MovieList.vue 부터 구현

​			a. v-if / v-else 에 따라 MovieList가 달리 나오게 구성

​				(1) 버튼을 누르지 않은 경우 v-if 블럭

​				(2) 버튼을 누른 경우 v-else 블럭

​			b. v-else 블럭에 들어가면 MovieListItem 컴포넌트를 v-for를 이용하여 반복적으로 호출



​		\- MovieList에서 반복적으로 호출 될 MovieListItem.vue 구현

​			a. 부트스트랩의 Card 를 이용하여 구성

​			b. movie는 props 를 이용하여 MovieList에서 받아옴

​			c. Card 내부에 버튼을 트리거로 모달창을 생성

​				=> 모달창은 다른 컴포넌트로 구성(MovieListItemModal)

​		

​		\- MovieListItemModal.vue 구현

​			=> MovieListItem 내 버튼을 누르면 나올 모달창의 내용 구성

​			=> 해당 movie 데이터가 있어야하므로 역시 props로 movie 데이터를 받음

​			

> ​	\*\*\* **모달창 구현 시 주의사항**
>
> ​			 \- 모달은 data-target이라는 속성으로 target을 식별
>
> ​				=> 모달창을 식별하는 id인 셈
>
> ​				=> 선택자 특성상 해당 id를 가진 target을 찾아, <u>먼저 발견되는 target을</u> modal로 띄움
>
> ​				=> 각자 다른 data-target , id 쌍을 구성해야 각기 다른 모달창을 띄울 수 있다.
>
> ​				`단, id는 한글, 숫자로 시작하면 안 된다.`



​	ㅁ. Video 페이지

​		\- VideoSearch와 VideoItem 컴포넌트로 구성

​		=> Search는 검색창 / Item은 검색 내용 리스트 중 한 요소

​		

​		\- VideoSearch.vue

​			a. input 창에 text 입력 후 엔터를 누르거나 search 클릭 시 search 함수를 수행

​			b. $emit 을 통해 이벤트를 전달

​				=> 입력받은 data를 상위 컴포넌트에서 활용할 것이므로

​			c. VideoView 에서 해당 이벤트를 듣고 있다가 오면 <u>axios 요청을 통해</u> videos를 갱신

​		

​		\- VideoItem.vue / VideoItemDetail.vue

​			=> VideoItem에서 ul 태그 내 VideoItemDetail 컴포넌트를 반복 호출(v-for를 통해)

​			



##### \*\* 완성 후 느낀점 나열

- 장고 프로젝트와는 달리 각 페이지가 여러 컴포넌트로 이뤄졌기 때문에 코드의 재사용성이 훨씬 높다고 느꼈다. 그렇다 보니 장고 프로젝트 때 보다 각자의 역할을 나눴을 때 뚜렷한 구분감이 느껴졌다.

- 어떤 페이지를 만들고 뿌듯함을 느끼려면 꾸미는 방법을 공부하는 것에 소홀해선 안 되겠다.

- 하나하나 다 이해하고 하기 보다는

  우선 직관대로 고쳐보고, 결과를 확인해보고, 그 다음 이해해봐야 할 것 같은데..

  그게 맘 처럼 잘 안 돼서 공부 진도가 쭉쭉 안 빠지는 것 같다..