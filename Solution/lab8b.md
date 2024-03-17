# Solution to Lab8b

## Encryption and Decryption

1. Use command `gpg --decrypt file1.txt.gpg`, the content is "Quack".
2. `gpg --import`

3. `gpg --armor --export [KEY_ID] > publickey.asc`
4. `gpg --list-keys`

5. First run `gpg --import lab8privkey`, then `gpg --decrypt file2.txt.gpg`, and the content is "Woof".

## Hashing (Checksums)

1. ddbefc9c1d8a8d9195a420a7181352e9

2. e9f61163d7265caa71877eb8e76726f906f6cfeb

## File Security

1. `-rw-r--r--  1 nobody   mygroup`, this means user "nobody" has read and write permission. Other members in the group and the others only have read permission.
2. The content is "aching flair".
3. `sudo chown your_username file6.txt`
4. `chmod 400 file7.txt`
5. `sudo chown root:root file8.txt` and `sudo chmod 400 file8.txt`
6. `sudo chown your_username file9.txt` and `chmod 400 file9.txt`
