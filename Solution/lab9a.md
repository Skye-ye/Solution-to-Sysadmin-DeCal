# Solution to Lab9a

## Task 2 - Symmetric Encryption

1. "(´・ω・`)"

2. `gpg --cipher-algo TWOFISH --symmetric --armor myinfo.txt`

## Task 3 - Asymmetric Encryption

0. `gpg --full-generate-key`

1. AA278FB286778401F1D650AFC064270DAB546DBC

2. `gpg --armor --export [key-id] > mypublickey.asc` to export and `gpg --send-keys [key-id] --keyserver [destination]` to send key.

3. 0C282BAC3954314E8891930E05F9D799333D7F28

4. `gpg --verify directions.txt.asc` and the result is "gpg: BAD signature from "decal-staff <decal@ocf.berkeley.edu>" [unknown]".

5. `~/.gnupg/private-keys-v1.d/`

## Task 4 - Hashing

1. **SHA256:** e33d7b1ea7a9e2f38c8f693215dd85254c3a4fe446f93f563279715b68d07987
2. By providing a signature over the hashes of files, the CentOS project efficiently ensures the integrity and authenticity of the files it distributes. This method protects against malicious attempts at file corruption, tampering, or impersonation, offering a high level of security while remaining practical for large-scale distribution.
## Task 5 - File Security

1. `chmod +r <filename>`
2. `sudo chown <YourUsername> <filename>`, then `chmod 400 <filename>`
3. `sudo chown root:root <filename>` then `sudo chmod 400 <filename>`
4. `sudo chown <your_username> file4.txt file5.txt`, then `chmod 400 file4.txt file5.txt`
5. First create a new user group: `sudo groupadd newgroup` then add you and decal to the user group: `sudo usermod -a -G newgroup your_username; sudo usermod -a -G newgroup decal`. After this, change the group ownership of the file: `sudo chown :newgroup filea.txt fileb.txt`. Lastly, set file permission: `sudo chmod 440 filea.txt fileb.txt`.
## Task 6 - Network Security Lab Activity

1. `sudo netstat -tulpn | grep LISTEN | awk '{print $7}' | cut -d'/' -f1 | xargs -L1 ps -o pid=,user=,comm= -p` 

2. No one else.

## Optional Task: Letsencrypt on an nginx instance!

It seems that only UC Berkley's students can do this task.
