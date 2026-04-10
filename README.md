<!DOCTYPE html><html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Health AI</title><style>
body{
    font-family: Arial;
    margin:0;
    background: linear-gradient(135deg,#4facfe,#00f2fe);
}

.container{
    padding:20px;
}

.card{
    background:white;
    border-radius:20px;
    padding:20px;
    box-shadow:0 10px 25px rgba(0,0,0,0.2);
}

h2{
    text-align:center;
    color:white;
}

input, select{
    width:100%;
    padding:12px;
    margin-top:10px;
    border-radius:10px;
    border:none;
    background:#f1f1f1;
}

label{
    display:block;
    margin-top:6px;
}

button{
    width:100%;
    padding:15px;
    margin-top:15px;
    border:none;
    border-radius:12px;
    background:#4facfe;
    color:white;
    font-weight:bold;
}

.result{
    margin-top:20px;
    background:#f9f9f9;
    padding:15px;
    border-radius:15px;
    line-height:1.6;
}

.notify{
    position:fixed;
    bottom:20px;
    left:50%;
    transform:translateX(-50%);
    background:#333;
    color:white;
    padding:10px 20px;
    border-radius:20px;
    display:none;
}
</style></head><body><h2>🌿 Smart Health AI</h2><div class="container">
<div class="card"><h3>Thông tin</h3>
<input id="weight" placeholder="Cân nặng (kg)">
<input id="height" placeholder="Chiều cao (cm)"><h3>Vấn đề</h3><label><input type="checkbox" value="Béo phì"> Béo phì</label>
<label><input type="checkbox" value="Giảm mỡ nhẹ"> Giảm mỡ nhẹ</label>
<label><input type="checkbox" value="Mỡ nội tạng"> Mỡ nội tạng</label>
<label><input type="checkbox" value="Kháng insulin"> Kháng insulin</label>

<label><input type="checkbox" value="Mụn"> Mụn</label>
<label><input type="checkbox" value="Da dầu"> Da dầu</label>
<label><input type="checkbox" value="Lão hóa"> Lão hóa</label>

<label><input type="checkbox" value="Đau lưng"> Đau lưng</label>
<label><input type="checkbox" value="Vai gáy"> Vai gáy</label>

<label><input type="checkbox" value="Tiêu hóa kém"> Tiêu hóa kém</label>
<label><input type="checkbox" value="Stress"> Stress</label>
<label><input type="checkbox" value="Mất ngủ"> Mất ngủ</label>

<label><input type="checkbox" value="Bận rộn"> Bận rộn</label>

<h3>Cường độ</h3>
<select id="level">
<option>Nhẹ</option>
<option>Trung bình</option>
<option>Nặng</option>
</select><button onclick="generate()">✨ Tạo kế hoạch</button>

<div class="result" id="result"></div></div>
</div><div class="notify" id="notify"></div><script>

function generate(){

let weight = parseFloat(document.getElementById("weight").value);
let height_cm = parseFloat(document.getElementById("height").value);

let problems = Array.from(document.querySelectorAll("input[type=checkbox]:checked"))
.map(e => e.value);

let level = document.getElementById("level").value;

let result = "<b>📊 KẾ HOẠCH</b><br><br>";

// kiểm tra nhập
if(!weight || !height_cm){
    result += "⚠️ Vui lòng nhập đủ thông tin";
    document.getElementById("result").innerHTML = result;
    return;
}

// đổi cm -> m
let height = height_cm / 100;

// BMI
let bmi = weight / (height * height);

result += "📈 BMI: " + bmi.toFixed(1) + "<br>";

// phân loại
if(bmi < 18.5){
    result += "⚠️ Gầy<br><br>";
}
else if(bmi < 25){
    result += "👍 Bình thường<br><br>";
}
else if(bmi < 30){
    result += "⚠️ Thừa cân<br><br>";
}
else{
    result += "🚨 Béo phì<br><br>";
}

// gợi ý
result += "<b>🎯 Gợi ý:</b><br>";

if(problems.includes("Béo phì") || bmi >= 30){
    result += "- Cardio + giảm đường + trà gừng<br>";
}

if(problems.includes("Giảm mỡ nhẹ")){
    result += "- Đi bộ 30p + ăn nhẹ<br>";
}

if(problems.includes("Mỡ nội tạng")){
    result += "- Giảm đường + trà lá sen<br>";
}

if(problems.includes("Kháng insulin")){
    result += "- Giảm tinh bột + đi bộ sau ăn<br>";
}

if(problems.includes("Mụn")){
    result += "- Trà hoa cúc + nha đam<br>";
}

if(problems.includes("Da dầu")){
    result += "- Uống nước nhiều + hạn chế dầu<br>";
}

if(problems.includes("Lão hóa")){
    result += "- Trà xanh + ngủ đủ<br>";
}

if(problems.includes("Đau lưng")){
    result += "- Giãn cơ + yoga<br>";
}

if(problems.includes("Vai gáy")){
    result += "- Giãn cổ + nghỉ ngơi<br>";
}

if(problems.includes("Tiêu hóa kém")){
    result += "- Sữa chua + ăn nhẹ<br>";
}

if(problems.includes("Stress")){
    result += "- Thiền + đi bộ<br>";
}

if(problems.includes("Mất ngủ")){
    result += "- Trà hoa cúc + ngủ sớm<br>";
}

if(problems.includes("Bận rộn")){
    result += "- Tập nhanh 15p/ngày<br>";
}

// cường độ
result += "<br><b>⏱ Thời gian:</b><br>";

if(level=="Nhẹ"){
    result += "20–30 phút/ngày";
}
else if(level=="Trung bình"){
    result += "40–50 phút/ngày";
}
else{
    result += "60 phút+/ngày";
}

result += "<br><br>💚 Kiên trì mỗi ngày!";

document.getElementById("result").innerHTML = result;

showNotify("✅ Đã tạo kế hoạch!");
}

// notify
function showNotify(text){
let box = document.getElementById("notify");
box.innerText = text;
box.style.display="block";

setTimeout(()=>{
box.style.display="none";
},3000);
}

// reminder
setInterval(()=>{
showNotify("💧 Nhớ uống nước!");
},60000);

</script></body>
</html><!DOCTYPE html><html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Health AI</title><style>
body{
    font-family: Arial;
    margin:0;
    background: linear-gradient(135deg,#4facfe,#00f2fe);
}

.container{
    padding:20px;
}

.card{
    background:white;
    border-radius:20px;
    padding:20px;
    box-shadow:0 10px 25px rgba(0,0,0,0.2);
}

h2{
    text-align:center;
    color:white;
}

input, select{
    width:100%;
    padding:12px;
    margin-top:10px;
    border-radius:10px;
    border:none;
    background:#f1f1f1;
}

label{
    display:block;
    margin-top:6px;
}

button{
    width:100%;
    padding:15px;
    margin-top:15px;
    border:none;
    border-radius:12px;
    background:#4facfe;
    color:white;
    font-weight:bold;
}

.result{
    margin-top:20px;
    background:#f9f9f9;
    padding:15px;
    border-radius:15px;
    line-height:1.6;
}

.notify{
    position:fixed;
    bottom:20px;
    left:50%;
    transform:translateX(-50%);
    background:#333;
    color:white;
    padding:10px 20px;
    border-radius:20px;
    display:none;
}
</style></head><body><h2>🌿 Smart Health AI</h2><div class="container">
<div class="card"><h3>Thông tin</h3>
<input id="weight" placeholder="Cân nặng (kg)">
<input id="height" placeholder="Chiều cao (cm)"><h3>Vấn đề</h3><label><input type="checkbox" value="Béo phì"> Béo phì</label>
<label><input type="checkbox" value="Giảm mỡ nhẹ"> Giảm mỡ nhẹ</label>
<label><input type="checkbox" value="Mỡ nội tạng"> Mỡ nội tạng</label>
<label><input type="checkbox" value="Kháng insulin"> Kháng insulin</label>

<label><input type="checkbox" value="Mụn"> Mụn</label>
<label><input type="checkbox" value="Da dầu"> Da dầu</label>
<label><input type="checkbox" value="Lão hóa"> Lão hóa</label>

<label><input type="checkbox" value="Đau lưng"> Đau lưng</label>
<label><input type="checkbox" value="Vai gáy"> Vai gáy</label>

<label><input type="checkbox" value="Tiêu hóa kém"> Tiêu hóa kém</label>
<label><input type="checkbox" value="Stress"> Stress</label>
<label><input type="checkbox" value="Mất ngủ"> Mất ngủ</label>

<label><input type="checkbox" value="Bận rộn"> Bận rộn</label>

<h3>Cường độ</h3>
<select id="level">
<option>Nhẹ</option>
<option>Trung bình</option>
<option>Nặng</option>
</select><button onclick="generate()">✨ Tạo kế hoạch</button>

<div class="result" id="result"></div></div>
</div><div class="notify" id="notify"></div><script>

function generate(){

let weight = parseFloat(document.getElementById("weight").value);
let height_cm = parseFloat(document.getElementById("height").value);

let problems = Array.from(document.querySelectorAll("input[type=checkbox]:checked"))
.map(e => e.value);

let level = document.getElementById("level").value;

let result = "<b>📊 KẾ HOẠCH</b><br><br>";

// kiểm tra nhập
if(!weight || !height_cm){
    result += "⚠️ Vui lòng nhập đủ thông tin";
    document.getElementById("result").innerHTML = result;
    return;
}

// đổi cm -> m
let height = height_cm / 100;

// BMI
let bmi = weight / (height * height);

result += "📈 BMI: " + bmi.toFixed(1) + "<br>";

// phân loại
if(bmi < 18.5){
    result += "⚠️ Gầy<br><br>";
}
else if(bmi < 25){
    result += "👍 Bình thường<br><br>";
}
else if(bmi < 30){
    result += "⚠️ Thừa cân<br><br>";
}
else{
    result += "🚨 Béo phì<br><br>";
}

// gợi ý
result += "<b>🎯 Gợi ý:</b><br>";

if(problems.includes("Béo phì") || bmi >= 30){
    result += "- Cardio + giảm đường + trà gừng<br>";
}

if(problems.includes("Giảm mỡ nhẹ")){
    result += "- Đi bộ 30p + ăn nhẹ<br>";
}

if(problems.includes("Mỡ nội tạng")){
    result += "- Giảm đường + trà lá sen<br>";
}

if(problems.includes("Kháng insulin")){
    result += "- Giảm tinh bột + đi bộ sau ăn<br>";
}

if(problems.includes("Mụn")){
    result += "- Trà hoa cúc + nha đam<br>";
}

if(problems.includes("Da dầu")){
    result += "- Uống nước nhiều + hạn chế dầu<br>";
}

if(problems.includes("Lão hóa")){
    result += "- Trà xanh + ngủ đủ<br>";
}

if(problems.includes("Đau lưng")){
    result += "- Giãn cơ + yoga<br>";
}

if(problems.includes("Vai gáy")){
    result += "- Giãn cổ + nghỉ ngơi<br>";
}

if(problems.includes("Tiêu hóa kém")){
    result += "- Sữa chua + ăn nhẹ<br>";
}

if(problems.includes("Stress")){
    result += "- Thiền + đi bộ<br>";
}

if(problems.includes("Mất ngủ")){
    result += "- Trà hoa cúc + ngủ sớm<br>";
}

if(problems.includes("Bận rộn")){
    result += "- Tập nhanh 15p/ngày<br>";
}

// cường độ
result += "<br><b>⏱ Thời gian:</b><br>";

if(level=="Nhẹ"){
    result += "20–30 phút/ngày";
}
else if(level=="Trung bình"){
    result += "40–50 phút/ngày";
}
else{
    result += "60 phút+/ngày";
}

result += "<br><br>💚 Kiên trì mỗi ngày!";

document.getElementById("result").innerHTML = result;

showNotify("✅ Đã tạo kế hoạch!");
}

// notify
function showNotify(text){
let box = document.getElementById("notify");
box.innerText = text;
box.style.display="block";

setTimeout(()=>{
box.style.display="none";
},3000);
}

// reminder
setInterval(()=>{
showNotify("💧 Nhớ uống nước!");
},60000);

</script></body>
</html>
