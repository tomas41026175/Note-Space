# 領域驅動設計(Domain Driven Design)
-----
## intro

- DDD 是 Domain-Driven Design 的縮寫。其主要的思想是，我們在設計軟件時，先從業務出發，理解真實的業務含義，將業務中的一些概念吸收到軟件建模中來，避免造出“大而無用”軟件。也避免軟件設計沒有內在聯系，否則一團散沙，無法繼續演進。

- 領域（Domain）是軟件要解決的業務問題和訴求。通俗來說，領域就是業務需求。不過這些業務有一些內在邏輯需要分析，存在一些專業性，比如財務、CRM、OA、電商等不同領域。計算機只是自動化的處理領域問題，領域知識可能不是開發人員擅長的。

- 領域模型（Model）是業務概念在程序中的一種表達方式。面向對象的編程語言使用類作為業務概念的承載體，也可以用 UML 可視化的表達模型。模型是用來設計和理解整個軟件結構，切記不要事無巨細的模型。在模型思維中，模型是簡單的，能反應業務概念即可。

- 通用語言（Ubiquitous language）是指在軟件設計中，業務人員和開發人員需要使用無歧義的統一語言來對話。這些語言包括對概念的統一理解和定義，以及業務人員參與到軟件建模中，否則業務的變化會造成軟件巨大的變化。

- 模型驅動的設計和面向對象，是計算機對現實世界的映射。理解現實世界需要用到哲學的工具，比如概念的內涵和外延、本體和客體，因此 DDD 會有一點哲學的意味，需要適應。

- DDD 最能展現其價值的地方就是他的方法論可以被用來有系統地解構複雜的問題，而不是單純的就軟體設計來做討論。

- **DDD 很大的的一個部份是在討論商業，系統，使用者流程的分析**，而不是技術面上的分析。而這也是，我個人認為，其最大的價值所在。在經過這個分析和設計之後，理想狀況就是，你的團隊可以用一樣詞彙來溝通，系統和團隊間應該有清楚的界線；而且，對你的每一個商業流程圖，你應該可以在你的資訊系統內找到相對應的功能和清楚的對應關係。

- 這個方法論在不成熟的產品上，很多時候會是一個浪費。

## 建模概念

- 實體（Entity）是領域模型面向對象語言的具體體現，一般是一個類。領域模型可以是一個廣義的概念，建模的結果和中間過程其實都可以看做模型。 值對象 （Value Ojbect）是一種特殊的實體，但一般認為沒有自己的狀態和生命周期。實體可以使用 ID 標識，但是值對象是用屬性標識，任何屬性的變化都視為新的對象。比如一個銀行賬戶，可以由 ID 唯一標識，幣種和余額可以被修改但是還是同一個賬戶；交易單中的金額由幣種和數值組成，無論修改哪一個屬性，金額都不再是原來的金額。

- 聚合 （Aggregate）是一組生命周期一致的實體集合，表達統一的業務意義。 聚合的意義在於讓業務統一、一致，在面向對象中有非常重要價值。

- 聚合根（ Aggregate Root）是聚合中最核心的對象，是聚合的領航員。要管理聚合必須使用一個聚合根，然後使用聚合根來實現發現、持久化聚合的作用。聚合中有且只有一個聚合根，一個實體可以獨立作為一個聚合。

- 界限上下文（ Bounded context） 有統一業務目標和概念的聚合組成的集合。大型項目都會存在多種模型，這些模型在不同的上下文中，可能有相似業務概念，但是他們的業務目標完全不一樣。識別上下文可以從概念的二義性著手，比如商品的概念在物流、交易、支付含義完全不一樣，但具有不同內涵和外延，實際上他們處在不同上下文。

- 界限上下文可以用於微服務劃分、避免模型的不正確覆用帶來的問題。

## 程序架構概念

- 服務（Service）是領域模型的操作者，承載領域的業務規則。 模型用於承載數據和系統狀態，業務規則的事情就交給服務，讓邏輯更為清晰明了。

- 模塊（Module）同領域的類或者對象組成的集合。 模塊的劃分沒有固定的模式，如果不是特別覆雜的業務邏輯可以使用上下文劃分模塊，次一級的包使用對象類型組織即可。

- 工廠（Factory）是以構建模型為職責的類或方法。工廠可以把不同的業務參數轉化為領域模型，在簡單的業務邏輯中可以不使用工廠，實際工作中工廠不是一個具體的概念，為了簡化我們可以把靜態工廠方法放到 DOT 或者其他類中。 倉庫（Repository）是以持久化領域模型為職責的類。 倉庫的目的是屏蔽業務邏輯和持久化基礎設施的差異，由於大部分項目使用關系數據庫作為存儲基礎設施，倉庫層大多被 ORM 代為實現，如果不使用 ORM，需要自己實現倉庫。

- 規格 (Specfication) 是一些特殊的業務規則，一般表現為計算結果是真或者假的函數。規格可以用於業務邏輯的校驗、查詢條件，一般來說規格是可選的，不過對於覆雜的業務抽象出規格可以覆用這些業務邏輯。

## 分層設計概念

- DDD 在落地時可以使用四層構架，這四層有不同的意義，必要時候可以進行裁剪。

- 用戶界面層，向用戶顯示信息，處理用戶輸入。 對於服務端應用而言，用戶界面不是指 UI，而是指接入的協議，HTTP、websocket、LDAP 等協議都屬於用戶界面層。

- 應用層，組織業務場景，編排業務，隔離場景對領域層的差異。應用層最大的用處是處理業務場景，對應面向對象的思想就是 “關注點分離”。如果是一個用戶社區應用，用戶面、作者面、後台管理多個面實際是多個應用，而共享一套領域代碼，可以做到既能關注點分離，又能覆用核心業務邏輯的目的。

- 領域層，實現具體的業務邏輯、規則。 實際處理業務的地方，領域層需要對應用層提供無差別的服務和能力。比如用戶注冊，用戶可以通過郵箱自己注冊，也可以由管理員在後台應用添加。注冊的邏輯需要由領域層完成，但是處理用戶輸入參數的部分需要由應用層屏蔽。

- 基礎設施層，提供具體的技術實現，比如存儲，基礎設施對業務保持透明。 如果無法對領域層提供透明的能力，說明這部分代碼不適合放入基礎設施層。比如，在使用 JPA 時，Repository 的 Interface 定義，不應該認為是基礎設施，而 ORM 對這些 Interface 的實現和具體的 SQL 處理則可以認為是基礎設施層的代碼。

- 在使用框架時，需要弄清楚分層不是絕對的。比如，Spring MVC 的 controller，實際不是用戶界面層，而是應用層，因為接入協議的已經被框架處理了。

