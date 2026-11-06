```
class Spongecake {
public:
  typedef int SpongeNumber;
  SpongeNumber weight;
  SpongeNumber diameter;
};

int main() {
  Spongecake::SpongeNumber myweight = 30;
  Spongecake fluff;
  fluff.weight = myweight;
  return 0;
}
```