Annotation
======
- 클래스나 메소드위에 붙여서 사용
- 소스코드에 메타코드(추가정보)를 주는 것
- Annotation을 이용하면 사용시 값을 설정하는 방식등과 Reflection을 통해 Validation Check같은 단순노동 로직이 조금 더 간편해질 수 있다.
  1. VO(domain)의 method에 최소값, 최대값은 이것이다 하는 Annotation을 설정한다.
  1. Validation하는 객체를 생성
  1. Validation 객체안에는 넘어온 VO의 어노테이션 정보를 받아와서 어노테이션에 설정된 각각의 값들을 추출해 VO의 값과 비교하면서 validation check를 진행한다.
  1. Validation check가 완료됐다면 reflection을 통해서 setter메소드를 불러와 VO에 설정까지 가능하다.

