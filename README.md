<!DOCTYPE html>
<html>
<head>
  <title>注文フォーム</title>
  <script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
</head>
<body>

<h2>注文フォーム</h2>

<label>商品：</label>
<select id="product">
  <option value="Aセット">Aセット</option>
  <option value="Bセット">Bセット</option>
</select>

<br>

<label>日付：</label>
<input type="date" id="date">

<br>

<label>人数：</label>
<input type="number" id="people">

<br><br>

<button onclick="sendOrder()">注文する</button>

<script>
async function main() {
  await liff.init({ liffId: "YOUR_LIFF_ID" });
}
main();

async function sendOrder() {
  const product = document.getElementById("product").value;
  const date = document.getElementById("date").value;
  const people = document.getElementById("people").value;

  const message = `
【注文内容】
商品：${product}
日付：${date}
人数：${people}人
`;

  if (!liff.isLoggedIn()) {
    liff.login();
    return;
  }

  await liff.sendMessages([
    {
      type: "text",
      text: message
    }
  ]);

  alert("注文を送信しました！");
  liff.closeWindow();
}
</script>

</body>
</html>
