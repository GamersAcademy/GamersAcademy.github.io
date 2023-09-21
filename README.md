<!DOCTYPE html>
<html>
<head>
  <title>Adobe Codes Organizer</title>
  <style>
    body {
      background-color: #111;
      color: #fff;
      font-family: Arial, sans-serif;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #af6dff;
      margin-top: 0;
    }

    .box {
      border-radius: 6px;
      padding: 20px;
      margin-bottom: 20px;
      text-align: left;
    }

    .codes {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      margin-bottom: 10px;
    }

    .code-input,
    .code-result,
    .extra-codes-result {
      width: 100%;
      height: 200px;
      padding: 10px;
      background-color: #222;
      border: none;
      border-radius: 6px;
      color: #fff;
      resize: none;
      text-align: center;
      overflow: auto;
    }

    select {
      padding: 5px;
      font-size: 16px;
      margin-bottom: 10px;
    }

    .button-container {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 10px;
      flex-wrap: wrap;
    }

    button {
      padding: 10px 20px;
      background-color: #7557E4;
      border: none;
      color: #fff;
      font-size: 16px;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      margin: 5px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    button:hover {
      background-color: #8E69FF;
      box-shadow: 0 0 5px rgba(255, 255, 255, 0.3);
    }

    .code-list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      margin-bottom: 10px;
    }

    .code {
      flex-basis: calc(33.33% - 10px);
      margin-bottom: 10px;
      word-wrap: break-word;
    }

    .extra-codes-box {
      margin-top: 20px;
      text-align: center;
    }

    .extra-codes-box .box {
      min-height: 200px;
    }

    .extra-codes-text {
      font-size: 12px;
      color: #888;
      margin-bottom: 10px;
    }

    .extra-codes-result {
      width: 100%;
      min-height: 100px;
      padding: 10px;
      background-color: #222;
      border: none;
      border-radius: 6px;
      color: #fff;
      resize: vertical;
      overflow-y: auto;
      margin-bottom: 10px;
      text-align: center;
      white-space: pre-line;
    }

    .copy-button-container {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 10px;
    }

    .copy-button {
      padding: 10px 20px;
      background-color: #7557E4;
      border: none;
      color: #fff;
      font-size: 16px;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      margin: 5px;
      display: none;
      align-items: center;
      justify-content: center;
    }

    .copy-button:hover {
      background-color: #8E69FF;
      box-shadow: 0 0 5px rgba(255, 255, 255, 0.3);
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Adobe Codes Organizer</h1>
    <div class="box">
      <h2>Enter Codes</h2>
      <div class="codes">
        <textarea class="code-input" id="codesInput" placeholder="Enter codes"></textarea>
      </div>
      <div class="button-container">
        <select id="monthsSelect">
          <option value="1">1 Month</option>
          <option value="3">3 Months</option>
          <option value="6">6 Months</option>
          <option value="12">12 Months</option>
        </select>
      </div>
      <div class="button-container">
        <button onclick="organizeCodes()">Organize</button>
      </div>
    </div>
  </div>

  <div class="container">
    <div class="result-container">
      <h2>Result</h2>
      <div class="code-result" id="resultCodes"></div>
      <div class="copy-button-container">
        <button class="copy-button" onclick="copyCodes()" id="copyCodesButton">Copy Result</button>
      </div>
    </div>
    <div class="extra-codes-box">
      <div class="box">
        <h2>Extra Codes</h2>
        <div class="extra-codes-result" id="extraCodesResult"></div>
        <div class="copy-button-container">
          <button class="copy-button" onclick="copyExtraCodes()" id="copyExtraCodesButton">Copy Extra Codes</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    function organizeCodes() {
      var codesInput = document.getElementById("codesInput").value;
      var monthsSelect = document.getElementById("monthsSelect");
      var numCodesPerList = parseInt(monthsSelect.value);
      var codes = codesInput.split("\n").map(function(code) {
        return code.replace(/-/g, "").trim();
      });

      var extraCodes = "";
      var numExtraCodes = codes.length % numCodesPerList;
      if (numExtraCodes > 0) {
        extraCodes = codes.slice(-numExtraCodes).join("\n");
        codes = codes.slice(0, -numExtraCodes);
      }

      var codeLists = [];
      for (var i = 0; i < codes.length; i += numCodesPerList) {
        codeLists.push(codes.slice(i, i + numCodesPerList));
      }

      var result = "";
      for (var j = 0; j < codeLists.length; j++) {
        var codeList = "<div class='code'><pre>" + codeLists[j].join(" | ") + "</pre></div>";
        result += codeList;
      }

      document.getElementById("extraCodesResult").innerHTML = extraCodes;
      document.getElementById("resultCodes").innerHTML = result;

      var copyCodesButton = document.getElementById("copyCodesButton");
      if (result.trim() !== "") {
        copyCodesButton.style.display = "flex";
      } else {
        copyCodesButton.style.display = "none";
      }

      var copyExtraCodesButton = document.getElementById("copyExtraCodesButton");
      if (extraCodes) {
        copyExtraCodesButton.style.display = "flex";
      } else {
        copyExtraCodesButton.style.display = "none";
      }
    }

    function copyCodes() {
      var resultCodes = document.getElementById("resultCodes");
      var tempTextArea = document.createElement("textarea");
      tempTextArea.value = resultCodes.textContent.trim();
      document.body.appendChild(tempTextArea);
      tempTextArea.select();
      document.execCommand("copy");
      document.body.removeChild(tempTextArea);
    }

    function copyExtraCodes() {
      var extraCodesResult = document.getElementById("extraCodesResult");
      var tempTextArea = document.createElement("textarea");
      tempTextArea.value = extraCodesResult.textContent.trim();
      document.body.appendChild(tempTextArea);
      tempTextArea.select();
      document.execCommand("copy");
      document.body.removeChild(tempTextArea);
    }
  </script>
</body>
</html>
