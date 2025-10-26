---
layout: crime-dinner
permalink: /crime-dinner/
nav: false
title: Crime Dinner
description: An elegant evening of mystery and intrigue
---

# The will of Samuel von Jung

<div class="content">
  <p>Dear friend, dear investigator, thanks for not giving up and arriving until here. Hopefully many aspects of my (foreseeable) passing away have been clarified by now. But probably a last mistery remains. 
  <br>
  This question that remains is: who did, in fact, kill me, Samuel von Jung? 
  <br>
  In order to solve this crime and reveal my will, you will need to pass this final test.</p>
  <div style="text-align: center;">
    <form id="caesarForm">

      <div style="margin-bottom: 20px;">
        <label for="key">Key Phrase: </label><br>
        <input type="text" 
               id="key" 
               name="key" 
               value="" 
               pattern="[A-Za-z ]+" 
               required 
               style="text-transform: uppercase;">
      </div>

      <!-- Only decryption is allowed per requirements; removed encrypt/decrypt selector -->

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

document.getElementById('caesarForm').addEventListener('submit', function(e) {
  e.preventDefault();
  // Encoded message is stored but not shown in UI
  var message = 'eocokaecdmvidvl! Yzc xawns eao vqdxgd hifupt nap jjvz. Iylwqf, cpxbtltaeo ptzfelbwe cla ttypzk ah ojz lonqwfa, sfcxekqfs ws aqde wmeaps.';
  var keyPhrase = document.getElementById('key').value;
  // Only allow decryption
  var isDecrypting = true;
  
  // Validate that key contains only letters and spaces
  if (!/^[A-Za-z ]+$/.test(keyPhrase)) {
    alert('Please enter only letters and spaces in the key');
    return;
  }

  // The saved first word of the decoded message (letters-only)
  var savedDecodedFirstWord = 'CONGRATULATIONS';

  // Perform decryption
  var result = multiKeyCaesarCipher(message, keyPhrase, isDecrypting);

  // Extract the first contiguous word of letters from the decrypted result
  var firstWordMatch = (result.match(/[A-Za-z]+/) || [''])[0].toUpperCase();

  var outEl = document.getElementById('encryptedText');
  // Only show the decrypted output if the first decoded word matches the saved one
  // Cancel any ongoing typewriter before starting a new reveal
  if (outEl._typewriterTimer) {
    clearInterval(outEl._typewriterTimer);
    outEl._typewriterTimer = null;
  }

  if (firstWordMatch === savedDecodedFirstWord) {
    // Typewriter reveal for the full decrypted result
    var typingText = result;
    outEl.textContent = '';
    var ti = 0;
    outEl._typewriterTimer = setInterval(function() {
      outEl.textContent += typingText.charAt(ti);
      ti++;
      if (ti >= typingText.length) {
        clearInterval(outEl._typewriterTimer);
        outEl._typewriterTimer = null;
      }
    }, 40); // ms per character
  } else {
    // Typewriter reveal for incorrect answer
    var typingText = 'Incorrect answer';
    outEl.textContent = '';
    var ti = 0;
    outEl._typewriterTimer = setInterval(function() {
      outEl.textContent += typingText.charAt(ti);
      ti++;
      if (ti >= typingText.length) {
        clearInterval(outEl._typewriterTimer);
        outEl._typewriterTimer = null;
      }
    }, 10); // ms per character
  }
});
</script>
