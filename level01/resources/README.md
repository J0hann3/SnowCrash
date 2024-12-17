find / -type f -exec grep -H "flag01" {} + 2>/dev/null; # The command search in every normal file if it contains the word `flag01`

# The file `/etc/passwd` contains the password of the flag01
# The flag is encrypted in DES(Data Encryption Standard)
# With `John The Riper` I decrypted the password to get `abcdefg`
