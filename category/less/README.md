#less

정의 방법
> `<link rel="stylesheet/less" type="text/css" href="styles.less">`  
	`<script src="less.js" type="text/javascript"></script>`  
	

1. [변수](#var)  
1. [믹스인(Mixins)](#mixins)  
1. [충첩 또는 포함](#overlap)  
1. [함수와 연산](#function)

##<a href="#" name="var">변수를 사용하여 활용 가능하다.</a>
		
	@color:red;

	section{
		color:@color;
	}

	h1{
		color:@color;
	}

	// @arguments 변수 사용법
	.box-shadow(@x:0, @y:0, @blur:1px, @color:#000){
		box-shadow:@arguments;
	}
	.box-shadow:(2px, 5px);

##<a href="#" name="mixins">믹스인(Mixins)</a>  
하나의 클래스에서 하나의 속성을 지정하여 활용 가능한 방식이다.
		
	.borders(@radius:5px){
		border-radius:@radius;
		-webkit-border-radius:@radius;
		-moz-border-radius:@radius;
	}

	header{
		.borders;
	}

	footer{
		.borders(4px);
	}

##<a href="#" name="overlap">중첩 또는 포함</a>
선택자 안에서 또 다른 선택자를 포함할 수 있다.
		
	// less
	#header{
		h1{
			font-size:12px;
			color:red;
		}
		h1:hover{
			color:green;
		}
	}

	// css
	#header h1{}
	#header h1:hover{}

##<a href="#" name="function">함수와 연산</a>
		
	@borders:4px;
	@baseColor:#111;
	@red:#842210;

	#header{
		color:@baseColor * 3;
		border-left:@borders;
		border-right:@borders * 2;
	}
