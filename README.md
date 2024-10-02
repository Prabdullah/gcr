<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown Timer</title>
    <style>
        body, html {
            height: 100%;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            color: white;
            font-family: Arial, sans-serif;
        }

        /* شاشة التحميل الدائرية */
        .loading-container {
            position: relative;
            width: 150px;
            height: 150px;
            border: 10px solid white;
            border-radius: 50%;
            border-top: 10px solid red;
            animation: spin 2s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* الرقم العمودي في وسط الشاشة */
        .countdown {
            font-size: 5rem; /* حجم الرقم 5rem */
            color: red;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
    </style>
</head>
<body>

    <!-- شاشة التحميل الدائرية -->
    <div class="loading-container" id="loading">
        <!-- حذف كلمة التحميل -->
    </div>

    <!-- الرقم العمودي في وسط الشاشة -->
    <div class="countdown" id="countdown" style="display: none;">
        00<br>00<br>00<br>00<br>00<br>00
    </div>

    <script>
        // شاشة التحميل تدوم 5 ثوانٍ
        setTimeout(() => {
            document.getElementById('loading').style.display = 'none'; // إخفاء شاشة التحميل
            document.getElementById('countdown').style.display = 'block'; // إظهار العد التنازلي

            // اختيار رقم عشوائي بين 999 دقيقة و 9999999 دقيقة
            let randomMinutes = Math.floor(Math.random() * (9999999 - 999 + 1)) + 999;

            // تحويل الدقائق العشوائية إلى ثواني
            let timeInSeconds = randomMinutes * 60;

            // تحديث العد التنازلي بشكل عمودي
            const countdownElement = document.getElementById("countdown");
            const countdownInterval = setInterval(() => {
                // حساب السنوات، الأشهر، الأيام، الساعات، الدقائق والثواني
                let years = Math.floor(timeInSeconds / (3600 * 24 * 365));
                let months = Math.floor((timeInSeconds % (3600 * 24 * 365)) / (3600 * 24 * 30));
                let days = Math.floor((timeInSeconds % (3600 * 24 * 30)) / (3600 * 24));
                let hours = Math.floor((timeInSeconds % (3600 * 24)) / 3600);
                let minutes = Math.floor((timeInSeconds % 3600) / 60);
                let seconds = timeInSeconds % 60;

                // إضافة صفر أمام القيم الأقل من 10
                months = months < 10 ? '0' + months : months;
                days = days < 10 ? '0' + days : days;
                hours = hours < 10 ? '0' + hours : hours;
                minutes = minutes < 10 ? '0' + minutes : minutes;
                seconds = seconds < 10 ? '0' + seconds : seconds;

                // تحديث العد التنازلي بشكل عمودي
                countdownElement.innerHTML = `${years}<br>${months}<br>${days}<br>${hours}<br>${minutes}<br>${seconds}`;

                // تقليل الوقت بمقدار ثانية واحدة
                timeInSeconds--;

                // إنهاء العد التنازلي عند الوصول إلى الصفر
                if (timeInSeconds < 0) {
                    clearInterval(countdownInterval);
                    countdownElement.innerHTML = "Time's up!";
                }
            }, 1000); // التحديث كل 1000 ميلي ثانية (1 ثانية)

        }, 5000); // مدة التحميل 5 ثوانٍ
    </script>

</body>
</html>
