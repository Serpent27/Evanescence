# Evanescence

A cipher-suite based on a combination of the [Vigenere cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher) and an [Autokey cipher](https://en.wikipedia.org/wiki/Autokey_cipher). The Evanescence cipher encryption/decryption tool is written in JavaScript, and the cipher itself is designed to be usable purely by hand.

## You can use the tool by visiting [cipher.serpentsec.com](http://cipher.serpentsec.com/)
- **The tool has been tested on the following devices:**
    - ***Google Chrome** (version 74.0.3729.131 on **Windows 10**)*
    - ***Firefox** (version 66.0.3 on **Windows 10**)*
    - ***Safari** (on **iPhone 6s**)*
    - *Google Chrome* (version 74.0.3729.136 on *Google Pixel 2 XL*)
    - *Firefox* (version 66.0.5 on *Google Pixel 2 XL*)
    - *Firefox* 65.0.1 on Linux 4.19.0 (Parrot OS, based on Debian)
    - *Chromium* 73.0.3683.75 on Linux 4.19.0 (Parrot OS, based on Debian)

- *If the tool doesn't work, try switching browsers.* Firefox is recommended, but it should work on any modern web browser, including on **phones**!



#### How to encrypt messages:

To encrypt messages by hand, you'll need a [shared secret](https://en.wikipedia.org/wiki/Shared_secret)[key] and a personal secret, unique to each recipient. It is encouraged to choose both the secret [key], and the personal secret, as randomly as you (reasonably) can. The personal secret functions as an [iv](https://en.wikipedia.org/wiki/Initialization_vector).
The personal secret is optional (but recommended), and if not specified defaults to a single letter "A", which functions as not modifying the message (In the Vigenere cipher, an "A" combined with any letter is the same letter).

There are a few things to know before encrypting a message:
- The key should be one or more words. The JavaScript code provided only handles messages written primarily in English, or another language with the English alphabet. Any non-English characters are left as-is after encryption.
	- The key can (and should) be more than 1 English word. They should also have varying lengths, since this will increase the effective length of the key. 
	- The key should be changed with each message.
- The personal secret should also be more than 1 word. Longer keys = better. The personal secret should be unique to each recipient. For example, Alice would give Bob a different personal secret than she gives to Charlie.


#### A step-by-step guide to encryption/decryption is available within the app

- Try encrypting and decrypting yourself to see if you're doing it right. You can also use the JavaScript encryption/decryption tool to test your skills with other messages. Once you get the hang of it, it should be fairly easy!
- Make sure to practice both encrypting *and* decrypting messages.
- If you can read JavaScript, the encryption code can be found in the `evanescence_encrypt(...)` and `evanescence_decrypt(...)` functions, when you download the tool.

