---
layout: crime-dinner
permalink: /crime-dinner/
nav: false
title: Crime Dinner
description: An elegant evening of mystery and intrigue
---

# The will of Samuel von Jung

<div class="content" style="text-align: center;">
  <p>Dear friend, thanks for arriving until here. Hopefully many aspects of my passing away have been clarified by now. But most likely a last mistery remains: 
  <br><br>
  Who did, in fact, committed the crime? 
  <br><br>
  This page will reveal my will once our suspicions about the killer align. 
  Please vote to decide who is most likely to be blamed.</p>
  <div style="text-align: center;">
    <form id="caesarForm">

      <div style="margin-bottom: 20px;">
        <input type="text" 
               id="key" 
               name="key" 
               value="" 
               placeholder="Insert a single word"
               pattern="[A-Za-z ]+" 
               required 
               style="text-transform: uppercase;">
      </div>
      <button type="submit">Submit</button>
    </form>
    <p><span id="encryptedText" aria-live="polite"></span></p>
    <style>
    /* small jitter animation used when answer is incorrect */
    .jitter{animation:jitter 0.36s ease-in-out}
    @keyframes jitter{
      0%{transform:translateX(0)}
      20%{transform:translateX(-3px)}
      40%{transform:translateX(3px)}
      60%{transform:translateX(-2px)}
      80%{transform:translateX(2px)}
      100%{transform:translateX(0)}
    }
    </style>
  </div>
</div>
<script>
function letterToNumber(letter) {
  // Convert letter to uppercase and get its position in alphabet (A=0, B=1, etc)
  return letter.toUpperCase().charCodeAt(0) - 65;
}

function caesarShift(char, shift, isDecrypting) {
  if (!/[A-Za-z]/.test(char)) return char; // Return unchanged if not a letter
  
  // If decrypting, reverse the shift direction
  if (isDecrypting) shift = -shift;
  
  const base = char >= 'a' ? 97 : 65;
  return String.fromCharCode((char.charCodeAt(0) - base + shift + 26) % 26 + base);
}

function multiKeyCaesarCipher(str, keyPhrase, isDecrypting = false) {
  // Remove spaces and non-alphabetic characters from key
  const cleanKey = keyPhrase.toUpperCase().replace(/[^A-Z]/g, '');
  if (cleanKey.length === 0) return str;

  let result = '';
  let j = 0; // Counter for letters only (skipping spaces and special chars)

  for (let i = 0; i < str.length; i++) {
    if (/[A-Za-z]/.test(str[i])) {
      // Only increment j when we process a letter
      const keyChar = cleanKey[j % cleanKey.length];
      const shift = letterToNumber(keyChar);
      result += caesarShift(str[i], shift, isDecrypting);
      j++;
    } else {
      // For non-letters, just append without shifting
      result += str[i];
    }
  }
  return result;
}

// Make the placeholder disappear immediately on focus (click) and restore on blur if left empty.
var keyInput = document.getElementById('key');
if (keyInput) {
  keyInput.addEventListener('focus', function() {
    // save the placeholder text and clear it so it disappears on click/focus
    this.dataset._ph = this.placeholder;
    this.placeholder = '';
  });
  keyInput.addEventListener('blur', function() {
    // restore placeholder only if the field is still empty
    if (this.value.trim() === '') {
      this.placeholder = this.dataset._ph || 'Insert a single word';
    }
  });
}

// Load encoded messages when the page loads
var encodedData = {
  encodedMessages: ['ZINCS PGVNU'],
  expectedFirstWords: ['HELLO']
};

fetch('/assets/data/encoded_messages.json')
  .then(response => response.json())
  .then(data => {
    encodedData = data;
  })
  .catch(error => {
    console.error('Error loading encoded messages:', error);
    // Fallback message is already set in encodedData
  });

document.getElementById('caesarForm').addEventListener('submit', function(e) {
  e.preventDefault();
  var keyPhrase = document.getElementById('key').value;
  // Only allow decryption
  var isDecrypting = true;
  
  // Validate that key contains only letters and spaces
  if (!/^[A-Za-z ]+$/.test(keyPhrase)) {
    alert('Please enter only letters and spaces in the key');
    return;
  }

  // Try each message-firstWord pair
  var foundMatch = false;
  var matchedResult = '';

  for (var i = 0; i < encodedData.encodedMessages.length; i++) {
    var result = multiKeyCaesarCipher(encodedData.encodedMessages[i], keyPhrase, isDecrypting);
    var firstWordMatch = (result.match(/[A-Za-z]+/) || [''])[0].toUpperCase();

    if (firstWordMatch === encodedData.expectedFirstWords[i]) {
      foundMatch = true;
      matchedResult = result;
      break;
    }
  }

  var outEl = document.getElementById('encryptedText');
  // Cancel any ongoing typewriter before starting a new reveal
  if (outEl._typewriterTimer) {
    clearInterval(outEl._typewriterTimer);
    outEl._typewriterTimer = null;
  }

  if (foundMatch) {
    // Typewriter reveal for the full decrypted result
    var typingText = matchedResult;
    outEl.textContent = '';
    var ti = 0;
    outEl._typewriterTimer = setInterval(function() {
      outEl.textContent += typingText.charAt(ti);
      ti++;
      if (ti >= typingText.length) {
        clearInterval(outEl._typewriterTimer);
        outEl._typewriterTimer = null;
      }
    }, 20); // ms per character
  } else {
    // Custom error message incorporating the tried key
    var typingText = keyPhrase.toUpperCase() + '? What does ' + keyPhrase.toUpperCase() + ' have to do with all of this?';
    outEl.textContent = '';
    var ti = 0;
    outEl._typewriterTimer = setInterval(function() {
      outEl.textContent += typingText.charAt(ti);
      ti++;
      if (ti >= typingText.length) {
        clearInterval(outEl._typewriterTimer);
        outEl._typewriterTimer = null;
      }
    }, 20); // ms per character
  }
});
</script>
