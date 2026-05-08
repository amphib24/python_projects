import hashlib

#user selects wordlist and hash
wordlist = input('Enter wordlist file path:')
hash_input = input('Please enter the hash you want cracked:')

print('Available algorithms:',hashlib.algorithms_guaranteed)
algo = input('Please select the hash algorithm youd like to use from the list above:').lower()

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
