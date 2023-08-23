```
## Commands the can be done when connecting to an SMTP server with telnet

# AUTH is a service extension used to authenticate the client.
AUTH PLAIN

# The client logs in with its computer name and thus starts the session.
HELO

# The client names the email sender.
MAIL FROM

# The client initiates the transmission of the email.
DATA

# The client aborts the initiated transmission but keeps the connection between client and server.
RESET

# The client checks if a mailbox is available for message transfer.
VRFY

# The client also checks if a mailbox is available for messaging with this command.
EXPN

# The client requests a response from the server to prevent disconnection due to time-out.
NOOP

# The client terminates the session.
QUIT
```

```bash
# Connecting to SMTP server
telnet 10.129.14.128 25

# Basic scan
sudo nmap 10.129.14.128 -sC -sV -p25

# open relay scan
sudo nmap 10.129.14.128 -p25 --script smtp-open-relay -v (open relay)

```