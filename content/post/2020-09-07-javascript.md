---
title: React 
date: 2020-09-07
categories: ["2nd Deck"]
---

생활코딩 Javascript 강의   

Javascript 기본



 - object(객체)
 - function(함수)
 - Parameter(매개변수) 
 - Argument(인자)

### object 문법
```
var coworkers = {
  "programmer":"egoing",
  "designer":"leezche"
};
document.write("programmer : "+coverkers.programmer+"<br>");
document.write("designer : "+coverkers.designer+"<br>");
coworkers.bookkeeper = "doru";
document.write("bookkeeper : "+coverkers.bookkeeper+"<br>");
coworkers["data scientist"] = "taeho";
document.write("data scientist : "+coverkers.["data scientist"]+"<br>");
```
  - object 선언은 중괄호
  - key 값에 공백을 넣을 수 없으므로 대괄호 사용
  - object의 property 사이에 ,를 붙인다.

```
for(var key in coworkers) {
  document.write(key+' : ' + coworkers[key] +'<br>');
}
```
  - 반복문 for in
```
coworkers.showAll = function(){
  for(var key in this) {
    document.write(key+' : ' + this[key] +'<br>');
  }
}
```
  - method 지정 하기