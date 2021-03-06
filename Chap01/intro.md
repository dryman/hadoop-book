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

[^1]: 又另譯高延展性程式，或是高擴展性程式。目前似乎沒有一個好用的中文翻譯
