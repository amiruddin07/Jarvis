<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jarvis</title>
    <style>
body{
    background-color: cyan;
}
h1{
    color: red;
}

    </style>
</head>
<body>
<h1> Hello , I am Jarvis , Your Virtual Assistant , How Can I Help You ?</h1>
<div class="wrapper">
    <div class="actions">
        <button id="start">Talk</button>
        <button id="end">End</button>
    </div>
    <div id="transcript">
    </div>
</div>
<p>NOTE: This version is not completed yet, I am working on it.So, to start it 
    click on "talk" and on "end" it click on end
    You can only tell "YouTube" or "Facebook" or "Instagram"
</p>
<script>
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

const recognition = new SpeechRecognition();
recognition.interimResults = true;
const transcript_element = document.getElementById("transcript");
const talk_button = document.getElementById("start");
const end_button = document.getElementById("end");

let p = document.createElement("p");
transcript_element.appendChild(p);

recognition.addEventListener("result", (e) =>{
    const transcript = Array.from(e.results)
    .map(result => result [0])
    .map(result => result.transcript)
    .join("");
    p.textContent = transcript;
    if(e.results[0].isFinal){
        p = document.createElement("p")
        p.textContent = transcript;
        transcript_element.appendChild(p);
        p.textContent = "";

        if(transcript.includes("YouTube")){
            window.open('https://www.youtube.com/')
        }
        if(transcript.includes("Facebook")){
            window.open('https://www.facebook.com/')
        }
        if(transcript.includes("Instagram")){
            window.open('https://www.instagram.com')
        }
    }

});

recognition.addEventListener("end", ()=>{
    end_button.disabled = false;
    talk_button.disabled = true;
});
talk_button.addEventListener("click", () =>{
    end_button.disabled = false;
    talk_button.disabled = true;
    recognition.start();
});
end_button.addEventListener("click", () => {
    end_button.disabled = true;
    talk_button.disabled = false;
    recognition.stop();
});

</script>
</body>
</html>
