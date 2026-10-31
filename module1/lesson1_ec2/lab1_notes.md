0. US Virgina Region

1. Secure the Parameter! Utilizing Security Group built in class for round This security group has Custom TCP port 8000 Custom Anywhere IPv4

2. Using the Launch template that was modified to include the new SG, I selected the linux AMI and Launched an EC2. The EC2 Type was T3.micro (we need at least 2 GB for this lab)

3. Once the instance is running, time to use ec2 connect to get inside the command prompt to begin programming using the run book.

4. Before following the runbook, I ran the command: whoami && TZ='America/New_York' date. For validation purposes

5. Began run book up until "upgrade pip" command. Fed the prompt this: /opt/balerica-bank/venv/bin/python3 -m pip install --upgrade pip

6. Follow Runbook steps 0-4

7. HTTP:// port for public access

8. http://'public DNS':8000 to access bank page

I asked Google Gemini "What's a COBOL Program". Apparently COBOL stands for Common Business-Oriented Language, and is one of the oldest programming languages still used today. The language was created back in 1959 for busines, finance, and administrative systems, like banking.

Run 1
I accidentally copied a piece of my notes along with pip install -- upgrade pip. It looked like the command messed up but read past the mistake and continued the update. I was actually kind of impressed by that. Also after asking Gemini what COBOL is, it makes sense that we're using it for this particular lab.

Run 2
This run I didn't use a template, made the EC2 from scratch for the practice.I missed up the initial command the last time, the command I used on [lab1_run1.jpg](screenshots/lab1_run1.jpg.png) had just whoami && TZ='American/New_York'. I noticed doing the run with my spotter Brent, that the command should've been; whoami && TZ='America/New_York' date && ec2-metadata -i && uptime -s. I also deleted my instance too early before copying the information to the table became a bit of a hassle.

Run 3
Went straight through, no issues. My laptop and browser needs to update though. I updated the (Chrome) browser, and Gemini (AI), stopped working. It was perfect for in browser AI.

Run 4
This time no issues, accept from the slowing up of my computer, probably do to the need for updates. I did notice the following command: git clone https://github.com/BalericaAI/SEIR-Foundations.git. This is likely what we'd use to clone our homework repo to the EC2 for a screenshot. I did happen to forget to take the screenshot at the beginning and took it at the end of the runboook instead. I think it workout, gives you a different view point of the progression through the runbook.

Run 5
Got in, got out. Another rep.

Run 6
Communicating and jumping back and forth between the AI sort of distracted me from running the script. However, utilizing it to review the runbook in real time helped me better understand what was going on. It also help me anticipate what is to happen next.

Run 7
Finally asked AI why my ctrl + V for pasting into the terminal was doubling my pasted content.


COBOL Practice