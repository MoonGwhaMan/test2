[index.html](https://github.com/user-attachments/files/22506967/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>상자 효과</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f4f8;
            transition: background-color 0.5s ease-in-out;
        }
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            gap: 2rem;
        }
        .box {
            width: 200px;
            height: 200px;
            background-color: #4f46e5;
            border-radius: 1.5rem;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease-in-out, background-color 0.3s ease-in-out;
            position: relative;
            overflow: hidden;
        }
        .box:hover {
            transform: translateY(-5px) scale(1.02);
            background-color: #4338ca;
        }
        .text {
            color: white;
            font-size: 5rem;
            font-weight: 700;
            opacity: 0;
            transform: scale(0.5);
            transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
            user-select: none;
        }
        .circle {
            position: absolute;
            background-color: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            pointer-events: none;
            opacity: 0;
            transform: scale(0);
            transition: transform 0.6s ease-out, opacity 0.6s ease-out;
        }
    </style>
</head>
<body>

<div class="container">
    <div id="clickable-box" class="box">
        <span id="box-text" class="text">ㅗ</span>
    </div>
    <p class="text-gray-600">상자를 클릭하면 어떤 일이 일어나는지 보세요!</p>
</div>

<script>
    const box = document.getElementById('clickable-box');
    const boxText = document.getElementById('box-text');

    box.addEventListener('click', (e) => {
        // 텍스트 보이기
        boxText.style.opacity = '1';
        boxText.style.transform = 'scale(1)';

        // 상자 크기를 일시적으로 키우는 동적 효과
        box.style.transform = 'scale(1.1)';
        setTimeout(() => {
            box.style.transform = 'scale(1)';
        }, 300);

        // 클릭한 위치에 물결 효과 생성
        const ripple = document.createElement('span');
        ripple.classList.add('circle');
        const diameter = Math.max(box.clientWidth, box.clientHeight);
        const radius = diameter / 2;
        ripple.style.width = ripple.style.height = `${diameter}px`;
        ripple.style.left = `${e.clientX - box.offsetLeft - radius}px`;
        ripple.style.top = `${e.clientY - box.offsetTop - radius}px`;
        
        box.appendChild(ripple);
        
        // 애니메이션 시작
        setTimeout(() => {
            ripple.style.transform = 'scale(1)';
            ripple.style.opacity = '1';
        }, 1);

        // 애니메이션이 끝나면 요소 제거
        ripple.addEventListener('transitionend', () => {
            ripple.remove();
        });
    });

</script>

</body>
</html>
