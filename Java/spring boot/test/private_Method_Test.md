# private Method Test

Created: Jan 28, 2020 5:39 PM
Timeline: Jan 28, 2020
Type: Java, Junit, Test

# 1. Reflection을 이용

---

    Method method = instance.getClass().getDeclaredMethod("메소드 이름", 파라미터...);
    method.setAccessible(true);
    method.invoke(인스턴스, 파라미터, 파라미터,...);

만약 static 메소드라면 invoke 의 object는 null로 한다.

    private int privateMethod(int a, int b)
    
    Method method = instance.getClass().getDeclaredMethod("privateMethod", int.class,int.class);
    method.setAccessible(true);
    method.invoke(null, 10)

# 2. Spring에서 ReflectionUtils를 이용

    //invokeMethod(인스턴스, 메소드명)
    ReflectionTestUtils.invokeMethod(instance, "privateMethod");