# Workspace에 대한 개념과 사용
## workspace의 개념
[참고문서](https://musma.github.io/2019/04/02/yarn-workspaces.html)<br>
Workspace는 SPA에서 각 앱들이 같은 모듈을 공유하고 서로를 참조할 수 있게 하는 공간이다. 앱 개발시 Workspace는 루트 폴더에 위치할 수 있는 yarn의 기능이며 Workspace를 통해 각 앱들은 루트의 node modules를 공유하면서 일부 devDependencies에 따라 소수의 모듈만을 앱 내에 받아 사용하게 되며 Workspace의 목록에 등록된 앱들이 모듈처럼 사용될 수 있게 만들어준다.

## Workspace의 사용 목적
* 많은 모듈이 사용되는 프로젝트에서 동일하게 사용되는 모듈을 하나로 사용한다.
* 여러 모듈들을 묶어 서로 이름으로 참조할 수 있게 한다.
* 프로젝트마다 모듈의 추가 및 관리를 공통적, 개별적으로 한다.

## Workspace의 구현방법
SPA프로젝트의 루트 폴더에 `package.json`을 생성하거나 이미 있는 것을 사용한다. 이곳에서 앱들을 Workspace에 등록한다.

```vue.js
//package.json
{
  "private": true
  "workspaces": [
  "사용할 앱의 폴더1", 
  "사용할 앱의 폴더2", 
  ...
  ]
}
```

위 내용을 `package.json`에 추가한다. Workspace는 private 상태일 때 동작하므로 `"private": true`를 설정 후 Workspace를 사용할 수 있다. 코드 작성 후 루트 폴더에서 이 코드를 yarn으로 설치를 해준다.

`$ yarn install`

그러면 `package.json`에 따라 루트 폴더에 node_modules와 yarn.lock 파일이 생성된다. 앱들은 node_moudules를 공유하게 되고 yarn은 워크스페이스의 앱들을 npm 로컬 패키지로 인식한다.

## Workspace 동작 확인
Worspace의 동작을 확인하기 위해 깃허브에 올라온 [데모](https://github.com/anuroopjoy/npm7-sample)를 이용해 동작을 확인해 보았다. 원본에는 루트의 `package.json`에 libs 하위 폴더만 추가되었기 때문에 apps의 하위 폴더도 등록을 해주고 돌려본 결과와 원본을 비교해보았다. 결론은 둘 다 같은 결과를 얻을 수 있었다. 이유는 Workspace에 등록 후 yarn이 libs의 하위 폴더에 있는 프로젝트들을 로컬 npm 패키지로 인식해 관리하기 때문에 앱들이 yarn start로 서버를 돌릴 때 같은 루트에 있는 앱들이 libs를 사용할 수 있게 된다. 다만 apps를 등록하지 않았을 경우 앱들은 별도로 자신의 node_modules가 필요해진다.

## Workspace구현
루트 폴더에 Host(layout), Remote(home), Remote2(sub)가 되는 프로젝트가 있다. Workspace를 사용하지 않는다면 각 프로젝트마다 노드모듈을 설치해 실행시키겠지만 루트 폴더의 `package.json`에서 프로젝트들을 등록하고 모듈들을 한 번에 관리할 수 있다.
### package.json
```json
{
  "private": true,
  "scripts": {},
  "devDependencies": {},
  "workspaces": [
    "home",
    "layout",
    "sub"
  ]
}

```


## Workspace 사용시 장점
* 모듈 설치의 시간과 용량을 줄일 수 있다.
* 한 번의 동작으로 여러 프로젝트에서 돌아갈 모듈을 돌릴 수 있다.
* 모듈을 묶어 배포가 쉬워진다.

## 정리
Workspace를 사용할 경우 모듈 공유와 참조가 쉽다는 이점이 있다. 위의 데모에서는 libs만 Workspace에 추가했지만 모듈의 공유를 위해 다른 앱들도 추가해서 node_modules를 하나로 사용하는게 더욱 효율적이라 생각된다.
