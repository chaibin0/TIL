# WebMvcTest에서 404를 받는다면?

Timeline: Jan 07, 2020

URI이가 제대로 입력해도 404(NOT_FOUND)를 받은 적이 있다.

### 해결방안

    @WebMvcTest(controllers = {TestController.class})

@WebMvcTest에서 Controllers를 안적으면 에러가 아니라 404(NOT_FOUND) 호출 받는다.
혹여나 이런 실수 또 하지 않게 적습니다.