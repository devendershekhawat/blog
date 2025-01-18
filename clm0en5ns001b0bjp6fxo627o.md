---
title: "Making browsers speak entered text using javascript"
seoTitle: "Making browsers speak entered text using javascript"
seoDescription: "Build a text-to-speech web app with SpeechSynthesisUtterance API, voice selection, input, and HTML, CSS, JavaScript integration using WebSpeech API"
datePublished: Fri Sep 01 2023 09:40:52 GMT+0000 (Coordinated Universal Time)
cuid: clm0en5ns001b0bjp6fxo627o
slug: making-browsers-speak-entered-text-using-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693561173462/02c479d2-2377-43d0-aa29-e7dfe09c81ae.png
tags: javascript, web-development, webdev, html5, frontend-development

---

The SpeechSynthesisUtterance API is a powerful tool that allows developers to incorporate text-to-speech functionality into their web applications. This API enables users to select a voice from available options and convert text into spoken words. In this article, we'll walk through the process of creating a simple web app that lets users select a voice from a dropdown menu and play the entered text using the SpeechSynthesisUtterance API.

### **Prerequisites**

Before we dive into building the web app, make sure you have a basic understanding of HTML, CSS, and JavaScript. Additionally, ensure that your browser supports the SpeechSynthesisUtterance API. Most modern browsers, including Chrome, Firefox, and Edge, support this API.

### **Setting Up the HTML Structure**

Let's start by creating the basic HTML structure for our web app.

```xml
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text-to-Speech App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Text-to-Speech App</h1>
    <div class="controls">
        <label for="voice-select">Select a Voice:</label>
        <select id="voice-select"></select>
        <input type="text" id="text-input" placeholder="Enter text...">
        <button id="speak-button">Speak</button>
    </div>
    <div id="output"></div>
    <script src="script.js"></script>
</body>
</html>
```

In the above code, we've created an HTML structure with a title, a dropdown to select voices, an input box to enter text, a button to trigger speech synthesis, and a container to display the spoken output.

### **Styling with CSS**

You can add some CSS styles to make your app visually appealing. Create a `styles.css` file and link it to your HTML file.

```css
/* styles.css */
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
}

h1 {
    color: #333;
}

.controls {
    margin: 20px auto;
    width: 80%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

label {
    font-weight: bold;
    margin-bottom: 10px;
}

select, input, button {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
}

#output {
    margin: 20px auto;
    width: 80%;
    border: 1px solid #333;
    padding: 10px;
    min-height: 100px;
}
```

This CSS code provides a clean and organized layout for your web app.

### **JavaScript for Text-to-Speech**

Now, let's create the JavaScript logic to make our web app functional. Create a `script.js` file and add the following code:

```javascript
// script.js
document.addEventListener('DOMContentLoaded', () => {
    const voiceSelect = document.getElementById('voice-select');
    const textInput = document.getElementById('text-input');
    const speakButton = document.getElementById('speak-button');
    const outputDiv = document.getElementById('output');
    let synth = window.speechSynthesis;

    // Populate the voice dropdown with available voices
    function populateVoiceList() {
        const voices = synth.getVoices();
        voiceSelect.innerHTML = '';

        voices.forEach((voice, index) => {
            const option = document.createElement('option');
            option.textContent = `${voice.name} (${voice.lang})`;
            option.setAttribute('data-index', index);
            voiceSelect.appendChild(option);
        });
    }

    // Initialize the voice dropdown
    populateVoiceList();

    // Handle button click to speak the entered text
    speakButton.addEventListener('click', () => {
        const selectedVoiceIndex = voiceSelect.options.selectedIndex;
        const selectedVoice = synth.getVoices()[selectedVoiceIndex];
        const textToSpeak = textInput.value;

        const utterance = new SpeechSynthesisUtterance(textToSpeak);
        utterance.voice = selectedVoice;

        synth.speak(utterance);

        // Display the spoken text
        outputDiv.textContent = `Spoken: ${textToSpeak}`;
    });
});
```

In this JavaScript code, we first wait for the DOM to load using the `DOMContentLoaded` event listener. We then get references to the necessary HTML elements, populate the voice dropdown with available voices, and handle the button click event to initiate text-to-speech synthesis.

### **Testing the App**

To test your web app, simply open the HTML file in a modern web browser that supports the SpeechSynthesisUtterance API. You can enter text in the input box, select a voice from the dropdown, and click the "Speak" button to hear the text spoken in the selected voice.

Congratulations! You've created a simple web app using the SpeechSynthesisUtterance API that allows users to select a voice and convert text into speech. You can further enhance this app by adding features like pausing or stopping speech synthesis or providing additional voice-related options.

---

> ***Follow me on*** [***twitter***](https://twitter.com/devcodesthings) ***to stay in touch. You can find my writings at*** [***devshekhawat.com***](http://devshekhawat.com)***. Also, subscribe to the newsletter here to get daily updates on 💻 web development, ☀️ life and 📚 productivity.***