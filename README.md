<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Smart Health AI</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  font-family: Arial;
  background: linear-gradient(135deg,#00c6ff,#0072ff);
  color:white;
  text-align:center;
  padding:20px;
}
.box{
  background: rgba(255,255,255,0.15);
  padding:20px;
  border-radius:20px;
  margin-top:20px;
}
input, select, button{
  padding:10px;
  margin:10px;
  border-radius:10px;
  border:none;
}
button{
  background:#ff4081;
  color:white;
  font-weight:bold;
}
</style>
</head>

<body>

<h1>💪 Smart Health AI</h1>

<div class="box">
<h3>Nhập thông tin</h3>

<input id="height" type="number" placeholder="Chiều cao (cm)">
<input id="weight" type="number" placeholder="Cân nặng (kg)">

<br>

<select id="issue">
<option value="">-- Chọn vấn đề --</option>
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
  let h = document.getElementById("height").value;
  let w = document.getElementById("weight").value;
  let issue = document.getElementById("issue").value;

  if(h=="" || w==""){
    document.getElementById("result").innerHTML="❌ Nhập đủ chiều cao và cân nặng!";
    return;
  }

  h = h/100;
  let bmi = w/(h*h);
  let text = "📊 BMI: " + bmi.toFixed(1) + "<br>";

  if(bmi < 18.5) text += "➡️ Gầy<br>";
  else if(bmi < 23) text += "➡️ Bình thường<br>";
  else if(bmi < 25) text += "➡️ Thừa cân<br>";
  else text += "➡️ Béo phì<br>";

  text += "<br>💡 Gợi ý:<br>";

  if(issue=="beophi"){
    text += "- Đi bộ 30 phút mỗi ngày<br>- Uống trà gừng<br>";
  }
  else if(issue=="mun"){
    text += "- Uống trà hoa cúc<br>- Hạn chế đồ dầu<br>";
  }
  else if(issue=="daulung"){
    text += "- Tập plank nhẹ<br>- Giãn cơ 10 phút<br>";
  }
  else if(issue=="tieudhoa"){
    text += "- Uống trà gừng<br>- Ăn chậm nhai kỹ<br>";
  }
  else{
    text += "- Ăn uống lành mạnh + tập thể dục<br>";
  }

  document.getElementById("result").innerHTML = text;
}
</script>

</body>
</html> 
	
