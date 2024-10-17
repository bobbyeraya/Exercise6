
ex6.php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Validation Example</title>
    <link rel="stylesheet" href="ex6.css">
</head>

<body>

    <?php include('header.php'); ?> 
    <main>
        <div class="container">
            <h1 class="titleForm">FORM VALIDATION</h1>
            <br>
            <form id="myForm" action="g5.php" method="POST" onsubmit="return validateForm()">
                <label for="name">Name:</label>
                <input type="text" id="name" name="name">
                <span class="error" id="nameError"></span><br><br>

                <label for="email">Email:</label>
                <input type="email" id="email" name="email">
                <span class="error" id="emailError"></span><br><br>

                <label for="password">Password:</label>
                <input type="password" id="password" name="password">
                <span class="error" id="passwordError"></span><br><br>
                <input type="submit" class="submit" value="Submit">
            </form>

            <div id="successModal" class="modal">
                <div class="modal-content">
                    <p>Form submitted successfully!</p>
                </div>
            </div>
        </div>
    </main>

    <script>
        function validateForm() {
            document.getElementById('nameError').innerText = '';
            document.getElementById('emailError').innerText = '';
            document.getElementById('passwordError').innerText = '';

            let valid = true;

            const name = document.getElementById('name').value;
            if (name === '') {
                document.getElementById('nameError').innerText = 'Name is required';
                valid = false;
            }

            const email = document.getElementById('email').value;
            const emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;
            if (email === '' || !email.match(emailPattern)) {
                document.getElementById('emailError').innerText = 'Valid email is required';
                valid = false;
            }

            const password = document.getElementById('password').value;
            if (password.length < 6) {
                document.getElementById('passwordError').innerText = 'Password must be at least 6 characters long';
                valid = false;
            }

            if (valid) {
                // Optional: Show a success modal (you might want to remove this if you are redirecting)
                document.getElementById('successModal').style.display = "block";
                setTimeout(() => {
                    closeModal();
                    // Allow the form to submit after the timeout
                    document.getElementById('myForm').submit(); 
                }, 1000); 
                return false; // Prevent default submission for now
            }

            return valid; 
        }

        function closeModal() {
            document.getElementById('successModal').style.display = "none";
            document.getElementById('myForm').reset(); 
        }
    </script>

    <?php require('footer.php'); ?>

</body>

</html>
