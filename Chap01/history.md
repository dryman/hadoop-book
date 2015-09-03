數據處理簡史
==========

不知道在學習大數據的讀者們有沒有想過，超級電腦的發明是1960年代的事，
為什麼直到近年大數據才紅起來？任何科技及技術都有其歷史脈絡，
學習一點相關歷史會讓自己在追逐新科技時更清楚自己要解決的問題的定位在哪邊。

### 傳統上的叢集運算

大型叢集電腦設計其實從電腦誕生的年代就有了。
傳統上的計算主流偏向科學計算（例如氣候模擬、飛彈、流體力學）等 High Performance Computing。
這類型的演算通常用到大量的線性代數、大量的浮點數運算、但實際處理的資料多半不會太大。
事實上，在許多學術及軍事機構中，還是有大量的這種超級電腦在進行演算以輔助研究。
它們從傳統上就與新進的大數據佔有不同市場，
使用的語言也不同 (fortran還是目前最快的 high performance computing language)。

不過隨著網路科技的演進，我們有了一個新的大型叢集運算的需求。
我們每天在網路上的各種行為，都會被記錄下來：搜尋、逛頁面、買東西、逛facebook、看到的廣告等等。
將這些數據蒐集起來並且拿來算錢，成了新的叢集運算新星。
處理這些數據時，和傳統的HPC非常不同。HPC的數據量一般不大，但需要大量的浮點數計算；
大數據技術則反之，數據量很大，但計算相較簡單。
與此相對的硬體設計也完全不同。HPC的硬體叫做blade，硬碟很小，但CPU、記憶體、主機板通通都是高檔貨；
大數據的硬體則通常要求每台主機都要有很大的硬碟，使得很多資料不需要在網路中傳輸，可以在本機計算就在本機計算。

## 大數據技術架構的起源

以下內容節錄並翻譯自 [The history of hadoop][historyofhadoop] 。
原作者有跟最早的hadoop開發者 Doug Cutting 求證過細節，而且得到他的背書！

一切源自於 Doug Cutting 在 1997 年開始的搜尋引擎專案 [Lucene](https://lucene.apache.org/core/) 。
Lucene 在 2000 年開放原始碼，並在 2001 年變成 ASF (Apache Software Foundation)[^1] 的專案。
直至今日，許多熱門的搜尋引擎實做 [Apache Solr](http://www.apache.org),
[Elastic search](https://www.elastic.co) 的底層都還是使用 Lucene 。
不過在一開始的時候 Lucene 只能搜尋很少的東西，而且也只能在一台機器上跑。

2001 年底， Doug Cutting 和 Mike Cafarell 將興趣轉向替網頁建立搜尋索引，
並開啟了一個新的專案名為 [Apache Nutch](http://nutch.apache.org) 。
Nutch 是網路爬蟲，使用 Nutch 爬下整個世界的網站，再使用 Lucene 建立索引進行搜尋。
如同大部份的開發專案，一開始 Cutting 與 Cafarella 只專注於將功能寫出來，之後再最佳化。
但是當欲建檔的網頁是全世界的時候，無法處理大數據的技術瓶頸就出現了。
當年他們能建檔的網頁的上限是一億 (100M)，而且只能在一台三千美金的機器上面跑。
如何處理大量的數據變成當時他們最迫切需要解決得問題。

### HDFS (Hadoop Distributed File System) 誕生

為了使 Nutch 能夠處理更多資料，Cutting 與 Cafarella 開始思考多台機器的儲存方案。
這儲存方案必須要符合以下的需求：

* 不需要傳統資料庫的 schema (鷹架)
* 一旦資料寫入系統就不需要擔心資料遺失 (durable)
* 如果有硬體壞掉，系統會自動處理好（備份、轉移資料等）
* 自動平衡資料負載。不需要手動將資料從一台伺服器搬到另一台去。

他們花了幾個月試圖實做這些規格，不過就在 2003 年， Google 發表了一篇 Google File System paper 。
裡面的描述恰恰好就符合他們要追求的檔案系統。
於是在 2004 年，他們就依據這篇 paper 實做出了 Nutch Distributed File System (NDFS.)

讀者可能會有疑問：為什麼不去使用當時其他的分散式檔案系統呢？
當時已經有許多超級電腦的儲存方案，為什麼不用這些方案呢？
筆者目前找不出完整的原因（也許要訪問 Doug Cutting吧）
但現有的 HDFS 比其他分散式儲存系統便宜大約二十倍，而且性能更好。
而且傳統的Xen/NAS等分散式儲存系統還需要專門的硬體及機房，
如果當時他們使用這樣的方案也許我們就不會看到大數據業蓬勃發展了。

### Map Reduce

有了分散式儲存技術還不夠。 Cutting 等人當時苦思如何善用手上硬體來進行平行化計算。
儘管當年MPI等HPC平行計算技術已經成熟，但卻主要用於小量快速資料傳輸。
在2004年 Google 又發表了一篇 Map Reduce 的 paper 。
這個平行計算的抽象化非常的通用，從網頁的權重計算、字詞分析、到網路流量的分析等都可以通用。
本書會以這個概念為主軸介紹如何設計出一系列的演算方式來解決大數據的問題。

2005 年七月， Cutting 宣布 Nutch 改寫以 Map Reduce 作為其建檔的計算引擎。

### Hadoop 出生

2006 年六月， Cutting 將 NDFS 及 Map Reduce 從 Nutch 專案中抽出來，
放在 Lucene 的子專案下，並重新命名為 Hadoop。

大約在同時間， Yahoo! 以 Eric Baldeschwieler
為首的團隊正在努力研究下一世代的 Yahoo 搜尋技術。
他們相中 Cutting 的 GFS/MapReduce 實做，
並且大膽的決定要以這個 prototype 在未來取代他們當年的搜尋引擎實做。
就在那年 Baldeschwieler 將 Cutting 納入團隊。

2007 及 2008 年有許多公司前仆後繼的加入 hadoop 的開發，包括
Twitter, Facebook, LinkedIn 等等。而在 2008 年時 Hadoop
從 Lucene 專案中切開來，成為自己獨立的專案。許多衍伸的專案也在
2008 年時加入 Hadoop 家族，如 Yahoo! pig, Facebook Hive,
ZooKeeper, HBase 等等。

之後重要的 Hadoop 編年史：

* 2008 Cloudera 成立
* 2009 Amazon elastic MR 誕生
* 2010 Hortonworks 從 Yahoo! 拆分出來成為新公司
* 2010 UC Berkeley open sourced Spark
* 2012 YARN 誕生
* 2012 Yahoo! 宣布他們的叢集達到 42000 nodes，為當時最大的 Hadoop 叢集
* 2014 Spark 成為 ASF top level project。並開始獲得大量的關注

### Side note:
其實 Hadoop 其中一個很有價值的應用是做 BI (Business Intelligence)。
但它的設計架構一開始並不是針對BI起家的，而是更貼近於搜尋引擎建立索引這樣的工作。
在 BI 中最關鍵的事是處理時間序列的資料，資料清理，以及資料整合 (data join)。
以筆者個公司來說，就必須客制非常多的架構來讓它變得更適合 BI。
儘管 pig/hive 等上層工具一部分目的也是使其更容易操作 BI 。


[historyofhadoop]: https://medium.com/@markobonaci/the-history-of-hadoop-68984a11704
[^1]: Apache Software Foundation http://www.apache.org
