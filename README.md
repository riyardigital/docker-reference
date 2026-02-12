# Docker參考

### 1. Docker部屬完畢後
在Docker目錄下建立src資料夾
把Laravel專案放到src資料夾即可

### 2. 前端主機的佈署檔案參考 (後面有加上 -front，記得名稱要改正即可)
- docker-compose-front.yml
- Dockerfile-front
- cychfront.conf

### 3. 如果本機開發過，資料夾內會有 node_modules。
如果不忽略它，Docker 會把本機裡的 node_modules 複製進去，
導致建置時間變長而報錯。

請在 Dockerfile 同一層目錄新增 .dockerignore：

Plaintext
node_modules
dist
.git
.vscode
nginx/logs

### 4. 因為要匯出PDF、EXCEL、壓縮檔
請參考Dockerfile-back

[新增] libreoffice-writer: 核心轉檔軟體
[新增] default-jre-headless: LibreOffice 依賴的 Java 環境 (無 GUI 版)
[新增] fonts-noto-cjk: Google Noto CJK 字型 (解決中文亂碼/方塊字問題)
[新增] libzip-dev: Word/Excel/ZipArchive 依賴