- List
    - 切換目錄
    ```
    cd 路徑
    ```
    - 建立資料夾
    ```
    mkdir 資料夾名稱
    ```
    - 建立檔案
    ```
    touch 檔案名稱
    ```
    - 刪除資料夾
    ```
    rm -r 資料夾名稱
    ```
    - 刪除檔案
    ```
    rm 檔案名稱
    ```
    - 列出當前目錄內的檔案
    ```
    ls
    ```
    - 清理當前顯示紀錄
    ```
    clear
    ```
    - 回到上一層
    ```
    ..
    ```
    - 複製檔案
    ```
    cp
    ```
    - 移動檔案
    ```
    mv
    ```

    - 變更檔案權限
    ```
    chmod
    ```
    - 提升權限
    ```
    sudo
    ```
    - 關機
    ```
    poweroff
    ```
    - 查詢使用手冊
    ```
    man 指令
    ```

    - 總和實例
    ```
    [PC workSpace]$ mkdir newFolder
    [PC workSpace]$ ls
    newFolder //這行是系統產生的,表示當前資料夾的檔案&資料夾列表
    [PC workSpace]$ touch newFile
    [PC workSpace]$ ls
    newFile  newFolder
    [PC workSpace]$ cd newFolder
    [PC newFolder]$ ls
    [PC newFolder]$ cd ..
    [PC workSpace]$
    [PC workSpace]$ rm -r newFolder/
    [PC workSpace]$ ls
    newFile
    ```