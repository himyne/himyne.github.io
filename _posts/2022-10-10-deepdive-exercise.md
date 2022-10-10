---
published: true
layout : single
title : "[JS] 모던 Javascript Deep Dive 29장~32장 관련 문제 모음"

categories:
  - DeepDive
tags:
  - Deepdive
  - Date
  - RegExp
  - Math
  - 정규표현식

toc: true
toc_sticky: true
toc_label: "29장~32장 관련 문제 모음"
--- 

# Math

[[JS] 백준 1546번 평균](https://himyne.github.io/baekjoon/boj-1546/)

# Date

[코딩테스트 연습 - 2016년](https://school.programmers.co.kr/learn/courses/30/lessons/12901)

```jsx
function solution(a, b) {
    const date = new Date(`2016/${a}/${b}`);
    let answer = '';
    answer = date.toString().slice(0,3).toUpperCase();
    return answer;
}
```

# RegExp

## 프로그래머스 - 신규 아이디 추천

[코딩테스트 연습 - 신규 아이디 추천](https://school.programmers.co.kr/learn/courses/30/lessons/72410?language=javascript)

### 내 풀이

```jsx
function solution(new_id) {
  let answer, regexr;
  answer = new_id.toLowerCase();
  regexr = /[^\d\a-z\-\_\.]/g; 
  answer = answer.replace(regexr, "");
  regexr = /\.{2,}/g;
  answer = answer.replace(regexr, ".");
  regexr = /^\.|\.$/g;
  answer = answer.replace(regexr, "");

  if (answer === "") {
    answer = "a";
  }
  if (answer.length >= 16) {
    answer = answer.substr(0, 15);
    regexr = /\.$/g;
    answer = answer.replace(regexr, "");
  }
  //repeat
  if (answer.length <= 2) {
    while (answer.length < 3) {
      answer += answer[answer.length - 1];
    }
  }
  return answer;
}
```

### 모범 풀이

```jsx
function solution(new_id) {
    const answer = new_id
        .toLowerCase() // 1
        .replace(/[^\w-_.]/g, '') // 2
        .replace(/\.+/g, '.') // 3
        .replace(/^\.|\.$/g, '') // 4
        .replace(/^$/, 'a') // 5
        .slice(0, 15).replace(/\.$/, ''); // 6
    const len = answer.length;
    return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
}
```

## 백준 - FBI

[2857번: FBI](https://www.acmicpc.net/problem/2857)

```jsx
const ERRORMSG = 'HE GOT AWAY!'
const fs = require('fs');
let input = fs.readFileSync('./input.txt').toString().split('\n');

const regExp = /FBI/g;
let answer = '';
answer = input.filter((item) => regExp.test(item))

for(let i=0; i<answer.length; i++){
  console.log(input.indexOf(answer[i])+1+' ')
}

if(answer.length === 0){
  console.log(ERRORMSG)
}
```

### 정규표현식 시각화 사이트

[Online Regex tester and visualizer - Python, PHP, Ruby, JavaScript, Java](https://extendsclass.com/regex-tester.html)