# Dashboard-project
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Appointment Booker</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        form { max-width: 400px; margin: auto; }
        label { display: block; margin-top: 10px; }
        input, button { width: 100%; padding: 8px; margin-top: 5px; }
        button { background: #007bff; color: white; border: none; cursor: pointer; }
        button:hover { background: #0056b3; }
        #appointments { margin-top: 20px; }
        .appointment { border: 1px solid #ccc; padding: 10px; margin: 5px 0; }
    </style>
</head>
<body>
    <h1>Book an Appointment</h1>
    <form id="appointmentForm">
        <label for="name">Name:</label>
        <input type="text" id="name" required>
        
        <label for="email">Email:</label>
        <input type="email" id="email" required>
        
        <label for="date">Date:</label>
        <input type="date" id="date" required>
        
        <label for="time">Time:</label>
        <input type="time" id="time" required>
        
        <button type="submit">Book Appointment</button>
    </form>
    
    <h2>Your Appointments</h2>
    <div id="appointments"></div>
    
    <script>
        const form = document.getElementById('appointmentForm');
        const appointmentsDiv = document.getElementById('appointments');
        
        // Load existing appointments from localStorage
        let appointments = JSON.parse(localStorage.getItem('appointments')) || [];
        displayAppointments();
        
        form.addEventListener('submit', (e) => {
            e.preventDefault();
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const date = document.getElementById('date').value;
            const time = document.getElementById('time').value;
            
            const appointment = { name, email, date, time };
            appointments.push(appointment);
            localStorage.setItem('appointments', JSON.stringify(appointments));
            displayAppointments();
            form.reset();
            alert('Appointment booked!');
        });
        
        function displayAppointments() {
            appointmentsDiv.innerHTML = '';
            appointments.forEach((appt, index) => {
                const div = document.createElement('div');
                div.className = 'appointment';
                div.innerHTML = `<strong>${appt.name}</strong> - ${appt.email} - ${appt.date} at ${appt.time} 
                    <button onclick="deleteAppointment(${index})">Delete</button>`;
                appointmentsDiv.appendChild(div);
            });
        }
        
        function deleteAppointment(index) {
            appointments.splice(index, 1);
            localStorage.setItem('appointments', JSON.stringify(appointments));
            displayAppointments();
        }
    </script>
</body>
</html>
