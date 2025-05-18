#### GLSL



셰이더는 그래픽스 파이프라인의 일부이다.

그렇다면 '그래픽스 파이프라인' 이란 무엇이고 셰이더는 그 중 얼만큼의 비중을 차지하는가?



```js
renderer.render(scene, camera);
```



### 1단계

위와 같은 코드를 실행하면 모든 `Scene graph` 를 순회해서 visible한 객체를 먼저 찾는다고 한다.

- [Scene graph](https://threejs.org/manual/?q=scene#en/scenegraph)

frustum culling을 적용해 카메라에 보이는 객체만 그릴 대상에 넣는다.



### 2단계

다음으로는 이 그려질 대상들(mesh)의 geometry와 material 정보를 WebGL 코드로 변환한다 (넘겨준다?).

- geometry 안에는 3D모델의 좌표정보, 노멀벡터, UV 정보 등이 있다.
  - 좌표정보?
  - 노멀벡터?
  - UV?
- WebGL에서는 이를 `VBO(Vertex Buffer Object)` 라는 형태로 GPU에 올린다.
  - 이걸 해주는게 WebGLBufferRenderer 라는 Three.js 내부 모듈이라고 한다.



### 3단계

3단계는 셰이더 프로그램을 만든다. WebGL에 올린다.



```js
const vertexShader = gl.createShader(gl.VERTEX_SHADER);
const fragmentSHader = gl.createShader(gl.FRAGMENT_SHADER);

gl.shaderSource(vertexShader, vertexShaderCode);
gl.compileShader(vertexShader);
```



- 2단계와 3단계의 차이가 뭐지?



### 4단계

카메라 정보를 셰이더에 전달한다. 

카메라 정보라는건..

- 카메라의 뷰 행렬
  - 뭐지?
- 프로젝션 행렬
  - 뭐지?

이란다.



```glsl
uniform mat4 modelViewMatrix;
uniform mat4 projectionMatrix;
```



```js
gl.uniformMatrix4fv(
	projectionLocation,
  false,
  camera.projectionMatrix.elements
)
```





### 5단계

GPU야 그려줘!

```
gl.drawArrays(gl.TRIANGLES, 0, vertexCount);
```



이 명령이 실행되면 GPU가 버텍스

`버텍스 셰이더` => `래스터라이저` => `프래그먼트 셰이더`

순서로 처리한다.



- 왜 이 순서로 처리하는건지, 중간에 래스터라이저는 무슨 역할을 하는지*