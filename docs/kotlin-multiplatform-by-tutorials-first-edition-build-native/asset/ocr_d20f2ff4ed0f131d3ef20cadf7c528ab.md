viewModel block to account for the added parameter in its constructor.

```
viewModel {
    AboutViewModel(get(), get())
}
```

Do the same for its factory in KoinCommon.kt:

```
factory { AboutViewModel(get(), get()) }
```

Next, open AboutView.kt in the androidApp module. Change the ContentView composable function to accept a footer and then show it at the bottom of row items:

```
@Composable
private fun ContentView(
    items: List<AboutViewModel.RowItem>,
    footer: String?,
) {
    LazyColumn(
    modifier = Modifier
    .fillMaxSize()
    .semantics { contentDescription = "aboutView" },
    ) {
    items(items) { row ->
    RowView(title = row.title, subtitle = row.subtitle)
    }
    footer?.let {
    item {
    Text(
    text = it,
    style = MaterialTheme.typography.caption,
    textAlign = TextAlign.Center,
    modifier = Modifier
    .fillMaxWidth()
    .padding(8.dp),
    )
    }
    }
}
```

This code is pretty straightforward. It looks rather long, but it’s mostly styling and what’s already been there.

Finally, update the AboutView composable function where you used ContentView .

```
@Composable
fun AboutView(
    viewModel: AboutViewModel = getViewModel(),
    onUpButtonClick: () -> Unit
)
```