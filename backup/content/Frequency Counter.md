---
title: "Frequency Counter"
description: "https&#x3A;//codepen.io/cskwork/pen/KKWwwKe?editors=0011"
date: 2021-05-06T23:09:50.975Z
tags: []
---
Compare Two Arrays Frequency
```js
/*
Q:
Write a function called same, that accepts two arrays.

The function should return true if every value in the array has it's corresponding value squared in the second array. The frequency of values must be the same.
*/

function same(arr1, arr2){

  //---------------------------------
	//비교 가능한 배열인지 확인
  if(arr1.length !== arr2.length){
		return false;
	}
  //---------------------------------
  //횟수 카운트 배열 초기화
	let frequencyCounter1 = {};
	let frequencyCounter2 = {};
  //---------------------------------

  //---------------------------------
  //배열값이 등장하는 횟수 세기 
	for(let val of arr1){
		frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1; //frequency counting. 
	}
  //---------------------------------

	for(let val of arr2){
		frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1;
	}

  //---------------------------------
  //배열 ^2 조건 충족하는지 확인
  for(let key in frequencyCounter1){
		if(!(key ** 2 in frequencyCounter2)){
			return false;
		}
		if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
			return false;
		}
	}
	//console.log(frequencyCounter1);
	//console.log(frequencyCounter2);
	return true;
  //---------------------------------
}

console.log(same([1,2,3] , [1,4,5])); //false
console.log(same([1,2,3] , [1,4,9])); //true
```

https://codepen.io/cskwork/pen/KKWwwKe?editors=0011

Compare Strings (Anagram)
```js
/*
Q:
Given two strings, write a function to determine if the second string is an anagram of the first.

(Anagram is a word, phrase, or name formed by rearranging the letters of another, such as cinema, formed from iceman.)
*/
function validAnagram(first, second){
  //--------------------------------
  //스트링 길이가 맞는지 비교
	if(first.length !== second.length){
		return false;
	}
  //--------------------------------
	
  //--------------------------------
  //횟수 세기 위한 배열 초기화
	const lookup = {}; //obj as freq.counter
  //--------------------------------

  //--------------------------------
  //횟수 세기 배열에 첫번째 배열에 있는 문자를 키값에 넣고 반복해서 나온 만큼 카운드 증가 (value 값에 담음).
	//Break down the first string.
	for(let i=0; i < first.length ; i++){
		let letter = first[i];
		//if letter exists, increment, otherwise set to 1
		lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
	}
  //--------------------------------

  //--------------------------------
  //횟수 세기 배열에 값이 있는지 확인
  //있으면 true 및 -1로 카운트 감소.
	//Break down the second string
	//then check to first string.
	for(let i=0; i < second.length; i++){
		let letter = second[i];
		//can't find letter or letter is zero then not anagram.
		if(!lookup[letter]){
			return false;
		}else{
			lookup[letter] -= 1;
		}	
	}
	return true;
  //--------------------------------
}

console.log(validAnagram('anagram','nagaram'));
console.log(validAnagram('anagram','nagparam'));


```