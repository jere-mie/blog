---
title: Self-Hosting Your Own ngrok Alternative with Reverse SSH Tunneling
date: 2024-01-16
draft: false
author: Jeremie Bornais (with help from ChatGPT 😎)
--- 

Are you tired of relying on third-party services like ngrok to expose your local development environment to the internet? Good news! You can achieve similar functionality by setting up a reverse SSH tunnel. In this guide, we'll walk through the process of creating your own self-hosted tunneling solution.

## Prerequisites

- Local development environment with a service running on a specific port (e.g., http://localhost:8000).
- SSH access to a remote server with a publicly accessible IP address.

## Step 1: Initiate a Reverse SSH Tunnel

Open a terminal on your local machine and use the following command to create a reverse SSH tunnel to the remote server:

```bash
ssh -f -N -R 8080:localhost:8000 user@remote-server
```

- `-f`: Runs SSH in the background.
- `-N`: Instructs SSH not to execute any commands on the remote server.

If you don't want to run this in the background, and instead want to have an open shell of your remote server, you can omit the `-f -N`.

Adjust the port numbers and usernames as needed. This command establishes a connection that forwards traffic from port 8080 on the remote server to port 8000 on your local machine.

## Step 2: Confirm Tunnel Setup

To verify that the tunnel is established, you can check the list of active SSH connections on the remote server:

```bash
netstat -an | grep 8080
```

If the tunnel is active, you should see a line indicating that port 8080 is in use.

## Step 3: Access Your Local Service

Now that the tunnel is established, anyone connecting to port 8080 on the remote server will be accessing the service on your local machine.

```plaintext
http://remote-server-ip:8080
```

Replace `remote-server-ip` with the actual IP address of your remote server.

## Step 4: Run the Tunnel as a Background Process

If you want to keep the tunnel running in the background, use the following command:

```bash
ssh -f -N -R 8080:localhost:8000 user@remote-server
```

### Terminating the Tunnel

To terminate the tunnel later, find the process ID and use the `kill` command:

```bash
pgrep -f "ssh -f -N -R 8080:localhost:8000 user@remote-server"
kill <process_id>
```

If you're a Windows user, you won't have pgrep installed, so you can use the following command in Powershell to get the process ID of the tunnel:

```sh
Get-Process | Where-Object { $_.ProcessName -match 'ssh' }
```

And then use the following command to stop the tunnel (replacing <PID> with the ID obtained from the previous step):

```sh
Stop-Process -Id <PID>
```

## Coupling This With Caddy and a Custom Domain

Since your local process is now accessible on your remote server on a specific port, you can treat it like any other service running on your remote server. Thus, you can use something like Caddy and a custom domain to make it appear like any other website.

Check out my tutorial on hosting web applications using GCP and Caddy [here](https://blog.bornais.ca/posts/2023-10-18-gcp-caddy-tutorial/).

## Conclusion

Congratulations! You've successfully set up a reverse SSH tunnel to expose your local service to the internet through your own server. This self-hosted solution provides similar functionality to ngrok but gives you more control over your tunneling environment.

Feel free to customize the port numbers and server configurations based on your needs. Happy tunneling!

*This article was written in part using ChatGPT*
