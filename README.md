### docker-compose-lamp

參考往參考網址

https://hackmd.io/@titangene/docker-lamp

安裝步驟

Step1:開啟docker 或是 docker-toolbox

Step2:找到當前目錄(我的是C:\Program Files\Docker Toolbox)

Step3:將參考網址的檔案下載到當前目錄(我的是C:\Program Files\Docker Toolbox)

Step4:進入該資料夾(進入要執行的資料夾，docker-compose要能執行，一定要在當前目錄下，且有yml檔，才能執行)

```
cd docker-lamp-test/2_docker-compose-build-image
```

Step5:檢查 docker-compose.yml 檔案

build: ./php ()

volumes:
  前(本地端檔案):後(容器端檔案)
  
```
version: '3.3'

services:
  phpapache:
    build: ./php
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - mysql
    volumes:
      - /c/Users/Default/test001/www:/var/www/html
  mysql:
    build: ./mysql
    ports:
      - "3306:3306"
    volumes:
      - ./mysql/data:/var/lib/mysql
    environment:
      MYSQL_USERNAME: titan
      MYSQL_PASSWORD: password
      MYSQL_ROOT_PASSWORD: admin
      #MYSQL_DATABASE: testdb
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
      - "8080:80"
    depends_on:
      - mysql
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306
```

Step6:執行docker-compose

```
docker-compose up -d 或是 (docker-compose -f 自定義名稱.yml up -d)
```

Step6:進入容器檢查volume是否有對應到本地端檔案
