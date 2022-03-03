# Project #1: ImplementingLuxo



![luxo](https://github.com/LittleSamakFox/luxo_threejs/blob/main/luxo.png?raw=true)



### 기반

three module을 이용하여 Luxo램프를 제작하였습니다.



### 개요

proj1-skeleton.html와 데모영상, Requirements를 베이스로 하여, luxo lamp를 제작하였습니다.
GUI 컨트롤 패널로 각 부분을 조절할 수 있도록 updateLuxo()함수를 수정하였고,
luxo lamp 제작에 필요한 요소를 차례대로 제작하였습니다.
또한 bulb에서 spotlight가 나와 그림자가 출력되게 하였습니다.



### 구성 요소

#### luxo lamp bone

스탠드의 뼈대를 제작하기 위해 base와 baseMesh, baseDisc, baseDiscMesh를 기반으로,
각 조인트와 암 부분을 차례대로 add하는 형식으로  baseGreenJoint, lowerBlueArm, middleGreenJoint, upperBlueArm, headGreenJoint을 추가하였습니다.
조인트와 암은 CylinderBufferGeometry 모델을 사용하였습니다.

#### luxo lamp bulb

headGreenJoint에 각 램프에 필요한 요소를 추가하였습니다.
bulbLamp(램프 헤드)부분은 CylinderBufferGeometry , bulb(전구)부분은 SphereBufferGeometry 모델로 추가하였습니다.
bulbLight(램프 빛)는 SpotLight을 사용하고 bulb에 타겟을 준 뒤 각도를 변경하였고, castShadow시켜 SpotLight가 비췄을때 그림자가 생기도록 하였습니다.
bulbLight가 비춰지는 범위를 알려주기 위한 bulbLightHelper를 SpotLightHelper를 이용하여 제작하였습니다.

#### gui

gui를 통한 장면에 변화를 줄 경우, updateLuxo() 함수를 호출하도록 하였습니다.
gui는 4부분으로 구분지었습니다. 각 gui 부분은 표에 적힌 범위와 stepsize에 맞게 변경되도록 하였습니다.

- base (red box) : base의 x축 y축 높이 변경을 하도록 하였습니다.
- arm(blue) lengths : lowerBlueArm과 upperBlueArm의 길이가 변경되도록 하였습니다.
  baseDisc를 회전시키는 부분의 gui 위치를 데모영상을 토대로 base에서 arm으로 수정하였습니다.
- joint(green) angles: baseGreenJoint, middleGreenJoint, upperGreenJoint의 각도가 변경되도록 하였습니다.
- lightbulb : bulbLight 전구의 SpotLight가 비추는 범위를 변경되도록 하였습니다.
- bulbLightHelper(Spotlight 범위선)을 버튼으로 키고 끌 수 있도록 하였습니다.

#### function updateLuxo()

각 뼈대에 해당하는 height, angle, position 변화되는 부분을 명시하여 각각 구분지어 작성하였고, bulbLightHelper가 정상적으로 업데이트 되도록 하였습니다.
lowerBlueArm과 upperBlueArm의 길이가 오브젝트에 적절하도록 Scale set하였고,
basicArmHeight(Arm기본 길이)를 변수로 설정하여 비율에 맞게 arm의 길이가 변화되도록 하였습니다.
bulb의 위치와, bulbLight가 비춰지는 부분이 알맞도록 position을 변경하였습니다.

#### add PointLight and objects shadow

그림자 표현을 위해 renderer shadowMap을 enable 시켰습니다.
PointLight의 castShadow가 명시되지 않았기에 true로 변경하여 그림자가 발생하도록 하였습니다.
주변 사물은 TorusKnotGeometry, DodecahedronGeometry, IcosahedronGeometry, SphereGeometry 모델을 사용하여 제작하였고, 광원을 보이도록 MeshPhongMaterial로 재질을 설정하였습니다.