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

*** Note: This explanation is outdated. For an accurate explanation, you'll need to read the JavaScript. ***

To encrypt messages by hand, you'll need a [shared secret](https://en.wikipedia.org/wiki/Shared_secret) and a unique identifier for the message. It is encouraged to choose both the secret, and the message identifier, as randomly as you (reasonably) can. The message identifier functions as an [iv](https://en.wikipedia.org/wiki/Initialization_vector).
The IV is optional (but recommended), and if not specified defaults to a single letter "A", which functions as not modifying the message (In the Vigenere cipher, an "A" combined with any letter is the same letter).

There are a few things to know before encrypting a message:
- The key should be one or more words. The JavaScript code provided only handles messages written primarily in English, or another language with the English alphabet. Any non-English characters are left as-is after encryption.
	- The key can (and should) be more than 1 English word. They should also have varying lengths, since this will increase the effective length of the key. The effective length of the keys "cat" and "dog" is only 3 letters, while the effective length of "cat" and "dogs" is 12. You calculate the effective length by taking the [least common multiple](https://en.wikipedia.org/wiki/Least_common_multiple) of the key lengths.
- The IV should also be more than 1 word, but an IV containing more words than the key will have some of the words ignored.



#### Steps for *En*crypting a message:

- Encrypt the key using the Vigenere cipher. The key will take the place of the Vigenere cipher's *plaintext*, and the *key* will be the first word in the IV. Once encrypted, this will be the ***encrypted key***.
- In each round, you'll perform the following steps:
	
	- Take the corresponsing word within the IV: (for the odd-numbered rounds) put it *before* the corresponsing word on the key, and (for the even-numbered rounds) put the IV after the key. This will be the ***round key***. For example:
		- For the key "`salmon tastes great`" and IV "`yeah it does`", the round key would be "`yeah salmon`" for the first round.
		- For the second round, the round key would then be "`tastes it`" using the same key and IV.

	- Perform the Vigenere encryption on the plaintext of your message. Once done, the result becomes the plaintext input for the next round.

- Once you've gone through every word in the key, you have your encrypted message. Send it to whoever you want.



#### Steps for *De*crypting a message:

The steps to decrypt a message are the same as the encryption steps, but you do the rounds in reverse order. Also, you use the Vigenere *de*cryption instead of *en*cryption.



### Example:

To encrypt the message "`My name is John`" with the key "`salmon tastes great`" and the IV "`yeah it does`":

- Encrypt the words "`salmon tastes great`" with the key "`yeah`", using the Vigenere cipher. The key is now "`qeltmr thqxez evehr`"
- (Round 1) Add the first word of the IV to the beginning of the new key (1 is an odd number), and use that as your round key "`yeahqeltmr`"
- Encrypt the message "My name is John" with the key "`yeahqeltmr`"
    - For round 1, it's a modified version of the Vigenere cipher. Rounds 2+ use the standard version.
        - Every time you encrypt a letter, add the encrypted letter to the end of the key, after shifting it 1 place.
        - For example, if you already have the key "`ab`" and the next letter of ciphertext is "`b`", the key becomes "`abc`" (note that "**c**" was added, not "**b**").
            - This makes sure the *effective key length* is at least as long as the message, preventing certain attacks on the encryption.
    - The result should be "`Kc nhci tl Vfsq`"

- (Round 2) Add the second word of the IV, "`it`" to the *end* (since round 2 is even-numbered) of the second word of the (encrypted) key, "`thqxez`", getting "`thqxezit`"
- Encrypt "`Kc nhci tl Vfsq`" with the key "`thqxezit`"
    - This time, you just use standard Vigenere encryption. Only round 1 is different.

- ***Repeat the process until you've completed all rounds...***

- Once you're done, the *final result* of your encryption should be the ciphertext "`Gx hwkc fl Fpwr`"



	- Try doing this yourself to see if you're doing it right. You can also use the JavaScript encryption/decryption tool to test your skills with other messages. Once you get the hang of it, it should be fairly easy!
	- Make sure to practice both encrypting *and* decrypting messages.
	- If you can read JavaScript, the encryption code can be found in the `evanescence_encrypt(...)` and `evanescence_decrypt(...)` functions, when you download the tool.



#### Copyright (c) 2019 Alex Anderson. All rights reserved.
