### GLSL에서 attribute란 무엇인가?

attribute는 각 정점(vertex)마다 GPU로 전달되는 입력 데이터를 의미한다.

주로..

- 정점 위치
- 색상
- 텍스처 좌표
- 법선  벡터

를 말한다.



정점 셰이더는 모든 정점에 대해 개별적으로 실행된다.

각 정점마다 고유한 정보를 셰이더에게 전달해야 할 필요가 있다.



---



### 1. **attribute의 기본 개념과 역할**

- **정점 단위의 데이터** 로서, CPU로부터 GPU에 데이터를 전달하는 방식
  - 따라서 Vertex Shader에서만 사용된다.
  - Fragment Shader에서는 정점이 아니라 **픽셀** 을 다룬다.
- '정점 단위의 데이터' 에는 위치, 색상, UV좌표, 노멀 등이 있다

- `uniform`, `varying`과의 차이점



------

### 2. **attribute와 버텍스 버퍼 객체 (VBO)**

- attribute는 GPU에 올려진 VBO에서 데이터를 읽음
- `glVertexAttribPointer`를 사용해 바인딩



------

### 3. **attribute 데이터 타입과 제한**

- 사용 가능한 타입: `float`, `vec2`, `vec3`, `vec4` 등
- attribute의 개수에는 하드웨어적인 제한이 있음



------

### 4. attribute와 레이아웃(location)

- `layout(location = x)`를 사용하면 쉐이더와 CPU 코드 간의 연결이 명확해짐
- 위치를 수동으로 지정하지 않으면 `glGetAttribLocation` 필요



------

### 🔹 5. **WebGL에서의 attribute 사용**

- `gl.getAttribLocation`, `gl.enableVertexAttribArray`, `gl.vertexAttribPointer`의 기본 사용법