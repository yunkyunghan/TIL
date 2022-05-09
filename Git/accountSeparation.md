# 프로젝트 저장소 별 계정 분리 설정

개인과 회사의 계정을 분리하여 git을 올리고 싶을 때 사용하는 방법이다. <br>
global에 회사 계정이 등록되어서 개인 git에 올릴 때 repository를 생성할 때만 잔디(commit)가 심어지고 그 이후에는 더 이상 잔디가 심어지지 않는 것을 발견했다. 😥

## 계정 설정 정보 확인
### global
```bash
git config --list 
```

### local
```bash
git config --local --list 
```

## global 계정 설정
만약 `git config --list`를 통해서 계정이 있다면 따로 설정을 하지 않아도 된다. <br>하지만 없다면 아래와 같이 설정해주면 된다.

```bash
git config --global user.name "username"
git config --global user.email "username@email.com"
```

## local 계정 설정
위와 같이 global로 설정해주면 git 프로젝트/ 저장소에 global 계정 정보가 모두 반영된다. <br>
따라서 특정 프로젝트에서 다른 계정 (=회사에서 개인계정으로 올리고 싶을 때)을 사용하고 싶으면 `해당 저장소에서 local 설정`을 해주면 된다. <br>
**📍 local이 global보다 우선순위가 높기 때문**!

```bash
git config --local user.name "username"
git config --local user.email "username@email.com"
```
이렇게 설정을 각각 해주고 다시 계정 설정 정보 확인을 해주면 된다 :>
