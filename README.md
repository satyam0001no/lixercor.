<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Lixercor Payment</title>
  <style>
    body {
      background: #0d1117;
      color: #c9d1d9;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px;
      text-align: center;
    }
    h1 {
      color: #58a6ff;
      margin-bottom: 10px;
    }
    #qrcode {
      margin: 20px auto;
      padding: 20px;
      background: #ffffff;
    }
    #timer {
      font-size: 24px;
      margin-top: 10px;
      color: #ffa657;
    }
    .footer {
      margin-top: 30px;
      font-size: 14px;
      color: #8b949e;
    }
    a {
      color: #58a6ff;
      text-decoration: none;
    }
  </style>
</head>
<body>

  <h1>Welcome to Lixercor</h1>
  <p>Scan the QR code below to make a payment</p>

  <div id="qrcode"></div>

  <div id="timer">15:00</div>
  <p>QR code is only valid for 15 minutes</p>

  <div class="footer">
    <p>WhatsApp: <a href="https://wa.me/917520221141" target="_blank">7520221141</a></p>
    <p>Instagram: <a href="https://www.instagram.com/lixercor" target="_blank">@lixercor</a></p>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/qrcode/build/qrcode.min.js"></script>
  <script>
    // Generate UPI payment link
    const upiId = "7520221141@ptsbi";
    const name = "Lixercor";
    const txnId = "TID" + Math.floor(Math.random() * 1000000000);
    const url = `upi://pay?pa=${upiId}&pn=${name}&tid=${txnId}&cu=INR`;

    // Generate QR Code
    QRCode.toCanvas(document.createElement('canvas'), url, { width: 220 }, function (err, canvas) {
      if (err) console.error(err);
      const container = document.getElementById('qrcode');
      container.innerHTML = "";
      container.appendChild(canvas);
    });

    // Countdown Timer (15 minutes)
    let minutes = 15;
    let seconds = 0;
    const timerEl = document.getElementById("timer");
    const countdown = setInterval(() => {
      if (seconds === 0) {
        if (minutes === 0) {
          clearInterval(countdown);
          timerEl.innerText = "Expired";
          document.getElementById("qrcode").innerHTML = "<p style='color:red;'>QR code expired</p>";
          return;
        }
        minutes--;
        seconds = 59;
      } else {
        seconds--;
      }
      timerEl.innerText = `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
    }, 1000);
  </script>
</body>
</html>
