> 翻譯：CMW
# 集合類型 (Collection Types)
-----------------

本頁包含內容：

- [陣列（Arrays）](#arrays)
- [字典（Dictionaries）](#dictionaries)
- [集合的可變性（Mutability of Collections）](#mutability_of_collections)

Swift 語言提供經典的陣列和字典兩種集合類型來存儲集合數據。陣列用來按順序存儲相同類型的數據。字典雖然無序存儲相同類型數據值但是需要由獨有的標識符引用和尋址（就是鍵值對）。

Swift 語言裡的陣列和字典中存儲的數據值類型必須明確。這意味著我們不能把不正確的數據類型插入其中。同時這也說明我們完全可以對獲取出的值類型非常自信。 Swift 對顯式類型集合的使用確保了我們的代碼對工作所需要的類型非常清楚，也讓我們在開發中可以早早地找到任何的類型不匹配錯誤。

> 注意：
>
Swift 的陣列結構在被聲明成常量和變量或者被傳入函數與方法中時會相對於其他類型展現出不同的特性。獲取更多信息請參見[集合的可變性](#mutability_of_collections)與[集合在賦值和復制中的行為](09_Classes_and_Structures.html#assignment_and_copy_behavior_for_collection_types)章節。

<a name="arrays"></a>
## 陣列

陣列使用有序列表存儲相同類型的多重數據。相同的值可以多次出現在一個陣列的不同位置中。

Swift 陣列對存儲數據有具體要求。不同於Objective-C 的`NSArray`和`NSMutableArray`類，他們可以存儲任何類型的實例而且不提供他們返回對象的任何本質信息。在Swift 中，數據值在被存儲進入某個陣列之前類型必須明確，方法是通過顯式的類型標註或類型推斷，而且不是必須是`class`類型。例如： 如果我們創建了一個`Int`值類型的陣列，我們不能往其中插入任何不是`Int`類型的數據。 Swift 中的陣列是類型安全的，並且它們中包含的類型必須明確。

<a name="array_type_shorthand_syntax"></a>
### 陣列的簡單語法

寫Swift 陣列應該遵循像`Array<SomeType>`這樣的形式，其中`SomeType`是這個陣列中唯一允許存在的數據類型。我們也可以使用像`SomeType[]`這樣的簡單語法。儘管兩種形式在功能上是一樣的，但是推薦較短的那種，而且在本文中都會使用這種形式來使用陣列。

<a name="array_literals"></a>
### 陣列構造語句

我們可以使用字面語句來進行陣列構造，這是一種用一個或者多個數值構造陣列的簡單方法。字面語句是一系列由逗號分割並由方括號包含的數值。
`[value 1, value 2, value 3]`。

下面這個例子創建了一個叫做`shoppingList`並且存儲字符串的陣列：

    var shoppingList: String[] = ["Eggs", "Milk"]
    // shoppingList 已經被構造並且擁有兩個初始項。

`shoppingList`變量被聲明為“字符串值類型的陣列“，記作`String[]`。因為這個陣列被規定只有`String`一種數據結構，所以只有`String`類型可以在其中被存取。在這裡，`shoppinglist`陣列由兩個`String`值（`"Eggs"` 和`"Milk"`）構造，並且由字面語句定義。

> 注意：
>
> `Shoppinglist`陣列被聲明為變量（`var`關鍵字創建）而不是常量（`let`創建）是因為以後可能會有更多的數據項被插入其中。

在這個例子中，字面語句僅僅包含兩個`String`值。匹配了該陣列的變量聲明（只能包含`String`的陣列），所以這個字面語句的分配過程就是允許用兩個初始項來構造`shoppinglist`。

由於Swift 的類型推斷機制，當我們用字面語句構造只擁有相同類型值陣列的時候，我們不必把陣列的類型定義清楚。 `shoppinglist`的構造也可以這樣寫：

    var shoppingList = ["Eggs", "Milk"]

因為所有字面語句中的值都是相同的類型，Swift 可以推斷出`String[]`是`shoppinglist`中變量的正確類型。

<a name="accessing_and_mo​​difying_an_array"></a>
### 訪問和修改陣列

我們可以通過陣列的方法和屬性來訪問和修改陣列，或者下標語法。
還可以使用陣列的只讀屬性`count`來獲取陣列中的數據項數量。

    println("The shopping list contains \(shoppingList.count) items.")
    // 輸出"The shopping list contains 2 items."（這個陣列有2個項）

使用布爾項`isEmpty`來作為檢查`count`屬性的值是否為0 的捷徑。

    if shoppingList.isEmpty {
        println("The shopping list is empty.")
    } else {
        println("The shopping list is not empty.")
    }
    // 打印"The shopping list is not empty."（shoppinglist不是空的）

也可以使用`append`方法在陣列後面添加新的數據項：

    shoppingList.append("Flour")
    // shoppingList 現在有3個數據項，有人在攤煎餅

除此之外，使用加法賦值運算符（`+=`）也可以直接在陣列後面添加數據項：

    shoppingList += "Baking Powder"
    // shoppingList 現在有四項了

我們也可以使用加法賦值運算符（`+=`）直接添加擁有相同類型數據的陣列。

    shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
    // shoppingList 現在有7項了

可以直接使用下標語法來獲取陣列中的數據項，把我們需要的數據項的索引值放在直接放在陣列名稱的方括號中：

    var firstItem = shoppingList[0]
    // 第一項是 "Eggs"

注意第一項在陣列中的索引值是`0`而不是`1`。 Swift 中的陣列索引總是從零開始。

我們也可以用下標來改變某個已有索引值對應的數據值：

    shoppingList[0] = "Six eggs"
    // 其中的第一項現在是"Six eggs" 而不是"Eggs"

還可以利用下標來一次改變一系列數據值，即使新數據​​和原有數據的數量是不一樣的。下面的例子把`"Chocolate Spread"`，`"Cheese"`，和`"Butter"`替換為`"Bananas"`和`"Apples"`：

    shoppingList[4...6] = ["Bananas", "Apples"]
    // shoppingList 現在有六項

> 注意：
>
>我們不能使用下標語法在陣列尾部添加新項。如果我們試著用這種方法對索引越界的數據進行檢索或者設置新值的操作，我們會引發一個運行期錯誤。我們可以使用索引值和陣列的`count`屬性進行比較來在使用某個索引之前先檢驗是否有效。除了當`count`等於0 時（說明這是個空陣列），最大索引值一直是`count - 1`，因為陣列都是零起索引。

調用陣列的`insert(atIndex:)`方法來在某個具體索引值之前添加數據項：

    shoppingList.insert("Maple Syrup", atIndex: 0)
    // shoppingList 現在有7項
    // "Maple Syrup" 現在是這個列表中的第一項

這次`insert`函數調用把值為`"Maple Syrup"`的新數據項插入列表的最開始位置，並且使用`0`作為索引值。

類似的我們可以使用`removeAtIndex`方法來移除陣列中的某一項。這個方法把陣列在特定索引值中存儲的數據項移除並且返回這個被移除的數據項（我們不需要的時候就可以無視它）:

    let mapleSyrup = shoppingList.removeAtIndex(0)
    //索引值為0的數據項被移除
    // shoppingList 現在只有6項，而且不包括Maple Syrup
    // mapleSyrup常量的值等於被移除數據項的值"Maple Syrup"

數據項被移除後陣列中的空出項會被自動填補，所以現在索引值為`0`的數據項的值再次等於`"Six eggs"`:

    firstItem = shoppingList[0]
    // firstItem 現在等於 "Six eggs"

如果我們只想把陣列中的最後一項移除，可以使用`removeLast`方法而不是`removeAtIndex`方法來避免我們需要獲取陣列的`count`屬性。就像後者一樣，前者也會返回被移除的數據項：

    let apples = shoppingList.removeLast()
    // 陣列的最後一項被移除了
    // shoppingList現在只有5項，不包括cheese
    // apples 常量的值現在等於"Apples" 字符串

<a name="iterating_over_an_array"></a>
### 陣列的遍歷

我們可以使用`for-in`循環來遍歷所有陣列中的數據項：

    for item in shoppingList {
        println(item)
    }
    // Six eggs
    // Milk
    // Flour
    // Baking Powder
    // Bananas

如果我們同時需要每個數據項的值和索引值，可以使用全局`enumerate`函數來進行陣列遍歷。 `enumerate`返回一個由每一個數據項索引值和數據值組成的鍵值對組。我們可以把這個鍵值對組分解成臨時常量或者變量來進行遍歷：

    for (index, value) in enumerate(shoppingList) {
        println("Item \(index + 1): \(value)")
    }
    // Item 1: Six eggs
    // Item 2: Milk
    // Item 3: Flour
    // Item 4: Baking Powder
    // Item 5: Bananas

更多關於`for-in`循環的介紹請參見[for 循環](05_Control_Flow.html#for_loops)。

<a name="creating_and_initializing_an_array"></a>
### 創建並且構造一個陣列

我們可以使用構造語法來創建一個由特定數據類型構成的空陣列：

    var someInts = Int[]()
    println("someInts is of type Int[] with \(someInts.count) items。")
    // 打印"someInts is of type Int[] with 0 items。"（someInts是0數據項的Int[]陣列）

注意`someInts`被設置為一個`Int[]`構造函數的輸出所以它的變量類型被定義為`Int[]`。

除此之外，如果代碼上下文中提供了類型信息， 例如一個函數參數或者一個已經定義好類型的常量或者變量，我們可以使用空陣列語句創建一個空陣列，它的寫法很簡單：`[]` （一對空方括號）：

    someInts.append(3)
    // someInts 現在包含一個INT值
    someInts = []
    // someInts 現在是空陣列，但是仍然是Int[]類型的。

Swift 中的`Array`類型還提供一個可以創建特定大小並且所有數據都被默認的構造方法。我們可以把準備加入新陣列的數據項數量（`count`）和適當類型的初始值（`repeatedValue`）傳入陣列構造函數：

    var threeDoubles = Double[](count: 3, repeatedValue:0.0)
    // threeDoubles 是一種Double[]陣列, 等於[0.0, 0.0, 0.0]

因為類型推斷的存在，我們使用這種構造方法的時候不需要特別指定陣列中存儲的數據類型，因為類型可以從默認值推斷出來：

    var anotherThreeDoubles = Array(count: 3, repeatedValue: 2.5)
    // anotherThreeDoubles is inferred as Double[], and equals [2.5, 2.5, 2.5]

最後，我們可以使用加法操作符（`+`）來組合兩種已存在的相同類型陣列。新陣列的數據類型會被從兩個陣列的數據類型中推斷出來：

    var sixDoubles = threeDoubles + anotherThreeDoubles
    // sixDoubles 被推斷為Double[], 等於[0.0, 0.0, 0.0, 2.5, 2.5, 2.5]

<a name="d​​ictionaries"></a>
## 字典

字典是一種存儲相同類型多重數據的存儲器。每個值（value）都關聯獨特的鍵（key），鍵作為字典中的這個值數據的標識符。和陣列中的數據項不同，字典中的數據項並沒有具體順序。我們在需要通過標識符（鍵）訪問數據的時候使用字典，這種方法很大程度上和我們在現實世界中使用字典查字義的方法一樣。

Swift 的字典使用時需要具體規定可以存儲鍵和值類型。不同於Objective-C 的`NSDictionary`和`NSMutableDictionary` 類可以使用任何類型的對象來作鍵和值並且不提供任何關於這些對象的本質信息。在Swift 中，在某個特定字典中可以存儲的鍵和值必須提前定義清楚，方法是通過顯性類型標註或者類型推斷。

Swift 的字典使用`Dictionary<KeyType, ValueType>`定義,其中`KeyType`是字典中鍵的數據類型，`ValueType`是字典中對應於這些鍵所存儲值的數據類型。

`KeyType`的唯一限制就是可哈希的，這樣可以保證它是獨一無二的，所有的Swift 基本類型（例如`String`，`Int`， `Double`和`Bool`）都是默認可哈希的，並且所有這些類型都可以在字典中當做鍵使用。未關聯值的枚舉成員（參見[枚舉](08_Enumerations.html)）也是默認可哈希的。

<a name="d​​ictionary_literals"></a>
## 字典字面語句

我們可以使用字典字面語句來構造字典，他們和我們剛才介紹過的陣列字面語句擁有相似語法。一個字典字面語句是一個定義擁有一個或者多個鍵值對的字典集合的簡單語句。

一個鍵值對是一個`key`和一個`value`的結合體。在字典字面語句中，每一個鍵值對的鍵和值都由冒號分割。這些鍵值對構成一個列表，其中這些鍵值對由方括號包含並且由逗號分割：

    [key 1: value 1, key 2: value 2, key 3: value 3]

下面的例子創建了一個存儲國際機場名稱的字典。在這個字典中鍵是三個字母的國際航空運輸相關代碼，值是機場名稱：

    var airports: Dictionary<String, String> = ["TYO": "Tokyo", "DUB": "Dublin"]

`airports`字典被定義為一種`Dictionary<String, String>`,它意味著這個字典的鍵和值都是`String`類型。

> 注意：
>
> `airports`字典被聲明為變量（用`var`關鍵字）而不是常量（`let`關鍵字）因為後來更多的機場信息會被添加到這個示例字典中。

`airports`字典使用字典字面語句初始化，包含兩個鍵值對。第一對的鍵是`TYO`，值是`Tokyo`。第二對的鍵是`DUB`，值是`Dublin`。

這個字典語句包含了兩個`String: String`類型的鍵值對。他們對應`airports`變量聲明的類型（一個只有`String`鍵和`String`值的字典）所以這個字典字面語句是構造兩個初始數據項的`airport`字典。

和陣列一樣，如果我們使用字面語句構造字典就不用把類型定義清楚。 `airports`的也可以用這種方法簡短定義：

    var airports = ["TYO": "Tokyo", "DUB": "Dublin"]

因為這個語句中所有的鍵和值都分別是相同的數據類型，Swift 可以推斷出`Dictionary<String, String>`是`airports`字典的正確類型。

<a name="accessing_and_mo​​difying_a_dictionary"></a>
### 讀取和修改字典

我們可以通過字典的方法和屬性來讀取和修改字典，或者使用下標語法。和陣列一樣，我們可以通過字典的只讀屬性`count`來獲取某個字典的數據項數量：

    println("The dictionary of airports contains \(airports.count) items.")
    // 打印"The dictionary of airports contains 2 items."（這個字典有兩個數據項）

我們也可以在字典中使用下標語法來添加新的數據項。可以使用一個合適類型的key 作為下標索引，並且分配新的合適類型的值：

    airports["LHR"] = "London"
    // airports 字典現在有三個數據項

我們也可以使用下標語法來改變特定鍵對應的值：

    airports["LHR"] = "London Heathrow"
    // "LHR"對應的值 被改為 "London Heathrow

作為另一種下標方法，字典的`updateValue(forKey:)`方法可以設置或者更新特定鍵對應的值。就像上面所示的示例，`updateValue(forKey:)`方法在這個鍵不存在對應值的時候設置值或者在存在時更新已存在的值。和上面的下標方法不一樣，這個方法返回更新值之前的原值。這樣方便我們檢查更新是否成功。

`updateValue(forKey:)`函數會返回包含一個字典值類型的可選值。舉例來說：對於存儲`String`值的字典，這個函數會返回一個`String?`或者“可選`String`”類型的值。如果值存在，則這個可選值值等於被替換的值，否則將會是`nil`。

    if let oldValue = airports.updateValue("Dublin Internation", forKey: "DUB") {
        println("The old value for DUB was \(oldValue).")
    }
    // 輸出"The old value for DUB was Dublin."（DUB原值是dublin）

我們也可以使用下標語法來在字典中檢索特定鍵對應的值。由於使用一個沒有值的鍵這種情況是有可能發生的，可選類型返回這個鍵存在的相關值，否則就返回`nil`：

    if let airportName = airports["DUB"] {
        println("The name of the airport is \(airportName).")
    } else {
        println("That airport is not in the airports dictionary.")
    }
    // 打印"The name of the airport is Dublin Internation."（機場的名字是都柏林國際）

我們還可以使用下標語法來通過給某個鍵的對應值賦值為`nil`來從字典裡移除一個鍵值對：

    airports["APL"] = "Apple Internation"
    // "Apple Internation"不是真的APL機場, 刪除它
    airports["APL"] = nil
    // APL現在被移除了

另外，`removeValueForKey`方法也可以用來在字典中移除鍵值對。這個方法在鍵值對存在的情況下會移除該鍵值對並且返回被移除的value或者在沒有值的情況下返回`nil`：

    if let removedValue = airports.removeValueForKey("DUB") {
        println("The removed airport's name is \(removedValue).")
    } else {
        println("The airports dictionary does not contain a value for DUB.")
    }
    // prints "The removed airport's name is Dublin International."

<a name="iterating_over_a_dictionary"></a>
### 字典遍歷

我們可以使用`for-in`循環來遍歷某個字典中的鍵值對。每一個字典中的數據項都由`(key, value)`元組形式返回，並且我們可以使用暫時性常量或者變量來分解這些元組：

    for (airportCode, airportName) in airports {
        println("\(airportCode): \(airportName)")
    }
    // TYO: Tokyo
    // LHR: London Heathrow
`for-in`循環請參見[For 循環](05_Control_Flow.html#for_loops)。

我們也可以通過訪問他的`keys`或者`values​​`屬性（都是可遍歷集合）檢索一個字典的鍵或者值：

    for airportCode in airports.keys {
        println("Airport code: \(airportCode)")
    }
    // Airport code: TYO
    // Airport code: LHR

    for airportName in airports.values​​ {
        println("Airport name: \(airportName)")
    }
    // Airport name: Tokyo
    // Airport name: London Heathrow

如果我們只是需要使用某個字典的鍵集合或者值集合來作為某個接受`Array`實例API 的參數，可以直接使用`keys`或者`values​​`屬性直接構造一個新陣列：

    let airportCodes = Array(airports.keys)
    // airportCodes is ["TYO", "LHR"]

    let airportNames = Array(airports.values​​)
    // airportNames is ["Tokyo", "London Heathrow"]

> 注意：
>
> Swift 的字典類型是無序集合類型。其中字典鍵，值，鍵值對在遍歷的時候會重新排列，而且其中順序是不固定的。

<a name="creating_an_empty_dictionary"></a>
### 創建一個空字典

我們可以像陣列一樣使用構造語法創建一個空字典：

    var namesOfIntegers = Dictionary<Int, String>()
    // namesOfIntegers 是一個空的Dictionary<Int, String>

這個例子創建了一個`Int, String`類型的空字典來儲存英語對整數的命名。它的鍵是`Int`型，值是`String`型。

如果上下文已經提供了信息類型，我們可以使用空字典字面語句來創建一個空字典，記作`[:]`（中括號中放一個冒號）：

    namesOfIntegers[16] = "sixteen"
    // namesOfIntegers 現在包含一個鍵值對
    namesOfIntegers = [:]
    // namesOfIntegers 又成為了一個Int, String類型的空字典

> 注意：
>
> 在後台，Swift 的陣列和字典都是由泛型集合來實現的，想了解更多泛型和集合信息請參見[泛型](22_Generics.html)。

<a name="mutability_of_collections"></a>
## 集合的可變性

陣列和字典都是在單個集合中存儲可變值。如果我們創建一個陣列或者字典並且把它分配成一個變量，這個集合將會是可變的。這意味著我們可以在創建之後添加更多或移除已存在的數據項來改變這個集合的大小。與此相反，如果我們把陣列或字典分配成常量，那麼他就是不可變的，它的大小不能被改變。

對字典來說，不可變性也意味著我們不能替換其中任何現有鍵所對應的值。不可變字典的內容在被首次設定之後不能更改。
不可變性對陣列來說有一點不同，當然我們不能試著改變任何不可變陣列的大小，但是我們可以重新設定相對現存索引所對應的值。這使得Swift 陣列在大小被固定的時候依然可以做的很棒。

Swift 陣列的可變性行為同時影響了陣列實例如何被分配和修改，想獲取更多信息，請參見[集合在賦值和復制中的行為](09_Classes_and_Structures.html#assignment_and_copy_behavior_for_collection_types)。

> 注意：
>
> 在我們不需要改變陣列大小的時候創建不可變陣列是很好的習慣。如此Swift 編譯器可以優化我們創建的集合。
