# Hash Cracker 

## Description
This is an educational Python project to demonstrate coding skills and a general understanding of password auditing and hash verification.

## Disclaimer
This was designed for educational purposes only and is not intended for illegal or malicious use of any kind.

## Features
   - MD5 hash cracking
   - SHA1 hash cracking
   - SHA256 hash cracking
   - Wordlist-based password matching
   - Command-line interaction

```python
import hashlib

#user selects wordlist and hash
wordlist = input('Enter wordlist file path:')
hash_input = input('Please enter the hash you want cracked:')

print('Available algorithms:',hashlib.algorithms_guaranteed)

#Prompt until valid algorithm is entered( modify this in to replace the current block of code below)
while True:
    algo = input('Select the hash algorithm you’d like to use: ').lower()
    if algo in hashlib.algorithms_available:
        break
    else:
        print(f"Invalid choice '{algo}'. Please select one of the supported algorithms.")
try:
    with open(wordlist, 'r') as file:
        for line in file:
            #get rid of whitespace and encode the string
            data = line.strip().encode()

            #create hash object using selected algo
            try:
               hash = hashlib.new(algo,data)
            except ValueError:
               print('Invalid algo choice: {algo}')
               exit(1)

            hashed_password = hash.hexdigest()
        
            #compare hash to input
            if hashed_password == hash_input:
                print('Clear text password:' + line.strip())
                exit(0)
    print('No luck')
except FileNotFoundError:
    print('Wordlist not found, try again')
```
