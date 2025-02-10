<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Medical Registration & Sign In</title>
    <style>
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        @keyframes slideIn {
            from {
                transform: translateY(30px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        body {
            font-family: Arial, sans-serif;
            background: url('https://assets.onecompiler.app/4362rf85w/4362r33bk/medpic2.avif') no-repeat center center fixed;
            background-size: cover;
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        .container {
            text-align: center;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            animation: fadeIn 1s ease-in-out;
            z-index: 1;
        }

        .button-container {
            margin-top: 20px;
        }

        .form-container {
            display: none;
            margin-top: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            animation: slideIn 0.5s ease-in-out;
        }

        .form-container h2 {
            margin-bottom: 20px;
        }

        .error {
            color: red;
        }

        .success {
            color: green;
        }

        input {
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            width: 100%;
            box-sizing: border-box;
            border: 1px solid #ccc;
            transition: border-color 0.3s ease;
        }

        input:focus {
            border-color: #4CAF50;
        }

        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #45a049;
        }

        .bubbles {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
        }

        .bubble {
            position: absolute;
            bottom: -50px;
            width: 40px;
            height: 40px;
            background-color: rgba(255, 255, 255, 0.6);
            border-radius: 50%;
            animation: bubble 10s infinite;
            opacity: 0;
        }

        @keyframes bubble {
            0% {
                transform: translateY(0);
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="bubbles" id="bubbles"></div>

    <div class="container">
        <h1>Welcome to the Medical Portal</h1>
        <div class="button-container">
            <button onclick="showRegistration()">Registration</button>
            <button onclick="showSignIn()">Sign In</button>
        </div>
    </div>

    <!-- Registration Form -->
    <div class="form-container" id="registration-form">
        <h2>Registration Form</h2>
        <form id="registerForm">
            <input type="text" id="regUsername" placeholder="User Name" required><br>
            <input type="password" id="regPassword" placeholder="Password" required><br>
            <input type="text" id="address" placeholder="Address" required><br>
            <input type="date" id="birthday" placeholder="Birthday" required><br>
            <input type="tel" id="contactNumber" placeholder="Contact Number" required><br>
            <button type="button" onclick="registerUser()">Register</button>
        </form>
        <p id="registerMessage" class="error"></p>
    </div>

    <!-- Sign In Form -->
    <div class="form-container" id="signin-form">
        <h2>Sign In Form</h2>
        <form id="signinForm">
            <input type="text" id="signinUsername" placeholder="User Name" required><br>
            <input type="password" id="signinPassword" placeholder="Password" required><br>
            <button type="button" onclick="signIn()">Enter</button>
        </form>
        <p id="signinMessage" class="error"></p>
    </div>

    <script>
        let users = [];

        function showRegistration() {
            document.getElementById('registration-form').style.display = 'block';
            document.getElementById('signin-form').style.display = 'none';
            document.getElementById('registerMessage').textContent = '';
        }

        function showSignIn() {
            document.getElementById('signin-form').style.display = 'block';
            document.getElementById('registration-form').style.display = 'none';
            document.getElementById('signinMessage').textContent = '';
        }

        function registerUser() {
            let username = document.getElementById('regUsername').value;
            let password = document.getElementById('regPassword').value;
            let address = document.getElementById('address').value;
            let birthday = document.getElementById('birthday').value;
            let contactNumber = document.getElementById('contactNumber').value;

            // Check if username or password already exists
            let existingUser = users.find(u => u.username === username);
            if (existingUser) {
                document.getElementById('registerMessage').textContent = 'User name already taken';
                document.getElementById('registerMessage').className = 'error';
                return;
            }

            if (username && password && address && birthday && contactNumber) {
                users.push({ username, password, address, birthday, contactNumber });
                document.getElementById('registerMessage').textContent = 'Registered Successfully';
                document.getElementById('registerMessage').className = 'success';
                document.getElementById('registerForm').reset();
                setTimeout(() => {
                    document.getElementById('registration-form').style.display = 'none';
                }, 2000);
            } else {
                document.getElementById('registerMessage').textContent = 'Please fill in all fields';
                document.getElementById('registerMessage').className = 'error';
            }
        }

        function signIn() {
            let signinUsername = document.getElementById('signinUsername').value;
            let signinPassword = document.getElementById('signinPassword').value;

            let user = users.find(u => u.username === signinUsername);
            if (!user) {
                document.getElementById('signinMessage').textContent = 'Incorrect username';
                document.getElementById('signinMessage').className = 'error';
            } else if (user.password !== signinPassword) {
                document.getElementById('signinMessage').textContent = 'Incorrect password';
                document.getElementById('signinMessage').className = 'error';
            } else {
                document.getElementById('signinMessage').textContent = 'Welcome, ' + signinUsername;
                document.getElementById('signinMessage').className = 'success';
                // Redirect to the details interface
                setTimeout(() => {
                    window.location.href = "details.html";
                }, 2000);
            }
        }

        function createBubble() {
            const bubble = document.createElement('div');
            bubble.className = 'bubble';
            const size = Math.random() * 60 + 20 + 'px';
            bubble.style.width = size;
            bubble.style.height = size;
            bubble.style.left = Math.random() * 100 + 'vw';
            bubble.style.animationDuration = Math.random() * 5 + 5 + 's';
            document.getElementById('bubbles').appendChild(bubble);

            setTimeout(() => {
                bubble.remove();
            }, 10000);
        }

        setInterval(createBubble, 500);
    </script>
</body>
</html>
