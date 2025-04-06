<!DOCTYPE html><html lang="fa">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Toska - طراحی لباس</title>
  <style>
    body {
      margin: 0;
      font-family: "Vazirmatn", sans-serif;
      background: #f7f4f0;
      text-align: center;
    }
    h1 {
      font-size: 3rem;
      margin-top: 2rem;
      color: #4e342e;
    }
    h2 {
      font-size: 2rem;
      color: #6d4c41;
    }
    .toska-logo {
      font-size: 4rem;
      font-weight: bold;
      color: #3e2723;
      margin-bottom: 1rem;
    }
    .page {
      display: none;
    }
    .active {
      display: block;
    }
    button {
      padding: 1rem 2rem;
      font-size: 1.2rem;
      margin: 1rem;
      background-color: #8d6e63;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    canvas {
      width: 100%;
      height: 400px;
      background: #e0dcd8;
      cursor: grab;
    }
  </style>
</head>
<body>
  <div id="page1" class="page active">
    <div class="toska-logo">Toska</div>
    <h1>خوش اومدین</h1>
    <h2>حالا وقتشه لباس مورد علاقتون رو خودتون طراحی کنید!</h2>
    <button onclick="goToPage(2)">شروع طراحی</button>
  </div>  <div id="page2" class="page">
    <h1>نوع لباس رو انتخاب کنید</h1>
    <button onclick="goToPage(3, 'woman')">لباس زنانه</button>
    <button onclick="goToPage(3, 'man')">لباس مردانه</button>
    <button onclick="goToPage(3, 'kid')">لباس بچگانه</button>
    <button onclick="goToPage(3, 'pet')">لباس حیوانات</button>
  </div>  <div id="page3" class="page">
    <h1 id="type-title"></h1>
    <button onclick="loadDesign('tshirt')">تی‌شرت</button>
    <button onclick="loadDesign('pants')">شلوار</button>
    <button onclick="loadDesign('hoodie')">هودی</button>
  </div>  <div id="design-page" class="page">
    <h1>طراحی لباس</h1>
    <canvas id="canvas3d"></canvas>
    <button onclick="uploadImage()">اضافه کردن عکس</button>
    <input type="file" id="file-input" style="display: none;" accept="image/*" />
    <button onclick="goToPage(1)">بازگشت</button>
  </div>  <script>
    let selectedType = '';
    let angle = 0;
    let isDragging = false;
    let lastX = 0;

    function goToPage(num, type = '') {
      document.querySelectorAll(".page").forEach(p => p.classList.remove("active"));
      document.getElementById("page" + num).classList.add("active");
      if (num === 3 && type) {
        selectedType = type;
        let titleMap = {
          woman: "لباس زنانه",
          man: "لباس مردانه",
          kid: "لباس بچگانه",
          pet: "لباس حیوانات"
        };
        document.getElementById("type-title").innerText = titleMap[type];
        if (type === "pet") {
          document.querySelectorAll("#page3 button").forEach((btn, i) => {
            if (i === 0 || i === 2) btn.style.display = 'inline-block';
            else btn.style.display = 'none';
          });
        } else {
          document.querySelectorAll("#page3 button").forEach(btn => btn.style.display = 'inline-block');
        }
      }
    }

    function loadDesign(item) {
      goToPage('design-page');
      drawClothing(item);
    }

    function drawClothing(label) {
      const canvas = document.getElementById("canvas3d");
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.save();
      ctx.translate(canvas.width / 2, canvas.height / 2);
      ctx.rotate(angle);
      ctx.fillStyle = '#a1887f';
      ctx.fillRect(-100, -150, 200, 300);
      ctx.fillStyle = '#3e2723';
      ctx.font = '24px sans-serif';
      ctx.fillText(`نمای چرخان ${label}`, -80, 10);
      ctx.restore();
    }

    const canvas = document.getElementById("canvas3d");
    canvas.addEventListener("mousedown", e => {
      isDragging = true;
      lastX = e.clientX;
    });

    canvas.addEventListener("mouseup", () => {
      isDragging = false;
    });

    canvas.addEventListener("mousemove", e => {
      if (isDragging) {
        const dx = e.clientX - lastX;
        angle += dx * 0.01;
        lastX = e.clientX;
        drawClothing("لباس");
      }
    });

    function uploadImage() {
      document.getElementById("file-input").click();
    }

    document.getElementById("file-input").addEventListener("change", function (e) {
      const file = e.target.files[0];
      const reader = new FileReader();
      reader.onload = function (event) {
        const img = new Image();
        img.onload = function () {
          const canvas = document.getElementById("canvas3d");
          const ctx = canvas.getContext("2d");
          ctx.drawImage(img, 50, 50, 100, 100);
        }
        img.src = event.target.result;
      }
      reader.readAsDataURL(file);
    });
  </script></body>
</html>
