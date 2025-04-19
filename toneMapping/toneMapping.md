**Tone Mapping**

`THREE.sRGBEncoding` : 값으로는 3001
`THREE.LinearEncoding` : 값으로는 3000

AR.js를 사용할 때 비디오에 밝은 색감이 기본으로 적용되어 있어 확인해보았다.

![before](./images/before.png)

```
console.log("toneMapping:", renderer.toneMapping);
console.log("outputEncoding:", renderer.outputEncoding);
console.log("videoTexture.encoding:", videoTexture.encoding);
```

outputEncoding이 3001, 즉 sRGBEncoding으로 설정되어있었다.

아래와 같이 LinearEncoding으로 바꿔준 결과..

```
renderer.outputEncoding = THREE.LinearEncoding;
```

![after](./images/after.png)

정상적인 색감으로 바뀌었음을 알 수 있다. 원래 이 장소가 조금 노르스름.

그렇다면 sRGBEncoding은 뭐고 LinearEncoding은 무엇인지?

videoTexture는 뭐고 감마보정은 뭐고!

하나씩 알아보자..

**감마보정(Gamma Correction)**

- 모니터나 디스플레이 장치의 색상 반응 특성(?)을 보정하는 과정
- 디스플레이는 선형적이지 않게 색을 처리(?)하는 경향이 있기 때문에 인간 눈에 맞는 색감을 위해 감마 보정이 필요

흠 그렇다고 한다.

둘의 차이도 중요하지만 AR.js에서 출력된 색상이 어색하게 밝았던건 비디오텍스처 인코딩은 LinearEncoding, 아웃풋인코딩은 sRGBEncoding으로 서로 달랐기 때문이었다. 알아보니 비디오텍스처 인코딩을 바꾸는 방법보다 아웃풋인코딩을 바꾸는 방법이 더 간편했으므로 이것을 Linear로 바꾸어 맞춰주었다.

이걸 '색상 공간이 다르다' 고 이야기하네?

---

### 읽을 거리

- https://en.wikipedia.org/wiki/Tone_mapping

- https://threejs.org/examples/#webgl_tonemapping
