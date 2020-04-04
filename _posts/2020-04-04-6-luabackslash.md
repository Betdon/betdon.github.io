---
layout: post
title:  "해머스푼으로 구글 크롬 브라우저 열기"
date:   2020-04-04
excerpt: ""
tag: []
comments: true
---

맥 매크로 앱인 해머스푼을 회사 개발자님에게 영업당해서 사용하던 중 자주 사용하는 디렉토리나 앱을 열고 싶어서 추가하기로 함.  
그전에는 그냥 날짜,시간을 입력하는 매크로와 복잡한데 자주 사용하는 Key값 정도만 쉽게 입력하기 위해 썼는데  
디렉토리나 앱을 건드리는건 조금 어려운 부분이었음.  
  
  
# 특정 디렉토리 열기
```
local function OpenDirectory(mods, key, dir)
    local mods = mods or {}
    hs.hotkey.bind(mods, key, function()
        local shell_command = "open " .. dir
        hs.execute(shell_command)
    end)
end

OpenDirectory({'control','cmd','alt'}, "f", "/Applications") --파인더.
```
- 컨트롤+알트+커맨드+f 를 입력하면 파인더->응용프로그램을 연다. dir부분을 수정해서 다른 디렉토리도 추가해서 사용.  
  
  
# 특정 어플리케이션 실행
```
local function OpenApplication(mods,key,targetApp)
    local mods = mods or {}
    hs.hotkey.bind(mods,key,function()
        local shell_command = "open -a " .. targetApp
        hs.execute(shell_command)
    end)
end

OpenApplication({'control','cmd','alt'}, "c", 'google\\ chrome') --구글 크롬.
```
- 컨트롤+알트+커맨드+c 를 입력하면 구글 크롬을 연다.  
이미 실행된 크롬이 있다면 새로 실행하지 않고 이미 있던 걸 활성화한다.  
여기서 문제가 좀 발생했었음.  
lua에서 string에 속한 BackSlash(\)를 string이 아닌 특정 커맨드의 시작으로 인식하는 바람에  
본래 쉘스크립트에선 google\ chrome으로 작동하는 라인에서 계속 에러를 뱉는 것이다.  
string에 포함된 BackSlash를 사용하려면 \\으로 BackSlash를 두번 쳐야 \로 인식한다.
