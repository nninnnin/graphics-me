```js
// Adapted from Dan Shiffman, natureofcode.com

mouseMoved = function () {
  background(255, 255, 255);
  resetMatrix();

  // Two PVectors, one for the mouse location and
  //  one for the center of the window
  var mouse = new PVector(mouseX, mouseY);
  var center = new PVector(width / 2, height / 2);

  // PVector subtraction!
  mouse.sub(center);

  var m = mouse.mag();
  fill(0, 0, 0);
  rect(0, 0, m, 10);

  // Draw a line to represent the vector.
  translate(center.x, center.y);
  stroke(255, 0, 0);
  strokeWeight(3);
  line(0, 0, mouse.x, mouse.y);
};
```

`mouse.sub(center)` 를 이해할 수 있는가?

벡터의 뺄셈의 결과는 결국 벡터이다. 따라서 이것은 어떤 벡터를 구하기 위함인데, 그 벡터는 무엇을 의미하는가?

마우스에서 센터를 뺀 것과 센터에서 마우스를 뺀 것은 어떻게 다른가?

예를 들어보자. 마우스는 (100, 100), 센터는 (500, 500) 이라고 가정하자.

마우스에서 센터를 뺀 벡터는 (-400, -400)일 것이다.

이 벡터의 의미는 무엇일까? 센터를 기준으로 이 벡터를 더하면 마우스의 위치가 나온다는 것을 알 수 있다. 따라서 이 벡터는 센터를 기준으로 마우스까지의 거리를 의미한다.

반대로 센터에서 마우스를 빼면 (400, 400) 이라는 벡터가 나온다. 이것은 방금과는 반대로 마우스를 기준으로 센터까지의 거리를 의미한다.

값으로 따지면 비슷한 의미인 듯 하지만 의미상 `Vector.sub(target - origin)` 을 지켜주어야 한다. 그렇게 해야 예제에서처럼 target에서 해당 벡터를 활용하는 것이 원활하다.

\*조금 이해가 어려우면 1차원으로 생각해보면 조금 더 쉽다. 선분에서 원점과 두 거점의 거리를 계산한다고 생각해보면 어디에서 어디를 빼면 어디를 기준으로 하는 거리의 값을 가질 수 있는지 더 쉽게 알아챌 수 있다.
