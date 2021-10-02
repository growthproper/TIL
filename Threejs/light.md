### THREE.AmbientLight
기본 광원 장면에 있는 객체의 현재 색상에 빛의 색상이 더해짐.

```
var ambiColor = "0c0c0c";
var ambientLight = new THREE.AmbientLight(ambiColor);
scene.add(ambientLight);
```

<br>

### THREE.PointLight
한 점에서 모든 방향으로 확산되는 빛. 이 광원은 그림자를 만드는 데 사용하지 못함.

<br>

### THREE.SpotLight
데스크의 램프나 천장의 등, 횃불 같은 원뿔 효과를 가진다. 이 광원은 그림자를 만들 수 있다.

```
var pointColor = "#ffffff";
var spotLight = new THREE.SpotLight(pointColor);
spotLight.position.set(-40, 60, -10);
spotLight.castShadow = true;
spotLight.target = plane;
scene.add(spotLight);
```
그림자가 고르지 못하게 보인다면 shadowMapWidth와 shadowMapHeight 속성값을 증가시키거나 객체 그림자를 계산하는 데 사용되는 영역이 객체를 잘 둘러싸고 있는지 확인
<br>

### THREE.DirectionLight
무한광이라고도 불린다. 이 광원의 광선은 태양광과 비슷해 보인다. 이 광원 역시 그림자를 만드는 데 사용할 수 있다.

<br>

### THREE.HemisphereLight
1. 표면 반사나 희미한 하늘을 흉내내어 좀 더 자연스러운 외부광을 만드는 데 사용된다. 이 광원 역시 그림자와 관련된 기능을 제공하지 않는다.
2. 좀 더 자연스러운 야외 조명을 만드는 가장 쉬운 방법

```
var hemiLight = new THREE.HemisphereLight(0x0000ff, 0x00ff00, 0.6);
hemiLight.position.set(0, 500, 0);
scene.add(hemiLight);
```
<br>

### THREE.AreaLight
1. 공간에서 한 지점 대신 빛을 발산하는 공간을 지정할 수 있다. 그림자를 만들지 못한다.
2. 기본 라이브러리에 포함되어 있지 않고 확장판에 포함되어 있어서 소스 추가를 해야함.
3. THREE.WebGLRenderer를 사용할 수 없다. 매우 복잡한 광원이어서 매우 심각한 성능 저하를 야기하기 때문
4. THREE.WebGLDefferedRenderer는 장면을 렌더링할 때 여러 단계로 분리하여 훨씬 복잡한 빛을 다룰 수 있다.

```
var areaLight1 = new THREE.AreaLight(0xff0000, 3);
areaLight1.position.set(-10, 10, -35);
areaLight1.rotation.set(-Math.PI / 2, 0, 0);
areaLight1.width = 4;
areaLight1.height = 9.9;
scene.add(areaLight1);
```

<br>

### THREE.LensFlare
광원은 아니지만 THREE.LensFlare로 장면의 광원에 렌즈 플레어 효과를 줄 수 있다.

```
flare = new THREE.LensFlare(texture, size, distance, blending, color, opacity);

var textureFlare0 = THREE.ImageUtils.loadTexture("../assets/texture/lensflare/lensflare0.png");
var flareColor = new THREE.Color(0xffaacc);
var lensFlare = new THREE.LensFlare(textureFlare0, 350, 0.0, THREE.AdditiveBlending, flareColor);
lensFlare.position = spotLight.position;
scene.add(lensFlare);
```