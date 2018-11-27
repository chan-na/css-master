# css-master

## flexbox

### flex-container와 flex-item

- flex-container는 display: flex가 적용된 엘리먼트이고, 그 엘리먼트 안에있는 엘리먼트들은 flex-item.
- flex-container에 css로 명령을 내리면 flex-item들에게 레이아웃이 적용되는 방식.
- flex-container 안에 직접적으로 들어있는 엘리먼트들만이 flex-item이다. (flex-item안의 엘리먼트에는 flex적용안됨)
- flexbox는 중첩될 수 있다. 즉 flex-item에 display: flex를 주면 flex-item이 다른 엘리먼트들의 flex container가 될 수 있다.

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

## grid

### grid-container와 grid-item

- flexbox와 마찬가지로 grid도 grid-container에 display: grid를 설정하고, 레이아웃은 grid-element들에 적용된다.

### grid-template-columns와 grid-template-rows

- grid-template을 정의한다. row와 column에 대해서, 몇줄이고 각 줄의 크기가 어느정도인지.
- ex)grid-template-columns: 10px 30px; grid-template-rows: 15px 15px; 이라면, 2x2 총 4개의 grid-element들이 명시된 크기에 따라 정렬되어 나타난다.

```
.grid-container {
    display: grid;
    grid-template-columns: 10px 30px;
    grid-template-rows: 15px 15px;
}
```

### grid-gap

- grid-element 사이의 간격을 나타낸다.

```
.grid-container {
    display: grid;
    grid-template-columns: 10px 30px;
    grid-template-rows: 15px 15px;
    grid-gap: 3px;
}
```

### grid-auto-columns와 grid-auto-rows

- grid-template만 정의해 놓는다면, template으로 정의해놓은 grid-element의 개수를 초과하는 element들은(row 2줄 column 2줄로 총 4칸의 grid를 정의하였다면, 5번째 element부터는 초과하는 element) 나타나지 않는다. 그래서 초과하는 element들이 자동으로 어떻게 나타날지를 정의하는것이 grid-auto-rows(columns)이다.
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

- grid-auto-columns와 grid-auto-rows중 어느 방향으로 남는 grid-element들을 추가할지를 경정한다.
- flexbox의 flex-direction과 비슷하다고 볼 수 있다.
- default로는 row로 설정되어있음. 보통 web의 ui가 아래쪽으로 늘어나기 때문.

### grid-template-areas와 grid-area

- row와 columns의 개수와 크기를 명시하는것이 아니라, 그림그리듯이 grid-templte을 결정하는 방식
- grid-container에서 grid-template-areas로 template을 명시하고, grid-element에서 grid-area로 template의 어떤 부분을 표현할지 결정한다.
- grid의 크기는 명시해 주지 못하기 때문에, grid-auto-rows 같은 속성으로 크기를 명시해 주어야한다.

```
.grid-container {
    display: grid;
    grid-auto-rows: 200px;
    grid-gap : 5px;
    grid-template-area: "header header header"
                        "content content sidebar"
                        "content content sidebar"
                        "footer footer footer"
}
.grid-element-first {
    grid-area: header;
}
.grid-element-second {
    grid-area: content;
}
.grid-element-third {
    grid-area: sidebar;
}
.grid-element-fourth {
    grid-area: footer;
}
```
