## 前言

Bernhard Mueller 撰寫, OWASP 行動應用專案。
科技的進步是相當快速的。就在不到10年前，智慧手機只是一個對於精通技術的商務人士所使用的一個昂貴的玩具，而且是一個又大然後有一個小小鍵盤的玩具。到今天，智慧手機已經變成我們每天不可缺少的一部份。我們開始依賴它，不只是在資訊的吸收上，甚至到導航，溝通，它已經成為了我們每天生活中工作和社交上一個獨特，重要而且難已被取代的工具。

每個新的技術也相對的帶著新的安全風險，而要跟上這些一直不斷出現的風險也是資安產業需要面對的一個大挑戰。防衛者一直都慢了幾步，舉例來說，一般人都會用舊的思維去做很多事情：智慧手機就像一台小電腦，行動應用程式就像是電腦上的程式，所以兩個東西對於資訊安全上的需求，應該就是一樣的吧？可是事實並非如此。智慧手機的作業系統與電腦的作業系統差異甚多，而行動應用程式也跟一般的網頁或電腦應用不同。再舉一個例子，電腦一般都會用特徵碼型態的防毒軟體去進行掃描，而在現今的行動作業系統上，這完全無法被合理化：因為這不只跟行動應用程式的發行模式不符合，同時也因為系統沙箱本身的限制造成技術上的困難。同時，有些弱點問題，例如緩衝區溢出或是跨網注入攻擊等點，是與常常以特殊或不尋常方式去執行的行動應用程式不相關，而這些問題卻是常在一般作業系統或是桌機應用程式上會看到的（當然也會有些例外）。

隨著時間的前進，我們的行業已經更好地掌握了行動應用威脅領域。 事實證明，行動應用安全是完全與資料保護相關：應用程式儲存了我們的個人訊息，圖片，錄音，筆記，帳戶資料，商業消息，位置等等。 它們成為了我們的端末設備，將我們連接到我們每天使用的服務，並做為處理我們與他人之間交換每條訊息的通信中心。 入侵一個人的智慧手機，你就可以獲得關於這個人未經過濾的與他息息相關的一切。 當我們認為行動電話更容易丟失或被盜或行動應用的惡意軟體正在增加時，對資料保護的需求就會變得更加明顯。

因此，行動應用的安全標準必須注意如何處理行動應用，儲存和保護敏感資料。 儘管iOS和Android等現代行動作業系統提供了許多用於安全資料儲存和通信的良好API，但是仍必須正確實施和使用這些API才有效。 資料儲存，應用程式之間的通信，加密API的正確使用和安全的網路通信只是需要仔細考慮的其中一方面而已。

需要這個行業共識的一個重要問題是，在保護資料的機密性和完整性方面應該要做到多嚴謹。 例如，我們大多數人都同意行動應用程式應該在TLS交換中驗證伺服器憑證。 但是SSL憑證綁定呢？ 不這樣做會導致漏洞嗎？ 應用程式處理中有要求要處理敏感資料，是否應該處理，還是這可能適得其反？ 我們是否需要加密儲存在SQLite資料庫中的資料，即使作業系統對應應用程式進行沙盒處理？ 適用於一個應用程式的需求可能對另一個應用程式不切實際。 MASVS嘗試使用不同的威脅情況和其驗證級別來標準化這些需求。

此外，出現於根系統中的惡意軟體和遠端管理工具使人們意識到行動作業系統本身具有可利用的缺陷，因此有越來越多的容器化策略用於為敏感資料提供額外保護並防止用戶端篡改。 這反而讓事情變得更複雜。 硬體支援的安全功能和作業系統級容器化解決方案（例如Android for Work和Samsung Knox）確實存在，但它們並非在所有的設備上都可以使用。 就像OK繃一樣，這可以施作於軟體的保護措施 - 但遺憾的是，沒有任何標准或測試流程來驗證這些類型的保護措施。

因此，行動應用安全測試報告充斥各處：例如，一些測試人員將Android應用中缺乏模糊處理或根檢測報告認定為“安全漏洞”。 另一方面，字符串加密，除錯器檢測或控制流混淆等措施不被視為需被強制執行。 然而，這種看待事物的二位元方式沒有任何意義，因為彈性不是二位元命題：它取決於一個旨在防範的特定用戶端威脅。 軟體保護並非無用，但最終可以繞過它們，因此絕不能將它們用作資安控制的替代品。

MASVS的總體目標是為行動應用安全（MASVS-L1）提供基准，同時還允許包含縱深防禦措施（MASVS-L2）和針對用戶端威脅的保護（MASVS-R））。 MASVS旨在實現以下目標：

- 為尋求開發安全行動應用程式的軟體架構師和開發人員提供需求;
- 提供可在行動應用安全審查中進行測試的行業標準;
- 明確軟體保護機制在行動安全中的作用，並提供方式驗證其有效性的需求;
- 針對不同範例建議其安全級別並提供具體建議。

我們知道要做到 100％ 的行業共識是不可能實現的。 儘管如此，我們希望MASVS能夠在行動應用程式開發和測試的所有階段提供指導。 作為開源標準，MASVS將隨著時間的推進而發展，我們歡迎任何貢獻和建議。
