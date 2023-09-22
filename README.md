
<html>

<head>
    <meta charset="UTF-8">
    <title>استخراج معلومات أوفيس 365</title>
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
            margin: 10px 0;
        }

        .account-info {
            display: flex;
            justify-content: center;
            align-items: center;
            padding-left: 83px;
        }

        #inputField {
            width: 300px;
            padding: 5px;
            margin: 10px 0;
        }

        .account-email,
        .account-password {
            padding: 10px;
            background-color: #222;
            border: none;
            border-radius: 5px;
            width: 300px;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 18px;
            margin-right: 10px; /* Added margin for space to the right */
        }

        .account-email {
            background-color: #9027e3;
            margin-bottom: 10px;
        }

        .account-password {
            background-color: #5a008c;
            margin-bottom: 10px;
        }

        .copy-button {
            background-color: #9027e3;
            color: white;
            border: none;
            padding: 5px 10px;
            text-align: center;
            text-decoration: none;
            display: none; /* Initially hidden */
            font-size: 14px;
            border-radius: 5px;
            cursor: pointer;
        }

        .account-info:hover .copy-button {
            display: inline-block;
        }
    </style>
</head>

<body>
    <h1>استخراج معلومات اوفيس 365</h1>
    <div class="container">
        <!-- Input Field for Custom Account -->
        <input type="text" id="inputField" placeholder="أدخل البيانات (الايميل | كلمة السر)">
        <button class="button" onclick="separateAccount()">استخراج</button>

        <!-- Display Separated Account -->
        <div class="account" id="result" style="display: none;"> <!-- Initially hidden -->
            <div class="account-info">
                <div class="account-email" id="email">الايميل</div>
                <button class="copy-button" id="copyEmail" onclick="copyToClipboard('email')">انسخ الايميل</button>
            </div>
            <div class="account-info">
                <div class="account-password" id="password">كلمة السر</div>
                <button class="copy-button" id="copyPassword" onclick="copyToClipboard('password')">انسح كلمة السر</button>
            </div>
        </div>

        <!-- Open Office 365 Button -->
        <a href="https://www.office.com/?auth=2" target="_blank" class="button">ادخل حسابك اوفيس 365</a>
    </div>

    <script>
        function separateAccount() {
            const inputField = document.getElementById('inputField').value.trim();
            
            // Use a regular expression to extract the email and password
            const regex = /([^\s|]+@[^\s|]+) \| ([^\s|]+)/;
            const match = inputField.match(regex);

            if (match) {
                const email = match[1];
                const password = match[2];

                document.getElementById('email').textContent = email;
                document.getElementById('password').textContent = password;

                // Show the copy buttons
                document.getElementById('copyEmail').style.display = 'inline-block';
                document.getElementById('copyPassword').style.display = 'inline-block';

                // Show the result section
                document.getElementById('result').style.display = 'block';
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
