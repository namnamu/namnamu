# minecract

### scoreboard
- 만들기   
/scoreboard objective add \<보드변수\> <dummy || deathCount || playerKillCount || totalKillCount || health> [title]
   
   `scoreboard objectives add sc minecraft.used:minecraft.carrot_on_a_stick  `
   
- 리스트 확인하기   
/scoreboard objectives list

- 보이기   
/scoreboard objectives setdisplay <list || sidebar || belowName> <보드변수>
```
  list : tab으로 확인
  sidebar : 오른쪽 점수판
  belowName : 플레이어 닉네임 아래
```   
  
   `scoreboard objectives setdisplay sidebar sc`

- 삭제하기   
/scoreboard objectives remove <보드변수>


