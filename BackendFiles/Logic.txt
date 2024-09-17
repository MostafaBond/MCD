function generateKey() {
    const maxKey = 99999999; // Maximum 8-digit number
    const generatedKey = Math.floor(Math.random() * maxKey);
    document.getElementById('key').value = generatedKey;
}

function codeMessage() {
    const message = document.getElementById('message').value;
    const key = document.getElementById('key').value;

    if (message.trim() === '' || key.trim() === '') {
        alert('Please enter both message and key.');
        return;
    }

    let codedMessage = vigenereCipher(message, key);
    codedMessage = btoa(codedMessage); // Base64 encoding

    document.getElementById('result').value = codedMessage;
}

function decodeMessage() {
    const message = document.getElementById('message').value;
    const key = document.getElementById('key').value;

    if (message.trim() === '' || key.trim() === '') {
        alert('Please enter both coded message and key.');
        return;
    }

    let decodedMessage = vigenereDecipher(atob(message), key); // Base64 decoding and Vigenere decipher

    document.getElementById('result').value = decodedMessage;
}

function vigenereCipher(message, key) {
    let result = '';
    for (let i = 0; i < message.length; i++) {
        const charCode = (message.charCodeAt(i) + key.charCodeAt(i % key.length)) % 256;
        result += String.fromCharCode(charCode);
    }
    return result;
}

function vigenereDecipher(codedMessage, key) {
    let result = '';
    for (let i = 0; i < codedMessage.length; i++) {
        const charCode = (codedMessage.charCodeAt(i) - key.charCodeAt(i % key.length) + 256) % 256;
        result += String.fromCharCode(charCode);
    }
    return result;
}
