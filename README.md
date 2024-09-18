
# IPv6 Proxy Setup on CentOS 7 ( none Password )

## Requirements
- CentOS 7
- IPv6 /64

## Installation

1. **Enable IPv6**  
   To verify if IPv6 is enabled, run the following command:
   ```bash
   ping6 google.com
   ```

2. **If IPv6 is not working**  
   Run these commands to fix repository and network issues:
   ```bash
   sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/*.repo
   sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/*.repo
   sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/*.repo
   echo "sslverify=false" >> /etc/yum.conf
   ```

   Configure your IPv6 address and gateway:
   ```bash
   IPV6ADDR=<Your IPv6 Address>
   IPV6_DEFAULTGW=<Your IPv6 Gateway>
   ```

   Update your network configuration:
   ```bash
   echo "IPV6_FAILURE_FATAL=no
   IPV6_ADDR_GEN_MODE=stable-privacy
   IPV6ADDR=$IPV6ADDR/64
   IPV6_DEFAULTGW=$IPV6_DEFAULTGW" >> /etc/sysconfig/network-scripts/ifcfg-eth0
   service network restart
   ```

3. **System update and package installation**  
   Run the following commands:
   ```bash
   yum update -y
   yum install wget -y
   ```

4. **Install the IPv6 Proxy Script**  
   Run the command below to download and execute the installation script:
   ```bash
   curl -sO https://raw.githubusercontent.com/secondsvn/ipv6-proxy-creator/main/ipv6.sh && chmod +x ipv6.sh && bash ipv6.sh
   ```

5. **Download the Proxy Configuration**  
   After installation, download the `proxy.zip` file. The file structure will be in the format:
   ```bash
   IP4:PORT
   ```

## Test Your Proxy
To check if your proxy is functioning correctly, visit [ipv6-test.com](http://ipv6-test.com/) and verify your connection.
