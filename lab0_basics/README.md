| Deployment | Public IPv4 address | Connection method | Screenshot | Instance terminated? |
|---|---|---|---|---|
| 10.13.268thgate | 34.228.73.138 | EC2 Connect | [![View Screenshot](screenshots\deployment-3.png)](screenshots\deployment-3.png) | Yes |
| 10.13.268thgate | 34.203.214.92  | EC2 Connect | [![View Screenshot](screenshots\deployment-2.png)](screenshots\deployment-2.png) | Yes |
| 10.13.268thgate | 107.27.141.98 | EC2 Connect | [![View Screenshot](screenshots\Deployment-1.png)](screenshots\Deployment-1.png) | Yes |

I used the EC2 Instance that we made in class to create a Launch Template before terminating that instance. I used the EC2 connect to get into each Instance and verify that they were working (see screenshots). However, in class, I acknowledged that if I would've created these individually, I would've had to start in the EC2 dashboard, launch instance, and configure the instance. Midway through the configuration, after choosing an AMI and creating Key Pairs I would need to create a Security Group. Open up another tab, configure the Security Group; 2 inbound rules, 1 SSH and 1 HTTP. Get back into the EC2 configuration tab and select the Security Group. I copied the User Data from class and bootstrapped it under additional information and launched the EC2. After this, is when I went ahead and created a launch template; to create the 3 instances simultaneously for this homework.

CPU: Instance CPU tells you the amount of computing effort or load the instance is currently experiencing.

Memory: This is the RAM. The amount of memory the Instance has available.

Disk: The capcity of storage memory or the root storage attached to the Instance.

Uptime: the amount of time the Instance has been running.

Side Project: Inititate Project "The Fittest App"
I'm currently working along on a project that I hope will become profitable some day, manifesting one of my ideas for another line of income. I'm using this project also to reinforce learning from my Udemy Terraforming and SIER Foundation w/ class 8. 

Goal was to SSH into the EC2 of my infrastructure which I was successful with doing. Please see screenshot, if you're interested: ![screenshot](screenshots\ssh_fittest_fitness.png)