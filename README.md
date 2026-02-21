[idex.html](https://github.com/user-attachments/files/25455683/idex.html)<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BMI Calculator Pro</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #4facfe, #00f2fe);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    background: white;
    padding: 30px;
    border-radius: 15px;
    width: 350px;
    text-align: center;
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

h2 {
    margin-bottom: 20px;
}

input {
    width: 90%;
    padding: 8px;
    margin: 8px 0;
    border-radius: 8px;
    border: 1px solid #ccc;
}

button {
    padding: 10px 20px;
    background: #4facfe;
    border: none;
    color: white;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #00c6ff;
    transform: scale(1.05);
}

.result {
    margin-top: 15px;
    font-weight: bold;
    font-size: 18px;
}

.bar {
    height: 20px;
    background: #eee;
    border-radius: 10px;
    margin-top: 10px;
    overflow: hidden;
}

.fill {
    height: 100%;
    width: 0%;
    background: green;
    transition: 0.5s;
}

table {
    margin-top: 20px;
    width: 100%;
    font-size: 13px;
    border-collapse: collapse;
}

td {
    border: 1px solid #ccc;
    padding: 5px;
}
</style>
</head>

<body>

<div class="container">
    <h2>ỨNG DỤNG TÍNH BMI</h2>

    <input type="number" id="weight" placeholder="Cân nặng (kg)">
    <input type="number" id="height" placeholder="Chiều cao (m)">

    <button onclick="tinhBMI()">Tính BMI</button>

    <div class="result" id="result"></div>

    <div class="bar">
        <div class="fill" id="fill"></div>
    </div>

    <table>
        <tr><td><18.5</td><td>Gầy</td></tr>
        <tr><td>18.5 - 24.9</td><td>Bình thường</td></tr>
        <tr><td>25 - 29.9</td><td>Thừa cân</td></tr>
        <tr><td>>=30</td><td>Béo phì</td></tr>
    </table>
</div>

<script>
function tinhBMI() {
    let w = parseFloat(document.getElementById("weight").value);
    let h = parseFloat(document.getElementById("height").value);
    let result = document.getElementById("result");
    let fill = document.getElementById("fill");

    if (w <= 0 || h <= 0 || isNaN(w) || isNaN(h)) {
        result.innerHTML = "Dữ liệu không hợp lệ!";
        result.style.color = "red";
        fill.style.width = "0%";
        return;
    }

    let bmi = w / (h * h);
    bmi = bmi.toFixed(2);

    let message = "";
    let color = "";
    let widthPercent = Math.min(bmi * 3, 100);

    if (bmi < 18.5) {
        message = "Gầy";
        color = "blue";
    }
    else if (bmi < 25) {
        message = "Bình thường";
        color = "green";
    }
    else if (bmi < 30) {
        message = "Thừa cân";
        color = "orange";
    }
    else {
        message = "Béo phì";
        color = "red";
    }

    result.innerHTML = "BMI = " + bmi + " → " + message;
    result.style.color = color;

    fill.style.width = widthPercent + "%";
    fill.style.background = color;
}
</script>

</body>
</html>
{
  "name": "BMI Calculator Pro",
  "short_name": "BMI App",
  "start_url": "index.html",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#4facfe",
  "icons": [
    {
      "src": "icon.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
[service-worker.js](https://github.com/user-attachments/files/25455685/service-worker.js)
}
self.addEventListener("install", function(event) {
  event.waitUntil(
    caches.open("bmi-cache").then(function(cache) {
      return cache.addAll([
        "index.html",
        "manifest.json",
        "icon.png"
      ]);
    })
  );
});

self.addEventListener("fetch", function(event) {
  event.respondWith(
    caches.match(event.request)
  );
});
![z7532580459153_f2f2a029ac4b4f11a549f1ccb48329df](https://github.com/user-attachments/assets/f1e49cd0-db90-4b00-8e32-851f65848d10)
