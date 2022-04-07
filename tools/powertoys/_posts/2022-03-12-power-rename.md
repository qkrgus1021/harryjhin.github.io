---
title: "PowerToys (9) : PowerRename"
excerpt: "다수의 파일 이름을 원하는대로 한 번에 변경할 수 있는 기능"
---

다수의 파일을 검색하여 선택한 파일들을 규칙에 따라 이름을 변경합니다.

## 정규식

프로그래밍에서 문자열을 다루기 위해 쓰는 식입니다.

정규식을 통해서 파일을 검색할 수 있습니다.

정규식에 대한 자세한 내용은 [다음](https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/regular-expression-language-quick-reference)을 참고하세요.

## Bost 라이브러리 사용

표준 라이브러리 대신 Boost 라이브러리를 사용하면 [Lookbehind](https://www.boost.org/doc/libs/1_74_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html#boost_regex.syntax.perl_syntax.lookbehind)와 같은 확장 기능을 사용할 수 있습니다.
