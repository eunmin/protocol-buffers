# Language Guide (proto3)

https://developers.google.com/protocol-buffers/docs/proto3

## 메시지 타입 정의하기

먼저 간단한 예제를 보자. 쿼리 문자열과 페이지 번호, 페이지 당 결과 개수를 포함하는 검색 요청 메시지 포멧을
정의한다고 하자. 메시지 타입을 정의하는 `.proto` 파일은 다음과 같다.

```proto3
syntax = "proto3";

message SearchRequest {
  string query = 1;
  int32 page_number = 2;
  int32 result_per_page = 3;
}
```

- 첫번째 줄은 `proto3`를 사용한다는 의미다. 기본으로는 `proto2`를 사용한다. 첫번째 줄은 비어 있으면
  안된다.
- 이름/값 페어를 갖는 `SearchRequest` 메시지를 정의한다. 각 필드는 이름과 값을 가지고 있다.

### 필드 타입 명시하기

위 예제는 정수 스칼라 타입 두개와 문자열 스칼라 타입 하나를 정의 했다. 컴포지트 타입이나 열거형 타입 다른
메시지 타입도 쓸 수 있다.

### 필드 번호 부여하기

필드 마다 유일한 번호가 붙어 있음을 볼 수 있다.

### 필드 규칙 명시하기

### 다른 메시지 추가하기

`.proto` 파일 하나에 여러 메시지를 정의할 수 있다. 관련된 메시지가 있다면 유용하다. 예를 들면
검색 요청에 관련해서 `SearchResponse` 메시지를 정의할 수 있다.

```proto3
message SearchRequest {
  string query = 1;
  int32 page_number = 2;
  int32 result_per_page = 3;
}

message SearchResponse {
 ...
}
```

### 주석 추가하기

`.proto` 파일에 주석을 추가하기위해 C나 C++처럼 `//`나 `/* ... */` 문법을 쓸 수 있다.

```proto3
/* SearchRequest represents a search query, with pagination options to
 * indicate which results to include in the response. */

message SearchRequest {
  string query = 1;
  int32 page_number = 2;  // Which page number do we want?
  int32 result_per_page = 3;  // Number of results to return per page.
}
```

### 예약 필드

## 스칼라 값 타입

## 기본 값

메시지가 파싱되었는데 인코딩된 메시지에 특정 단일 항목이 없다면 그 필드의 파싱 결과는 기본 값이 설정된
형태로 파싱된다. 타입별로 기본 값은 다음과 같다:

- 문자열은 빈 문자열
- 바이트는 빈 바이트
- 불리언은 false
- 숫자 타입은 0
- 열거형은 첫번째 정의된 열거형 값 (0이 어야 한다.)
- 메시지 필드는 세팅되지 않고 언어 종속적인 값을 갖는다. 자세한 내용은 코드 생성 가이드를 참조하라

반복 필드의 기본값은 빈 값이다. (보통 언어에 따라 빈 리스트)
