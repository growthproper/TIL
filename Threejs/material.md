### 물질
1. MeshBasicMaterial : 기본 물질
2. MeshDepthMaterial : 카메라로부터의 거리로 메시의 색상을 결정할 때 사용하는 물질
3. MeshNormalMaterial : 일반 벡터의 표면 색상에 기반을 둔 간단한 물질
4. MeshFaceMaterial : 지오메트리의 각각의 면에 고유한 물질을 지정할 수 있도록 해 주는 컨테이너
5. MeshLambertMaterial : 빛을 받아 무광의 객체를 생성할 때 사용하는 물질
6. MeshPhongMaterial : 빛을 받아 유광의 객체를 생성할 때 사용하는 물질
7. ShaderMaterial : 꼭지점의 위치와 픽셀 색상을 직접 제어할 수 있는 사용자 정의 셰이더 프로그램을 지정할 수 있게 해주는 물질
8. LineBasicMaterial : 색상이 있는 라인을 만드는 THREE.Line 지오메트리에 쓰이는 물질
9. LineDashMaterial : LineBasicMaterial과 동일하지만 점선 효과를 만듬

<br>

### THREE.RawShaderMaterial
THREE.BufferGeometry와 함께 쓸 때만 사용할 수 있는 특수한 물질. 이것은 정적인 지오메트리에 최적화 된 특수한 형태

### THREE.MeshBasiMaterial

1. 생성자의 인수로 전달
```
var material = new THREE.MeshBasicMaterial({
    color: 0xff0000, 
    name: 'material-1,
    opacity: 0.5,
    transperency: true,
});
```
2. 인스턴트를 만들고 개별적으로 속성을 전달
```
var material = new THREE.MeshBasicMaterial();
material.color = new THREE.Color(0xff0000);
material.name = 'material-1;
material.opacity = 0.5;
material.transparency = true;
```

### THREE.MeshDepthMaterial
1. 객체가 보이는 방법은 조명이나 특정 물질 속성에 의해 정의되지 않고 카메라로부터 객체까지의 거리에 의해 정의됨.
2. 이 물질은 다른 물질과 결합해 쉽게 페이딩 효과를 낼 수 있음.

```
var cubeMaterial = new THREE.MeshDepthMaterial();
var colorMaterial = new THREE.MeshBasicMaterial({
    color: 0x00ff00,
    transparent: true,
    blending: THREE.MultiplayBlending
});

var cube = new THREE.SceneUtils.createMultiMaterialObject(cubeGeometry, [colorMaterial, cubeMaterial]);
cube.children[1].scale.set(0.99, 0.99, 0.99);

```

### THREE.SmoothShading
객체의 면을 부드럽게 렌더링

### THREE.MeshFaceMaterial
1. 지오메트리의 각 면에 서로 다른 물질을 지정할 수 있게 해줌.
2. 정육면체 각각의 면에 다른 물질을 지정하는 방법
```
var matArray = [];
matArray.push(new THREE.MeshBasicMaterial({color: 0x009e60}));
matArray.push(new THREE.MeshBasicMaterial({color: 0x009e60}));
matArray.push(new THREE.MeshBasicMaterial({color: 0x0051ba}));
matArray.push(new THREE.MeshBasicMaterial({color: 0x0051ba}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xffd500}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xffd500}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xff5800}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xff5800}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xC41E3A}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xC41E3A}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xffffff}));
matArray.push(new THREE.MeshBasicMaterial({color: 0xffffff}));

var faceMaterial = new THREE.MeshFaceMaterial(matArray);

var cubeGeom = new THREE.BoxGeometry(3, 3, 3);
var cube = new THREE.Mesh(cubeGeom, faceMaterial);
```

### THREE.MeshLambertMaterial
```
var meshMaterial = new THREE.MeshLambertMaterial({color: 0x7777ff});
```

<속성>
 + ambient :  물질의 주변색
 + emissive : 방출하는 색
 + wrapAround : true로 설정되어 있으면 half-lambert 조명 기술을 사용할 수 있다. 빛의 감소를 줄어들게 함.
 + wrapRGB : true로 설정되어 있으면 THREE.Vector3를 사용해 빛이 줄어드는 속도를 제어할 수 있다.

### THREE.MeshPhongMaterial
<속성>
 + ambient : 물질의 주변색
 + emissive : 방출하는 색
 + specular : 물질이 어떻게 빛나고 어떤 색으로 빛나는지 정의
 + shininess : 정반사성 하이라이트가 얼마나 반짝이는지 정의함. 기본값 300
 + metal : true로 설정되어 있으면 Three.js 는 객체를 좀 더 금속처럼 보이게 하기위해 픽셀의 색상을 계산하는 데 조금 다른 방식을 사용함.
 + wrapAround : true로 설정되어 있으면 half-lambert 조명 기술을 사용할 수 있다. 빛의 감소를 줄어들게 함.
 + wrapRGB : true로 설정되어 있으면 THREE.Vector3를 사용해 빛이 줄어드는 속도를 제어할 수 있다.

 ```
 var meshMaterial = new THREE.MeshPhongMaterial({color: 0x7777ff});
 ```

### THREE.ShaderMaterial

+ 웹GL 컨텍스트에서 직접 동작하는 사용자 정의 셰이더를 만들 수 있음.

<속성>
 + fragmentShader : 전달되는 각각의 픽셀의 색상을 정의. 프레그먼트 셰이더 프로그램의 문자열 값을 전달해야 함.
 + VertexShader : 전달되는 각 꼭지점의 위치를 변경할 수 있음. 자신의 꼭지점 셰이더 프로그램의 문자열 값을 전달해야 함.
 + uniforms : 셰이더에 정보를 보냄. 동일 정보가 각 꼭지점과 프레그먼트에 전송됨.
 + defines : #define 코드 프레그먼트를 변환. 이 프레그먼트를 사용하면 셰이더 프로그램에 몇 개의 추가 전역 변수를 설정할 수 있음.
 + attributes : 각 꼭지점과 프레그먼트 사이를 변경할 수 있음. 위치 및 데이터를 전달하는 데 사용됨. 지오메트리의 모든 꼭지점에 대한 정보를 제공해야 함.
 + lights : 조명 데이터가 셰이더에 전달되어야 하는 지 여부를 결정. 기본값은 false.

+ vertexShader : 지오메트리의 각 꼭지점에서 동작. 꼭지점의 위치를 이동해 지오메트리를 변환하는데 이 셰이더를 사용할 수 있음.
+ fragmentShader : 지오메트리의 각 프레그먼트에서 동작. vertexShader에서 각각의 프레그먼트에서 보여질 색상을 반환.

### THREE.LineBasicMaterial
<속성>
 + color
 + linewidth
 + linecap : 선의 끝 모양을 정의. 사용가능한 값은 butt, round, square. WebGLRenderer에서 지원 안됨
 + linejoin : 선의 연결 부위를 시각화하는 방법을 정의. 사용 가능한 값은 round와 bevel, miter. WebGLRenderer에서 지원 안됨
 + vertexColors : THREE.VertexColors 값으로 설정하면 각 꼭지점에 특정한 색을 제공할 수 있음.
 + fog : 물질이 전체 안개 설정에 영향을 받는지 여부를 결정.