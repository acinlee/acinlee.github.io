---
layout: post
title: React 반복문
---
### 고유키
+ React에서 반복문을 사용 할 때 배열 렌더링 시 key 항목을 넣어야 렌더링시에 각 항목에 대한 추적이 명확하게 가능하다.
+ 공식 문서를 참조 하면 반복으로 렌더링하는 모든 항목에는 항상 고유 키를 전달해야 한다고 되어 있다.
  + 고유키 사용하지 않을 시 React가 콘솔에 경고를 기록하며 앱이 이상하게 작동할 위험성이 있다고 함.
  

예제 소스  
``` js
  const taskList = props.tasks.map(task => (
        <Todo
            id={task.id}
            name={task.name}
            completed={task.completed}
            key={task.id}
        />
      )
  );
```
### 참고
+ [react 공식 document](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_components)

***
