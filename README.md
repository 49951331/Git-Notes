##Git-Notes

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

github懶人包

Windows：http://help.github.com/win-set-up-git/

MacOS X：http://help.github.com/mac-set-up-git/

Linux：http://help.github.com/linux-set-up-git/

「Add your SSH key to GitHub」這個步驟是 GitHub 的設定，可以跳過

寫給大家的 Git 教學
第三版，2012

Littlebtc (Hsiao-Ting Yu)

改寫自 Scott Chacon 的「Pro Git」電子書。Creative Commons License

Part 1

Why Git

為什麼要版本控制？為什麼要用 Git？

這是程式設計師的日常

當你寫了一個新東西，卻發生了以下的悲劇…

忘了自己改了哪些地方
把舊的東西改壞了，改不回來
拿去跟別人的成果合併，卻兜不起來
→有沒有辦法解決？

有！「版本控制系統」

當你使用版本控制系統時：

忘了自己改了哪些地方→每次的更動都會被記錄下來
把舊的東西改壞了，改不回來→可以隨時退回到過去的版本
拿去跟別人的成果合併，卻兜不起來→提供機制處理多人協作的衝突
→「凡走過必留下痕跡」、「三個臭皮匠，勝過一個諸葛亮」，這就是版本控制的精神。

版本控制系統的演進

單機式（rcs）
中心式（CVS、Subversion）
分散式（Git、Mercurial、Bazaar）
版本控制系統的演進


單機式
為了達成「凡走過必留下痕跡」：

本機中建立一個資料庫
記下每個檔案的版本變更
rcs (1982) 屬於此類（至今還有人使用！）

→問題：兩人以上協作時，如何同步每個人的版本資料庫？

版本控制系統的演進


中心式
為了讓三個臭皮匠可以一起作業：

版本資料庫放在中心統一控管
每個人從中心取出（Checkout）東西
修改完後將內容提交（Commit）回中心
早期盛行CVS (1990)、現在主流為 Subversion (2000)

→中心一旦故障，大家的作業都會出問題，該怎麼辦？

版本控制系統的演進


分散式
…何不讓每個人都有一份完整的資料庫？

「大家都能獨立工作」
「Server 爛了？不要緊，拿到一份好的資料庫灌回去就可以全部復原！」
Git (2005) 是主流、Mercurial (2005) 跟 Bazaar (2005) 也很盛行

→又來了：怎麼解決每個人之間的同步問題？
引進非線性的開發模式！

Git 的歷史

簡言之：為了解決 Liunx 核心的開發問題，所以有了 Git

過去，Linux 核心開發沒有使用版本控制系統（主因是 Linus Torvalds 不喜歡中心式的系統）。
2002 年，開始改用專有的分散式版本控制系統 BitKeeper，讓自由軟體/開源社群不滿（自由的東西用非自由的開發工具，成何體統？）。
2005 年 BitKeeper 跟 Linux 開發團隊鬧翻，不再免費供應系統。Git 的開發自此開始。
Git 的強項

`快
簡單
非線性開發
（分支、合併、不受單一主線拘束）
完全分散式
處理超大資料的能力
（Linux 核心的程式碼超過一千萬行！）
這些專案都在用 Git`

Linux Kernel
Android
GNOME
KDE
PHP (Since 2012)
Ruby on Rails
django
Part 2

Setup Git

設定屬於你的 Git 開發環境。

設定 Git

Git 的操作大部分都是透過命令列，但也有許多的圖形介面工具。

無論如何，以下的設定都是必要的：

安裝 Git 軟體
這不用說了吧 XD
產生一個 SSH 金鑰
為什麼？因為 Git 可以利用 SSH 進行使用者驗證
調整 Git 的組態
設定姓名和電子郵件地址
有懶人包幹嘛不用？

GitHub 他們寫了三種平台下安裝 Git 的懶人包，以下提供連結：

Windows：http://help.github.com/win-set-up-git/
MacOS X：http://help.github.com/mac-set-up-git/
Linux：http://help.github.com/linux-set-up-git/
「Add your SSH key to GitHub」這個步驟是 GitHub 的設定，可以跳過去 :)

Windows

照上面懶人包安裝後，您會把 Git for Windows 安裝好。

Git for Windows 有兩種不同的使用方式：

Git Bash：一個 Bash Shell，你可以在裡頭以命令列方式使用 Git。
Git GUI：一個簡單的圖形使用介面。
圖形介面工具推薦
TortoiseGit
免費，在檔案總管下使用，需先安裝 Git for Windows
Git Extensions（免費）
SmartGit（跨平台，非商業使用免費）

MacOS X

安裝完後在「工具程式」→「終端機」以命令列使用 Git。

（Mac 下另外建議您使用 iTerm 2 取代內建的終端機程式）

圖形介面工具推薦
SourceTree
免費，也支援 Mercurial 和 SVN
GitX
免費，有只能瀏覽歷史和 Commit 的原始版，和後人改過的全方位版
GitHub for Mac（免費）
Tower（USD $59）
Xcode 4 內建 Git 支援（需要 Lion 以上）


Linux

在終端機中以命令列使用 Git。

圖形介面工具推薦（GNOME）
RabbitVCS
免費，Nautilus 檔案管理員下操作
Ubuntu 12.04 內附的版本沒有 Git 支援，請參照官網設定 PPA 安裝
gitg
GitX 的 GNOME fork
giggle


四　建立Repository
(不只有一份完整的資料庫，不用網路連線也能單獨工作，閱讀版本歷史與提交變更的動作和所有事也能在本機運行。
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

二十五 Git 遠端的選擇

網路上的現有服務：GitHub、Bitbucket、…
自行架設：Gitolite、Gitosis、…
檔案系統（NFS、隨身碟…）
Dropbox（雖然可以，但就失去 Git 的價值了）

二十六 GitHub

主打社群網路功能的 Git 托管服務
具有強大的群組、Fork / Pull Request 和其他附加功能，方便多人協作與溝通
公開 / Open Source 的專案免費，私密專案則要購買收費服務
https://github.com/

二十七 Bitbucket

早期只支援 Mercurial，近期開始支援 Git
類似 GitHub，也有 Fork / Pull Request 的機制
公開專案和五人以下協作的私密專案免費，另有收費服務
https://bitbucket.org/

二十八 自行架設

假如您有一個自己的 Linux 主機，您可以使用 Gitosis 或 Gitolite 架設一個自己的 Remote Server，

請參考 Pro Git 上的說明：

Gitolite（推薦）
Gitosis
或著，如果您有 NFS 或隨身碟，可以直接透過檔案系統作為 Remote。

二十九 Remote Protocol

Git 提供以下四種 Remote 的協定：

Local：以本機路徑作為 Remote 目標，適用於架設於 NFS 時。
/paths/to/remote.git 或 file:///opt/git/project.git
SSH：連接網路的協定，可讀可寫。可以透過 SSH Key 進行認證。
username@server.tld:project.git
通常會使用 SSH，因為其方便且安全性佳。

Git 提供以下四種 Remote 的協定：
Git：連接網路的協定，唯讀，但速度很快
git://server.tld/project.git
HTTP(S)：連接網路的協定，可讀可寫。
速度較慢，但適用於公司行號內有防火牆，只有 HTTP(S) Port 對外開放的環境
http://server.tld/project.git

三十 Cloning

git clone git@github.com:littlebtc/my-project.git

這行指令會：

把程式碼從指定的地方抓下來
在抓下來的 Repository 中設定好一個叫做 origin 的 Remote 指向該處

三十一 Remote Branches

在 Remote 中 Repository 的狀態會被記錄下來
因此 Remote 中也會有 Branch，前面會加上 Remote 的名字來作識別
origin/master 就是指 origin 這個 Remote 中的 master Branch

三十二 Remote 的相關指令

git fetch：將 Remote 更新到最新的版本。
git pull：進行 Fetch 後，將 Remote Branch 的變動合併進本機的 Branch。
git push：將本機的 Branch 變動合併到 Remote Branch。

三十三 實例

在未設定 Remote 的 Repository 中，新增 Remote 後 Push：

git remote add origin git@github.com:littlebtc/my-project.git
git push -u origin master

三十四 其他 Git 的教學資源

Pro Git
Git Ready
ihower 的 Git 心得文


##Git VCS

Git 團隊協同開發指令

上一章介紹了在本地端用git init初始了一個Repository。

不過，比較常常發生的情況是你是從拷貝一個已經存在的 Repository 開始開發。

一 Git 有以下四種方法來存取遠端的Git伺服器：

SSH 安全性最佳
git clone git@github.com:ihower/sandbox.git
HTTP/HTTPS 速度最差，但能突破防火牆限制
git clone https://ihower@github.com/ihower/sandbox.git
Git protocol 速度最快，但缺認證機制(因此只能做成唯讀)
git clone git://github.com/ihower/sandbox.git
File 本機目錄 (有人用 Dropbox 分享 git init –bare –shared 目錄!! Crazy!!)
git clone file://path/to/repo.git
以 GitHub Repository 為例

GitHub 是基於 Git 這套分散式版本控制系統的 Repository hosting 應用，

只要是開放原始碼軟體，都可以免費的使用這個服務。

二 這裡就使用Github來進行練習：

在 Github 上建立一個專案

產生 SSH Key
ssh-keygen -t rsa -C "your_email@youremail.com"
至 Github 註冊，設定你的 SSH Public Key，並開一個專案
git remote add origin git@github.com:your_account/sandbox.git
git push -u origin master
之後只需要 git push
出現 ![rejected] 表示需要先做 git pull
編輯專案的 Settings，加入別人成為你專案的 Collaborators。這樣別人就可以用 SSH 協定來 clone 你的專案。

在 Github 上     Clone 下來

三 以筆者的專案 Sandbox 為例，如果你有寫入權限的話(被加入成Collaborators)，就可以用 SSH 協定 Clone 下來：

git clone git@github.com:ihower/sandbox.git
如果沒有寫入權限(Collaborators)的話，因為這個專案是公開的，所以你還是可以用Git協定Clone下來：

git clone git://github.com/ihower/sandbox.git
如果有防火牆問題，改用 HTTPS 協定：

git clone https://github.com/ihower/sandbox.git
Pull - 從遠端更新

git pull 或 git pull origin master
實際作用是先 git fetch 遠端的 branch，然後與本地端的 branch 做 merge，產生一個 merge commit 節點

四 所謂的”遠端”預設叫做origin，當你有多個不同遠端伺服器時，就會取不同名子了。
Push - 將 Commit 送出去

git push 或 git push origin master
實際的作用是將本地端的 master branch 與遠端的 master branch 作 fast-forward 合併。

如果出現 [rejected] 錯誤的話，表示你必須先作 pull。

預設不會 push tags 資訊：

git push --tags
列出和取出遠端 branch

git branch -r
git checkout -t origin/foobar
git branch -r --merged (列出已經被合併的)	
刪除遠端 Branch

git push origin :foobar
git pull 和 git fetch 不會清除已經被刪掉的 branch
請用 git fetch -p
git push –tags

預設不會 push tags 資訊
git push --tags

(本講義內容來自 版本控制系統Git精要http://ihower.tw/git/remote.html)

(本檔案標題為git VCS［Version control system = 版本控制系統］）
