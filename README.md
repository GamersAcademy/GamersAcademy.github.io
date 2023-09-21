<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Office 365 Account Separator</title>
    <style>
        body {
            background-color: #111216;
            color: white;
            font-family: Arial, sans-serif;
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
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
            align-items: center;
        }

        #inputField {
            width: 300px;
            padding: 5px;
            margin-bottom: 10px;
        }

        #result {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .account-email,
        .account-password {
            margin-bottom: 10px;
        }
    </style>
</head>

<body>
    <h1>Office 365 Account Separator</h1>
    <div class="container">
        <!-- Input Field for Custom Account -->
        <input type="text" id="inputField" placeholder="Enter an account (email | password)">
        <button class="button" onclick="separateAccount()">Separate</button>

        <!-- Display Separated Account -->
        <div class="account" id="result">
            <div class="account-email" id="email">Email</div>
            <button class="button" id="copyEmail" onclick="copyToClipboard('email')">Copy Email</button>
            <div class="account-password" id="password">Password</div>
            <button class="button" id="copyPassword" onclick="copyToClipboard('password')">Copy Password</button>
        </div>

        <!-- Open Office 365 Button -->
        <a href="https://www.office.com/?auth=2" target="_blank" class="button">Open Office 365</a>
    </div>

    <script>
        function separateAccount() {
            const inputField = document.getElementById('inputField').value.trim();
            const accountParts = inputField.split('|');

            if (accountParts.length === 2) {
                const email = accountParts[0].trim();
                const password = accountParts[1].trim();

                document.getElementById('email').textContent = email;
                document.getElementById('password').textContent = password;

                // Show the result section
                document.getElementById('result').style.display = 'flex';
            } else {
                alert('Please enter an account in the format "email | password".');
            }
        }

        function copyToClipboard(elementId) {
            const textToCopy = document.getElementById(elementId).textContent;
            const tempInput = document.createElement('input');
            tempInput.value = textToCopy;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);
            alert('Copied to clipboard: ' + textToCopy);
        }
    </script>
</body>

</html>
