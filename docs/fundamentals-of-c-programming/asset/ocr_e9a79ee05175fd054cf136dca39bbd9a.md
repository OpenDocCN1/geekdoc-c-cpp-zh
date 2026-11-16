```
#ifndef ALT_TEXT2_H_INCLUDED
#define ALT_TEXT2_H_INCLUDED

#include <string>

// The kinds of text objects supported (added Bounded)
enum class TextType { Plain, Fancy, Fixed, Bounded };

class AltText2 {
  TextType type;
  std::string text;
  std::string left_bracket;
  std::string right_bracket;
  std::string connector;
  size_t length_limit; // Maximum number of characters in the text

public:
  AltText2(TextType type, const std::string& t);
  AltText2(TextType type, const std::string& t, const std::string& left,
           const std::string& right, const std::string& conn);
  AltText2(TextType type);

  // Constructor for a length-bounded text object
  AltText2(TextType type, const std::string& t, size_t limit);
  std::string get() const;
  void append(const std::string& extra);
};

#endif
```

We extended the enumeration to include TextType::Bounded. We added one more field (limit) to the Text class, which means every Text object will have a limit field whether they need it or not. We also added one more constructor overload to properly initialize a bounded text object.

Listing 17.14 (alttext2.cpp) implements the methods in the new Text class.

# Listing 17.15: name.cpp

```
#include "alttext2.h"

AltText2::AltText2(TextType type, const std::string& t): type(type), text(t) {}

AltText2::AltText2(TextType type, const std::string& t, const std::string& left,
                   const std::string& right, const std::string& conn)
  : type(type), text(t), left_bracket(left), right_bracket(right),
    connector(conn) {}

AltText2::AltText2(TextType type): type(type), text("FIXED") {}

AltText2::AltText2(TextType type, const std::string& t, size_t limit):
  type(type),
  text(t.substr(0, limit)), // Ensure text initially does not exceed bound
  length_limit(limit) {}

std::::string AltText2::get() const {
  switch (type) {
  case TextType::Plain:
```