Title: Demonstrating Confidentiality through File Encryption and Decryption (OpenSSL)

Objective
To demonstrate data confidentiality
ensureing that the sensitive imformation can only be accessed by the authorized person by encrypting and decrypting a file using AES-256-CBC encryption with openSSL.

concept overview
Confidentially is one of the core principles of cybersecurity (CIA Tried: confidentality integrity and availability)
it ensures that data is hidden from unathorized access by using encryption techneques.
In This practcal,AES (Advance Encryption Standard) with a 256-bit key is used to protect the data making it unreadable without the correct password.

TOOL USED
Operating system:Kali linux
Encryption Algorithm:AES-256-CBC
Hash Algorithm: SHA-256(for integrity verification)

   step 1
   create a simple file with this command
   
   echo "this is a confidential report" > report.txt

EXPLANATION
A plain text file named report.txt is created containing sensitive information.
This is our original unprotected data.
step 2
now we will encrypt the File using AES-256-CBC

openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 -pass pass:DemoPass123 -in report.txt -out report.enc

COMMAND EXPLANATION

enc: Command to perform encryption or decryption.

-aes-256-cbc: Algorithm (AES encryption, 256-bit key, Cipher Block Chaining mode).

-salt: Adds randomness to strengthen encryption.

-pbkdf2: Modern key derivation method (more secure).

-iter 100000: Increases brute-force resistance.

-pass pass:DemoPass123: Defines password for encryption.

-in: Input file.

-out: Output encrypted file.

NOTE
now the report.enc is created unreadable without the key or password

STEP 3
cat report.enc

after running this command it will desplay the encrypted file content as we can see it in the given screenshot below

<img width="1366" height="662" alt="Screenshot_2025-10-28_11_40_10" src="https://github.com/user-attachments/assets/d7a609c2-770b-4a02-921e-9867313eb4db" />

appears as random binary or garbled text, proving the data is not readable.

STEP 4
now decrypt the file using the below command

openssl enc -d -aes-256-cbc -salt -pbkdf2 -iter 100000 -pass pass:DemoPass123 -in report.enc -out decrypted.txt

EXPLANATION
Decrypts the encrypted file back to its readable form using the same algorithm and password
after this a new file decrypted.txt is created containing the original text.

Step 5
now we will verify the decypted data  

cat decrypted.txt

Output:this is a confidential report
as you can see it in the screenshot

Explanation:
Shows that decryption successfully recovered the original data, confirming confidentiality was preserved.and now it protected

<img width="1366" height="662" alt="Screenshot_2025-10-28_12_53_14" src="https://github.com/user-attachments/assets/5514b370-9be0-4bcb-bec4-55e99cad2501" />


Step 6

Verify Integrity with SHA-256 Hash

to do that run these sommands separetly
sha256sum report.txt > before.sha256

sha256sum decrypted.txt > after.sha256

Explanation:
After running these commands it will Generates cryptographic hashes before and after encryption/decryption.
If both hashes match, it confirms data integrity 
the decrypted file is identical to the original.Generates cryptographic hashes before and after encryption/decryption.
If both hashes match, it confirms data integrity 
the decrypted file is identical to the original.

<img width="1366" height="662" alt="Screenshot_2025-10-28_12_53_14" src="https://github.com/user-attachments/assets/5514b370-9be0-4bcb-bec4-55e99cad2501" />

after that you can check
NOT RUN THESE COMMANDS SPERATELY AS SHOWN IN THE SCREENSHOT

cat before.sha256
cat after.sha256



Learning Outcome:

Understood how encryption ensures Confidentiality.

Used OpenSSL to perform AES-256 encryption and decryption.

Verified Integrity using SHA-256 hashing.

Demonstrated real-world encryption skills for a cybersecurity portfolio.
