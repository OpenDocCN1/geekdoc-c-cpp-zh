```
MediaHolder() : Count(0) {}
};

class BookHolder : public MediaHolder<Book> {
public:
  enum GenreEnum
    {childrens, scifi, romance,
     horror, mainstream, ownnotto};
  GenreEnum GenreOfAllBooks;
};

class MagazineHolder : public MediaHolder<Magazine> {
public:
  bool CompleteSet;
};

int main() {
  MagazineHolder dl;
  dl.Add(new Magazine(
      "Dummies Life", "Vol 1 No 1", "Wile E."));
  dl.Add(new Magazine(
      "Dummies Life", "Vol 1 No 2", "Wile E."));
  dl.Add(new Magazine(
      "Dummies Life", "Vol 1 No 3", "Wile E."));
  dl.CompleteSet = false;
  cout << dl.Count << endl;

  BookHolder bh;
  bh.Add(new Book(
      "Yellow Rose", "Sandy Shore", "Wile E."));
  bh.Add(new Book(
      "Bluebells", "Sandy Shore", "Wile E."));
  bh.Add(new Book(
      "Red Tulip", "Sandy Shore", "Wile E."));
  bh.GenreOfAllBooks = BookHolder::childrens;
  cout << bh.Count << endl;
  return 0;
}
```

When you run this example, you see the magazine count of 3 first, and the book count of 3 second.