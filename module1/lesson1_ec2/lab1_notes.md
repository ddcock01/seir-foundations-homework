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
Got in, got out. Another rep. Took the screenshot in the beginning of the runbook and not at the end. That was a mistake that I've pretty much thought was standard but realized I was doing it
all wrong after the fact. I did make some mistakes and did it the right way; taking the screenshot at the conclusion of the runbook.

Run 6
Communicating and jumping back and forth between the AI sort of distracted me from running the script. However, utilizing it to review the runbook in real time helped me better understand what was going on. It also help me anticipate what is to happen next.

Run 7
Finally asked AI why my ctrl + V for pasting into the terminal was doubling my pasted content.


COBOL Practice
I technically used Run 8 Instance ID i-027841605f75588bd, I'll list the [screenshot](screenshots/lab1_run8.jpg.png)
Code	Meaning
0	success — account found / payment POSTED Command = ./cobol/bin/payment_post TXN-DC-0001 100001 555.55 USD INV-1001
4	warning — account not found Command = ./cobol/bin/payment_post TXN-DC-0001 555.55 USD INV-1001
8	business rejection — not ACTIVE, zero amount, funds Command = ./cobol/bin/payment_post TXN-DC-0001 100001 0.00 USD INV-2026
12	environment failure — missing file, malformed args Command = /opt/balerica-bank/cobol/bin/account_lookup 100001
Lines from the journal:
TXN-DC-0001         555.55000000000000INVREJECTED
TXN-DC-0001         100001000000055555USDPOSTED  INV-1001
TXN-DC-0001         100001000000000000USDREJECTEDINV-2026
TXN-DC-0002         100001000000055555USDPOSTED  INV-2027

BAM_2.1
IAM Role: ec2_bedrock 
Instance ID: i-0b903d3ea4af8f0ee

BAM_2.2
Launch Template ID: lt-0e9016240ae0204fa
Version: 2
#!/bin/bash
# SEIR Foundations - Amazon Linux 2023 EC2 User Data
# Combined SSH/dashboard + HTTP web server configuration
# Paste this entire file into:
# EC2 > Advanced details > User data

set -u

###############################################################################
# PART 1 — SEIR FOUNDATIONS SSH DASHBOARD
###############################################################################

cat > /usr/local/bin/seir-dashboard <<'DASH'
#!/bin/bash
# Interactive SSH dashboard; no AWS credentials or external packages required.
[ -t 1 ] || exit 0

RESET='\033[0m'
CYAN='\033[1;36m'
GREEN='\033[1;32m'
YELLOW='\033[1;33m'
BLUE='\033[1;34m'

printf "${CYAN}"

cat <<'ART'
  ____  _____ ___ ____     _____ ___  _   _ _   _ ____    _  _____ ___ ___  _   _ ____
 / ___|| ____|_ _|  _ \   |  ___/ _ \| | | | \ | |  _ \  / \|_   _|_ _/ _ \| \ | / ___|
 \___ \|  _|  | || |_) |  | |_ | | | | | | |  \| | | | |/ _ \ | |  | | | | | |  \| \___ \
  ___) | |___ | ||  _ <   |  _|| |_| | |_| | |\  | |_| / ___ \| |  | | |_| | |\  |___) |
 |____/|_____|___|_| \_\  |_|   \___/ \___/|_| \_|____/_/   \_\_| |___\___/|_| \_|____/
ART

printf "${RESET}\n"
printf "${GREEN}CHEWBACCA OPERATIONS CENTER${RESET}  |  Welcome to your first EC2!\n"
printf "${BLUE}-----------------------------------------------------------------------${RESET}\n"

hostname_val=$(hostname 2>/dev/null || echo unknown)
uptime_val=$(uptime -p 2>/dev/null || echo unavailable)
cores=$(nproc 2>/dev/null || echo '?')
load=$(cut -d' ' -f1-3 /proc/loadavg 2>/dev/null || echo unavailable)
mem=$(free -h 2>/dev/null | awk '/^Mem:/ {print $3 " used / " $2 " total"}')
disk=$(df -h / 2>/dev/null | awk 'NR==2 {print $3 " used / " $2 " total (" $5 " full)"}')

# /proc/stat counters sampled 0.2 seconds apart;
# reflects approximate system-wide CPU busy percent.
read -r _ u n s i w irq sirq st _ < /proc/stat
idle1=$((i+w))
total1=$((u+n+s+i+w+irq+sirq+st))

sleep 0.2

read -r _ u n s i w irq sirq st _ < /proc/stat
idle2=$((i+w))
total2=$((u+n+s+i+w+irq+sirq+st))

dt=$((total2-total1))
di=$((idle2-idle1))

if [ "$dt" -gt 0 ]; then
    cpu=$((100*(dt-di)/dt))
else
    cpu=0
fi

printf "Hostname      : %s\n" "$hostname_val"
printf "Uptime        : %s\n" "$uptime_val"
printf "CPU           : %s%% busy (approx.) | %s vCPU(s)\n" "$cpu" "$cores"
printf "Load average  : %s (1, 5, 15 minutes)\n" "$load"
printf "Memory        : %s\n" "${mem:-unavailable}"
printf "Root disk     : %s\n" "${disk:-unavailable}"

# IMDSv2 only. If unavailable, skip metadata without delaying SSH login.
token=$(curl -fsS --connect-timeout 1 --max-time 2 -X PUT \
  -H 'X-aws-ec2-metadata-token-ttl-seconds: 60' \
  http://169.254.169.254/latest/api/token 2>/dev/null || true)

if [ -n "$token" ]; then

    meta() {
        curl -fsS --connect-timeout 1 --max-time 2 \
          -H "X-aws-ec2-metadata-token: $token" \
          "http://169.254.169.254/latest/meta-data/$1" 2>/dev/null || true
    }

    iid=$(meta instance-id)
    itype=$(meta instance-type)
    az=$(meta placement/availability-zone)

    printf "Instance ID   : %s\n" "${iid:-unavailable}"
    printf "Instance type : %s\n" "${itype:-unavailable}"
    printf "AWS zone      : %s\n" "${az:-unavailable}"
fi

printf "${BLUE}-----------------------------------------------------------------------${RESET}\n"
printf "${YELLOW}COST REALITY CHECK${RESET}\n"
printf "  CPU at 1%% does NOT mean free. Charges depend on instance type,\n"
printf "  running time, storage, network usage, and your AWS account benefits.\n"
printf "  Check AWS Billing > Free Tier and Cost Explorer. Set a budget alert.\n"
printf "  Stop the instance when the lab is done (EBS storage can still cost).\n"
printf "${BLUE}-----------------------------------------------------------------------${RESET}\n"
printf "${GREEN}RRRAAAWWWRRR!${RESET} Chewbacca says: Verify first. Panic later.\n"
printf "Run ${CYAN}seir-dashboard${RESET} anytime to see this again.\n\n"
DASH

chmod 755 /usr/local/bin/seir-dashboard

###############################################################################
# PART 2 — AUTOMATIC DASHBOARD ON SSH LOGIN
###############################################################################

cat > /etc/profile.d/seir-dashboard.sh <<'PROFILE'
if [ -n "${PS1:-}" ] && [ -t 1 ] && [ -z "${SEIR_DASHBOARD_SHOWN:-}" ]; then
    export SEIR_DASHBOARD_SHOWN=1
    /usr/local/bin/seir-dashboard || true
fi
PROFILE

chmod 644 /etc/profile.d/seir-dashboard.sh

echo 'SEIR dashboard installed.'

###############################################################################
# PART 3 — INSTALL APACHE HTTP SERVER FOR PORT 80
###############################################################################

# Install Apache HTTP server
yum update -y
yum install -y httpd

# Start Apache immediately
systemctl start httpd

# Make Apache start automatically after reboot
systemctl enable httpd

###############################################################################
# PART 4 — RETRIEVE EC2 INSTANCE METADATA USING IMDSv2
###############################################################################

# Get the IMDSv2 token
TOKEN=$(curl -X PUT \
    "http://169.254.169.254/latest/api/token" \
    -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

# Retrieve metadata
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
    -s http://169.254.169.254/latest/meta-data/local-ipv4 \
    &> /tmp/local_ipv4 &

curl -H "X-aws-ec2-metadata-token: $TOKEN" \
    -s http://169.254.169.254/latest/meta-data/placement/availability-zone \
    &> /tmp/az &

curl -H "X-aws-ec2-metadata-token: $TOKEN" \
    -s http://169.254.169.254/latest/meta-data/network/interfaces/macs/ \
    &> /tmp/macid &

# Wait for all background metadata requests
wait

macid=$(cat /tmp/macid)
local_ipv4=$(cat /tmp/local_ipv4)
az=$(cat /tmp/az)

# Retrieve VPC ID
vpc=$(curl \
    -H "X-aws-ec2-metadata-token: $TOKEN" \
    -s \
    http://169.254.169.254/latest/meta-data/network/interfaces/macs/${macid}/vpc-id)

###############################################################################
# PART 5 — CREATE THE PORT 80 WEB PAGE
###############################################################################

cat > /var/www/html/index.html <<EOF
<!doctype html>
<html lang="en" class="h-100">
<head>
    <title>Details for EC2 instance</title>
</head>

<body>
<div>
    <h1>AWS Instance Details: Class 8 Edition</h1>
    <h1>Dusty Cloud Engineer in training!</h1>
    <h2>I will survive the AI Tsunami!</h2>

    <br>

    <img src="https://www.w3schools.com/images/w3schools_green.jpg"
         alt="W3Schools.com">

    <br>

    <p>
        <b>Instance Name:</b>
        $(hostname -f)
    </p>

    <p>
        <b>Instance Private Ip Address:</b>
        ${local_ipv4}
    </p>

    <p>
        <b>Availability Zone:</b>
        ${az}
    </p>

    <p>
        <b>Virtual Private Cloud (VPC):</b>
        ${vpc}
    </p>

</div>
</body>
</html>
EOF

###############################################################################
# PART 5.5 - GIT COBOL BANK INSTALLATION
###############################################################################

# Install Git
sudo dnf install -y git

# Clone the course repository
git clone https://github.com/BalericaAI/SEIR-Foundations.git

# Run the automated installer to set up GnuCOBOL, python venv, and compile the bank core
bash SEIR-Foundations/module1/lesson1_ec2/API/install/install.sh


###############################################################################
# PART 6 — CLEAN UP
###############################################################################

rm -f /tmp/local_ipv4
rm -f /tmp/az
rm -f /tmp/macid

echo 'Apache HTTP server installed and configured.'
echo 'SEIR SSH dashboard installed.'
echo 'Combined EC2 user-data script completed.'

BAM_2.3
AMI ID: BAM_2.3_AMI
Snapshot ID: snap-06a6dd843c65b2458
Intance ID: i-0c0c596b54db6c25a