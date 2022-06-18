---
title: "JS - snippets"
description: "Event Binding "
date: 2022-04-21T01:35:06.995Z
tags: []
---
### Event Bind HTML TAG
```js
let eventBinding =  () => {
	this.clickBindHtmlIdTag("subjectType", this.changeSort);	
};
    
 let changeSort = () => {	 
	console.log('changesort');
};
	
let actionBindId = (tagId, actionFunction) => {
	let tagIdEvent = document.getElementById(tagId);
	tagIdEvent.addEventListener("input", actionFunction);
};

let valueBindId= (tagId, value) => {
   let tagHtml = document.getElementById(tagId);
   tagHtml.innerHTML = value;
};
```

### SWTICH CASE STRING
```js
	convertDayNameEngToKor : (day) =>
	({
	    'Monday' 	: '월',
	    'Tuesday'	: '화',
	    'Wednesday'	: '수',
	    'Thursday'	: '목',
	    'Friday'	: '금',
	    'Saturday'	: '토',
	    'Sunday'	: '일'
	})[day] ,
```

### SWITCH CASE FUNCTION with Sort
```js
let subjTypeTag = 'ASC'
let itemList = [] ;

let sortedList = {
  'ASC': function (itemList) {
	itemList.sort((a, b) => a.year < b.year ? -1 : a.year > b.year ? 1 : 0) 
	itemList.sort((a, b) => a.smstrCd < b.smstrCd ? -1 : a.smstrCd > b.smstrCd ? 1 : 0) 
    return itemList;
  },
  'DESC': function (itemList) {
	itemList.sort((a, b) => a.year > b.year ? -1 : a.year < b.year ? 1 : 0)
	itemList.sort((a, b) => a.smstrCd > b.smstrCd ? -1 : a.smstrCd < b.smstrCd ? 1 : 0) 
    return itemList;
  },
};

itemList = sortedList[subjTypeTag](itemList);
```

### Check If Empty
```js
let isEmpty = (value) => { 
	if( value == "" || value == null || value == undefined 
		|| (value != null && typeof value == "object"	&& !Object.keys(value).length) ){ 
		return true 
	}else{
	  return false 
	} 
};
```

### SHOW TAG
```js
showTagId : function(tagId){
  let tagIdEvent = document.getElementById(tagId);
  tagIdEvent ? tagIdEvent.style.display = "block" : ''; // inline
},

```

### IS !ACTIVE
```js
if(!selectedTag.classList.contains('active')){
	 console.log('isNotActive');
}
```

### Mouse Click Event
```js
var mouseClick = function (elem) {
	if(!elem) return;
	// Create our event (with options)
	var evt = new MouseEvent('click', {
		bubbles: true,
		cancelable: true,
		view: window
	});
	// If cancelled, don't dispatch our event
	var canceled = !elem.dispatchEvent(evt);
};
```

### Show Hide If Class Exist
```js
var showHideInputIfClassExist =  (inputTag, elementClasses, className) =>{
	if(!elementClasses) return;
	elementClasses.forEach( (item) =>{
		if(item.includes(className)){
			if( inputTag != ''){
				//$(searchIcon).show();   
				document.querySelector('.'+item).style.display = "inline-block";
			}else{
				//$(searchIcon).hide(); 
				document.querySelector('.'+item).style.display = "none";  
			}	
		};    
	});	
}
```

### Use console.table()

### 출처
https://velog.io/@joilnam/%EB%8B%B9%EC%8B%A0%EC%9D%84-%EB%8D%94-%EB%82%98%EC%9D%80-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EB%A1%9C-%EB%A7%8C%EB%93%A4%EC%96%B4-%EC%A4%84-%EC%88%98-%EC%9E%88%EB%8A%94-8%EA%B0%80%EC%A7%80-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8A%B8%EB%A6%AD