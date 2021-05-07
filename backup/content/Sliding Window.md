---
title: "Sliding Window"
description: "Multiple Pointer Application -> Sliding Pointers첫번째와 마지막 위치를 기준으로 누적된 합을 이동시키고 비교하는 방법. "
date: 2021-05-07T00:16:31.740Z
tags: []
---
Multiple Pointer Application -> Sliding Pointers

첫번째와 마지막 위치를 기준으로 누적된 합을 이동시키고 비교하는 방법. 

```js
/*Write function called maxSubArraySum - accepts array of integers and number n.

This function calculates max. sum of n. consecutive elements in array. 
(largest sum in array)
*/
//O(N)
function maxSubArraySum(arr, num){
    let maxSum = 0;
    let tempSum = 0;
    if(arr.length < num) return null; //Check input validity

    //------------------------------------------
    //횟수만큼 순차적으로 증가한 값을 maxSum에 보관
    for(let i=0; i< num; i++){
        maxSum += arr[i]; //Init maxSum
    }
    tempSum = maxSum;
    //------------------------------------------
    
    //------------------------------------------
    //첫번째 누적합은 넘기고 다음 누적합을 만들어서 찻반째 누적합하고 비교해서 누적 합이 큰 값을 리턴 
    for(let i= num; i < arr.length; i++){
        //------------------------------------------
        //첫번째 누적합 - 배열의 최초 위치 값 + 누작합이 끝나는 위치 값
        //누적합이 그대로 우측으로 이동한다. (sliding window) 
        tempSum = tempSum - arr[i - num] + arr[i]; //Init input window
			  //------------------------------------------	
      
        //Add by init num. - first array value of window = only the sum of window.   
        maxSum = Math.max(maxSum, tempSum);
    }
    return maxSum;
    //------------------------------------------
} 
console.log(maxSubArraySum([2,6,9,2,1,8,5,6,3], 3)); //19
```

## 참고
https://medium.com/swlh/sliding-window-a-common-technique-for-solving-algorithmic-problems-involving-string-array-44adf35e2d5d