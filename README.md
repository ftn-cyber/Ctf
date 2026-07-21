<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>404 - Defaced by AJG Hack</title>
    <style>
        /* Reset dasar */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #050505; /* Latar belakang hitam pekat */
            color: #ffffff;
            font-family: 'Courier New', Courier, monospace; /* Font gaya hacker */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            text-align: center;
        }

        /* Efek Garis Scanline (seperti monitor lama) */
        body::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            z-index: 2;
            background-size: 100% 2px, 3px 100%;
            pointer-events: none;
        }

        .container {
            position: relative;
            z-index: 3;
            padding: 20px;
            border: 2px solid #ff0000; /* Border merah */
            background-color: rgba(0, 0, 0, 0.8);
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
            max-width: 90%;
            width: 600px;
        }

        /* Logo Tengkorak Besar */
        .skull-icon {
            font-size: 100px;
            margin-bottom: 20px;
            animation: pulse 1.5s infinite;
        }

        /* Judul Error 404 */
        h1.error-code {
            font-size: 80px;
            color: #ff0000;
            text-shadow: 2px 2px 0px #fff;
            margin-bottom: 10px;
            letter-spacing: 5px;
        }

        /* Peringatan Darurat */
        .warning-box {
            background-color: #ff0000;
            color: #000;
            padding: 10px;
            font-weight: bold;
            text-transform: uppercase;
            margin-bottom: 20px;
            display: inline-block;
            border: 2px solid #fff;
        }

        /* Teks Deface */
        .defaced-by {
            font-size: 24px;
            color: #fff;
            margin-top: 20px;
            border-top: 1px solid #555;
            padding-top: 20px;
        }

        .name {
            color: #ff0000;
            font-weight: bold;
            font-size: 30px;
            text-shadow: 0 0 10px #ff0000;
        }

        /* Animasi Berkedip */
        @keyframes pulse {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.1); opacity: 0.8; }
            100% { transform: scale(1); opacity: 1; }
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: ; }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Logo Tengkorak -->
        <div class="skull-icon">💀</div>

        <!-- Peringatan Darurat -->
        <div class="warning-box">
            ⚠️ DANGER / PERINGATAN DARURAT ⚠️
        </div>

        <!-- Judul 404 -->
        <h1 class="error-code">404</h1>
        
        <!-- Pesan Tambahan -->
        <p style="font-size: 18px; margin-bottom: 20px;">SYSTEM COMPROMISED<br>DATA HAS BEEN EXTRACTED</p>

        <!-- Tulisan Deface by -->
        <div class="defaced-by">
            DEFACE BY<br>
            <span class="name">AJG Hack</span>
        </div>
    </div>

</body>
</html>
