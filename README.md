# RV-Hacker

## git clone to project
''''

     git clone "https://github.com/Vishwajitji/RV-Hacker.git"
     cd RV-Hacker


''''





Here's a basic example of a login system in PHP:

# Database Connection
First, you'll need to connect to your database. Create a file named `db.php` with the following code:

```
<?php
$servername = "localhost";
$username = "your_username";
$password = "your_password";
$dbname = "your_database";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

# Login Form
Create a file named `login.php` with the following code:

```
<?php
session_start();
require_once 'db.php';

if (isset($_POST['login'])) {
    $username = $_POST['username'];
    $password = $_POST['password'];

    $query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
    $result = mysqli_query($conn, $query);

    if (mysqli_num_rows($result) > 0) {
        $row = mysqli_fetch_assoc($result);
        $_SESSION['username'] = $row['username'];
        header("Location: dashboard.php");
    } else {
        echo "Invalid username or password";
    }
}
?>

<form action="" method="post">
    <input type="text" name="username" placeholder="Username">
    <input type="password" name="password" placeholder="Password">
    <button type="submit" name="login">Login</button>
</form>
```

# Dashboard
Create a file named `dashboard.php` with the following code:

```
<?php
session_start();
if (!isset($_SESSION['username'])) {
    header("Location: login.php");
}

echo "Welcome, " . $_SESSION['username'];
?>
```

# Security Considerations
This is a basic example and doesn't include security measures like password hashing, validation, or sanitization. You should consider implementing these measures to secure your login system.

# Password Hashing
You can use PHP's built-in `password_hash()` function to hash passwords. Here's an example:

```
$password = password_hash($_POST['password'], PASSWORD_DEFAULT);
```

# Validation and Sanitization
You can use PHP's built-in `filter_var()` function to validate and sanitize user input. Here's an example:

```
$username = filter_var($_POST['username'], FILTER_SANITIZE_STRING);
```

Remember to always follow best practices for security and validation when building a login system.
