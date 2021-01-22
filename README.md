# The Making of Digital Crate
數位作品箱的製作與相關工具
_____
面臨當代作品媒材不穩定性與因地制宜的短暫性，以及科技日新月異的推陳出新，時基媒體作品（Time-based Media）從典藏到維護都為典藏單位帶來許多的挑戰，最常見的疑惑是：「究竟什麼是作品？」、「時基作品被典藏進入美術館庫房的是什麼？」

經過將近20年的摸索與對話，典藏機構與圖書資訊管理及其他相關領域合作，逐漸建置一套可以信賴的機制與長期保存的策略，不僅在對面不同的技術和格式時，可以提供具有一制性的決策模式，並利用數位物件的特質，對照實體庫房的管理模式與思維，打造可以有效驗證數位物件的完整性、並控管安全層級的數位庫房。

這篇內容旨在提供美術館相關工具與指令，得以在購藏的過程中，製作具備作品指紋（Checksum）、數位影音檔案技術設定的元資料（Technical Metadata）和標準化的數位作品箱（BagIt），以確保數位物件在入庫過程不遭受任何可能的變動與修改，以確認作品的真實與完整性。

### 由保存領域共同開發的自由軟體 ###

以下介紹在時基修護領域常用的自由軟體，其開放程式碼的特質，尤其在數位保存的領域運用受到相當程度的重視與歡迎，其中一個原因在於專用（proprietary）軟體例如微軟Windows，一旦格式、技術遭到淘汰，或是經營公司消失倒閉，因為背後的程式碼與技術從未開放，未來維持相關的軟體將會非常的困難也極具挑戰性。

基於保護資料不受篡改的特性，數位保存與時基媒體領域大量採用數位鑑識科學使用的軟硬體，原生數位工作站最基本的架製可以使用BitCurator、VirtualBox及外接防讀寫硬體。
- [Bitcurator](https://wiki.bitcurator.net/index.php?title=Main_Page) 是由北卡羅來納大學教堂山分校（School of Information and Library Science at the University of North Carolina, Chapel Hill）和馬里蘭人文技術學院（Maryland Institute for Technology in the Humanities）的圖書資訊科學學院共同合作開發的一個自由系統。BitCurator綜合許多自由軟體，為博物館、檔案局、圖書館等的數位館藏提供具有數位鑑識功能的工作平台。
- 在PC或Mac的工作環境下，Bitcurator需要安裝[Virtual Box](https://www.virtualbox.org/wiki/Downloads) 才能運行，VirtualBox是虛擬化平臺，提供使用者在不同的作業系統上，虛擬其它不同的作業環境。
- [Forensic ComboDock FCDv5.5](http://www.cru-inc.com/products/wiebetech/forensic-combodock-v5-5/) 是在Digital Intelligence所推出的[FRED]（https://digitalintelligence.com/products/fred/) 之外，價錢較為平易的工具，在連結外接存取媒介時，具有只讀不寫的功能，能夠滿足美術館基本的需求，藉此確認數位檔案的不變性。

以下建議的工作流程，主要：
Guymager or ddrescue -> ffmpeg -> mediainfo -> bagit-python <br>

## MediaInfo
[MediaInfo](https://mediaarea.net/en/MediaInfo) 是一個開放原始碼的自由軟體 ，它可以用來顯示媒體檔案相關的技術資訊，以及許多視聽相關的標籤資訊。MediaInfo支援大量流行的影片格式（例如AVI、WMV、QuickTime、Real、DivX、XviD）以及新興的格式，例如MKV。

Mediainfo用來存取視聽檔案的相關技術元資料（Technical Metadata），並可用以下的指令，將技術元資料轉存為國際通用可延伸標記式語言XML。
    
    mediainfo (inputfile) --output=XML --logfile=(outputfile.log)
