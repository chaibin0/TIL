# String에 대한 NotBlank NotEmpty NotNull

Created: Jan 08, 2020 2:02 PM
Timeline: Jan 08, 2020
Type: Java, Spring

# 1. @NotBlank

---

    @Getter
    public class ValidationNotBlank {
    
      @NotBlank
      @JsonProperty("data")
      String data;
    }

## 1.1 데이터가 존재할 경우(통과)

      @DisplayName("1. Blank 테스트(데이터 O)")
      @Test
      void testValidNotBlank1() throws Exception {
    
        String data = "data";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step1")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 1.2 "" 데이터(실패)

      @DisplayName("2. Blank 테스트(empty)")
      @Test
      void testValidNotBlank2() throws Exception {
    
        String data = "";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step1")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 1.3 Null 데이터(실패)

      @DisplayName("3. Blank 테스트(null)")
      @Test
      void testValidNotBlank3() throws Exception {
    
        String data = null;
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step1")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 1.4 whitespace 데이터(실패)

     @DisplayName("4. Blank 테스트(whitespace)")
      @Test
      void testValidNotBlank4() throws Exception {
    
        String data = "        ";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step1")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 1.5 Trim이 필요한 데이터(통과)

    @DisplayName("5. Blank 테스트(trimData)")
      @Test
      void testValidNotBlank5() throws Exception {
    
        String data = "    data    ";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step1")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

# 2. @NotNull

---

    @Getter
    public class ValidationNotNull {
    
      @NotNull
      @JsonProperty("data")
      String data;
    }

## 2.1 데이터가 존재할 경우(통과)

      @DisplayName("1. Null 테스트(데이터 O)")
      @Test
      void testValidNotNull1() throws Exception {
    
        String data = "data";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step3")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 2.2 "" 데이터(통과)

      @DisplayName("2. Null 테스트(empty)")
      @Test
      void testValidNotNull2() throws Exception {
    
        String data = "";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step3")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 2.3 Null 데이터(실패)

      @DisplayName("3. Null 테스트(null)")
      @Test
      void testValidNotNull3() throws Exception {
    
        String data = null;
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step3")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }
    

## 2.4 whitespace 데이터(통과)

      @DisplayName("4. Null 테스트(whitespace)")
      @Test
      void testValidNotNull4() throws Exception {
    
        String data = "        ";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step3")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 2.5 Trim이 필요한 데이터(통과)

      @DisplayName("5. Null 테스트(trimData)")
      @Test
      void testValidNotNull5() throws Exception {
    
        String data = "    data    ";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step3")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }
    

# 3. @NotEmpty

---

    @Getter
    public class ValidationNotEmpty {
    
      @NotEmpty
      @JsonProperty("data")
      String data;
    }

## 3.1 데이터가 존재할 경우(통과)

      @DisplayName("1. Empty 테스트(데이터 O)")
      @Test
      void testValidNotEmpty1() throws Exception {
    
        String data = "data";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step2")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 3.2 "" 데이터(실패)

      @DisplayName("2. Empty 테스트(empty)")
      @Test
      void testValidNotEmpty2() throws Exception {
    
        String data = "";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step2")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 3.3 Null 데이터(실패)

      @DisplayName("3. Empty 테스트(null)")
      @Test
      void testValidNotEmpty3() throws Exception {
    
        String data = null;
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step2")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 3.4 whitespace 데이터(통과)

      @DisplayName("4. Empty 테스트(whitespace)")
      @Test
      void testValidNotEmpty4() throws Exception {
    
        String data = "        ";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step2")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

## 3.5 Trim이 필요한 데이터(통과)

      @DisplayName("5. Empty 테스트(trimData)")
      @Test
      void testValidNotEmpty5() throws Exception {
    
        String data = "    data    ";
        RequestDto dto = new RequestDto(data);
        String json = mapper.writeValueAsString(dto);
        mvc.perform(get("/valid/step2")
            .contentType(MediaType.APPLICATION_JSON)
            .content(json))
            .andExpect(status().isOk())
            .andExpect(content().string("valid"));
      }

![image/String%20NotBlank%20NotEmpty%20NotNull/Untitled.png](image/String%20NotBlank%20NotEmpty%20NotNull/Untitled.png)

겸으로 숫자에서는 @NotBlank @NotEmpty 쓰면 안됩니다.