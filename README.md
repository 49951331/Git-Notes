Git-Notes

一　使用版本控制系統
1.版本更動紀錄
2.版本還原
3.提供機制改善多人協作衝突

二　版本控制系統演進
1.單機式(rcs)
本機建立資料庫、記錄檔案版本變更
缺點：多人協作，難以同步版本資料庫
2.中心式(CVS、Subversion)
版本資料庫放在中心統一控管、每個人從中心取出東西、修改完後將內容提交回中心
缺點：中心故障，作業流程會出問題
3.分散式(Git、Mercurial、Bazaar)
獨立作業、伺服器產生異常，提取一份好的資料庫灌回就可復原
缺點：仍然無法解決同步問題

三　git優點

簡單且速度快，非線性開發與完全分散式和處理龐大資料的能力

設定git
1.安裝git軟體
2.產生ssh金鑰
3.調整git組態

四　建立Repository

1.git對版本資料庫的稱呼為 repository(套件庫）
2.下達git init，會在該目錄建立repository
3.repository所需檔案將放置在.git目錄中（請勿誤砍）

五　範例:建立名為playground的空目錄，在那裏建立git repository:
1.mkdir playground
2.cd playground
3.git init
4.或用git init playground 一次建立空目錄與repository

六　基本觀念-commit
1.git將現狀紀錄稱為commit
2.commit包含作者和時間‵log與前後對應commit等資訊，方便追蹤管理

　　基本觀念-staging
1.在你的目錄(working directory工作中目錄)進行作業
2.只有放進staging Arta(暫存區)裡的更動會被commit
3.多項目同時作業，可分開切成多個commit、不用擔心未完成或暫存資料影響commit
4.同一檔案，可以只有些許改動加入staging

　　基本觀念-檔案狀態
untracked:無納入版本控制範圍之檔案
unmodified/modified/:無變動/有變動但尚未staging的檔案
staged:staging area中的檔案

七　新增指令
1.git add:把檔案新增或變動加入staging area
2.git status:檢視檔案狀態
3.git commit:開啟編輯器，確認變動輸入訊息送出commit，指令後加-m 'commit訊息'會直接commit
4.git commit--amend:將上次commig跟新更動合併為新的commit
訣竅:git commit -a =將所有變更加入staging area之後 commit

　　移除或補救指令

1.git reset HEAD <paths> :把檔案中staging的部分註銷
2.git rm<paths>:將檔案從版本控制中移除並刪除檔案，加-r採遞迴方式 加--cached則不刪除原來檔案
3.git checkout--<paths>:恢復檔案為未更動狀態(對staging無效)

八　第一個commit
1.用touch readme建立一個空的readme
2.git add readme
3.git commit -m 'first commit'
4.建立一個commit 將readme納入版本控制

　　Commit的內部結構
1.利用tree將檔案存在blob
2.所有資料用sha| checksum標記,防止損毀或中途更改
3.git針對檔案版本獨立紀錄，並不只記錄之間差異

　　捨棄這個commit
如果尚未push給別人，可將整個樹退回前一次commit時的狀態
git reset HEAD^

如果已經Push給別人,用revert製造一個與目前commit差異相反的commit

git revert head



九　當commit超過一個
1.git以束狀方式記錄commit繼承關係，在每個commit中記下parent
2.git允許commit分岔與合併，可進行複雜樹狀操作

十　tag和branch
1.使用中的branch指向位置會在新commit出現後自動移動，repository預設branch稱為master
(git會使用head指標紀錄目前的branch，可隨時新增與切換和刪除，分岔的branch可透過merge和rebase)

    tag是不會動的:對特定的commit加上標記，指向位置不會隨著新commit出現更動，用於標記釋出版本或里程碑
