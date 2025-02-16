# Assignment: Creating Interactive Elements and Form Validation

## Objective:
Build a functional webpage that incorporates event handling, interactive elements, and form validation using JavaScript.

## Requirements:

Interactive Button with onclick:

Add a button that toggles the background color of the webpage between two colors.
Slider with Real-Time Feedback (oninput):

Add a slider that adjusts the size of a paragraph text dynamically.
Modal with Event Listeners:

Create a modal that displays when a button is clicked and hides when the user clicks a close button.

## Form with Validation:

Include a form with the following fields:
Name (required, minimum 3 characters).
Email (valid email format).
Password (minimum 8 characters, at least one uppercase letter and one number).
Display error messages if validation fails.
Prevent form submission if there are errors.
Bonus (Optional):

Add a dropdown menu that displays a custom message when the selected option changes (onchange).

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Webpage</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            transition: background-color 0.5s;
        }

        .container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
        }

       
        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 300px;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
        }

        .error {
            color: red;
            font-size: 14px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Interactive Webpage</h1>

        <button onclick="toggleBackground()">Toggle Background Color</button>

    
        <p id="text">Adjust my size using the slider below!</p>
        <input type="range" min="14" max="40" value="16" oninput="adjustTextSize(this.value)">
        
 
        <button onclick="openModal()">Open Modal</button>

       
        <div class="modal-overlay" id="modal-overlay" onclick="closeModal()"></div>
        <div class="modal" id="modal">
            <p>This is a modal popup.</p>
            <button onclick="closeModal()">Close</button>
        </div>

       
        <form id="userForm" onsubmit="return validateForm()">
            <h2>Sign Up</h2>
            <label>Name:</label>
            <input type="text" id="name">
            <span class="error" id="nameError"></span><br><br>

            <label>Email:</label>
            <input type="email" id="email">
            <span class="error" id="emailError"></span><br><br>

            <label>Password:</label>
            <input type="password" id="password">
            <span class="error" id="passwordError"></span><br><br>

            <button type="submit">Submit</button>
        </form>


        <h2>Select an Option</h2>
        <select id="dropdown" onchange="showMessage()">
            <option value="">-- Choose an option --</option>
            <option value="hello">Say Hello</option>
            <option value="bye">Say Goodbye</option>
        </select>
        <p id="dropdownMessage"></p>
    </div>

    <script>
        let isDark = false;

        function toggleBackground() {
            document.body.style.backgroundColor = isDark ? "white" : "#222";
            document.body.style.color = isDark ? "black" : "white";
            isDark = !isDark;
        }

        function adjustTextSize(size) {
            document.getElementById("text").style.fontSize = size + "px";
        }

        function openModal() {
            document.getElementById("modal").style.display = "block";
            document.getElementById("modal-overlay").style.display = "block";
        }

        function closeModal() {
            document.getElementById("modal").style.display = "none";
            document.getElementById("modal-overlay").style.display = "none";
        }

        function validateForm() {
            let name = document.getElementById("name").value;
            let email = document.getElementById("email").value;
            let password = document.getElementById("password").value;
            let valid = true;

            document.getElementById("nameError").innerText = name.length < 3 ? "Name must be at least 3 characters" : "";
            document.getElementById("emailError").innerText = !email.includes("@") ? "Enter a valid email" : "";
            document.getElementById("passwordError").innerText = password.length < 8 || !/[A-Z]/.test(password) || !/\d/.test(password) 
                ? "Password must be at least 8 chars, 1 uppercase & 1 number" 
                : "";

            if (name.length < 3 || !email.includes("@") || password.length < 8 || !/[A-Z]/.test(password) || !/\d/.test(password)) {
                valid = false;
            }

            return valid;
        }

        function showMessage() {
            let dropdown = document.getElementById("dropdown").value;
            let message = dropdown === "hello" ? "Hello, welcome!" : dropdown === "bye" ? "Goodbye, see you soon!" : "";
            document.getElementById("dropdownMessage").innerText = message;
        }
    </script>

</body>
</html>

