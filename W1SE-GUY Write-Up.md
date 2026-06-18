W1seGuy TryHackMe Walkthrough: It's As Simple As Can Be!

For new people to cybersecurity or cryptography, encryption rooms may seem a bit daunting at first. In this walkthrough, we are going to be simplifying the W1seGuy room on TryHackMe using the most basic of terms. No complex math needed!

--
The Task

Upon connection to the target, we're met with a network port to which we can connect. Upon connection, we're given a huge string of random characters and numbers (a Hexadecimal string) that are explained as follows: "Here is an encrypted message. If you can find the 5-character password (key) it's been encrypted with, I'll give you your prize."

---

The Basic Idea: How XOR works.

The server is using a very common digital form of locking known as an XOR cipher.

XOR works a bit like a very specific light switch:

*   If we take our secret message (Plaintext) and "flip" it using a secret password (Key), it is converted into incomprehensible garbage (Ciphertext).
*   The beautiful part of XOR is that it is completely reversible. If we take that unreadable garbage (Ciphertext) and flip it again using the same Key, we are left with our original message again!

The flaw in the plan: A Known-Plaintext Attack

Normally, breaking encryption would be nearly impossible without knowing the password. We are given a massive hint, though: We know what the message starts with.

Every TryHackMe flag starts with: THM{.

Because of how XOR math works, if we take the encrypted gibberish and combine it with our known plain text (THM{), we can reverse the encryption and get our password! This type of attack is called a Known-Plaintext Attack.

---

Step-by-Step Instructions

Step 1: Connecting to the Target Machine

We will use the netcat (nc) tool within our Linux terminal to make a live connection to the room's server. We will use the following command, substituting the placeholder with your target IP:

``bash
nc <TARGET_IP> 1337
The server immediately responds with a very long string encoded in Hexadecimal. Keep this terminal window open.

---

Step 2: Unlocking the Secret Key

Instead of writing our own scripts, we'll be using an online tool called CyberChef (sometimes referred to as the cyber Swiss-Army knife).

1.  Copy the first 8 characters of the string that the server gave you. (8 hex characters are equivalent to the first 4 letters of the encrypted message.)
2.  Go to the CyberChef website.
3.  Paste these 8 characters into the Input box (the top right box).
4.  Search for From Hex on the left-hand menu, and drag it into the middle box. This removes the basic formatting.
5.  Now, search for the XOR operation, and drag it into the middle box below the previous operation.
6.  In the settings that pop up for the XOR operation:
    *   Set the Key Type dropdown to UTF-8.
    *   In the box that appears, type in our known starting text: THM{.

7.  The Output box will immediately display the first 4 characters of the server's password!

---

Step 3: Finding the Last Character

The server claims the password is 5 characters long, but we've only revealed the first 4. We need to find the 5th character.

1.  Clear the Input box on CyberChef, and paste the full, long string of Hex characters back into it.
2.  Go back to the XOR box in the middle section.
3.  In the key box, type the 4 characters we found in Step 2.
4.  Remove the THM{ that you have used earlier and only type the 4 characters
5.  After typing these 4 characters, simply start typing random keyboard characters (letters, numbers, etc.). The 5th character, when correctly entered, will cause the entire gibberish to become legible English text, starting with THM{`.

Congratulations! You've cracked the cipher. The legible text that appears in the Output box is Flag 1.

---

Step 4: Retrieving Flag 2

Now that we know the 5-character secret password:

1.  Go back to the terminal window where we're still connected to the server.
2.  Type or paste the exact 5-character password into the prompt.
3.  Press Enter.

The server will acknowledge that we've cracked it and display Flag 2 directly to your terminal.

You can now submit both flags to the room page to claim completion!
