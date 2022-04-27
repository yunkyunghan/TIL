# 현재 설정된 계정 정보 확인 및 변경

회사와 개인 개정을 분리하고 싶을 때 계정 정보를 바꾸면 된다. 

## 현재 설정된 계정 정보 확인

```bash
$ git config user.name

$ git config user.email
```

## 계정 변경

```bash
$ git config --global user.name // 변경 희망하는 계정

$ git config --globla user.email // 변경 희망하는 이메일
```

이후 다시 계정 정보 확인 명령어를 통해 `변경된 계정 및 이메일을 확인` 하면 된다.