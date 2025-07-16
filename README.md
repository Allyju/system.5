# system.5
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M_in_X.Tech</title>
    <style>
        :root {
            --primary: #6366f1;
            --dark: #1e293b;
            --light: #f8fafc;
            --card: #fff;
        }
        * {
            margin: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }
        body {
            background: var(--light);
            color: var(--dark);
        }
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 1rem;
        }
        #login-page, #dashboard { min-height: 100vh; display: flex; flex-direction: column; }
        #dashboard { display: none; }
        header {
            background: var(--card);
            padding: 1rem 0;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .logo {
            font-size: 1.5rem;
            font-weight: 800;
            background: linear-gradient(90deg, var(--primary), #8b5cf6);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .login-card {
            background: var(--card);
            border-radius: 8px;
            padding: 2rem;
            margin: auto;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        input, button {
            width: 100%;
            padding: 0.8rem;
            margin: 0.5rem 0;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
        button {
            background: var(--primary);
            color: white;
            border: none;
            font-weight: 600;
            cursor: pointer;
        }
        .menu {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
        }
        .menu a {
            padding: 0.5rem 1rem;
            border-radius: 4px;
            text-decoration: none;
            color: var(--dark);
            font-weight: 500;
        }
        .menu a.active, .menu a:hover {
            background: rgba(99, 102, 241, 0.1);
            color: var(--primary);
        }
        .content {
            flex: 1;
            padding: 2rem 0;
        }
        .card {
            background: var(--card);
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1rem;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        @media (max-width: 768px) {
            nav { flex-direction: column; gap: 1rem; }
            .menu { flex-wrap: wrap; justify-content: center; }
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div id="login-page">
        <header>
            <div class="container">
                <nav>
                    <div class="logo">M_in_X.Tech</div>
                </nav>
            </div>
        </header>
        <div class="container">
            <div class="login-card">
                <h2 style="margin-bottom:1rem;text-align:center">Welcome Back</h2>
                <input type="text" id="username" placeholder="Username">
                <input type="password" id="password" placeholder="Password">
                <button onclick="login()">Login</button>
            </div>
        </div>
    </div>

    <!-- Dashboard -->
    <div id="dashboard">
        <header>
            <div class="container">
                <nav>
                    <div class="logo">M_in_X.Tech</div>
                    <button onclick="logout()" style="background:none;color:var(--primary);padding:0">Logout</button>
                </nav>
            </div>
        </header>
        <div class="container">
            <div class="menu">
                <a href="#" class="active" data-page="dashboard">Dashboard</a>
                <a href="#" data-page="billing">Billing</a>
                <a href="#" data-page="services">Services</a>
                <a href="#" data-page="discount">Discount</a>
            </div>
            <div class="content">
                <div class="card" id="dashboard-page">
                    <h2>Dashboard</h2>
                    <p>Welcome to your M_in_X.Tech dashboard</p>
                </div>
                <div class="card" id="billing-page" style="display:none">
                    <h2>Billing</h2>
                    <p>Your billing information and invoices</p>
                </div>
                <div class="card" id="services-page" style="display:none">
                    <h2>Our Services</h2>
                    <p>Custom Software, Web Development, Mobile Apps</p>
                </div>
                <div class="card" id="discount-page" style="display:none">
                    <h2>Special Discounts</h2>
                    <p>Current promotions and offers</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Login function
        function login() {
            const user = document.getElementById('username').value;
            const pass = document.getElementById('password').value;
            if(user && pass) {
                localStorage.setItem('loggedIn', 'true');
                document.getElementById('login-page').style.display = 'none';
                document.getElementById('dashboard').style.display = 'flex';
            } else {
                alert('Please enter credentials');
            }
        }

        // Logout function
        function logout() {
            localStorage.removeItem('loggedIn');
            document.getElementById('login-page').style.display = 'flex';
            document.getElementById('dashboard').style.display = 'none';
        }

        // Check login status
        if(localStorage.getItem('loggedIn') === 'true') {
            document.getElementById('login-page').style.display = 'none';
            document.getElementById('dashboard').style.display = 'flex';
        }

        // Menu navigation
        document.querySelectorAll('.menu a').forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                document.querySelectorAll('.menu a').forEach(a => a.classList.remove('active'));
                e.target.classList.add('active');
                document.querySelectorAll('.card').forEach(card => card.style.display = 'none');
                document.getElementById(`${e.target.dataset.page}-page`).style.display = 'block';
            });
        });
    </script>
</body>
</html>
