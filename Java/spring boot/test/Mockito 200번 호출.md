# Mockito 원치않는 200번 호출되었다면

Timeline: Jan 07, 2020

## 1. given(BDD)이나 when메소드에서 제대로 매칭이 안됨

원치않는 200번이 호출되는 현상

    given(voteService.vote(Mockito.eq(name), Mockito.eq(phone), Mockito.eq(uid), Mockito.eq(votingList)))
                .willReturn(ResponseEntity.created(URI.create("/vote/success")).build());
    
    given(voteService.vote(name, phone, uid, votingList))
                .willReturn(ResponseEntity.created(URI.create("/vote/success")).build());
    

> java.lang.AssertionError: Status expected:<201> but was:<200>

created로 반환해야 하는데 ok로 반환되어버렸다.

##2. 해결방안

    given(voteService.vote(Mockito.anyString(), Mockito.anyString(), Mockito.anyString(),
            Mockito.anyList()))
                .willReturn(ResponseEntity.created(URI.create("/vote/success")).build());

any메소드를 이용하면 임시적으로 해결이 됩니다.