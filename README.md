<!DOCTYPE html>
<html>
<head>
    <title>Neon Sketchpad</title>
    <style>
        body { margin: 0; overflow: hidden; background: #050505; font-family: sans-serif; }
        canvas { display: block; }
        .controls { position: absolute; top: 10px; left: 10px; background: rgba(255,255,255,0.1); padding: 10px; border-radius: 8px; backdrop-filter: blur(5px); }
        button, input { padding: 8px 12px; margin-right: 5px; cursor: pointer; border: none; border-radius: 4px; font-weight: bold; }
    </style>
</head>
<body>
    <div class="controls">
        <input type="color" id="colorPicker" value="#00ffcc">
        <button onclick="clearCanvas()">Clear Screen</button>
    </div>
    <canvas id="paintCanvas"></canvas>

    <script>
        const canvas = document.getElementById('paintCanvas');
        const ctx = canvas.getContext('2d');
        let painting = false;

        function resize() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
        window.addEventListener('resize', resize);
        resize();

        function startPosition(e) { painting = true; draw(e); }
        function endPosition() { painting = false; ctx.beginPath(); }
        
        function draw(e) {
            if (!painting) return;
            ctx.lineWidth = 6;
            ctx.lineCap = 'round';
            ctx.strokeStyle = document.getElementById('colorPicker').value;
            ctx.shadowBlur = 10;
            ctx.shadowColor = ctx.strokeStyle;

            ctx.lineTo(e.clientX || e.touches[0].clientX, e.clientY || e.touches[0].clientY);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(e.clientX || e.touches[0].clientX, e.clientY || e.touches[0].clientY);
        }

        canvas.addEventListener('mousedown', startPosition);
        canvas.addEventListener('mouseup', endPosition);
        canvas.addEventListener('mousemove', draw);
        canvas.addEventListener('touchstart', (e) => { e.preventDefault(); startPosition(e); });
        canvas.addEventListener('touchend', endPosition);
        canvas.addEventListener('touchmove', (e) => { e.preventDefault(); draw(e); });

        function clearCanvas() { ctx.clearRect(0, 0, canvas.width, canvas.height); }
    </script>
</body>
</html>


        
