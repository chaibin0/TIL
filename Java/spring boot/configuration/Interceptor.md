# Interceptor

Created: Jan 22, 2020 11:07 AM
Timeline: Jan 22, 2020
Type: Java, Spring

## 1. 등록은 WebMvcConfigurer에서한다.

@Bean을 주입해야 인터셉터에서 @Autowired가 가능합니다.

    @Configuration
    public class WebMvcConfig implements WebMvcConfigurer {
    
      @Override
      public void addInterceptors(InterceptorRegistry registry) {
    
        registry.addInterceptor(apiInterceptor()).addPathPatterns("/api/v1/interceptor");
    
    
      }
    
      @Bean
      public ApiInterceptor apiInterceptor() {
    
        return new ApiInterceptor ();
      }
    }

## 2. HandlerInterceptor

PreHandle에서 처리

    public class ApiInterceptor implements HandlerInterceptor {
    
      @Autowired
      MemberRepository memberRepository;
    
      @Override
      public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
          throws Exception {
    
        UserDetails user =
            (UserDetails) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
    
        Member member = memberRepository.findById(user.getUsername())
            .orElseThrow(() -> CustomException.MEMBER_NOT_FOUND);
    
        if (member.getStatus().equals(UserStatusType.Block)) {
          response.sendError(403, "Error");   //에러메시지 보내줄 때
    			//response.sendRedirect("/black"); 다른곳으로 강제이동 할 때
        }
    
        return HandlerInterceptor.super.preHandle(request, response, handler);
      }
    
    }