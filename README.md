<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Medical Registration & Sign In</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: url('https://assets.onecompiler.app/4362rf85w/4362r33bk/medpic2.avif') no-repeat center center fixed;
            background-size: cover;
            margin: 0;
            padding: 0;
            height: 100vh;
        }
        .container {
            text-align: center;
            margin-top: 100px;
        }
        .form-container {
            display: none;
            margin-top: 30px;
            background-color: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
        }
        .error {
            color: red;
        }
        .success {
            color: green;
        }
        input {
            padding: 10px;
            margin: 10px;
            border-radius: 5px;
            width: 200px;
        }
        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Welcome to the Medical Portal</h1>
        <button onclick="showRegistration()">Registration</button>
        <button onclick="showSignIn()">Sign In</button>
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
                document.getElementById('registerMessage').textContent = 'You have already registered';
                document.getElementById('registerMessage').className = 'error';
                return;
            }

            let existingPassword = users.find(u => u.password === password);
            if (existingPassword) {
                document.getElementById('registerMessage').textContent = 'Password unavailable';
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
    </script>

</body>
</html>

