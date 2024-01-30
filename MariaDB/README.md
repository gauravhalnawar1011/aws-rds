---

# Documentation: Connecting to RDS Database and Creating New Users with Various Permissions

## Introduction
This document provides step-by-step instructions for connecting to an Amazon Relational Database Service (RDS) and creating new users with different permission levels. The process involves setting up a VPN connection, accessing the EC2 instance, and using a database client like DBeaver.

## Prerequisites
- OpenVPN Client installed on your system.
- Access to AWS Management Console with necessary permissions.
- DBeaver or MySQL Workbench installed on your system.

## Step-by-Step Guide

### 1. Install OpenVPN Client
If you don't have a VPN installed, download and install the OpenVPN client from [OpenVPN Website](https://openvpn.net/vpn-client/).

### 2. Access EC2 Instance
- Navigate to the EC2 instance section in AWS Management Console.
- SSH into the EC2 instance using your preferred method (CLI or AWS Connect).

### 3. Create a New User on the EC2 Instance
- SSH into `/home/ubuntu/` directory.
- Use the command `sudo adduser newusername` to create a new user.
- Set a password for the new user using `sudo passwd newusername`.

### 4. Download the .ovpn File
- Create a new .ovpn file with your desired name.
- Download the file using SCP or Termius.

### 5. Upload and Connect Using the .ovpn File
- Open OpenVPN and upload the .ovpn file.
- Connect to the VPN to ensure secure communication with the RDS.

### 6. Install Database Client
Download and install a database client like [DBeaver](https://dbeaver.io/download/) or MySQL Workbench.

### 7. Connect to RDS Database
- Go to the AWS RDS section and select the Mumbai region.
- Copy the endpoint of your RDS database.
- Open DBeaver and set up a new connection with the MariaDB engine.
- Enter the endpoint in the hostname field, ensure the port is set to 3306, and enter the admin username and password.
- Test the connection to ensure it's successful.

### 8. Create New Users with SQL Commands
In DBeaver's SQL editor, execute the following commands:

#### For a user with read-only permission:
```sql
CREATE USER 'testonlyuser'@'%' IDENTIFIED BY 'test123';
GRANT SELECT ON `dev1equip9_development`.* TO 'testonlyuser'@'%';
FLUSH PRIVILEGES;
```

#### For a user with read and write permission:
```sql
CREATE USER 'testonlywrite'@'%' IDENTIFIED BY 'test123';
GRANT SELECT, INSERT, UPDATE, DELETE ON `dev1equip9_development`.* TO 'testonlywrite'@'%';
FLUSH PRIVILEGES;
```

## Conclusion
Thank you for following this documentation. We hope it has been helpful in guiding you through the process of connecting to an RDS database and creating new users with various permissions. If you have any questions or need further assistance, please feel free to reach out.

---
