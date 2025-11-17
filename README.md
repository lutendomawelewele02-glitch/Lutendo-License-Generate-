# Lutendo-License-Generate-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lutendo License Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            max-width: 400px;
            width: 100%;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        label {
            display: block;
            margin-top: 15px;
            font-weight: bold;
        }
        input {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            margin-top: 20px;
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: #fff;
            font-weight: bold;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .output {
            margin-top: 20px;
            word-wrap: break-word;
            background: #f5f5f5;
            padding: 10px;
            border-radius: 5px;
            font-family: monospace;
            color: #222;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Lutendo License Generator</h1>

        <label for="account">Account Number:</label>
        <input type="text" id="account" placeholder="Enter client account number">

        <label for="expiry">Expiry Date:</label>
        <input type="date" id="expiry">

        <label for="secret">Secret Key:</label>
        <input type="text" id="secret" placeholder="Enter your secret key">

        <button onclick="generateLicense()">Generate License</button>

        <div class="output" id="licenseOutput">Your license will appear here.</div>
    </div>

    <script>
        async function sha256(message) {
            const msgBuffer = new TextEncoder().encode(message);
            const hashBuffer = await crypto.subtle.digest('SHA-256', msgBuffer);
            const hashArray = Array.from(new Uint8Array(hashBuffer));
            return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
        }

        async function generateLicense() {
            const account = document.getElementById('account').value.trim();
            const expiry = document.getElementById('expiry').value;
            const secret = document.getElementById('secret').value.trim();

            if (!account || !expiry || !secret) {
                alert("Please fill all fields.");
                return;
            }

            const combined = `ACC:${account}|EXP:${expiry}|KEY:${secret}`;
            const hash = await sha256(combined);

            const licenseCode = `ACC:${account}|EXP:${expiry}|KEY:${hash}`;
            document.getElementById('licenseOutput').innerText = licenseCode;
        }
    </script>
</body>
</html>
