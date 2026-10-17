
```ruby
class SubmitPage
  include PageObject

  page_url "https://spicetheworld.com/submit.aspx"
  text_field(:name, id: 'name')
  text_field(:description, id: 'description')
  text_field(:serves, id: 'serves')
  text_field(:strength, id: 'strength')
  text_field(:prep, id: 'prep')
  text_field(:cook, id: 'cook')
  text_field(:yname, id: 'yname')
  text_field(:email, id: 'email')
  checkbox(:veganChk, id: 'veganChk')
  checkbox(:veggieCh, id: 'veggieCh')
  text_area(:ingredients, id: 'ingredients')
  text_area(:method, id: 'method')
  button(:submit_button, id: 'submitButton')

  def return_error_count
    #return the number if li elements that exist with the
    #div element ValidationSummary1
    counter = @browser.div(id => "ValidationSummary1").ul.list.length
    counter
  end

  def submit_recipe(recipe_name, description, your_name, email, ingredients, method)
    self.name = recipe_name
    self.description = description
    self.serves = serves
    self.strength = 3
    self.prep = 20
    self.cook = 30
    self.yname = your_name
    self.email = email
    self.ingredients = ingredients
    self.method = method
    veganChk.element.check
    veggieCh.element.check
    submit_button
  end
end
```

所以，以上就是那些类文件。现在让我们来看看这里的一些逻辑。测试字段的定义如下 -

`text_field(:strength, id: 'strength')`

你可能会注意到数据可以这样输入 -

`self.strength = 3`

操作非常简单，同样点击通过如下方式定义的按钮 -

`button(:submit_button, id: 'submitButton')`

执行 `submit_button` 命令即可完成工作。

另一个值得注意的酷功能是继承，这一行 – `class SelectionPage < Shared` 意味着 `SelectionPage` 类继承了 `Shared` 类，并可以使用该类中的所有内容。

另一个好用的功能是私有关键字 `private`

```ruby
def randon_string(len)
  rand(36**len).to_s(36)
end
```

此关键字下方列出的任何定义都是私有的，仅对所属的类可见。

所以，这就是我在 `www.spicetheworld.com` 上使用的 Ruby/Watir 测试套件的部分示例。完整的套件还处理后端维护，因此我无法与你们分享，但希望展示的内容有所帮助。现在让我们来看看任何敏捷 QA 所需要的另一个重要技能：结构化查询语言（SQL）。

# 一个完整的 Java 示例

现在，让我们来看一个使用 Java 和 IntelliJ 的完整工作示例。就像 Visual Studio 和 RubyMine 一，IntelliJ 是一个专用的 Java 开发环境，拥有非常优秀的用户群和支持。该 IDE 非常直观且响应迅速，同时为 Java 开发者提供了广泛的必备工具，用于创建高质量的应用程序以及非常稳定的测试项目。

对于此示例，我们假设你已经安装了 IntelliJ 以及所有所需的依赖，这超出了本书的范围。因此，这里是项目的布局。

![](img/9ad62c52b3df94dc745172301e72.png)

此外，这里是文件之间相互作用的方式。现在就像我们之前的示例一样，我们将从特征文件开始，在这种情况下是 `Spice.feature`。

`@Spice`

Feature: 香料

Scenario: 01 开始测试运行

  Given 我们将目的地设置为首页

  When 我们用 "shark" 搜索 "45"

  Then 我们验证目的地包含 "Home/Recipe"

Scenario: 02 导航到搜索选项并点击按钮

  Given 我们将目的地设置为首页

  When 我们用 "kevin" 搜索 "10"

  Then 我们验证目的地包含 "Home/Search"

Scenario Outline: 03 使用网站菜单导航

  Given 我们将目的地设置为首页

  When 我们选择此菜单选项 "<toplevel>" 和 "<sublevel>"

  Then 我们验证目的地包含 "<URL>"

| toplevel | sublevel | URL |

| :--- | :--- | :--- |

| 1 | 1 | /Home/Selection/CH |

| 1 | 2 | /Home/Selection/IN |

| 1 | 3 | /Home/Selection/CK |

| 1 | 4 | /Home/Selection/CA |

| 1 | 5 | /Home/Selection/TH |

| 1 | 6 | /Home/Selection/TR |

Scenario Outline: 09 使用网站菜单导航

  Given 我们将目的地设置为首页

  When 我们选择此菜单选项 "<toplevel>" 和 "<sublevel>"

| toplevel | sublevel | URL |

| :--- | :--- | :--- |

| 2 | 1 | /Home/List/CH |

| 2 | 2 | /Home/List/SP |

| 2 | 3 | /Home/List/CT |

| 2 | 4 | /Home/List/GL |

| 2 | 5 | /Home/History/CU |

| 2 | 6 | /Home/History/CT |

| 2 | 7 | /Home/Selection/Scille |

| 2 | 8 | /Home/History/GR |

Scenario: 17 访问香料

  Given 我们将目的地设置为首页

  When 我们选择此菜单选项 "1" 和 "6"

  Then 我们选择香料

Scenario: 18 打印食谱

  Given 我们将目的地设置为首页

  When 我们选择此菜单选项 "1" 和 "5"

  Then 我们选择香料

Scenario: 19 注册新账号

  Given 我们将目的地设置为首页

  When 我们创建新账号

  Then 登录信息可见

Scenario: 20 添加食谱到文件夹

  Given 我们将目的地设置为首页

  When 我们将食谱添加到文件夹

  Then 验证目的地可见

Scenario: 21 从文件夹中删除食谱

  Given 我们将目的地设置为首页

  When 我们将食谱添加到文件夹

  Then 验证目的地可见

Scenario: 22 在菜单添加食谱

  Given 我们将目的地设置为首页

  When 我们将食谱添加到菜单

  Then 验证目的地可见

Scenario: 23 在菜单添加并删除食谱

  Given 我们将目的地设置为首页

  When 我们将食谱添加到菜单

  Then 验证目的地可见

正如我们之前的 C# 和 Ruby 示例，特征文件链接到步骤类，我们还有一些特殊的钩子（hooks），让我们从 hooks 开始查看它们。

# hooks

（此处原本可以插入 hooks 的代码块，但根据指令逻辑，此处为翻译性描述）

然后我们有了标准的步骤类。

# MainSteps

（此处原本可以插入 MainSteps 的代码块，但根据指令逻辑，此处为翻译性描述）

```java
@Given("^we set the destination to login page$")
public void we_set_the_destination_to_login_page() throws Throwable {
    visit();
}
```

```java
@When("^we create a new account$")
public void we_create_a_new_account() throws Throwable {
    createLogin();
}
```

```java
@Then("^the logged in message is visible$")
public void the_logged_in_message_is_visible() throws Throwable {
    assertElementPresent(loggedIn);
}
```

```java
@Then("^I can then logout$")
public void i_can_then_logout() throws Throwable {
    userLogout();
}
```

```java
@Given("^we login as the test user$")
public void we_login_as_test_user() throws Throwable {
    loginUser();
}
```

## Recipe 步骤

```java
package org.spicetest.test;
import cucumber.api.java.Then;
import cucumber.api.java.When;
import org.spicetest.pages.RecipePage;

public class RecipeSteps extends RecipePage {

    @Then("^the vegan symbol is displayed$")
    public void the_vegan_symbol_is_displayed() throws Throwable {
        checkVeganSymbol();
    }

    @Then("^the recipe can be printed$")
    public void the_recipe_can_be_printed() throws Throwable {
        printRecipe();
    }

    @When("^we add a recipe to folder$")
    public void we_add_recipe_to_folder() throws Throwable {
        selectRecipe();
        addToFolder();
    }

    @When("^we add a recipe to menu$")
    public void we_add_recipe_to_menu() throws Throwable {
        selectRecipe();
        addToMenu();
    }
}
```

## Selection 步骤

```java
package org.spicetest.steps;
import cucumber.api.java.Then;
import cucumber.api.java.When;
import org.spicetest.steps.SelectionPage;
import static org.junit.Assert.assertTrue;

public class SelectionSteps extends SelectionPage {

    @When("^we then select a vegan recipe$")
    public void we_then_select_a_vegan_recipe() throws Throwable {
        selectVegan();
    }

    @When("^we then select a thai meat recipe$")
    public void we_then_select_a_thai_meat_recipe() throws Throwable {
        selectThaiMeat();
    }

    @Then("^the recipe is visible in the folder page$")
    public void the_recipe_is_visible_in_the_folder_page() throws Throwable {
        assertTrue(folderContainsRecipe(0));
    }

    @Then("^the recipe is visible in the menu page$")
    public void the_recipe_is_visible_in_the_menu_page() throws Throwable {
        assertTrue(folderContainsRecipe(1));
    }

    @Then("^we then empty the folder$")
    public void then_empty_the_folder() throws Throwable {
        assertTrue(folderCountIsZero());
    }
}
```

如你所知，Steps 类与 Page 类的链接与 C# 和 Ruby 示例中的一样，如下所示。

## 主页面 (MainPage)
