<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jarvis Mobile Assistant</title>
<a href="index-.html">Open Agent Page</a>
<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #020617, #0f172a);
    color: white;
    text-align: center;
}
.container {
    padding: 30px 15px;
}
h1 {
    color: #38bdf8;
}
#status {
    margin-top: 10px;
    color: #94a3b8;
}
button {
    margin-top: 25px;
    padding: 15px 25px;
    font-size: 18px;
    background: #22c55e;
    border: none;
    border-radius: 12px;
    color: white;
    cursor: pointer;
}
.box {
    margin-top: 30px;
    background: #1e293b;
    padding: 20px;
    border-radius: 15px;
}
h3 { color: #38bdf8; }
p { min-height: 24px; }
</style>
</head>

<body>

<div class="container">
    <h1>🤖 Jarvis Mobile Assistant</h1>
    <p id="status">Tap the button and speak...</p>

    <button onclick="startListening()">🎤 Start Jarvis</button>

    <div class="box">
        <h3>You said:</h3>
        <p id="userText">...</p>

        <h3>Jarvis Response:</h3>
        <p id="jarvisText">Waiting...</p>
    </div>
</div>

<script>
const status = document.getElementById("status");
const userText = document.getElementById("userText");
const jarvisText = document.getElementById("jarvisText");

function startListening() {
    const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

    if (!SpeechRecognition) {
        alert("Use Chrome browser on mobile");
        return;
    }

    const recognition = new SpeechRecognition();
    recognition.lang = "en-US";

    status.innerText = "Listening... 🎧";
    recognition.start();

    recognition.onresult = function(event) {
        const transcript = event.results[0][0].transcript.toLowerCase();
        userText.innerText = transcript;
        processCommand(transcript);
    };

    recognition.onend = function() {
        status.innerText = "Tap the button and speak...";
    };
}

function speak(text) {
    const speech = new SpeechSynthesisUtterance(text);
    speech.rate = 1;
    window.speechSynthesis.speak(speech);
}

function processCommand(command) {
    let response = "Sorry KK, I didn't understand.";

    if (command.includes("hello") || command.includes("hi")) {
        response = "Hello KK! Jarvis ready.";
    }

    else if (command.includes("time")) {
        response = "The time is " + new Date().toLocaleTimeString();
    }

    else if (command.includes("date")) {
        response = "Today is " + new Date().toDateString();
    }

    else if (command.includes("open youtube")) {
        response = "Opening YouTube";
        window.open("https://www.youtube.com", "_blank");
    }

    else if (command.includes("open google")) {
        response = "Opening Google";
        window.open("https://www.google.com", "_blank");
    }

    else if (command.includes("search")) {
        let query = command.replace("search", "").trim();
        response = "Searching for " + query;
        window.open("https://www.google.com/search?q=" + query, "_blank");
    }

    else if (command.includes("play music")) {
        response = "Playing music";
        window.open("https://www.youtube.com/results?search_query=music", "_blank");
    }

    else if (command.includes("weather")) {
        response = "Showing weather report";
        window.open("https://www.google.com/search?q=weather", "_blank");
    }

    else if (command.includes("calculator")) {
        response = "Opening calculator";
        window.open("https://www.google.com/search?q=calculator", "_blank");
    }

    else if (command.includes("who are you")) {
        response = "I am Jarvis, your mobile AI assistant.";
    }

    jarvisText.innerText = response;
    speak(response);
}
</script>

</body>
</html>
