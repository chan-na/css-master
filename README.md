# css-master

## flexbox

- flex-container와 flex-item
  --flex-container는 display: flex가 적용된 엘리먼트이고, 그 엘리먼트 안에있는 엘리먼트들은 flex-item.
  -- flex-container에 css로 명령을 내리면 flex-item들에게 디자인이 적용되는 방식.
  -- flex-container 안에 직접적으로 들어있는 엘리먼트들만이 flex-item이다. (flex-item안의 엘리먼트에는 flex적용안됨)
  -- flexbox는 중첩될 수 있다. 즉 flex-item에 display: flex를 주면 flex-item이 다른 엘리먼트들의 flex container가 될 수 있다.

- flex-direction
  -- flex-direction에 설정된 방향이 main-axis가 되고, 그 방향의 수직인 쪽이 cross-axis가 된다.
  -- flex-direction의 default는 row
  -- row-reverse와 column-reverse도 존재

- justify-content와 align-items
  -- justify-content는 main-axis에 적용되고, align-items는 cross-axis에 적용된다.
  -- default는 flex-start

- flex-wrap
  -- flex-wrap은 공간이 부족해서 flex-item들이 겹치게 되었을때 어떤 디자인을 적용할지 설정한다.
  -- default는 nowrap : flex-item들의 크기가 자동으로 줄어들어서 공간에 맞춘다.
  -- wrap : flex-item에 설정해놓은 크기값을 신경써서, 공간에 안들어가면 다음줄로 이동.

- align-self
  -- flex-item에 직접 적용하는 css 속성이다.
  -- align이 붙은것을 보면 알수 있듯이 cross-axis에 적용된다.
  -- 특적 flex-item에만 align-items를 적용하고 싶을때 사용한다.
