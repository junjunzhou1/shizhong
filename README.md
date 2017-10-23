<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
	<style type="text/css">
		*{
			margin: 0;
			padding: 0;
		}
		body{
			font-family: '微软雅黑';
		}
		.clock{
			width: 200px;
			height: 200px;
			border-radius: 100%;
			background: #000;
			margin: 50px auto;
			position: relative;
		}
		.clock .line-min li,.clock .line-hour li{
			top: 50%;
			left: 50%;
			position: absolute;
			list-style: none;
			background: #fff;
			transform-origin: left center;
			
		}
		.clock .line-hour li{
			width: 10px;
			height: 2px;
		}
		.clock .line-min li{
			width: 5px;
			height: 2px;
		}
		.clock .number{
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%,-50%);
			width: 150px;
			height: 150px;
		}
		.clock .number li{
			list-style: none;
			position: absolute;
			color: #fff;
			transform: translate(-50%,-50%);
		}
		.pointer li{
			position: absolute;
			top: 50%;
			left: 50%;
			transform-origin: left center;
			background: #fff;
			margin-top: -1px;
		}
		.pointer li.circle{
			width: 10px;
			height: 10px;
			border-radius: 100%;
			margin-top: -5px;
			margin-left: -5px;
		}
		.pointer li.hour{
			width: 45px;
			height: 3px;
		}
		.pointer li.min{
			width: 60px;
			height: 2px;
		}
		.pointer li.sec{
			width: 80px;
			height: 1px;
		}
	</style>
</head>
<body>
<div class="clock">
	<ul class="line-min"></ul>
	<ul class="line-hour"></ul>
	<ol class="number"></ol>
	<ul class="pointer">
		<li class="circle"></li>
		<li class="hour"></li>
		<li class="min"></li>
		<li class="sec"></li>
	</ul>
</div>
</body>
<script type="text/javascript" src="http://s0.qhimg.com/lib/jquery/183.js"></script>
	<script type="text/javascript">
		$(function(){
			function drawLines(wrap,total,translateX){
				var gap=360/total;
				var strhtml='';
				for(var i=0;i<total;i++){
					strhtml+='<li style="transform:rotate('+(i*gap)+'deg) translate('+translateX+'px,-50%)"></li>';
				}
				wrap.html(strhtml);
			}


			function drawNumbers(wrap){
				var radius=wrap.width()/2;
				var strhtml='';
				for(var i=1;i<=12;i++){
					var myAngle=(i-3)/6*Math.PI;

					var myX=radius+radius*Math.cos(myAngle),
					myY=radius+radius*Math.sin(myAngle);

					strhtml+='<li style="left:'+myX+'px;top:'+myY+'px">'+i+'</li>';
				}
				wrap.html(strhtml);
			}


			function move(){
				var domHour=$(".hour"),
				domMin=$(".min"),
				domSec=$(".sec");
				function tick(){
					var now=new Date(),
					hour=now.getHours(),
					min=now.getMinutes(),
					sec=now.getSeconds();

					var secAngle=sec*6-90,
					minAngle=min*6+sec*0.1-90,
					hourAngle=hour*30+min*0.5-90;

					domSec.css('transform','rotate('+secAngle+'deg)');
					domMin.css('transform','rotate('+minAngle+'deg)');
					domHour.css('transform','rotate('+hourAngle+'deg)');
				}
				setInterval(tick,1000)
				tick();
			}

			function init(){
				drawLines($('.line-min'),60,85);
				drawLines($('.line-hour'),12,80);
				drawNumbers($('.number'));
				move();
			}
			init();
		});
	</script>
</html>
