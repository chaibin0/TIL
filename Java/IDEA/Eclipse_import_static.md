# Eclipse에서 import static된 메소드 못 불러올 때

Created: Jan 17, 2020 10:15 AM
Timeline: Jan 17, 2020
Type: Java, Spring, eclipse

이 문제는 진짜 짜증난다. Eclipse는 똑똑하지 않아서 import static은 내가 지정한 것만 불러올 수 있다.

그래서 import static 할만한 것들을 미리 지정하자

import static 남용하는건 안좋다. 대부분 쓰는곳만 import static한다.

~~가장 쉬운건 Eclipse 버리고 IntelliJ로 갈아타자~~

## 1. import static 등록



### 1.1 메소드 위치 찾기

Ctrl + H 를 통해 search하고 메소드 검색
Search For에서 찾으려고 하는 클래스(Type) 메소드(Method)를 선택

![image/Eclipse%20import%20static/Untitled.png](image/Eclipse%20import%20static/Untitled.png)

메소드 찾으면 더블클릭해서 들어가준다.

![image/Eclipse%20import%20static/Untitled%201.png](image/Eclipse%20import%20static/Untitled%201.png)

### 1.2 Import static 등록

오른쪽 버튼 누르고 Copy Qualified Name 클릭

- Window - Preferences - Java - Editor - Content Assist - Favorites

New Type(클래스단위) new Member(함수 단위)로 하고 안에있는 데이터에 매개변수()만 제거해준다.

클래스단위라면 메소드까지 제거해준다.

![image/Eclipse%20import%20static/Untitled%202.png](image/Eclipse%20import%20static/Untitled%202.png)

등록 후 확인

![image/Eclipse%20import%20static/Untitled%203.png](image/Eclipse%20import%20static/Untitled%203.png)

## 2. import static 사용하는 클래스(정리중)



### 2.1 Test(Mock,Mockito, BDD, assertJ)
* Slice Test와 Mockito는 importStatic으로 하면 편합니다.

org.assertj.core.api.Assertions

org.junit.Assert

org.mockito.Mockito

org.mockito.BDDMockito

org.mockito.Matchers

org.mockito.ArgumentMatchers

org.springframework.security.test.web.servlet.request.SecurityMockMvcRequestBuilders

org.springframework.security.test.web.servlet.request.SecurityMockMvcRequestPostProcessors

org.springframework.security.test.web.servlet.response.SecurityMockMvcResultMatchers

org.springframework.security.test.web.servlet.setup.SecurityMockMvcConfigurers

org.springframework.test.web.client.match.MockRestRequestMatchers

org.springframework.test.web.client.response.MockRestResponseCreators

org.springframework.test.web.servlet.request.MockMvcRequestBuilders

org.springframework.test.web.servlet.result.MockMvcResultHandlers

org.springframework.test.web.servlet.result.MockMvcResultMatchers

## 2. Spring HATEOAS
* methodOn이나 LinkTo같은 메소드 사용할떄는 Import static으로 사용함

org.springframework.hateoas.server.mvc.WebMvcLinkBuilder

## 3. Spring REST Docs

org.springframework.restdocs.operation.preprocess.Preprocessors.*

org.springframework.restdocs.payload.PayloadDocumentation.*