Here's a complete implementation of your description using HTML, CSS, and JavaScript. The page allows users to register, login, describe symptoms, get a diagnosis, and book an appointment. The logic is split into sections as described, with functionality like symptom checkboxes, doctor selection, and appointment confirmation.

### Full HTML, CSS, and JavaScript Implementation:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Depressed People Support</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f7fa;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 100%;
            max-width: 500px;
            margin: auto;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        .form-group input {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .form-group button {
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .form-group button:hover {
            background-color: #0056b3;
        }
        .symptom-checkboxes {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        .symptom-checkboxes label {
            width: 45%;
        }
        .login-link {
            text-align: center;
            margin-top: 15px;
        }
        .login-link a {
            text-decoration: none;
            color: #007bff;
        }
        .diagnosis-result {
            text-align: center;
            margin-top: 30px;
        }
        .doctor-info {
            text-align: center;
            margin-top: 20px;
        }
        .doctor-info p {
            font-weight: normal;
        }
        .appointment-section {
            display: none;
            margin-top: 20px;
        }
        .appointment-confirmation {
            display: none;
            text-align: center;
            margin-top: 30px;
            color: green;
        }
        .doctor-list {
            list-style-type: none;
            padding: 0;
        }
        .doctor-list li {
            margin-bottom: 10px;
            font-weight: bold;
        }
        .calendar {
            margin-top: 20px;
        }
        .calendar input {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <div class="container" id="registration-section">
        <h1>Register</h1>
        <form id="registration-form">
            <div class="form-group">
                <label for="reg-username">Username</label>
                <input type="text" id="reg-username" placeholder="Enter your username" required>
            </div>
            <div class="form-group">
                <label for="reg-email">Email</label>
                <input type="email" id="reg-email" placeholder="Enter your email" required>
            </div>
            <div class="form-group">
                <label for="reg-password">Password</label>
                <input type="password" id="reg-password" placeholder="Enter your password" required>
            </div>
            <div class="form-group">
                <button type="submit">Register</button>
            </div>
        </form>
        <div class="login-link">
            <p>Already have an account? <a href="#" id="login-link">Login</a></p>
        </div>
    </div>

    <!-- Login Section -->
    <div class="container" id="login-section" style="display: none;">
        <h1>Login</h1>
        <form id="login-form">
            <div class="form-group">
                <label for="login-username">Username</label>
                <input type="text" id="login-username" placeholder="Enter your username" required>
            </div>
            <div class="form-group">
                <label for="login-password">Password</label>
                <input type="password" id="login-password" placeholder="Enter your password" required>
            </div>
            <div class="form-group">
                <button type="submit">Login</button>
            </div>
        </form>
    </div>

    <!-- Symptom Description -->
    <div class="container" id="symptoms-section" style="display: none;">
        <h1>Describe Your Symptoms</h1>
        <div class="form-group">
            <textarea id="symptoms" placeholder="Describe your symptoms..." rows="5" required></textarea>
        </div>
        <div class="symptom-checkboxes">
            <label><input type="checkbox" class="symptom" value="fever"> Fever</label>
            <label><input type="checkbox" class="symptom" value="headache"> Headache</label>
            <label><input type="checkbox" class="symptom" value="cough"> Cough</label>
            <label><input type="checkbox" class="symptom" value="fatigue"> Fatigue</label>
        </div>
        <div class="form-group">
            <button id="check-symptoms-button">Check Symptoms</button>
        </div>
    </div>

    <!-- Diagnosis Result -->
    <div class="container" id="diagnosis-result" style="display: none;">
        <h2 style="font-weight: bold;">Diagnosis: <span id="diagnosis"></span></h2>
        <h3>Common Symptoms:</h3>
        <div>
            <input type="checkbox" disabled checked> Running nose<br>
            <input type="checkbox" disabled checked> Cough<br>
            <input type="checkbox" disabled checked> Sneezing<br>
            <input type="checkbox" disabled checked> Sore throat<br>
            <input type="checkbox" disabled checked> Headache<br>
            <input type="checkbox" disabled checked> Fever<br>
        </div>
        <div class="doctor-info">
            <p><b>Dr. Sarah Smith</b> - General Medicine</p>
            <p>Experience: 15 years</p>
            <p><b>Dr. James Wilson</b> - Family Medicine</p>
            <p>Experience: 12 years</p>
        </div>
        <div class="form-group">
            <button id="book-appointment-button">Book Appointment</button>
        </div>
    </div>

    <!-- Appointment Booking -->
    <div class="container appointment-section" id="appointment-section">
        <h1>Book an Appointment</h1>
        <ul class="doctor-list">
            <li><input type="radio" name="doctor" value="Dr. Sarah Smith"> Dr. Sarah Smith - General Medicine</li>
            <li><input type="radio" name="doctor" value="Dr. James Wilson"> Dr. James Wilson - Family Medicine</li>
        </ul>
        <div class="calendar">
            <label for="appointment-date">Select Date:</label>
            <input type="date" id="appointment-date" required>
        </div>
        <div class="calendar">
            <label for="appointment-time">Select Time:</label>
            <input type="time" id="appointment-time" required>
        </div>
        <div class="form-group">
            <button id="confirm-appointment-button">Confirm Appointment</button>
        </div>
    </div>

    <!-- Appointment Confirmation -->
    <div class="container appointment-confirmation" id="appointment-confirmation">
        <h2>Appointment Confirmed!</h2>
        <p id="confirmation-details"></p>
    </div>

    <script>
        // Registration functionality
        document.getElementById("registration-form").addEventListener("submit", function(e) {
            e.preventDefault();
            alert("Registration successful! Please log in.");
            document.getElementById("registration-section").style.display = "none";
            document.getElementById("login-section").style.display = "block";
        });

        // Login functionality
        document.getElementById("login-link").addEventListener("click", function() {
            document.getElementById("registration-section").style.display = "none";
            document.getElementById("login-section").style.display = "block";
        });

        document.getElementById("login-form").addEventListener("submit", function(e) {
            e.preventDefault();
            document.getElementById("login-section").style.display = "none";
            document.getElementById("symptoms-section").style.display = "block";
        });

        // Symptom Check functionality
        document.getElementById("check-symptoms-button").addEventListener("click", function() {
            const symptoms = [];
            document.query
