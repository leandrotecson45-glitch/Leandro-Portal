```html
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

*{
box-sizing:border-box;
}

body{
font-family:Arial, sans-serif;
margin:0;
padding:15px;
background:url("https://images.unsplash.com/photo-1500530855697-b586d89ba3ee") no-repeat center center fixed;
background-size:cover;
display:flex;
justify-content:center;
align-items:flex-start;
min-height:100vh;
}

.container{
background:rgba(0,0,0,0.85);
padding:20px;
border-radius:12px;
width:100%;
max-width:480px;
color:white;
box-shadow:0 0 25px rgba(0,0,0,0.6);
margin:auto;
}

h2{
text-align:center;
font-size:22px;
margin-bottom:5px;
}

.subtitle{
text-align:center;
font-size:13px;
color:#cbd5f5;
margin-bottom:15px;
}

label{
font-size:13px;
margin-top:10px;
display:block;
color:#e5e7eb;
}

input{
width:100%;
padding:10px;
margin-top:4px;
border-radius:6px;
border:none;
background:#1f2937;
color:white;
font-size:14px;
}

input:focus{
outline:none;
background:#374151;
}

button{
width:100%;
padding:12px;
margin-top:18px;
border:none;
border-radius:8px;
background:#3b82f6;
color:white;
font-size:16px;
cursor:pointer;
}

button:hover{
background:#2563eb;
}

img{
width:100%;
margin-top:10px;
border-radius:8px;
}

.slider-container{
display:flex;
align-items:center;
gap:10px;
margin-top:8px;
}

.slider-container span{
width:50px;
text-align:right;
}

</style>
</head>

<body>

<div class="container" id="loginScreen">

<h2>🔥 LEANDRO POGI LOGIN 🔥</h2>
<p class="subtitle">Enter your credentials</p>

<label>Username</label>
<input id="username">

<label>Password</label>
<input type="password" id="password">

<button onclick="checkLogin()">Login</button>

</div>


<div class="container" id="portalScreen" style="display:none">

<h2>🔥 LEANDRO POGI PORTAL 🔥</h2>
<p class="subtitle">Professional EXIF GeoTag Editor</p>

<label>Upload Photo</label>
<input type="file" id="upload">

<img id="preview">

<label>File Name</label>
<input id="filename">

<label>Camera Make</label>
<input id="make">

<label>Camera Model</label>
<input id="model">

<label>Software</label>
<input id="software">

<label>Date Taken</label>
<input id="date">

<label>Latitude</label>
<input id="lat">

<label>Longitude</label>
<input id="lng">

<label>Image Description</label>
<input id="desc">

<label>Width (px)</label>
<input id="width">

<label>Height (px)</label>
<input id="height">

<label>Output Quality</label>

<div class="slider-container">
<input type="range" id="quality" min="0.1" max="1" step="0.05" value="0.9">
<span id="qualityValue">90%</span>
</div>

<button onclick="downloadImage()">Download Image</button>

</div>


<script src="https://cdn.jsdelivr.net/npm/piexifjs"></script>

<script>

function checkLogin(){

let u=document.getElementById("username").value
let p=document.getElementById("password").value

if(u==="pogisileandro" && p==="sobrangpogitalaga"){
document.getElementById("loginScreen").style.display="none"
document.getElementById("portalScreen").style.display="block"
}
else{
alert("Wrong username or password")
}

}

let imageData=""

const quality=document.getElementById("quality")
const qualityValue=document.getElementById("qualityValue")

quality.addEventListener("input",function(){
qualityValue.innerHTML=Math.round(this.value*100)+"%"
})


document.getElementById("upload").addEventListener("change",function(e){

let file=e.target.files[0]

document.getElementById("filename").value=file.name.replace(/\.[^/.]+$/,"")

let reader=new FileReader()

reader.onload=function(event){

imageData=event.target.result

document.getElementById("preview").src=imageData

let img=new Image()

img.onload=function(){

document.getElementById("width").value=img.width
document.getElementById("height").value=img.height

}

img.src=imageData

}

reader.readAsDataURL(file)

})


function downloadImage(){

let filename=document.getElementById("filename").value
let qualityValue=parseFloat(document.getElementById("quality").value)

let img=new Image()

img.onload=function(){

let canvas=document.createElement("canvas")

canvas.width=img.width
canvas.height=img.height

let ctx=canvas.getContext("2d")

ctx.drawImage(img,0,0)

let compressed=canvas.toDataURL("image/jpeg",qualityValue)

let link=document.createElement("a")

link.href=compressed
link.download=filename+".jpg"

link.click()

}

img.src=imageData

}

</script>

</body>
</html>
```
