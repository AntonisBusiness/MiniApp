
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>$SUN☀️ Coin Mining</title>
    <style>
        body {
            background-color: #FFBF00;
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            font-size: 16px;
            font-weight: bold;
            width: 90%;
            margin: 0 auto;
            position: relative;
        }
        .header::after {
            content: "";
            position: absolute;
            left: 50%;
            top: 0;
            transform: translateX(-50%);
            width: 2px;
            height: 100%;
            background-color: #000000;
        }
        .separator {
            height: 2px;
            background-color: #000000;
            margin: 0 auto;
            width: 90%;
        }
        .progress-container {
            width: 90%;
            margin: 20px auto;
            background-color: #888;
            border-radius: 20px;
            overflow: hidden;
        }
        .progress-bar {
            width: 0%;
            height: 25px;
            background-color: #000000;
            color: white;
            line-height: 25px;
            font-weight: bold;
            font-size: 14px;
        }
        .claim-button {
            padding: 12px 24px;
            font-size: 16px;
            font-weight: bold;
            color: white;
            background-color: #000000;
            border: none;
            border-radius: 8px;
            margin-top: 15px;
            cursor: pointer;
            display: none;
        }
        .claim-button:disabled {
            background-color: #555;
            cursor: not-allowed;
        }
        .sun-logo {
            font-size: 60px;
            margin-top: 15px;
        }
        @media (max-width: 480px) {
            .header {
                font-size: 14px;
                padding: 8px;
            }
            .progress-bar {
                height: 20px;
                font-size: 12px;
            }
            .claim-button {
                padding: 10px 20px;
                font-size: 14px;
            }
            .sun-logo {
                font-size: 55px;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <span>$SUN☀️ Coin Mining</span>
        <span id="balance">$SUN☀️ Balance: 0</span>
    </div>
    <div class="separator"></div>
    <div class="progress-container">
        <div class="progress-bar" id="progress">0%</div>
    </div>
    <button class="claim-button" id="claimButton" onclick="claimSun()">Claim</button>
    <div class="sun-logo">☀️</div>

    <script>
        let balance = 0;
        let lastClaim = localStorage.getItem("lastClaim") || 0;
        let claimInterval = 24 * 60 * 60 * 1000; 

        function updateProgress() {
            let now = Date.now();
            let elapsed = now - lastClaim;
            let percentage = Math.min(100, (elapsed / claimInterval) * 100);
            document.getElementById("progress").style.width = percentage + "%";
            document.getElementById("progress").textContent = Math.floor(percentage) + "%";
            
            if (elapsed >= claimInterval) {
                document.getElementById("claimButton").style.display = "inline-block";
            } else {
                setTimeout(updateProgress, 1000);
            }
        }

        function claimSun() {
            balance += 10;
            document.getElementById("balance").textContent = `$SUN☀️ Balance: ${balance}`;
            lastClaim = Date.now();
            localStorage.setItem("lastClaim", lastClaim);
            document.getElementById("claimButton").style.display = "none";
            updateProgress();
        }

        updateProgress();
    </script>
</body>
</html>
