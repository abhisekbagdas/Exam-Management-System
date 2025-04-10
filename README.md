# Exam-Management-System
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exam Seat Finder</title>
    <style>
        body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f8f9fa;
    margin: 0;
}
.container {
    text-align: center;
    width: 400px;
}
h1 {
    font-size: 28px;
    font-weight: bold;
    margin-bottom: 20px;
    color: #333;
}
input {
    width: 100%;
    padding: 12px;
    font-size: 16px;
    border-radius: 24px;
    border: 1px solid #ddd;
    outline: none;
    box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
}
button {
    margin-top: 15px;
    background-color: #4285f4;
    color: white;
    padding: 12px 20px;
    font-size: 16px;
    border: none;
    border-radius: 24px;
    cursor: pointer;
    transition: background 0.3s;
}
button:hover {
    background-color: #357ae8;
}
.result{
    margin-top: 50px;
    width: 200%;
    border-radius: 15px;
    height: 60px;
    margin-left: -200px;
    justify-content: start;
    display: flex;
    background: #85c8ff;
    z-index: inherit;
}
#result {
    width: 200%;
    justify-content: start;
    display: flex;
    margin-top: 20px;
    margin-left: 100px;
    font-size: 18px;
    font-weight: bold;
}
    </style>
</head>
<body>
    <div class="container">
        <h1>Exam Seat Finder</h1>
        <input type="text" id="studentName" placeholder="Enter Student Name">
        <button onclick="findSeat()">Find Seat</button>
        <div class="result">
            <p id="result"></p>
        </div>
    </div>
    <script>
        async function loadJSON() {
            const response = await fetch("data.json");
            const jsonData = await response.json();
            return jsonData;
        }
        async function findSeat() {
            const jsonData = await loadJSON();
            const studentName = document.getElementById("studentName").value.trim().toUpperCase();
            let result = "Name not found!";
            for (const hall in jsonData) {
                for (const seat in jsonData[hall].seats) {
                    const details = jsonData[hall].seats[seat];
                    if (details.student && details.student.toUpperCase() === studentName) {
                        result = `Student: ${details.student}, Seat: ${seat}, Hall: ${hall}, Coordinates: (${details.x}, ${details.y})`;
                        break;
                    }
                }
            }
            document.getElementById("result").innerText = result;
        }
    </script>
</body>
</html>
