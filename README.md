<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Smart Health AI</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  font-family: Arial;
  background: linear-gradient(135deg,#667eea,#764ba2);
  color:white;
  text-align:center;
  padding:20px;
}
.box{
  background: rgba(255,255,255,0.1);
  padding:20px;
  border-radius:15px;
  margin-top:20px;
}
input, select, button{
  padding:10px;
  margin:8px;
  border-radius:10px;
  border:none;
}
button{
  background:#ff7eb3;
  color:white;
  font-weight:bold;
}
</style>
</head>

<body>

<h1>💪 Smart Health AI</h1>

<div class="box">
<h3>Thông tin cơ thể</h3>
<input id="height" placeholder="Chiều cao (cm)">
<input id="weight" placeholder="Cân nặng (kg)">
<br>

<select id="issue" multiple>
<option value="beophi">Béo phì</option>
<option value="mun">Mụn</option>
<option value="daulung">Đau lưng</option>
<option value="tieudhoa">Tiêu hóa kém</option>
</select>

<br>
<button onclick="analyze()">Phân tích</button>

<p id="result"></p>
</div>

<script>
function analyze(){
  let h = document.getElementById("height").value/100;
  let w = document.getElementById("weight").value;
  let issues = document.getElementById("issue").selectedOptions;

  if(!h || !w){
    document.getElementById("result").innerHTML="Nhập đủ thông tin!";
    return;
  }

  let bmi = w/(h*h);
  let text="BMI: "+bmi.toFixed(1)+"<br>";

  if(bmi<18.5) text+="Gầy<br>";
  else if(bmi<23) text+="Bình thường<br>";
  else if(bmi<25) text+="Thừa cân<br>";
  else text+="Béo phì<br>";

  text+="<br>Gợi
