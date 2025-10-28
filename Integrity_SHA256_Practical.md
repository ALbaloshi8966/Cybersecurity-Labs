Integrity Verification Practical (SHA-256 Hash Check)


STEP 1

COMMANDS 
mkdir -p cybersecurity-Lab/integrity_SHA256
cd cybersecurity-Lab/integrity_SHA256

EXPLANATION
A clean and organized folder was created to store all files related to the integrity test. 
This keeps the practical organized and makes it easy for reviewers to navigate.

STEP 2

Create the original test file

cat > integrity_test.txt <<'EOF'
This is Kaleem's original integrity test file.
This file will be used to demonstrate SHA-256 integrity checking.
EOF

EXPLANATION
after running these commands  it will creat a sample text file was created to act as the “original” file. 
This is the baseline data whose integrity will be verified later.


STEP 3
TO  Display the file content we run the following commands

echo "---- integrity_test.txt ----"
cat integrity_test.txt

SCREENSHOT
<img width="1366" height="662" alt="Screenshot_2025-10-28_18_51_34" src="https://github.com/user-attachments/assets/ba27ea8c-2a69-4ee4-86a1-8dd1f6f8bd7d" />

NOTE RUNN THESE COMMADNS SEPARATELY

Explanation:
this step will  shows the original file content before any changes.
It ensures the file was created successfully and helps document what the unmodified data looks like.

Step 4 

in this step we will Generate and save the original SHA-256 hash

sha256sum integrity_test.txt | tee original_sha256_sha256sum.txt

Explanation:
A cryptographic fingerprint (SHA-256 hash) was generated for the original file.
This hash uniquely represents the file’s contents and will be used later to detect any tampering.


Step 5

Now Generate and save the original SHA-256 hash using OpenSSL

openssl dgst -sha256 integrity_test.txt | tee original_sha256_openssl.txt

Explanation:
in this step demonstrates another tool (OpenSSL) to calculate the same SHA-256 hash. 
It shows versatility in using multiple command-line tools for verification.

as these steps are clearly shown in the screenshot below

<img width="1366" height="662" alt="Screenshot_2025-10-28_18_51_44" src="https://github.com/user-attachments/assets/6718a796-f698-478e-80d6-112a187ab4cc" />


Step 6

Display the saved original hash file

echo "---- original_sha256_sha256sum.txt ----"
cat original_sha256_sha256sum.txt

Explanation:

The saved hash file is displayed to record and verify the original hash value.
This serves as the reference point for comparison later.

Step 7
Now Simulate tampering

echo 'This line was added by an attacker!' >> integrity_test.txt

Explanation:

After running this command a new line was added to the file to simulate an unauthorized modification.
This helps demonstrate how even a small change in data alters its hash.

Step 8

Display the modified file  that is created already

echo "---- integrity_test.txt (after modification) ----"

now move into that directory by putting the command

cat integrity_test.txt

Explanation:
The file is displayed again to show the added line, confirming that tampering occurred.
This visual check proves that the file’s contents are no longer the same.

Step 9

Generate a new SHA-256 hash after modification

sha256sum integrity_test.txt | tee modified_sha256_sha256sum.txt

Explanation:

A new hash value was generated for the modified file. 
Since the content changed, this hash will differ from the original, proving loss of integrity.

Step 10

Display both hashes for comparison run all these commands one by one 

echo "Original (sha256sum):"
cat original_sha256_sha256sum.txt
echo
echo "Modified (sha256sum):"
cat modified_sha256_sha256sum.txt

Explanation:

Both the original and modified hash values are displayed side by side to visually compare them. 
The mismatch between them indicates data alteration.

Step 11

Verify the difference programmatically

diff original_sha256_sha256sum.txt modified_sha256_sha256sum.txt || echo "Hashes differ — integrity violated"

Explanation:
This command checks for differences between the two hash files. 
When they don’t match, a message appears confirming “Hashes differ — integrity violated.” This clearly shows that the file’s integrity has been compromised.

Step 12
this step is to Create a verification file for others its opetional step

sha256sum integrity_test.txt > integrity_test.txt.sha256

A .sha256 verification file is created so others can verify the file’s authenticity using this saved hash in the future.

<img width="1366" height="662" alt="Screenshot_2025-10-28_18_55_28" src="https://github.com/user-attachments/assets/d5917836-a8b4-4271-a75b-c876969050e8" />

SCREENSHOTS INCLUDED


<img width="1366" height="662" alt="Screenshot_2025-10-28_18_51_34" src="https://github.com/user-attachments/assets/ba27ea8c-2a69-4ee4-86a1-8dd1f6f8bd7d" />
<img width="1366" height="662" alt="Screenshot_2025-10-28_18_51_44" src="https://github.com/user-attachments/assets/6718a796-f698-478e-80d6-112a187ab4cc" />

<img width="1366" height="662" alt="Screenshot_2025-10-28_18_55_28" src="https://github.com/user-attachments/assets/d5917836-a8b4-4271-a75b-c876969050e8" />



