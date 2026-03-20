# QRCode

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Secret QR</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <style>
        body { 
            display: flex; flex-direction: column; align-items: center; 
            justify-content: center; height: 100vh; margin: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f2f5;
        }
        #monkey-container { display: none; text-align: center; }
        .monkey { font-size: 120px; animation: bounce 1s infinite; }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
        .qr-card {
            background: white; padding: 30px; border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center;
        }
    </style>
</head>
<body>

    <div id="monkey-container">
        <div class="monkey">🐵</div>
        <h1>You found the smiling monkey!</h1>
        <button onclick="window.location.href=window.location.pathname">Go Back</button>
    </div>

    <div id="setup-container" class="qr-card">
        <h2>Scan to reveal the secret</h2>
        <div id="qrcode"></div>
        <p>Use your phone camera</p>
    </div>

    <script>
        // 1. Check if we were redirected by the QR code
        const urlParams = new URLSearchParams(window.location.search);
        if (urlParams.has('showMonkey')) {
            document.getElementById('setup-container').style.display = 'none';
            document.getElementById('monkey-container').style.display = 'block';
        }

        // 2. Generate the QR code pointing to THIS file with a secret parameter
        // Note: For this to work on a phone, you'd need to host this file 
        // online (e.g., GitHub Pages) and replace 'window.location.href' 
        // with that actual URL.
        new QRCode(document.getElementById("qrcode"), {
            text: window.location.href + "?showMonkey=true",
            width: 200,
            height: 200,
            colorDark : "#333333",
            colorLight : "#ffffff",
            correctLevel : QRCode.CorrectLevel.H
        });
    </script>
</body>
</html>
