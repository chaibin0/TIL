# Mockito에서 wildcard Object 사용할 때

Timeline: Jan 07, 2020

## 1. 에러


**Controller & Service**

    //Controller
    @GetMapping("/step1")
    public ResponseEntity<?> read(@RequestParam(name = "id") Long id) {
    
        return domainService.read(id);
    }
    
    //Service
    public interface DomainService {
      ResponseEntity<?> read(Long id);
    }

**WebMvcTest**

    @WebMvcTest(controllers = DomainController.class)
    class DomainControllerTest {
    
      @AfterAll
      static void tearDownAfterClass() throws Exception {}
    
      @MockBean
      DomainService domainService;
    
      @Autowired
      MockMvc mvc;
    
      @Test
      void testRead() throws Exception {
    
        Long id = 1L;
        Domain domain = Domain.builder()
            .number(1L)
            .date(LocalDateTime.now())
            .name("하이").build();
    		
    	//여기서 에러
    	when(domainService.read(id)).thenReturn(ResponseEntity.ok(domain));
    
        doReturn(ResponseEntity.ok(domain)).when(domainService).read(id);
        mvc.perform(get("/chap3/step1").param("id", "1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("하이"))
            .andDo(print());
      }
    }

when - thenReturn (given - willReturn)으로 지정할 때 

domainService.read(id)은 ResponseEntity<?>를 반환하고
ResponseEntity.ok(domain)은 ResponseEntity<T>형을 반환한다.

domainService.read(id) Mock객체라서 ?을 판단할 수 없다.

## 2. 해결 방법

    doReturn(ResponseEntity.ok(domain)).when(domainService).read(id);

doReturn을 해서  ResponseEntity<T>을 알아낼 수 있게 해줘야 테스트가 가능하다.