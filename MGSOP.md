# Prepared before use

前置動作

到WERP-板手(其他設定資訊)
	主題選  其他
		單位選擇  專案整合組,專案製作部,接口技研組(研三),產品介接組(研三),遊戲開發組,雲端整合部
	內容
		GameType與遊戲連結提供在附件。
備註 
          PC部分遊戲為舊版翻成新版，提供在關閉清單。

提供給PMO的資料請參考附件『MG開放與關閉資料』(參考提供給PMO網址)

到sk視窗跟 PMO 講
「已接API 開放遊戲」 整合站 @0001 -【MG】機率遊戲清單更新 (201802)
GameType已經附上，再麻煩了，謝謝

組DB語法
參考廠商提供的資料(excel)
TNG2 - Flash HTML5 Download gamecodes URLs for API users v5.3

`WagersDB23`.`GameType`
語法範例 : 
INSERT INTO `WagersDB23`.`GameType` (`GameType`, `GameTypeName`, `HTML`, `PublicEnable`, `MobileEnable`, `Location`, `IconKind`, `OpenDate`, `HallIDisable`, `DisplayName`, `OtherSet`, `ModuleID`, `ClientID`, `GameCommGroup`) VALUES 
("23973", "Girls With Guns Jungle Heat", "Y", "N", "N", "N", "", "2018-02-06", "", "", "0", "10238", "40300", "14"),
("23634", "Girls With Guns Jungle Heat", "Y", "N", "N", "N", "", "2018-02-06", "", "", "0", "10238", "50300", "2" )

GameType  : 若發現有空隙沒用到的GameType可以使用，或由目前的往上增加
GameTypeName  : 電腦版看HTML5 Desktop、手機看HTML5 Mobile頁籤的Game
OpenDate : 上線的前一天。如2/7上線則為2/6
ModuleID : 電腦版看HTML5 Desktop、手機看HTML5 Mobile頁籤的 ModuleID
ClientID: 電腦版看HTML5 Desktop、手機看HTML5 Mobile頁籤的ClientID
GameCommGroup : 手機板的都是14，電腦版的HTML5 Desktop頁籤Category
SLOTS 老虎機
Table Games 桌上遊戲
PROGRESSIVES 彩金遊戲
	 

`WagersDB23`.`GameID`
語法範例:
INSERT INTO `WagersDB23`.`GameID` (`GameType`, `HTML5`, `zh`, `zh-tw`, `en`, `id`, `vi`, `fr`, `de`, `el`, `it`, `ja`, `ko`, `ru`, `es`, `tr`, `pt-br`) VALUES 
("23973", "girlsWithGunsJungleHeat", "", "", "", "", "", "", "", "", "", "", "", "", "", "", ""),
("23634", "girlsWithGunsJungleHeatDesktop", "", "", "", "", "", "", "", "", "", "", "", "", "", "", "")

HTML5 : 手機板的HTML5 Mobile ，電腦版的HTML5 Desktop 都是文件Game ID

`WagersDB23`.`GameMenuSetV3`
語法範例:
INSERT INTO `WagersDB23`.`GameMenuSetV3` (`GameType`, `MenuID`, `Sort`, `HallID`) VALUES 
#SLOTS, 
("23973", "1" , "553", "0"), 
("23973", "2" , "41" , "0"), 
("23973", "3" , "557", "0"), 
("23973", "84", "553", "0"),
#SLOTS, 
("23634", "1" , "560", "0"), 
("23634", "2" , "48" , "0"), 
("23634", "3" , "564", "0"), 
("23634", "84", "560", "0")

 
MenuID : 看該款屬於哪一類型的 若為老虎機則為3
Sort : 看MenuID 為3的 最後一號+1

提供給PMO網址:
手機 HTML5 Mobile
https://mobile2202.gameassists.co.uk/MobileWebServices_40/casino/game/launch/iGamingA2HTML5/girlsWithGunsJungleHeat/zh-tw/?lobbyURL=&bankingURL=&username=apitest21&password=bbin888&currencyFormat=%23%2C%23%23%23.%23%23&logintype=fullUPE&xmanEndPoints=https://xplay2202.gameassists.co.uk/xman/x.x

電腦HTML5 Desktop
 https://mobile2202.gameassists.co.uk/MobileWebServices_40/casino/game/launch/iGamingA2_Desktop/girlsWithGunsJungleHeatDesktop/zh-tw/?lobbyURL=&bankingURL=&username=apitest21&password=bbin888&currencyFormat=%23%2C%23%23%23.%23%23&logintype=fullUPE&xmanEndPoints=https://xplay2202.gameassists.co.uk/xman/x.x&host=Desktop

遊戲名稱ID : 手機看HTML5 Mobile  電腦HTML5 Desktop 該遊戲的 Game ID

組測試下注流程:
網址的帳密要改為bin96742256  密dd9d7e59
進遊戲下注完成後

要到中繼站下語法http://pma-ci.slave.prod/index.php
選擇WagersDB23-中繼DB-BETLOG


SELECT DisplayName, ModuleID, FROM `tb_Betlog_TNG2` WHERE `AccountNo` = 'bin96742256' AND `RoundDate` = '2018-01-30' AND `GameStartTime` >= '2018-01-30 08:38:00' AND `GameStartTime` <= '2018-01-30 08:43:59'

1.	確認每一款的ModuleID與ClientID與文件是否相同
若不正確，請跟MG確認。

2.	並根據下注回傳的DisplayName 去修改GameType裡的DisplayName資料，手機版的前面要多加*
修改範例:
UPDATE `WagersDB23`.`GameType` SET `DisplayName` = '*Girls With Guns - Jungle Heat'  WHERE `GameType` = 23973;

UPDATE `WagersDB23`.`GameType` SET `DisplayName` = 'Girls With Guns - Jungle Heat'  WHERE `GameType` = 23634;

上線需開啟的開關 : 
`WagersDB23`.`GameType`
範例: 美女抢手丛林激战
電腦版(23973)的
HTML  : Y 
PublicEnable : Y
MobileEnable : N
手機板(23634)的
HTML: Y
PublicEnable : N 
MobileEnable : Y










概念補充說明:
MG遊戲開放時程 : 兩個月才開放一次11、12月MG通知的遊戲，則在12月底至1月初之間整理，預計在2月份上線，而1、2月通知開放的清單，則在2月底3月初整理預計4月份上線，以此類推。整理時有重複的遊戲需要列出關閉清單，並且WagersDB23.GameType .OpenDate要再往前一個月，如2/6號 則改為1/6號，讓icon不顯示新遊戲。
提供給PMO網址: 使用帳號: apitest21 密碼: bbin888是沒錢的帳號。此網址是提供在『MG開放與關閉資料』裡面，同時一起上傳WERP。
組測試下注流程 : 此帳bin96742256  密dd9d7e59是正式站的test04 vip廳的帳號rd3test2，若沒錢測試，要轉帳至MG 。 
中繼站語法 : GameStartTime是巴黎時間，此次是(台灣時間)下午4點多下注，往後扣8小時，為早上8點，RoundDate 是美東時間，因(台灣時間)過12點下注，所以會是同一日2018-01-30。假若是(台灣時間)上午10點多下注，則RoundDate為2018-01-29日。
組DB語法 : GameCommGroup若企劃有說該款遊戲為特色遊戲則設為3
新增正式站 發送WERP範例參考
https://cy.iwerp.net/tech-request/require/require02.xhtml?m=0hX0-QWTTpebKDAgK-PfCe8cl2-sSwhmQDj_b3dRTtHEEhFa5_B4KtlSw7z_Z0QSAEjI-00EmdJxDGs9s0HDELUW0Vb2OOSp_tUorvsrJTaHQHCVL5dvU0TqIPUK7wXqSId4eoQnJ87yiToyOR-htw==&as=3ee2f079-0f20-450e-82db-9490c23fe393
上線需開啟的開關 : 
HTML : 若在遊戲只要有歸類到Excel 下圖的這兩個頁籤則為Y 
 
PublicEnable :若該款遊戲有在HTML5 Desktop頁籤，則電腦版的GameType 的PublicEnable要開為 Y，MobileEnable開為N
MobileEnable :若該款遊戲有在HTML5 Mobile頁籤，則手機版的GameType 的 MobileEnable要開為 Y，PublicEnable開為N

Flash(都是關閉為主，目前不會用到，留作參考)
https://redirect.contdelivery.com/Casino/Default.aspx?applicationid=1023&csid=15057&serverid=15057&theme=igamingA2&usertype=0&variant=instantplay&sext1=apitest21&sext2=bbin888&gameid=GirlsWithGuns&ul=zh-tw
Flash 的看 Flash gameID 裡面的GameCode



擂台賽

要通知 研一 & Mobile & PMO 三方
午安 ~
「程式需求」      整合站 @0001  - 【MG擂台賽___2月份 - “ 吠吠扬扬迎狗年”】相關需求     
這邊提供 擂台賽的GameType 再麻煩了 (bow)

提供文件請參考 『MG-吠吠扬扬迎狗年-擂台賽』

程式部分請參考以下連結
http://gitlab.rd3.vir888.com/rd3/ipl_main/commit/48e106a3de08652b2f1db26cecb243ad39e21ae0

member/www/outside.api/mg.game.main.php
member/www/outside.api/mghtml5.forward.game.php
不分手機或電腦版的 GameType都相同都要加入。
