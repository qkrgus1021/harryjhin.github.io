---
title: "[Winget] 이슈 해결 방법"
excerpt: "winget 관련 이슈 해결방법에 대해 설명합니다"
---

## 'winget' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다

```powershell
winget : 'winget' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오.
위치 줄:1 문자:1
+ winget
+ ~~~~~~
    + CategoryInfo          : ObjectNotFound: (winget:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

![winget error](../../../assets/images/winget-error-(1).png)

이 상황의 원인은 두 가지 입니다.

1. winget 앱 실행 별칭 옵션이 비활성화되어 있는 경우
2. 앱 설치 관리자가 설치되어 있지 않은 경우

### winget 앱 실행 별칭 활성화

1. `Win` + `S` 실행
2. 앱 실행 별칭 관리 검색 및 실행

    ![앱 실행 별칭 관리 접근](../../../assets/images/winget-solution-(1).png)

3. 'Windows Package Manager Client' 옵션 **켬**으로 바꾸기

    ![끔 -> 켬](../../../assets/images/winget-solution-(2).png)

### 앱 설치 관리자 설치 또는 업데이트

앱 설치 관리자는 Microsoft Store에서 [다운로드](https://www.microsoft.com/ko-kr/p/%ec%95%b1-%ec%84%a4%ec%b9%98-%ea%b4%80%eb%a6%ac%ec%9e%90/9nblggh4nns1?activetab=pivot:overviewtab)할 수 있습니다.

보통 이미 설치되어 있기 때문에 업데이트한 적이 없다면 업데이트가 필요합니다.

업데이트는 Microsoft Store 앱에서 진행할 수 있습니다.

1. Microsoft Store 실행
2. 좌측 하단의 **라이브러리** 클릭
3. 우측 상단에 위치한 **업데이트 다운로드** 클릭

    ![MS Store 업데이트](/assets/images/winget-solution-(3).png)
