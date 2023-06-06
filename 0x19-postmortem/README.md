# 0x19. Postmortem
In this project, I learned about postmortem report and practiced writing one:

## Security alert Web 01 Server’s Nginx installation failure to listen on port 80 incident report

### Issue Summary
Nginx installation on security alert _web_01 server denied all packets destined for its port, 80/TCP, from 9:32 AM to 10:02 AM SAST. All HTTP requests were answered by the server with the same error: (7) Connection to port 0 was unsuccessful because it was rejected. At its height, the problem prevented users from viewing websites, affecting 60% of all traffic to this server. An incorrect firewall configuration on the server was the main reason it rejected traffic on this port.

### Timeline (South African Standard Time, all times)
- 9:18 AM: Ngnix was set up on the server .
- 9:32 AM: The server began to receive traffic.
- 9:32 AM: Pagers alerted on-call Software Engineer, Chrisvy Koubangou.
- 9:40 AM: The root cause of the server’s port 80 rejection was determined.
- 9:42 AM: The server’s port 80 was successfully configured.
- 9:45 AM: Server restart begin.
- 10:02 AM: All traffic is back online.

### Problem
Ngnix was manually installed and configured on the server at 9:18 AM SAST. The group neglected to grant the server’s requests flowing through port 80 of the firewall permission. As a result, requests from other defined ports were allowed via the firewall but not ones from port 80, which is necessary for the server to provide services.

### Solution
The monitoring systems notified the on-call engineer, Chrisvy Koubangou, at 9:32 AM SAST. Chrisvy investigated the problem and then started to fix it.
Chrisvy set up the server’s firewall at 9:42 AM SAST, allowing port 80/TCP access.

### Correctional and Preventive Actions
To avoid another situation like this in the future, the team should: configure servers using Server Control Management solutions, such as GitLab :

- Before a server is made available to users, execute a number of tests.
 
Sincerely,  
Server Administration Group
