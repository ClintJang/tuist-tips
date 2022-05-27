# [Tuist](https://tuist.io/) 유용한 정보 모음입니다.

Xcode 프로젝트와의 생성, 유지 관리 및 상호 작용을 용이하게 하는 것을 목표로 하는 도구(Command-line interface, CLI)입니다. 

iOS 개발에서 git 병합할 때 충돌이 자주 발생하는 Xcode Project 설정파일을 Swift 코드로 관리하게 해주는 큰 장점이 있습니다.

Tuist 를 감사하게 사용하고 있습니다. 😁<br />
사용하면서 유용했던 정보들을 잘 정리해 두고 싶어서 작성했습니다.<br />
계속 잘 정리해서 처음 사용하시는 분들 혹은 익숙하지 않은 분들에게 도움이 될 수 있도록 하겠습니다. 😊

- 기본적인 설치, 프로젝트 실행에서 유용한 팁까지 정리해봅니다.
- 더욱 디테일 하게 업데이트 할 예정입니다.
- 이제 샘플을 만들며 정리하고 있는 중이고 계속 업데이트 해나갈 생각입니다.
- 아직은 자료 정리하면서 업데이트 하는 단계입니다.

<br /><br />

## 목차
[# 기본적인 설치방법](https://github.com/ClintJang/tuist-tips/blob/master/README.md#-기본적인-설치방법) <br />

[# 프로젝트 만들기](https://github.com/ClintJang/tuist-tips/blob/master/README.md#-프로젝트-만들기) <br />

[# 기존 프로젝트에서 정보 축출](https://github.com/ClintJang/tuist-tips/blob/master/README.md#-기존-프로젝트에서-정보-축출) <br />

[# 터미널 명령어](https://github.com/ClintJang/tuist-tips/blob/master/README.md#-터미널-명령어) <br />

[# 참고](https://github.com/ClintJang/tuist-tips/blob/master/README.md#-참고) <br />

# [기본적인 설치방법](https://guides.cocoapods.org/using/getting-started.html)

Tuist 도구를 설치

```
$ curl -Ls https://install.tuist.io | bash
```

# 프로젝트 만들기

```
$ tuist init --platform ios

$ tuist edit 

$ tuist generate
```

# [# 기존 프로젝트에서 정보 축출](https://docs.tuist.io/guides/adopting-tuist)

 타겟 빌드 셋팅 축출
 
 ```
$ tuist migration settings-to-xcconfig -p 프로젝트명.xcodeproj -t 타겟명 -x MyApp.xcconfig

→ MyApp.xcconfig 로 축출
```

프로젝트 빌드 셋팅 축출

 ```
$ tuist migration settings-to-xcconfig -p 프로젝트명.xcodeproj -x MyAppProject.xcconfig

→ MyAppProject.xcconfig 로 축출
```


축출한 xcconfig 파일 검증을 위해 ..

 ```
$ tuist migration check-empty-settings -p 프로젝트명.xcodeproj -t 타겟명
 ```
 
 마이그레이션의 시작은 타켓 셋팅 부터?

 ```
$ tuist migration list-targets -p 프로젝트명.xcodeproj
 ```

 ``` swift
// 예) 결과

[
  {
    "linkedFrameworksCount" : 0,
    "targetDependenciesNames" : [

    ],
    "targetName" : "TestProject001"
  },
  {
    "linkedFrameworksCount" : 0,
    "targetDependenciesNames" : [
      "TestProject001"
    ],
    "targetName" : "TestProject001Tests"
  },
  {
    "linkedFrameworksCount" : 0,
    "targetDependenciesNames" : [
      "TestProject001"
    ],
    "targetName" : "TestProject001UITests"
  }
]
 ```
 
 
# 터미널 명령어
## Xcode 프로젝트 설정 파일 생성

```
$ tuist generate
```

## 투이스트 디펜던시스 파일에 설치된 파일 로컬에 설치 

```
$ tuist fetch

```

## 깨끗하게!! 정리하고 디버깅
> 일부 Tuist 기능은 실행 간에 지속되는 로컬 상태를 저장합니다. 예를 들어, tuist generate는 프로젝트 생성 속도를 높이기 위해 프로젝트의 중간 표현을 저장합니다.

```
$ tuist clean
```

하위 집합까지 조절해서 데이터를 정리하면?

```
$ tuist clean manifests tests
```

- plugins: the plugins cache
- builds: the builds artifacts cache
- tests: the tests cache
- generatedAutomationProjects: the automation projects cache
- projectDescriptionHelpers: the project description helpers cache
- manifests: the manifests cache


## 버전

### 투이스트 버전 확인

```
$ tuist version

```

### 프로젝트별 다른 ..

- .tuist-version 파일을 만들어서 안에 해당 버전 정보를 작성해두면, 해당 버전 을 다운로드해서 해당 버전으로 실행시켜 줍니다.

### 로컬에 설치된 투이스트 버전 리스트

```
$ tuist local 
```

### 투이스트 버전 삭제

```
$ tuist uninstall 0.4.0

```

### 투이스트 실행할 버전

```
$ tuist local 1.0.0
```


# 참고
### 참고 링크
- [Xcode Build Settings](https://xcodebuildsettings.com): 사용 가능한 모든 빌드 설정과 그 의미에 대한 참조
- Tuist : https://tuist.io/
- Tuist Docs : https://docs.tuist.io/
- Tuist Github : https://github.com/tuist/tuist
- XcodeGen : https://github.com/yonaskolb/XcodeGen

## 블로그

### 버전 공통

- [Tuist 도입하며 느낀점](https://medium.com/@jang.wangsu/ios-swift-tuist-%EB%8F%84%EC%9E%85%ED%95%98%EB%A9%B0-%EB%8A%90%EB%82%80%EC%A0%90-902bc2c4de42)

### Tuist Version 1.X
- [프로젝트 생성/관리 도구 Tuist(1) - Start](https://minsone.github.io/mac/ios/ios-project-generate-with-tuist-1)


