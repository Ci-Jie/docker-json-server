## API-Server on Docker

### 簡介：
此範例提供你一個虛擬的 APIs 讓你在行動裝置或網頁前端開發上，更加便利、簡單、快速。作者是將現有的 [json-server](https://github.com/typicode/json-server) 套件建置於 docker 上，透過修改內部的 db.json 檔，就能打造出一個符合你需求的 APIs。

### 安裝 Docker：

執行 install.sh 安裝 Docker 環境：

```
./install.sh
```

安裝完成後，使用下列查詢指令觀看版本並且驗證是否安裝成功：

```
docker --version
```
> 執行後可以看到與範例類似的訊息： Docker version 1.10.1, build 9e83765。

### 建置 Json-Server：

使用 Dockerfile 與下列指令建置 Json-Server 映像檔(Image)：

```
sudo docker build -t <your username>/json-server .
```
> 這個部份的 your username 可依照使用者名稱自行輸入。

查看現有的 docker images：

```
docker images

#結果：
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
cijie/json-server   latest              f1eecd944426        2 hours ago         654.3 MB
node                argon               ce67537dc510        2 days ago          642.6 MB
```

### 啟動 Json-Server：

透過下列指令執行剛才所建立的 image ：

```
docker run -p 3000:3000 -d cijie/json-erver

#結果：
1d641e87066d83691e1079f386da2a7b7a01b856295dc47f5ad327a38a1c895a
```
> -d 參數表示以背景方式執行 <br />
> -p 3000:3000 參數表示 container 3000 port 對應到外部 3000 port

執行後，使用 `docker ps` 指令觀看執行中的 image 列表：

```
docker ps

#結果
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
1d641e87066d        cijie/json-server   "npm start"         2 hours ago         Up 2 hours          0.0.0.0:3000->3000/tcp   small_mahavira
```

### 設置 APIs 內容

可以透過修改 db.json 修改虛擬 APIs 內容：

```
{
  "users": [
    { "id": 1, "name": "張三"},
    { "id": 2, "name": "李四"}
  ]
}
```
> 更多 Json-Server 相關配置請[點我](https://github.com/typicode/json-server)

### Routes
```
GET    /users
GET    /users/1
POST   /users
PUT    /users/1
PATCH  /users/1
DELETE /users/1
```
> 可以透過 google 擴充軟體 [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 測試 APIs。


### 參考
[Dockerfile reference 官方文件](https://docs.docker.com/engine/reference/builder/) <br />
[Json-Server](https://github.com/typicode/json-Server)
