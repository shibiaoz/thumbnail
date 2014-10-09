thumbnail
=========

点击左右切换的缩略图

#html结构
```
    div.thumbnail>div.small_wraper
    div.thumbnail>div.big_wraper
    big_wraper>ul>li>img
```
1. big_wraper必须设置宽度和高度超出不现实
2. big_wraper 相对定位 ,ul采用绝对定位的方式
3. big_wraper>ul 的宽度要设置大于所有的li的宽度之和，这样才才能保证是横着的，而不是竖直的

```
<div class="thumbnail">
		<div class="small_wraper">
			<ul class="clear">
				<li class="li_active"><img src="./images/01.jpg"/></li>
				<li><img src="./images/02.jpg"/></li>
				<li><img src="./images/03.jpg"/></li>
				<li><img src="./images/04.jpg"/></li>
			</ul>
		</div>
		<div class="big_wraper">
			<ul class="clear">
				<li><img src="./images/01.jpg"/></li>
				<li><img src="./images/02.jpg"/></li>
				<li><img src="./images/03.jpg"/></li>
				<li><img src="./images/04.jpg"/></li>
			</ul>
		</div>
	</div>
```
#css
```
        ul,li{list-style: none;}
		.clear{clear: both;}
		.clear:before{content: ".";height: 0;visibility: hidden;clear: both;display: block;}
		.clear:after{content: ".";height: 0;visibility: hidden;clear: both;display: block;}
		li{float: left; cursor: pointer;}
		.li_active img{border: solid 1px red;}
		.small_wraper li{
			width: 128px;
			height: 96px;
			margin-right: 8px;
		}
		.big_wraper{width: 512px;overflow: hidden;position: relative;height: 384px;border: solid 1px gray;}
		/*the ul width must set bigger ,if not ,it will wrap */
		.big_wraper ul{position: absolute;width: 3000px;left: 0px;padding: 0;margin: 0;}
		.big_wraper ul li img{width: 512px;height:384px;display: block;}
```
#js
```
$(function  () {
			var flag = true;
			$('.small_wraper').find('li').on('click',function(){
					//alert( $(this).index() )
					var index = $(this).index();
					var width = $('.big_wraper').find('ul').find('li').eq(0).width();
					$(this).addClass('li_active').siblings().removeClass('li_active');
					if(flag){
						flag = false;
						$('.big_wraper').find('ul').animate({
							left:-(index*width)
						},600,function(){
							flag = true;
						});
					}
			})
		});
```
