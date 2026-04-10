<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Smart Health AI</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial;
      background: linear-gradient(135deg, #4facfe, #00f2fe);
      color: white;
      text-align: center;
      padding: 20px;
    }
    .box {
      background: rgba(255,255,255,0.1);
      padding: 20px;
      border-radius: 15px;
      margin-top: 20px;
    }
    input, button {
      padding: 10px;
      margin: 10px;
      border-radius: 10px;
      border: none;
    }
    button {
      background: #ff7eb3;
      color: white;
      font-weight: bold;
    }
  </style>
</head>

<body>

<h1>💪 Smart Health AI</h1>

<div class="box">
  <h3>Tính BMI</h3>
  <input id="height" placeholder="Chiều cao (cm)">
  <input id="weight" placeholder="Cân nặng (kg)">
  <br>
  <button onclick="calcBMI()">Tính</button>
  <p id="result"></p>
</div>

<script>
function calcBMI(){
  let h = document.getElementById("height").value / 100;
  let w = document.getElementById("weight").value;
  
  if(!h || !w){
    document.getElementById("result").innerHTML = "Nhập đầy đủ!";
    return;
  }

  let bmi = w / (h*h);
  let text = "";

  if(bmi < 18.5) text = "Gầy";
  else if(bmi < 23) text = "Bình thường";
  else if(bmi < 25) text = "Thừa cân";
  else text = "Béo phì";

  document.getElementById("result").innerHTML =
    "BMI: " + bmi.toFixed(1) + " → " + text;
}
</script>

</body>
</html>
