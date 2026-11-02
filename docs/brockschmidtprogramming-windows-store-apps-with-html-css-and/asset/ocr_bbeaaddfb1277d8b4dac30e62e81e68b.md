Finally, if for some reason you need to know when a flyout is loaded, listen to the `DOMNodeInserted` method on `document.body`:

```
```js
document.body.addEventListener("DOMNodeInserted", insertionHandler, false);
```
```

# ## Flyout Examples

A flyout control is created like any other WinJS control with `data-win-control` and `data-win-options` attributes and processed by `WinJS.UI.process/processAll`. Flyouts with relatively fixed content will typically be declared in markup where you can use data binding on specific properties of the elements within the flyout. Flyouts that are very dynamic, on the other hand, can be created directly from code by using `new WinJS.UI.Flyout(<element>, <options>)`, and you can certainly change its child elements at any time. It's all just part of the DOM! (Am I repeating myself?)

Like I said before (apparently I am repeating myself), a `Flyout` control can contain arbitrary HTML, styled as always with CSS. The flyout for scenario 1 in the sample appears as follows in `html/confirm-action.html` (condensed slightly):

```
```html
<div id="confirmFlyout" data-win-control="WinJS.UI.Flyout" aria-label="{Confirm purchase flyout}">
    <div>Your account will be charged $252.</div>
    <button id="confirmButton">Complete Order</button>
</div>
```
```

The login flyout in scenario 2 is similar, and it even employs an HTML form to attach the Login button to the Enter key (`html/collect-information.html`):

```
```html
<div id="loginFlyout" data-win-control="WinJS.UI.Flyout" aria-label="{Login flyout}">
    <form onsubmit="return false;">
        <p>
            <label for="username">Username: <br /></label>
            <span id="userNameError" class="error"></span>
            <input type="text" id="username" />
        </p>
        <p>
            <label for="password">Password: <br /></label>
            <span id="passwordError" class="error"></span>
            <input type="password" id="password" />
        </p>
        <button id="submitLoginButton">Login</button>
    </form>
</div>
```
```

The flyout is displayed by calling its `show` method. In scenario 1, for instance, the button's `click` event is wired to the `showConfirmFlyout` function (`js/confirm-action.js`), where the Buy button is given as the anchor element. Handling the Complete Order button just happens through a `click` handler attached to that element, and here we want to make sure to call `hide` to programmatically dismiss the flyout. Finally, the `afterHide` event is used to detect dismissal: