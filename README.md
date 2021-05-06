# VueJs Module Federation Demo

This example demos consumption of federated modules from a Webpack bundle. `layout` app depends on a component exposed by `home` app.

---

# Running Demo

Run `yarn start` . This will build and serve both `home` and `layout` on ports 3002 and 3001 respectively.

- HOST (layout): [localhost:3001](http://localhost:3001/)
- REMOTE (home): [localhost:3002](http://localhost:3002/)

# 추가된 것

workspace에 프로젝트들이 등록되어 있으므로 실행 전에 루트 폴더에서 `yarn install`을 한다. 이후 위의 Running Demo를 동작시킬 것.
sub앱이 추가되었다. 위와 마찬가지로 sub 폴더의 위치에서 `yarn start`를 한다.

- REMOTE2 (sub)): [localhost:3003](http://localhost:3003/)
