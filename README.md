# css-master

## flexbox

### flex-container와 flex-item

- flex-container는 display: flex가 적용된 엘리먼트이고, 그 엘리먼트 안에있는 엘리먼트들은 flex-item.
- flex-container에 css로 명령을 내리면 flex-item들에게 레이아웃이 적용되는 방식.
- flex-container 안에 직접적으로 들어있는 엘리먼트들만이 flex-item이다. (flex-item안의 엘리먼트에는 flex적용안됨)
- flexbox는 중첩될 수 있다. 즉 flex-item에 display: flex를 주면 flex-item이 다른 엘리먼트들의 flex-container가 될 수 있다.

### flex-direction

- flex-direction에 설정된 방향이 main-axis가 되고, 그 방향의 수직인 쪽이 cross-axis가 된다.
- flex-direction의 default는 row
- row-reverse와 column-reverse도 존재

### justify-content와 align-items

- justify-content는 main-axis에 적용되고, align-items는 cross-axis에 적용된다.
- default는 flex-start

### flex-wrap

- flex-wrap은 공간이 부족해서 flex-item들이 겹치게 되었을때 어떤 디자인을 적용할지 설정한다.
- default는 nowrap : flex-item들의 크기가 자동으로 줄어들어서 공간에 맞춘다.
- wrap : flex-item에 설정해놓은 크기값을 신경써서, 공간에 안들어가면 다음줄로 이동.

### align-self

- flex-item에 직접 적용하는 css 속성이다.
- align이 붙은것을 보면 알수 있듯이 cross-axis에 적용된다.
- 특적 flex-item에만 align-items를 적용하고 싶을때 사용한다.

```
.flex-container {
    display: flex;
    justify-content: center;
    align-items: flex-end;
    flex-wrap: wrap;
}
.one-of-flex-items {
    align-self: flex-start;
}
```

## grid

### grid-container와 grid-item

- flexbox와 마찬가지로 grid도 grid-container에 display: grid를 설정하고, 레이아웃은 grid-item들에 적용된다.

### grid-template-columns와 grid-template-rows

- grid-template을 정의한다. row와 column에 대해서, 몇줄이고 각 줄의 크기가 어느정도인지.
- ex)grid-template-columns: 10px 30px; grid-template-rows: 15px 15px; 이라면, 2x2 총 4개의 grid-item들이 명시된 크기에 따라 정렬되어 나타난다.

```
.grid-container {
    display: grid;
    grid-template-columns: 10px 30px;
    grid-template-rows: 15px 15px;
}
```

### grid-gap

- grid-item 사이의 간격을 나타낸다.

```
.grid-container {
    display: grid;
    grid-template-columns: 10px 30px;
    grid-template-rows: 15px 15px;
    grid-gap: 3px;
}
```

### grid-auto-columns와 grid-auto-rows

- grid-template만 정의해 놓는다면, template으로 정의해놓은 grid-item의 개수를 초과하는 element들은(row 2줄 column 2줄로 총 4칸의 grid를 정의하였다면, 5번째 element부터는 초과하는 element) 나타나지 않는다. 그래서 초과하는 element들이 자동으로 어떻게 나타날지를 정의하는것이 grid-auto-rows(columns)이다.
- ex)grid-auto-rows: 30px 이라면, 초과하는 element들에 대해서는 column은 grid-template-columns에 정의된 크기를 따르면서 row는 grid-auto-rows에 정의 된 크기대로 존재하는 모든 element들을 디스플레이한다.

```
.grid-container {
    display: grid;
    grid-template-columns: 10px 30px;
    grid-template-rows: 15px 15px;
    grid-gap: 3px;
    grid-auto-rows: 30px;
}
```

### grid-auto-flow

- grid-auto-columns와 grid-auto-rows중 어느 방향으로 남는 grid-item들을 추가할지를 결정한다.
- flexbox의 flex-direction과 비슷하다고 볼 수 있다.
- default로는 row로 설정되어있음. 보통 web의 ui가 아래쪽으로 늘어나기 때문.

### grid-template-areas와 grid-area

- row와 column의 개수와 크기를 명시하는것이 아니라, 그림그리듯이 grid-templte을 결정하는 방식
- grid-container에서 grid-template-areas로 template을 명시하고, grid-item의 grid-area 속성에서 정의된 template중 어떤 부분에 해당하는 grid-item인지를 명시해 준다.
- grid의 크기는 명시해 주지 못하기 때문에, grid-auto-rows 같은 속성으로 크기를 따로 명시해 주어야한다.

```
.grid-container {
    display: grid;
    grid-auto-rows: 200px;
    grid-gap : 5px;
    grid-template-area: "header header header"
                        "content content sidebar"
                        "content content sidebar"
                        "footer footer footer";
}
.grid-item-first {
    grid-area: header;
}
.grid-item-second {
    grid-area: content;
}
.grid-item-third {
    grid-area: sidebar;
}
.grid-item-fourth {
    grid-area: footer;
}
```

### fr Unit

- grid에서 길이를 표시하는 새로운 방법. (원래는 px, % 등으로 길이를 표시했었음.)
- fr은 fraction의 약자로 비율을 뜻한다.
- 반응형 디자인을 할 때 자동으로 비율에 맞춰 크기를 계산해 주기 때문에 편리하다.

### repeat

- template을 정의할때 여러번 써야할 수고를 덜어준다.
- repeat(횟수, 길이)로 표현한다.

```
.grid-container {
    display: grid;
    grid-auto-rows: 200px;
    grid-template-columns: repeat(3, 1fr) 3fr;  // 1fr 1fr 1fr 3fr 과 동일하다.
}
```

### minmax

- 길이를 표시하는 방법중 하나이다.
- minmax(최소로 가져야 하는 크기, 최대로 가질수 있는 크기);
- fr과 함께 사용하면 쉽게 반응형 디자인을 할 수 있다.

```
.grid-container {
    display: grid;
    grid-auto-rows: 200px;
    grid-template-columns: repeat(3, 1fr) minmax(200px, 1fr);
    // html에 4개의 div element가 정의되어 있다고 가정한다면
    // 처음에는 4개의 element가 각각 같은비율(1fr)로 width를 차지하고 있다. (각 element의 width는 200px 이상)
    // 브라우저의 width를 줄이는 점점 줄이다가 각 element의 width가 200px이 된 이후에
    // 브라우저 width를 계속 줄이면 마지막 element는 width가 200px로 고정되고(최소 200px크기를 가져야하므로),
    // 다른 element들은 남는 width를 같은비율(1fr)로 나누어서 width를 가지게 된다.
}
```

### max-content와 min-content

- 길이를 표시하는 방법중 하나이다.
- 해당하는 grid-item 안에 들어있는 content에 따라 다른 디자인이 적용된다.
- max-content의 경우, grid-item안에 들어있는 content에 따라서, 차지할수있는 최대의 크기를 차지한다.
- min-content의 경우, grid-item안에 들어있는 content에 따라서, 최소한의 크기만을 차지한다.

```
.grid-container {
    display: grid;
    grid-gap: 3px;
    grid-template-columns: max-content repeat(3, minmax(300px, 1fr));
    // html에 4개의 div element가 있고, 첫번째 element에는 긴 text content가 있다고 가정.
    // 두번째~네번째 element는 최소 300px을 가지므로 300px width를 가짐
    // 첫번째 element는 max-content이므로 content가 있는한 최대 크기(브라우저 width - 300px*3)를 가짐.
}
```

### auto-fill과 auto-fit

- repeat(횟수, 길이)를 사용할때, 횟수가 정확히 정해지지 않은경우에 횟수 부분에 auto-fill과 auto-fit을 사용할 수 있다.
- auto-fit
  - repeat(auto-fit, 길이)의 경우 지정된 길이로 **존재하는 grid-item들을 최대한 맞춰서** 채워 넣는다. 하지만 길이를 100px처럼 고정된 길이로 줄 경우, 남는 공간이 생길 수 있는 단점이 있다.
  - repeat(auto-fit, minmax(100px, 1fr)) 처럼 사용한다면, 100px로 채웠을때 남는공간이 있을때는 길이가 1fr이 되어서 딱 맞게 채워진다. 단 한줄로 복잡한 반응형 디자인을 적용할 수 있다.
- auto-fill
  - repeat(auto-fill, 길이)의 경우 지정된 길이로 **ghost grid(레이아웃)을 미리 만들어 놓고, ghost grid에 grid-item을 채워넣는다.**
  - ghost grid : 레이아웃을 잡기 위해서 콘텐츠 없는 grid를 만들어 놓은것을 ghost grid라고 표현했다. inspect로 살펴보면, grid-item이 없더라도 컨텐츠가 들어있지 않은 grid가 생성되어 있는 것을 볼 수 있다.
  - repeat(auto-fill, minmax(100px, 1fr)) 처럼 사용했을때, 무조건 100px크기로 레이아웃이 잡히는것 같다.
  - 아마도 레이아웃을 미리 잡아놓고 데이터를 로딩하면서 하나씩 채워넣는 경우에 사용하면 좋을듯 하다. 이런경우 auto-fit으로 한다면 데이터가 로딩되면서 사이즈가 왔다갔다 할 수도 있기 때문에, 고정된 레이아웃을 먼저 만들어 놓는 auto-fill이 유용할것이다.

```
.grid-container {
    display: grid;
    grid-gap: 5px;
    grid-auto-rows: 200px;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

### justify-content, align-content, place-content | justify-items, align-items, place-items

- justify는 horizontal, align은 vertical, place는 두개를 한꺼번에 표현하는데 차례대로 vertical horizontal순서.
- content는 grid-container자체를 움직인다. grid-container가 차지하고 있는 영역(블록)이 있을텐데, 그 영역안에서 grid-container가 어디에 위치할지를 지정한다.
- items는 grid 레이아웃 안의 각 셀에서, 셀안의 content(grid-item안의 content)의 위치를 지정한다.

```
.grid-container {
    display: grid;
    grid-gap: 5px;
    grid-template-rows: 100px 100px;
    grid-template-columns: 100px 100px;
    height: 100vh;
    justify-content: center;
    align-content: end;
    place-items: center center;
    // 2x2 레이아웃이 만들어진 상태애서, 레이아웃 전체가 수평으로는 중앙, 수직으로는 끝에 위치한다.
    // 2x2 레이아웃안의 각 셀에서, 셀안의 content(grid-item안의 content)는 수평, 수직으로 셀의 중앙에 위치한다.
}
```

### justify-self, align-self, place-self

- 특정 셀에만 justify-items, align-items를 적용하고 싶을때 사용한다.
- 적용하는 값들은 justify-items, align-items와 같다.
- place-self: aling-self justify-self 순서이다.

```
.grid-item-first {
    justify-self: end;
    align-self: center;
    //place-self: center end; 와 같다.
}
```

### grid-row, grid-row-start, grid-row-end | grid-column, grid-column-start, grid-column-end | grid-area

![grid-basic](https://webkit.org/wp-content/uploads/grid-concepts.svg)

- grid-item에 정의해주는 속성들이다. grid-container에는 레이아웃(템플릿)이 미리 정의되어있다고 가정한다.
- start, end는 grid-item이 레이아웃의 몇번째 line부터 몇번째 line 까지 차지할지를 나타낸다. 라인의 숫자는 1부터 시작하여 증가한다. 위의 그림을 보면 정확히 알 수 있다.
- grid-row와 grid-column은 단축된 표현으로서 **grid-row-start : 2; grid-row-end : 4;** 를 **grid-row : 2 / 4;** 로 줄여쓸 수 있다.
- 마지막 라인쪽에서는 -1부터 시작하여 감소하는 방식으로 라인을 셀 수 있다. grid-column : 1 -1; 로 하면 첫째 라인부터 마지막 라인까지 한줄 전체를 차지한다.
- 몇칸을 차지할지를 명시해주는 방식도 있다. grid-row: span 2; 는 해당 grid-item의 시작부터 2칸을 차지하게 된다. grid-row: 2 / span 2; 는 2번째 라인부터 2칸을 차지하게 된다.
- grid-area 속성을 사용하면 한번에 row-start / column-start / row-end / column-end 를 표현 할 수 있다.

```
.grid-item-first {
    grid-row-start: 2;
    grid-row-end: 5;
    grid-column: 3 / -1;
}
grid-item-second {
    grid-row: span 3;
    grid-column: 2 / span 2;
}
grid-item-thire {
    grid-area: 2 / 1 / 4 / -1;
}
```

### Line naming

- 레이아웃이 방대해 진다면 라인을 숫자로 표현하기 어려울 수 있다. 하나하나 세어가면서 몇번째 라인인지 확인해야하기 때문이다.
- 각 라인에 이름을 붙여주는 방식으로 해결 할 수 있다.
- 이름은 공백이 있으면 안된다.

```
.grid-container {
    display: grid;
    grid-auto-row: 100px;
    grid-template-columns: [first] 400px [main] 200px [side] 100px [last];
}
.grid-item-first {
    grid-row: first side;
    grid-column: span 3;
}
```

![grid-line-naming](https://webkit.org/wp-content/uploads/grid-definition.svg)
