I created ec2 from template we madee in class
I used chmod 400 "key pair name.pem" to secure the connection.
I then used ssh -i "your-key-name.pem" ex2-user@<your_instance_public_IP> to ssh inside, see BAM_1.1.jpg<screenshots\BAM_1.1.jpg>.
Next I used sudo nano /var/www/html to get inside and edit the text, uploaded the image of my mission_vission to github.
found the original HTML image tag and replaced it with "<img src="https://raw.githubusercontent.com/ddcock01/seir-foundations-homework/main/module1/lab0.5_basics_contd/screenshots/mission_vission_lab0.5.jpeg" alt="My Destination Picture" width="600">"
"C:\Users\ddcoc\Pictures\68141d54-b403-4fb0-89c6-4c44102d490f.jpeg"
I used the EC2 instance public ip address to connect to the webpage via http://"publicdns"


| Item    | Requirement                                       | Screenshot                  | Done?    |
|---------|---------------------------------------------------|-----------------------------|----------|
| BAM_1.1 | Local SSH client; `whoami` + `date` visible       | `screenshots/BAM_1.1.jpg`   | Yes / No |
| BAM_1.2 | Custom page: thank-you line, dollar line, picture | `screenshots/BAM_1.2.jpg`   | Yes / No |
| BAM_1.3 | Local SSH; `user_data` script displayed with `cat` | `screenshots/BAM_1.3.jpg`   | Yes / No |