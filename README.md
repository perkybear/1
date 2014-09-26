<!DOCTYPE HTML>
<html lang="en-US">
<head>
    <meta charset="UTF-8">
    <title>html5 canvas打造时钟</title>
    <style type="text/css">
        body,h3{margin:0;text-align:center}
        h3{
            padding:0;
            text-align:center;
            background:#333;
            font-size:1.5em;
            color:#fff;
            line-height:2em;
            text-shadow:0 0 10px rgba(0, 39, 245, 0.65);
        }
        #canvas{
            margin:20px 0;
            border:1px solid #bbb;
            background:#D6D5D5;
        }
        p{text-align:center;color:#bbb}
    </style>
</head>
<body>
<h3>html5 canvas打造时钟</h3>
<canvas id="canvas" width="600" height="600">
    您的浏览器不支持canvas,请使用高级浏览器。
</canvas>
<p>似水流年，且行且珍惜！</p>
<script type="text/javascript">
    var canvas=document.getElementById('canvas');
    if(canvas.getContext){
        var context=canvas.getContext('2d');
        drawClock(context);
        setInterval(function(){drawClock(context)},1000);
    }



    function  drawClock(canvas){
        var x=300,   //钟表圆心坐标
                y=300
        r=200;	 //钟表半径

        //清除画布
        canvas.clearRect(0,0,canvas.width,canvas.height);


        //修饰部分  即，建立一个白色的画布
        canvas.beginPath();
        canvas.moveTo(x,y);
        canvas.arc(x,y,r,0,360,false);
        canvas.closePath();
        canvas.fillStyle='#fff';
        canvas.fill();

        //镶嵌时钟数字




        var date=new Date(),//创建日期对象
                hours=date.getHours(),
                minutes=date.getMinutes(),
                seconds=date.getSeconds();


        var hoursValue=(-90 + hours*30+minutes/2)*Math.PI/180,
                minutesValue=(-90+minutes*6)*Math.PI/180,
                secondsValue=(-90+seconds*6)*Math.PI/180;


        canvas.beginPath();
        for(var i=0;i<60;i++){
            canvas.moveTo(x,y);
            canvas.arc(x,y,r,6*i*Math.PI/180,6*(i+1)*Math.PI/180,false);
        }


        canvas.closePath();
        canvas.stroke();

        canvas.beginPath();
        canvas.moveTo(x,y);
        canvas.fillStyle='#fff';

        canvas.arc(x,y,r*19/20,0,2*Math.PI,false);

        canvas.closePath();
        canvas.fill();

        canvas.beginPath();
        canvas.lineWidth=3;

        for(var i=0;i<12;i++){
            canvas.moveTo(x,y);

            canvas.arc(x,y,r,30*i*Math.PI/180,30*(i+1)*Math.PI/180,false)
        }
        canvas.closePath();
        canvas.stroke();

        canvas.beginPath();
        canvas.arc(x,y,r*18/20,0,2*Math.PI,false);
        canvas.closePath();
        canvas.fillStyle='#fff';
        canvas.fill();
        canvas.font="bold 16px Arial";
        canvas.textAlign='center';
        canvas.textBaseLine='middle';
        canvas.fillStyle='red';
        canvas.fillText('12',x,y-165,200);
        canvas.fillText('6',x,y+165,200);
        canvas.fillText('3',x+165,y+5,200);
        canvas.fillText('9',x-165,y+5,200);
        dyear=date.getFullYear(),
                dmonth=date.getMonth()+1,
                dDate=date.getDate(),
                weeks=date.getDay();
        canvas.fillText(dyear+'-'+dmonth+'-'+dDate+' '+dateWeek(weeks)+' '+hours+':'+toDouble(minutes)+':'+toDouble(seconds),x,y+60,200);


        canvas.lineWidth=1;
        canvas.beginPath();
        canvas.moveTo(x,y);
        canvas.arc(x,y,r*10/20,hoursValue,hoursValue,false);
        canvas.closePath();
        canvas.stroke();


        canvas.lineWidth=1;
        canvas.beginPath();
        canvas.moveTo(x,y);
        canvas.arc(x,y,r*14/20,minutesValue,minutesValue,false);
        canvas.closePath();
        canvas.stroke();

//
//        canvas.lineWidth=1;
//        canvas.beginPath();
//        canvas.moveTo(x,y);
//        canvas.arc(x,y,r*16/20,secondsValue,secondsValue,false);
//        canvas.closePath();
//        canvas.stroke();

        canvas.lineWidth=1;

        canvas.beginPath();
        canvas.moveTo(x,y);
        canvas.arc(x,y,r*18/20,secondsValue,secondsValue,false);
        canvas.closePath();
        canvas.stroke();
    }

    function toDouble(num){
        num>=10 ? num=''+num : num='0'+num ;
        return num;
    }

    function dateWeek(data){
        switch(data){
            case 1:
                return '星期一';
                break;
            case 2:
                return '星期二';
                break;
            case 3:
                return '星期三';
                break;
            case 4:
                return '星期四';
                break;
            case 5:
                return '星期五';
                break;
            case 6:
                return '星期六';
                break;
            case 0:
                return '星期日';
                break;
        }
    }
</script>
</body>
</html>
