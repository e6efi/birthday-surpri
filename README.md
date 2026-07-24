<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🎁 مفاجأة</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{
background:linear-gradient(180deg,#050816,#090f2f,#1d1145);
overflow:hidden;
height:100vh;
display:flex;
justify-content:center;
align-items:center;
color:white;
position:relative;
}

#stars{
position:fixed;
width:100%;
height:100%;
left:0;
top:0;
overflow:hidden;
}

.star{
position:absolute;
width:2px;
height:2px;
background:white;
border-radius:50%;
animation:twinkle 2s infinite alternate;
}

@keyframes twinkle{
from{
opacity:.2;
transform:scale(.6);
}
to{
opacity:1;
transform:scale(1.4);
}
}

.card{
position:relative;
z-index:5;
text-align:center;
padding:40px;
background:rgba(255,255,255,.08);
backdrop-filter:blur(10px);
border-radius:25px;
box-shadow:0 0 40px rgba(255,255,255,.15);
}

h1{
font-size:42px;
margin-bottom:20px;
animation:float 3s infinite ease-in-out;
}

p{
font-size:20px;
opacity:.9;
margin-bottom:30px;
}

button{
padding:18px 40px;
font-size:22px;
border:none;
border-radius:50px;
cursor:pointer;
background:#ff4d88;
color:white;
transition:.3s;
}

button:hover{
transform:scale(1.1);
background:#ff2f74;
}

@keyframes float{
0%{transform:translateY(0);}
50%{transform:translateY(-10px);}
100%{transform:translateY(0);}
}
</style>
</head>

<body>

<div id="stars"></div>

<div class="card">
<h1>🎁 مفاجأة بانتظارك</h1>

<p>اضغط الزر لتبدأ الرحلة...</p>

<button id="start">
ابدأ
</button>

</div>

<script>

for(let i=0;i<220;i++){

let s=document.createElement("div");

s.className="star";

s.style.left=Math.random()*100+"vw";

s.style.top=Math.random()*100+"vh";

s.style.animationDelay=Math.random()*3+"s";

document.getElementById("stars").appendChild(s);

}

document.getElementById("start").onclick=function(){

alert("🚀 المرحلة الثانية قادمة...");

}

</script>

</body>
</html>
