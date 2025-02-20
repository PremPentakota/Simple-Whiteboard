# Simple-Whiteboard
Simple Whiteboard
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Whiteboard</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        canvas {
            border: 2px solid black;
            background-color: white;
        }
        .toolbar {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="toolbar">
        <label for="color">Brush Color:</label>
        <input type="color" id="color">
        <label for="size">Brush Size:</label>
        <input type="range" id="size" min="1" max="10" value="5">
        <button id="clear">Clear</button>
    </div>
    <canvas id="board"></canvas>
    <script>
        const canvas = document.getElementById('board');
        const ctx = canvas.getContext('2d');
        const colorPicker = document.getElementById('color');
        const sizePicker = document.getElementById('size');
        const clearButton = document.getElementById('clear');

        canvas.width = window.innerWidth - 20;
        canvas.height = window.innerHeight - 100;

        let painting = false;

        function startPosition(e) {
            painting = true;
            draw(e);
        }
        function endPosition() {
            painting = false;
            ctx.beginPath();
        }
        function draw(e) {
            if (!painting) return;
            ctx.lineWidth = sizePicker.value;
            ctx.lineCap = 'round';
            ctx.strokeStyle = colorPicker.value;
            ctx.lineTo(e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop);
        }

        canvas.addEventListener('mousedown', startPosition);
        canvas.addEventListener('mouseup', endPosition);
        canvas.addEventListener('mousemove', draw);
        clearButton.addEventListener('click', () => ctx.clearRect(0, 0, canvas.width, canvas.height));
    </script>
</body>
</html>
