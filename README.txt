運行步驟：
1. 請將「AI cup 程式繳交」整個下載下來。裡面有必要的檔案：train_info.csv、test_info.csv、train_data資料夾、test_data資料夾。若有疑慮可以上傳到比賽單位新下載的資料，一樣是train_info.csv、test_info.csv、train_data資料夾、test_data資料夾。此步驟google drive會先壓縮再下載，需要一段時間，請耐心等待。
這一步驟也可以只下載「AI_cup程式 繳交版本.ipynb」，然後放到資料夾裡，該資料夾名稱應為「AI cup 程式繳交」，然後再到比賽官網下載train_info.csv、test_info.csv、train_data資料夾、test_data資料夾，丟進「AI cup 程式繳交」資料夾裡，再上傳到Google Drive裡，這樣會比較快，無需等待雲端硬碟下載時的壓縮時間。
2. 「AI cup 程式繳交」下載完之後請上傳至您的Google 雲端硬碟裡面，方便Google Colab可以讀取到資料。
3. 進入到Google Colab並登入您剛剛上傳檔案的帳戶，並用colab開啟「AI cup 程式繳交」裡面的「AI_cup程式 繳交版本」這個筆記本。
4. 找到左上角功能列表，執行階段->更變執行階段->執行階段類型選擇「Python 3」，硬體加速器選擇「CPU」->儲存。接著找到右上角「連線」按鈕並點擊。
5. 程式的一開頭會需要將colab連結到雲端硬碟，方便取用重要資料。按下程式旁邊cell的播放鍵執行程式。這個步驟一樣需要登入。
6. 在左側有五個按鈕，點擊第五個資料夾按鈕，會看到drive資料夾，就代表成功連結到Google Drive。接著打開drive資料夾，在打開MyDrive資料夾，找到您上傳的「AI cup 程式繳交」資料夾（若檔案較多可能會開比較久）。
7. 打開「AI cup 程式繳交」，裡面應該要有train_info.csv、test_info.csv、train_data資料夾、test_data資料夾。
8. 鼠標移到train_info.csv上面，會看到右邊會有三點的按鈕，點開並按「複製路徑」。將這個路徑取代「處理train_info和train_data」程式cell裡面的INFO_CSV_PATH這個變數的檔案位置。
例如：複製到的路徑為：「/content/drive/MyDrive/AI cup 程式繳交/train_info.csv」，那麽INFO_CSV_PATH那行程式為：INFO_CSV_PATH = “/content/drive/MyDrive/AI cup 程式繳交/train_info.csv”
這樣就能順利讀到train_info.csv檔案了。
9. 「處理train_info和train_data」這個cell裡面，TRAIN_DATA_DIR 的路徑也改成train_data資料夾的路徑；而OUTPUT_CSV_PATH改成「AI cup 程式繳交」資料夾的路徑，這個路徑是處理好的training特徵放的地方（預設檔案名稱為「train_with_features_73」，並且會輸出到「AI cup 程式繳交」資料夾裡）。
10. 接著來到「處理test_info和test_data」這個cell。類似地，INFO_CSV_PATH 的路徑改成test_info.csv的路徑；TRAIN_DATA_DIR 的路徑改成test_data資料夾的路徑；OUTPUT_CSV_PATH改成「AI cup 程式繳交」資料夾的路徑，這個路徑是處理好的test特徵放的地方（預設檔案名稱為「test_with_features_73」，並且會輸出到「AI cup 程式繳交」資料夾裡）。
11. 接下來，請滑到程式的最底下。將x_test 的讀檔路徑改為剛剛設定「test_with_features_73」的檔案位置，再來把「final_prediction.to_csv」這個程式後面的檔案輸出路徑改為「AI cup 程式繳交」資料夾的路徑，這樣會輸出最後的預測結果到該資料夾。預設的檔案名稱為「final_predication.csv」。
12. 注意，在訓練過程中，也會有一些讀取檔案的程式，已經有註解需要讀取的檔案在旁邊，若有錯誤，可以查看註解並排查，不然照著我預設的應該就可以執行。
12. 到這裡就可以開始運行了。可以一個一個由上往下，點cell旁邊的播放鍵執行，也可以在左上角「執行階段」裡面點選全部運行。

程式模塊的說明已經放在程式裡面。