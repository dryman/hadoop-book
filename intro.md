什麼是大數據
==========

這幾年來大數據非常的熱門，到處都有大數據分析的演講。
演講內容通常是宣傳各種大數據分析成功的案例。
但實際上大數據該怎麼做呢？
大部份的討論似乎都僅止於怎麼蒐集大量的數據，
然後用個工具（hadoop/spark）後就會馬上變出商機和錢來。

筆者是工程師而非技術或平台傳教者，我想用務實一點的方式來看待大數據。
大數據技術最重要的核心在於如何設計可以高性能處理大量數據的程式 (highly scalable programs.) [^1]

目前大數據相關工作可以粗分幾類。有資料系統串接者，
設計大數據演算法實做的人，以及管理大型叢集 (cluster) 的工程師。
很多人對大數據工程師的理解還停留在資料系統串接者的程度，
以為只要將資料匯入某個神奇系統，就能將自己想要的結果生出來。
但實際上數據量變得很大時，我們往往需要自己客制化自己的資料系統，並且撰寫特殊的演算法處理之。
以台灣和美國業界而言，第二種工程師是最稀少也需求量最高的。
這本書的目的就是由淺入深的介紹如何成為此類型的工程師。

有些人可能會有點意外，為什麼資料科學家不在其列？
因為其實資料科學從一開始就是和大數據獨立的概念。
而且一般而言大多數資料工程師處理的數據量也偏小，使用的演算法也多是 $$O(N^2)$$ 以上的複雜度。
閱讀本章之後，請不要再把「大數據分析」一詞掛在口中了。
只有非常少數能同時精通大數據演算法設計及資料科學的人，才有資格用到這個字。


數據處理簡史
----------

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

### 大數據技術架構的起源

以下內容節錄並翻譯自[The history of hadoop][historyofhadoop]。
作者有跟最早的hadoop開發者Doug Cutting求證過細節，而且得到他的背書！

1997 Lucene
Search Engine
2000 open sourced, 2001 moved to Apache Software Foundation

End of 2001, Doug Cutting + Mike Cafarell started Apache Nutch
for web page indexing. Suffer in scalling (100M), single machine.

* schemaless with no predefined structure, i.e. no rigid schema with tables and columns (and column types and sizes)
* durable once data is written it should never be lost
* capable of handling component failure without human intervention (e.g. CPU, disk, memory, network, power supply, MB)
* automatically rebalanced to even out disk space consumption throughout cluster


GFS 2003
Google MR 2004

2004 Nutch Distributed FileSystem
1PB -> 20PB

2005 MR is part of Nutch
2006 Jan aquired into yahoo
2006 Feb, becomes hadoop
2007 Yahoo! reported to use 1000 nodes.

2008. Hadoop separated out from Lucene.
many sub projects appears
Coudera was born.

2009 Amazon elastic MR

2010 Hortonworks
2012 42000 nodes
2012 YARN

2009 UC Berkeley. 2010 open sourced, 2013 ASF. 2014 top level.


2006 Cutting went to Yahoo.
Hadoop separated out from Nutch.

Side note: 其實hadoop其中一個很有價值的應用是做BI
但它的設計架構一開始並不是針對BI起家的
以筆者個公司來說，就必須寫非常多的架構來讓它變得更適合BI




* HPC
* RDBMS
* hadoop

[historyofhadoop]: https://medium.com/@markobonaci/the-history-of-hadoop-68984a11704



大數據工程師的核心技能指標
-------------------


大數據工程技能樹該如何點？
----------------------


[^1]: 又另譯高延展性程式
