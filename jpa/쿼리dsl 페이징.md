# < Querydsl의 간단한 페이징 전략 (검색 조건, 카테고리 등 필터링 가능) >

###  레포지토리 구현체에서 각 조건에 대한 빌더 메서드 생성
``` 
    private BooleanExpression usernameEq(String username) {
        return hasText(username) ? member.username.eq(username) : null;
    }

    private BooleanExpression teamNameEq(String teamName) {
        return hasText(teamName) ? member.team.name.eq(teamName) : null;
    }

    private BooleanExpression ageGoe(Integer ageGoe) {
        return ageGoe != null ? member.age.goe(ageGoe) : null;
    }

    private BooleanExpression ageLoe(Integer ageLoe) {
        return ageLoe != null ? member.age.loe(ageLoe) : null;
    }
```
###  where절에서 조건 붙여주기
```
    @Override
    public List<MemberTeamDto> search(MemberSearchCondition condition) {
        return queryFactory
                .select(new QMemberTeamDto(
                        member.id.as("memberId"),
                        member.username,
                        member.age,
                        team.id.as("teamId"),
                        team.name.as("teamName")
                ))
                .from(member)
                .leftJoin(member.team, team)
                .where(usernameEq(condition.getUsername()),
                        teamNameEq(condition.getTeamName()),
                        ageGoe(condition.getAgeGoe()),
                        ageLoe(condition.getAgeLoe())
                )
                .fetch();
    }

```

### 아래와 같이 컨트롤러를 작성해주면
```
     @GetMapping("/v2/members")
     public Page<MemberTeamDto> searchMemberV2(MemberSearchCondition condition,
 Pageable pageable) {
         return memberRepository.searchPageSimple(condition, pageable);
     }
```
- 'http://localhost:8080/v2/members?size=5&page=2' 이와 같은 구조의 get 요청에 대해 페이징 처리가 제대로 됨을 확인