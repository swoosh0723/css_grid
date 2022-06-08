# CSS Grid
CSS Grid(그리드)는 2차원(행과 열)의 레이아웃 시스템을 제공합니다.   
## grid란?
그리드는 수평선과 수직선으로 이루어진 집합체로, 디자인 요소를 정렬할 수 있는 대상 패턴을 생성한다. 이 디자인은 페이지에서 페이지로 이동할 때 요소가 널뛰거나 너비가 바뀌지 않는 디자인 생성에 도움을 주어 웹 사이트의 일관성을 높여준다.   

하나의 그리드은 대게 **columns**, **rows**로 구성되며, 각 행과 열 사이에 공백이 있는데, 대게는 이를 일컬어 **gutters**라고 부른다.   

<img
   src="img/grid_01.png"
   title="grid 설명"
   width="300px"
/>   

~~*위 레아아웃을 구현하려면 grid로 어떻게 해야할까?*~~

## Grid container 속성
| 속성                        | 의미                                            |
| --------------------------- | ----------------------------------------------- |
| display                     | 그리드 컨테이너(Container)를 정의               |
| grid-template-rows          | 명시적 행(Track)의 크기를 정의                  |
| grid-template-columns       | 명시적 열(Track)의 크기를 정의                  |
| grid-template-areas         | 영역(Area) 이름을 참조해 템플릿 생성            |
| grid-template               | grid-template-xxx의 단축 속성                   |
| row-gap(grid-row-gap)       | 행과 행 사이의 간격(Line)을 정의                |
| column-gap(grid-column-gap) | 열과 열 사이의 간격(Line)을 정의                |
| gap(grid-gap)               | xxx-gap의 단축 속성                             |
| grid-auto-rows              | 암시적인 행(Track)의 크기를 정의                |
| grid-auto-columns           | 암시적인 열(Track)의 크기를 정의                |
| grid-auto-flow              | 자동 배치 알고리즘 방식을 정의                  |
| grid                        | grid-template-xxx과 grid-auto-xxx의 단축 속성   |
| align-content               | 그리드 콘텐츠(Grid Contents)를 수직(열 축) 정렬 |
| justify-content             | 그리드 콘텐츠를 수평(행 축) 정렬                |
| place-content               | align-content와 justify-content의 단축 속성     |
| align-items                 | 그리드 아이템(Items)들을 수직(열 축) 정렬       |
| justify-items               | 그리드 아이템들을 수평(행 축) 정렬              |
| place-items                 | align-items와 justify-items의 단축 속성         |

## Grid Item 속성
| 속성              | 의미                                                             |
| ----------------- | ---------------------------------------------------------------- |
| grid-row-start    | 그리드 아이템(Item)의 행 시작 위치 지정                          |
| grid-row-end      | 그리드 아이템의 행 끝 위치 지정                                  |
| grid-row          | grid-row-xxx의 단축 속성(행 시작/끝 위치)                        |
| grid-column-start | 그리드 아이템의 열 시작 위치 지정                                |
| grid-column-end   | 그리드 아이템의 열 끝 위치 지정                                  |
| grid-column       | grid-column-xxx의 단축 속성(열 시작/끝 위치)                     |
| grid-area         | 영역(Area) 이름을 설정하거나, grid-row와 grid-column의 단축 속성 |
| align-self        | 단일 그리드 아이템을 수직(열 축) 정렬                            |
| justify-self      | 단일 그리드 아이템을 수평(행 축) 정렬                            |
| place-self        | align-self와 justify-self의 단축 속성                            |
| order             | 그리드 아이템의 배치 순서를 지정                                 |
| z-index           | 그리드 아이템의 쌓이는 순서를 지정                               |

----   
   
   

## Grid 장점?
### 1. 레이아웃 구성에 직관적이다.   

<img
   src="img/grid_02.png"
   title="grid 설명"
   width="250px"
/>   

위 레이아웃을 구성하려면 어떻게 해야할까?   
Flex VS Grid 비교해보자 (레이아웃 css만 표기함)

```html
Dom구조
<div class="grid-container2">
   <div class="grid-container2__item grid-container2__item--block1">1</div>
   <div class="grid-container2__item grid-container2__item--block2">2</div>
   <div class="grid-container2__item grid-container2__item--block3">3</div>
   <div class="grid-container2__item grid-container2__item--block4">4</div>
</div>
```

### Flex
```css
.grid-container2 {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;

  &__item {
    height: 150px;

    &--block1 {
      flex: 0 0 100%;
    }

    &--block2,
    &--block3 {
      flex: 0 0 calc(50% - 4px);
      margin-top: 8px;
    }

    &--block4 {
      flex: 0 0 100%;
      margin-top: 8px;
    }
  }
}
```

### Grid
```css
.grid-container2 {
  display: grid;
  grid-template-areas:
    "block1 block1"
    "block2 block3"
    "block4 block4";
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(3, 100px);
  gap: 8px;

  &__item {
    &--block1{
       grid-area: block1;
    }
    &--block2{
       grid-area: block2;
    }
    &--block3{
       grid-area: block3;
    }
    &--block4{
       grid-area: block4;
    }
  }
}
```
**flex**는 부모요소 `grid-container2` 레이아웃의 간격을 위해 `justify-content`만 사용되었고   
이외에는 간격, 사이즈를 자식요소에서 선언을 한다.  
   

반면에 **grid**는 부모요소 `grid-container2`에서 레이아웃을 온전히 소화를 한다.   
자식요소는 지정한 형태의 이름만 지정해주면 된다.
- 레이아웃 형태 (`grid-template-areas`)
- 레이아웃의 간격 (`gap`)
- 레이아웃 column의 개수와 값 (`grid-template-columns`)
- 레이아웃 row의 개수와 값 (`grid-template-rows`)
---