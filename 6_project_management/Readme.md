1. Resume From [🗂 PC2](<../5_PC2/>)
2. Hint:

`راهنمای مسابقه`

```text
۱. 
faraji:P@ssw0rd!
۲. 
دسترسی ادمین را بدست آورید 
```

3.ping project management server from pc2

```shell
ping pm
```

project management server ip :`10.233.58.241`

4. ssh to project management server from pc2

```shell
ssh faraji@10.233.58.241
ssh -p 2200 faraji@10.233.58.241
```

```shell
nc -zv 10.233.58.241 80
```

```shell
ssh -i ./id_ed25519 -p 2200 -L 18080:10.233.58.241:80 vpn_user@172.16.3.64
```

```shell
http://localhost:18080
```
