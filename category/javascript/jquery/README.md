# jQuery

## jQuery 라이브러리
> jQuery 사용에 앞서 jQuery 사용을 위한 라이브러리를 추가해야 한다.  
> google이 hosting 하고 있는 CDN(Content Delivery Network)를 이용한다.  
		
	<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js">

[google libraries](#https://developers.google.com/speed/libraries/devguide "google 라이브러리")  

> min.js는 해당 버전의 최소한의 코드만을 포함하고 있는 버전이다.  
> 이 외에 [jquery.com](#jquery.com "jquery 라이브러리")에서 download도 가능하다.  

## jQuery 문법
> jQuery 문법 작성시 아래와 같은 방법으로 작성할 수 있다.  
		
```javascript
jQuery('div');
$('div');
```

* '$'를 사용하여 코드 작성시 다른 스크립트에서 사용하는 '$'와 충돌하는 현상이 간간히 발생한다.  
* 충돌을 방지하기 위해 내부에서 '$' 매개변수를 사용하는 함수를 생성한다.  
* 충돌에 대한 걱정없이 내부 영역에서 '$'를 사용할 수 있다.  
* 익명함수를 호출하고 jQuery 개체를 전달한다.  
		
```javascript
(function($){
    $('div');
})(jQuery);
```

> head 내에서 jQuery 문법을 사용시 아래와 같이 DOM이 로드되면 실행 하라는 선언을 해야한다.  
> 제일 하단에 jQuery 문법 작성시 문서의 로드가 끝난 뒤 jQuery 문법을 처리하기 때문에 아래와 같이 ready() 메소드는 사용하지 않아도 된다.  
		
```javascript
$(document).ready(function(){
    $('a');
});
```

## jQuery DOM 선택
		
```javascript
$('a').length;  // a 요소 선택 후 count
$('#a').length;  // id 가 a 요소 선택 후 count
$('.a').length;  // class 가 a 요소 선택 후 count
$('.a, .b, .c').length;  // class 가 a, b, c 인 요소 선택 후 count
$('a',$('div')).length;  // div 안에서 a 요소 선택 후 count;
```

### .not()
		
```javascript
// a 요소 중 blogger class가 아닌 것 선택
$('a').not('.blogger');
$('a:not(.blogger)');
```

### .has() - tag 찾을 때 / .contains() - text 찾을 때
		
```javascript
/*
<p>test p tag</p>
<p>test p tag</p>
<p><span>test</span></p>
*/

// p 요소에서 span 요소를 가지고 있는 모든 요소 선택! 즉, 결과값은 1 이다.
$('p:has(span)').length;

// p 요소에서  'p' 라는 텍스트가 있는 p 요소 선택하여 텍스트 색을 빨간색으로 적용해 준다.
$('p:contains("p")').css('color','red');
```

### .animated() / .is()
		
```javascripty
$('div:animated');  // div 요소 중 animation 중인 요소 선택
$('div:not(div:animated)');  // div 요소 중 animation 동작 하지 않는 요소 선택

// animation 중인지 확인
var welAni = $('.animation');
if(welAni.is(':animated')){
    // animation 적용될 경우 true 반환하여 if문 실행
}
```

### :lt() - less than / :gt() - great than
		
```javascript
/*
<table>
  <tr><td>index 0</td></tr>
  <tr><td>index 1</td></tr>
  <tr><td>index 2</td></tr>
  <tr><td>index 3</td></tr>
</table>
*/

$('tr:lt(1)').css('color','red');  // 1보다 작은 index 선택, 즉 index 0 color red
$('tr:gt(2)').css('color','red');  // 2보다 큰 index 선택, 즉 index 3 color red
```

### :even() - 짝수, :odd() - 홀수
		
```javascript
/*
<div>test index 0</div>  // red
<div>test index 1</div>  // blue
<div>test index 2</div>  // red
<div>test index 3</div>  // blue
*/

$('div:even').css('color','red');
$('div:odd').css('color','blue');
```

### 제거 - remove(), detach()
		
```javascript
$('a').remove();  // a 요소 제거
$('a').remove('.remove');  // a 요소 중 remove class만 제거
```

> remove() 메소드는 요소를 제거할 뿐 아니라, 내부적으로 가지고 있는 캐시 테이터 및 모든 이벤트 처리기까지 제거한다.  
> 그러나, wrapper 집합에서는 제거되지 않는며, 계속해서 조작이 가능하다.  


> detach() 메소드는 remove() 메소드와 동일하게 제거 하지만,  
> 해당 요소 데이터(이벤트 등)는 제거하지 않는다.  


### 교체 - replaceWith(), replaceAll()
		
```javascript
/*
<div class="text">jquery</div>
*/

$('.text').replaceWith('<div class="sText">Hello World</div>');
```

* replaceAll() 메소드는 replaceWith() 메소드와 비슷하다.  
		
```javascript
/*
<div>jquery</div>
*/

$('<div class="sText">Hello World</div>').replaceAll('div');
```

### 걸러내거나 찾기 - filter(), find()
> filter() method와 find() method 사소하나 큰 차이가 있으니 주의깊게 숙지 후 사용해야 한다.  
		
```javascript
/*
<ul>
    <li></li>
    <li class="list"></li>
    <li class="list"></li>
    <li></li>
</ul>
*/

$('li').filter('list').length;  // 2, li 요소 중 list 클래스만 filter
$('li').find('list').length;  // 0, li 요소의 자식 요소 중 list 클래스만 find

$('ul').filter('list').length;  // 0, ul 요소 중 list 클래스만 filter
$('ul').find('list').length;  // 2, ul 요소의 자식 요소 중 list 클래스만 find
```

### 속성 제어 - attr()
		
```javascript
$('a').attr('href','http://www.google.co.kr/');  // a 요소 href를 설정
$('a').attr({'href':'http://www.google.co.kr/','title':'google'});  // a 요소 href와 title 설정
$('a').removeAttr('title');  // a 요소 title 제거
$('a').attr('style','color:red');  // a 요소 style 생성
```

### 부모 요소 생성, 부모 요소 제거 - wrap(), wrapAll(), wrapInner(), unwrap()
		
```javascript
/*
<div class="test_div">test</div>
<div class="test_div">test</div>
*/

$('.test_div').wrap('<div class="wrap"></div>');
/* result
<div class="wrap">
    <div class="test_div">test</div>
</div>
<div class="wrap">
    <div class="test_div">test</div>
</div>
*/

$('.test_div').wrapAll('<div id="wrap"></div>');
/* result
<div id="wrap">
    <div class="test_div">test</div>
    <div class="test_div">test</div>
</div>
*/

$('.test_div').wrapInner('<div id="wrap"></div>');
/* result
<div class="test_div">
    <div id="wrap">test</div>
</div>
<div class="test_div">
    <div id="wrap">test</div>
</div>
*/

/*
<div><span>test</span></div>
*/

$('span').unwrap();  // <span>test</span>
```

### 요소 및 text 값 - html(), text()
		
```javascript
/*
<div><span>text</span></div>
*/

$('div').html();  // <span>text</span>
$('div').text();  // text
```

### 요소 복제하기 - clone()
		
```javascript
/*
<ul class="default_ul">
 <li>test_li</li>
 <li>test_li</li>
 <li>test_li</li>
 <li>test_li</li>
</ul>

<ul class="clone_ul">
</ul>
*/

$('.default_ul li').clone().appendTo('.clone_ul');
/* result
<ul class="default_ul">
 <li>test_li</li>
 <li>test_li</li>
 <li>test_li</li>
 <li>test_li</li>
</ul>

<ul class="clone_ul">
 <li>test_li</li>
 <li>test_li</li>
 <li>test_li</li>
 <li>test_li</li>
</ul>
*/
```

### 선택자 연결 - andSelf()
> 두개의 선택자 동시에 선택하고자 할때 andSlef() 메소드를 사용한다.  
> 말로 설명하려니 어려움이....^^;  
		
```javascript
$('a')'.find('span').addClass('andself');  // a 요소 내의 span 요소를 찾아 andself 클래스를 추가해 준다.
$('a')'.find('span').andSelf().addClass('andself');  // a 요소와 span 요소 둘다 andself 클래스를 추가해 준다.
```

### method 종료 - end()
> end() method 사용시 미리 선언된 method들을 제거한다.  
		
```javascript
/*
<p>text</p>
<p class="text2">text2<span>test</span></p>
<p>text3</p>
*/

$('p').filter('.text2').length;  // 1
$('p').filter('.text2').end().length;  // 3
$('p').filter('.text2').find('span').end().end().length;  // 3
```

### 요소 배열로 반환 - get(), toArray(), reverse()
> 요소를 배열로 반환하는 방법을 알아보도록 하자.  
> 요소를 배열로 얻어내기 위한 두가지 방법이 있다.  
> get() 메소드와 toArray() 메소드 이다.  

* get() 메소드 : 숫자를 인자로 사용할 수 있다.  
* toArray() 메소드 : 숫자를 인자로 사용할 수 없다는 것이다.  
		
```javascript
/*
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
*/

$('ul').find('li').get(0);  // <li>1</li> 을 선택할 것이다.
$('ul').find('li').toArray().reverse();  // <li>3</li><li>2</li><li>1</li> 순으로 바뀔 것이다.
```

### iframe 접근
		
```javascript
/*
<iframe id="test"></iframe>
*/

$('#test').contents().find('div').css('background','#000');
```

### 기본 action 취소 - preventDefault()
		
```javascript
$('a').click(function(event){
	event.preventDefault();  // preventDefault() 사용 외에 return false를 사용하여도 된다.
});
```

### 외부 file 불러오기 - load()
		
```javascript
$('div').load('test.html');  // 전체 코드를 가져온다.
$('div').load('test.html .selector2');  // selector2 class로 매치된 부분만 가져온다.
$.getScript('script.js');  // 전체 코드를 가져온다. 
```

