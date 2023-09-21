<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Office 365 Accounts</title>
    <style>
        body {
            background-color: #111216;
            color: white;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }

        .account {
            margin: 10px;
        }

        .button {
            background-color: #9027e3;
            color: white;
            border: none;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            margin: 5px;
        }

        .account-info {
            display: flex;
            justify-content: space-between;
        }
    </style>
</head>

<body>
    <h1>Office 365 Accounts</h1>

    <!-- Account 1 -->
    <div class="account">
        <div class="account-info">
            <div class="account-email">A5565@office365-25.de</div>
            <button class="button" onclick="copyToClipboard('A5565@office365-25.de')">Copy</button>
        </div>
        <div class="account-password">t3JD8heP</div>
        <button class="button" onclick="copyToClipboard('t3JD8heP')">Copy</button>
    </div>

    <!-- Add more accounts here if needed -->

    <!-- Open Office 365 Button -->
    <a href="https://www.office.com" target="_blank" class="button">Open Office 365</a>

    <script>
        function copyToClipboard(text) {
            const tempInput = document.createElement('input');
            tempInput.value = text;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);
            alert('Copied to clipboard: ' + text);
        }
    </script>
</body>

</html>
