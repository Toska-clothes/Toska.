<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <title>طراحی لباس | Toska</title>
  <style>
    body {
      background-color: #f9f5f0;
      font-family: sans-serif;
      direction: rtl;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #5f3d2b;
    }
    canvas {
      border: 2px dashed #ccc;
      margin: 20px auto;
      display: block;
    }
    input, button, label {
      margin: 10px;
      padding: 10px;
      font-size: 1em;
    }
    .controls {
      margin-top: 20px;
    }
    #designArea {
      display: none;
    }
  </style>
</head>
<body>
  <h1>توسکا</h1>
  <p>خوش اومدین! حالا وقتشه لباس مورد علاقتون رو خودتون طراحی کنید!</p>

  <button onclick="startDesign()">شروع طراحی</button>

  <div id="designArea">
    <canvas id="designCanvas" width="400" height="500"></canvas>

    <div class="controls">
      <button onclick="changeColor()">تغییر رنگ پارچه</button>
      <br>
      <label>افزودن متن:
        <input type="text" id="textInput" placeholder="متن مورد نظر">
        <button onclick="addText()">افزودن</button>
      </label>
      <br>
      <label>افزودن تصویر:
        <input type="file" id="imageInput" accept="image/*">
      </label>
      <br>
      <label>تصویر آماده:
        <button onclick="useSampleImage()">استفاده از تصویر گربه</button>
      </label>
    </div>
  </div>

  <script>
    const canvas = document.getElementById("designCanvas");
    const ctx = canvas.getContext("2d");
    let currentColor = "#d2b48c";
    let addedText = null;
    let addedImage = null;
    let imageX = 150, imageY = 200, imageW = 100, imageH = 100;
    let textX = 170, textY = 350;
    let draggingImage = false, draggingText = false;

    function startDesign() {
      document.querySelector("button").style.display = "none";
      document.getElementById("designArea").style.display = "block";
      drawHoodie();
    }

    function drawHoodie() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = currentColor;
      ctx.fillRect(120, 150, 160, 220);
      ctx.fillRect(80, 150, 40, 120);
      ctx.fillRect(280, 150, 40, 120);

      if (addedText) {
        ctx.font = "20px Tahoma";
        ctx.fillStyle = "black";
        ctx.fillText(addedText, textX, textY);
        ctx.strokeRect(textX - 5, textY - 20, ctx.measureText(addedText).width + 10, 30);
      }

      if (addedImage) {
        ctx.drawImage(addedImage, imageX, imageY, imageW, imageH);
        ctx.strokeStyle = "#999";
        ctx.strokeRect(imageX, imageY, imageW, imageH);
      }
    }

    function changeColor() {
      const colors = ["#d2b48c", "#6b4e3d", "#fff", "#8b5e3c"];
      const index = colors.indexOf(currentColor);
      currentColor = colors[(index + 1) % colors.length];
      drawHoodie();
    }

    function addText() {
      addedText = document.getElementById("textInput").value;
      drawHoodie();
    }

    function useSampleImage() {
      const img = new Image();
      img.src = "https://cdn-icons-png.flaticon.com/512/616/616408.png";
      img.onload = () => {
        addedImage = img;
        drawHoodie();
      };
    }

    document.getElementById("imageInput").addEventListener("change", function(e) {
      const reader = new FileReader();
      reader.onload = function(event) {
        const img = new Image();
        img.src = event.target.result;
        img.onload = () => {
          addedImage = img;
          drawHoodie();
        };
      };
      reader.readAsDataURL(e.target.files[0]);
    });

    canvas.addEventListener("mousedown", function(e) {
      const rect = canvas.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      if (addedImage && x > imageX && x < imageX + imageW && y > imageY && y < imageY + imageH) {
        draggingImage = true;
      }
      if (addedText) {
        const textWidth = ctx.measureText(addedText).width;
        if (x > textX && x < textX + textWidth && y > textY - 20 && y < textY + 10) {
          draggingText = true;
        }
      }
    });

    canvas.addEventListener("mousemove", function(e) {
      if (!draggingImage && !draggingText) return;
      const rect = canvas.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      if (draggingImage) {
        imageX = x - imageW / 2;
        imageY = y - imageH / 2;
      }
      if (draggingText) {
        textX = x;
        textY = y;
      }
      drawHoodie();
    });

    canvas.addEventListener("mouseup", function() {
      draggingImage = false;
      draggingText = false;
    });
  </script>
</body>
</html>
