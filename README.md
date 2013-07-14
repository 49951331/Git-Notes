#Git-Notes

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

2.tag是不會動的:對特定的commit加上標記，指向位置不會隨著新commit出現更動，用於標記釋出版本或里程碑

十一 　範例一：我在哪裡

1.一個擁有三個commit的repository，此時只有一個預設的master(branch)     
2.建立一個新的branch叫testing，指向目前所在的commit(指令:git branch testing)
3.切換到testing branch:head變為指向testing，再切換到該branch指向的commit(指令:git checkout testing)
訣竅:git checkout -b testing 可一次做完並開新的branch + 切換
4.用git checkout master 切換到 master 和其對應的commit
5.在master下進行commit後，由於同一個commit有兩個分支，產生分岔

十二　branch岔開之後?

透過 Merge 合起來， 若目標只是這個 Branch 往後推的幾個 Commit，只要把 Branch 往後推就好，這樣叫 Fast-forward merge。
無法使用 Fast forward 的狀況，Git 會嘗試用策略去解決並合併分支。（過程簡單、問題較少，但合併次數一多，會讓樹看起來很亂）
或透過 Rebase 「接上去」（過程複雜，容易衍生問題，但結果較完美）
※已經 Push 給別人的東西千萬不要用 Rebase！

十三   範例二:Merge

1.以iss53 修正 Issue 53，但未寫完，
使用hotfix 解決現在 master 產生的問題，寫好後合併至 master
指令:git checkout master
     git merge hotfix

2.切回 master ，把 hotfix 裡的變更合併

因為合併對象是後幾個 Commit，可以透過 Fast Forward 把 Branch 後推解決
完成後，就能由 git branch -d hotfix 將不需要的 Branch 刪除
這時iss53 寫好了，需 Merge 回去
指令:git checkout master
git merge iss53

但這種 Merge 沒辦法透過 Fast Forward 解決，所幸有共同祖先，可以做 3-way Merge。
3-way Merge 的實作：比較祖先和合併對象間（C2 與 C4 間和 C2 與 C5 間）的變動，將這些變動合併
合併結果產生新的 Commit C6，C4 和 C5 是其共同的 parent。
至此完成分支的合併。

十四　範例三：rebase
想把 experiment 的變更丟進去 master，但又不想用 Merge 製造額外的分支，解法？
解：
指令：git checkout experiment
git rebase master

把 C3 的變更 「蓋到 master 裡面去」，接下來切回 master，把 experiment 合併好即完成

十五　範例四：複雜一點的rebase
由於伺服器寫得不太完善，想把client的變更蓋到master上而非伺服器之上
解：
指令：git rebase --onto master server client
檢查 client，由 client 和 server 的共同祖先和其比較看作了哪些變動，
把那些變更重新在 master 上面作過一遍，剩下的就是 Merge 而已了

十六　conflict!!

1.Git 遇到衝突會停下，將未衝突到的地方給 Staging 起來，把衝突到的地方標示起來。
2.此時可透過 git status 找出衝突的檔案（unmerged）
3.打開那些檔案，手動把衝突之處修正，再重新 Commit 就能解決衝突。

十七 branch的其他指令

1.git branch：顯示目前所有的 Branch，會用星號標示目前所在者，
並以 git branch -v同時顯示各 Branch 所在的 Commit
2.git branch --merged：顯示已合併到目前 Branch 的其他 Branch，（能把沒用到的 Branch 找出來刪除）
3.git branch --no-merged：顯示未合併到目前 Branch 的其他 Branch

十八　tag

1.git tag v1.0：把現在的 Commit 加上名為 v1.0 的 Tag
2.git tag v1.0 abcde：對代碼為 abcde 的 Commit 加上 v1.0 Tag
3.git tag -d v1.0：刪除名為 v1.0 的 Tag
4.Git 另有功能較為強大的 Annotated Tags，可以在 Tag 上註記作者資訊和認證機制。

(Push 時，用 git push --tags 才會把 Tag 給一起 Push 上去)

十九  推薦的分支方式
1.每個branch都採分開處理一項事情
2.將測試中版本與穩定版本分為不同branch
3.需長時間才可完成之獨立項目拆成branch
4.A successful Git branching model 一文中歸納了 Git 用於軟體開發時的分支最佳實踐。
(有人基於這個概念設計了 git-flow 工具)

二十 我想要乾淨的樹

進行 Branch 切換，或Rebase ，會要求 Working Directory 必須是沒有變動的，但改到一半的東西又無法放棄，何解？
解：
使用 Stashing 把變動放到外太空

git stash：把目前的變更（包含 Staging 的部份）放進新的 Stash
Stash 可以有很多個，會以堆疊的方式儲存（想成放進桶子裡）
git stash apply：把最新的 Stash 中的變更取出。
git stash list：檢視目前的 Stash 堆疊。

二十一 Remote(遠端)

1.將你的repository同步到其他伺服器中
2.需藉此整合眾人的東西進行多人協作
3.git允許附加多個遠端，因此可做複雜的同步工作

二十二　多人協作：單一中心式

類似中心式版本控制系統，所有人跟一個共同的遠端 Repository 進行同步。
但跟中心式相比，遇到衝突可透過 Merge 和 Rebase 來解決，不會有卡住的情形。
（適合人數跟規模較小的情況。）

二十三　多人協作：整合管理員式

有一個「正統」（Blessed）的 Repository 來存放最終版本
開發者把自己貢獻整理後，傳到自己公開的 Repository。
由整合管理員決定是否每個開發者改的東西合併到正統裡。
這種模式就是 GitHub 或 BitBucket 等系統的 Fork 與 Pull Request 機制：
開發者可以把正統版 Fork 下來改，改好後送 Pull Request 給整合管理員。

二十四 多人協作：司令官與附手

當專案規模超大時，就需要兩層甚至以上的組織。
每個開發者的成果由附手彙整後，交由司令官作最後整合。
