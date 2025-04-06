<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>دسته‌بندی‌ها | توسکا</title>
    <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Vazirmatn', sans-serif;
            text-align: center;
            background-color: #f0f0f0;
        }
        .category-btn {
            margin-top: 40px;
            padding: 15px 40px;
            background-color: #3e2723;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.5rem;
            cursor: pointer;
        }
        .category-btn:hover {
            background-color: #5d4037;
        }
    </style>
</head>
<body>
    <h1>دسته‌بندی لباس‌ها</h1>
    <button class="category-btn" onclick="window.location.href='women.html'">لباس زنانه</button>
    <button class="category-btn" onclick="window.location.href='men.html'">لباس مردانه</button>
    <button class="category-btn" onclick="window.location.href='kids.html'">لباس بچگانه</button>
    <button class="category-btn" onclick="window.location.href='animals.html'">لباس حیوانات</button>
</body>
</html><!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toska - طراحی لباس</title>
    <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Vazirmatn', sans-serif;
            text-align: center;
            background-color: #f0f0f0;
        }
        header {
            background-color: #3e2723;
            color: white;
            padding: 20px 0;
            font-size: 2rem;
        }
        h1 {
            font-size: 3rem;
            margin-top: 20px;
        }
        .btn {
            margin-top: 40px;
            padding: 15px 40px;
            background-color: #f5a623;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.5rem;
            cursor: pointer;
        }
        .btn:hover {
            background-color: #ff8c00;
        }
    </style>
</head>
<body>
    <header>
        <h1>خوش آمدید به توسکا!</h1>
        <p>حالا وقتشه لباس مورد علاقتون رو خودتون طراحی کنید!</p>
    </header>
    <button class="btn" onclick="window.location.href='categories.html'">شروع طراحی</button>
</body>
</html>
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لباس زنانه | توسکا</title>
    <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Vazirmatn', sans-serif;
            text-align: center;
            background-color: #f0f0f0;
        }
        .product-btn {
            margin-top: 40px;
            padding: 15px 40px;
            background-color: #f5a623;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.5rem;
            cursor: pointer;
        }
        .product-btn:hover {
            background-color: #ff8c00;
        }
    </style>
</head>
<body>
    <h1>لباس زنانه</h1>
    <button class="product-btn" onclick="window.location.href='hoodie.html'">هودی</button>
    <button class="product-btn" onclick="window.location.href='tshirt.html'">تیشرت</button>
    <button class="product-btn" onclick="window.location.href='pants.html'">شلوار</button>
</body>
</html>
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>طراحی 3D لباس | توسکا</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        body {
            font-family: 'Vazirmatn', sans-serif;
            text-align: center;
            background-color: #f0f0f0;
        }
        #container {
            width: 100%;
            height: 500px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>طراحی 3D لباس</h1>
    <div id="container"></div>

    <script>
        var scene = new THREE.Scene();
        var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        var renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.getElementById("container").appendChild(renderer.domElement);

        var geometry = new THREE.BoxGeometry();
        var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
        var cube = new THREE.Mesh(geometry, material);
        scene.add(cube);

        camera.position.z = 5;

        function animate() {
            requestAnimationFrame(animate);
            cube.rotation.x += 0.01;
            cube.rotation.y += 0.01;
            renderer.render(scene, camera);
        }

        animate();
    </script>
</body>
</html>
