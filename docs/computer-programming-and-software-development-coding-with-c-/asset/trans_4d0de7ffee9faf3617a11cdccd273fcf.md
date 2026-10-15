

selection statements. 让我们删除底部两个，然后我们将剩下一個比較示例繼續使用。然後在我們計算的值集合中，讓我們刪除 unansweredCount 計算。這樣就剩下三個更有趣的表達式語句，可以作為我們選擇語句的起點。接下來我們需要一個地方來存儲任務列表，這些任務將為市場部門調查創建。在 C# 中實現這一點的一個簡單選項是使用 list 類型。所以在我們 main 方法的最頂部，讓我們輸入 var tasks = new List，然後指定一個 string 和尖括號後跟括號。我們也可以將滑鼠懸停在我們的 list 上以引入正確的命名空間。作為提醒，命名空間本質上只是 .NET 類型所在的容器，因此當我們開始使用框架中的額外類型時，有時必須向它們添加新的引用。如果你對 C# 或編程一般還很陌生，並且還不理解這一行，這本書完全沒問題。

```
using System.Collections.Generic;

namespace WiredBrainCoffeeSurveys.Reports
{
    class Program
    {
        static void Main(string[] args)
        {
            var tasks = new List<string>();

            // Calculated Values
            double responseRate = QIResults.NumberResponded / QIResults.NumberSurveyed;
            double overallScore = (QIResults.ServiceScore + QIResults.CoffeeScore + QIResults.FoodScore + QIResults.Pr

            // Logical comparisons
            bool isCoffeeScoreLower = QIResults.CoffeeScore < QIResults.FoodScore;
        }
    }
}
```

list 只是一個允許我們在其中存儲多個項目的類型。我們使用這些尖括號指定它應該保存什麼樣的數據，對於我們來說，這些將只是代表市場團隊新任務的字符串。new 關鍵字實際上為我們創建了要使用的列表，然後它被分配給我們的 tasks 變量以供應用程序在整個過程中使用。接下來，讓我們編寫將創建任務的語句。所以，讓我們假設如果咖啡得分低於食物得分，市場團隊希望有一個任務來調查食譜和原料質量。我們可以使用簡單的 if 語句來實現這一點。在底部，我們已經使用布林值計算了這個問題的答案，所以讓我們利用它來做出決策。往下幾行，讓我們寫出 if (isCoffeeScoreLower) 然後使用我們的花括號搭建一個代碼塊。在塊內，讓我們說 tasks.add，這將使用我們之前創建的列表，並傳入一個字符串，說類似 Investigate coffee recipes and ingredient quality。

```
using System.Collections.Generic;

namespace WiredBrainCoffeeSurveys.Reports
{
    class Program
    {
        static void Main(string[] args)
        {
            var tasks = new List<string>();

            // Calculated Values
            double responseRate = QIResults.NumberResponded / QIResults.NumberSurveyed;
            double overallScore = (QIResults.ServiceScore + QIResults.CoffeeScore + QIResults.FoodScore + QIResults.Pric

            // Logical comparisons
            bool isCoffeeScoreLower = QIResults.CoffeeScore < QIResults.FoodScore;

            if (isCoffeeScoreLower)
            {
                tasks.Add("Investigate coffee recipes and ingredients.");
            }
        }
    }
}
```

因為 isCoffeeScoreLower 變量已經保存了布林 true 或 false 值，所以這實際上就是我們需要做的所有事情。如果分數較低，將添加一個任務來調查此事。如果不是，我們的程序流程將跳過此邏輯並繼續。這也凸顯了選擇語句的一個重要點。我們可以在決策中使用這樣的變量，或者我們也可以將比較表達式直接放在我們的括號內。舉個例子，我可以複製這個處理我們比較的表達式，然後直接粘貼到我們的 if 語句括號內。而且，這意味著我們實際上可以刪除上面更遠的那一行。

![](img/0155736aec718cf18821e9f10a5d308d_545_0.png)

這兩個選項的效果相同，所以它真的只是取決於可讀性以及你是否需要在多個地方重用相同的值。我們不需要在任何地方重用此比較，因此在沒有變量的情況下這種方法完全可行。現在讓我們使用我們的調試工具來驗證此代碼的行為以及它對程序流程的影響。所以讓我們在我們的 if 語句旁邊放置一個斷點，然後單擊運行。

![](img/0155736aec718cf18821e9f10a5d308d_545_1.png)

如預期，我們將在該斷點結束。當我們將滑鼠懸停在我們的 CoffeeScore 和 FoodScore 上時，我們可以看到 CoffeeScore 實際上是兩者中較高的，所以如果我單擊 Step Over 來逐步執行此代碼，我們實際上直接跳過了會添加新任務的那一行並跳到方法末尾。如果我們將滑鼠懸停在我們的 task 變量上，我們可以看到計數仍然為 0。我們的 if 表達式評估為 false，因此此代碼塊未執行。有趣的是，這是我們第一次運行應用程序，其中某些代碼行未執行。我們已成功改變了程序的流程。讓我們停止應用程序，快速地，如果你想看到情況的逆轉，你可以通過更改 Q1Results 文件中的值來做到這一點。所以，讓我們稍後切換過去。

```
public static class Q1Results
{
    // Aggregate ratings
    public static double ServiceScore { get; set; } = 8.0;
    public static double CoffeeScore { get; set; } = 8.5;
    public static double PriceScore { get; set; } = 6.0;
    public static double FoodScore { get; set; } = 7.5;
    public static double WouldRecommend { get; set; } = 6.5;
    public static string FavoriteProduct { get; set; } = "Cappucino";
    public static string LeastFavoriteProduct { get; set; } = "Granola";
    // Aggregate counts
    public static double NumberSurveyed { get; set; } = 500;
```

對於 CoffeeScore，你只需將其更改為低於 FoodScore 的值，例如 4 或 5，然後再次單擊運行。Visual Studio 將跳回我們的斷點，現在當我們使用調試器逐步執行時，這次我們實際上進入了我們的 if 代碼塊並向我們的列表添加了一個任務。

![](img/0155736aec718cf18821e9f10a5d308d_547_0.png)

讓我們再向前逐步執行幾次以確保該行執行，然後如果我們再次將滑鼠懸停在我們的任務列表上，Visual Studio 將確認字符串已添加。

![](img/0155736aec718cf18821e9f10a5d308d_547_1.png)

接下來，讓我們看一個使用 if/else 語句進行分支路徑的示例。

## Chapter 7 How to Create Branching Selection Statement

讓我們探討如何使用 if/else 語句來處理分支決策邏輯。所以讓我們說市場團隊希望使用這個整體評分來做出一些決定。如果整體分數高於 8，他們希望聯繫其他領導並找出如何獎勵公司各地的員工。

```
```csharp
static void Main(string[] args)
{
    var tasks = new List<string>();

    // Calculated Values
    double responseRate = Q1Results.NumberResponded / Q1Results.NumberSurveyed;
    double overallScore = (Q1Results.ServiceScore + Q1Results.CoffeeScore + Q1Results.FoodScore + Q1Results.PriceScore) / 4;

    if (Q1Results.CoffeeScore < Q1Results.FoodScore)
    {
        tasks.Add("Investigate coffee recipes and ingredients.");
    }
}
```
```

否則，如果分數低於 8，他們希望與員工聯繫以獲取提高此分數的想法。在我們目前的 if 語句下方，讓我們向下移動幾行以添加另一個選擇語句。所以讓我們再次說 if，對於表達式我們可以說 overallScore > 8 並創建我們的嵌套代碼塊。

對於我們的 if 表達式，讓我們檢查我們的響應率是否低於 .33 或 33%。然後在我們的代碼塊中，讓我們說 tasks.add 和類似研究提高響應率的選項。在我們的閉合大括號之後，讓我們然後使用這些特殊關鍵字添加一個 else if 場景。對於我們的表達式，讓我們說響應率大於 .33 且響應率小於 .66。這個 else if 場景是變量如何讓我們重用先前的計算並使新計算更簡單、更易讀的一個很好的例子。沒有變量的使用，這種組合和邏輯將非常冗長。讓我們也在這裡添加一個新任務，說類似 reward respondents with a free coffee to match our directions for marketing。最後，在末尾，讓我們添加一個簡單的 else 塊，並在其中添加另一個任務，讀取 rewards respondents with a discount coupon 或類似的內容。我們不需要為此 else 指定任何表達式，因為如果代碼到達此點，唯一的可能響應率將高於 .66。接下來，讓我們在這個新 if else 語句的開頭添加一個斷點，然後運行應用程序看看會發生什麼。在我們命中第一個斷點後，我們可以將滑鼠懸停在我們計算的響應率上，該值為 .65。

```
```csharp
if (responseRate < .33)
{
    tasks.Add("Research options to improve response rate.");
}
else if (responseRate > .33 && responseRate < .66)
{
    tasks.Add("Reward participants with free coffee coupon.");
}
else
{
    tasks.Add("Rewards participants with discount coffee coupon.");
}
```
```

