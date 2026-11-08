```
```cpp
    m_ingredients.emplace_back(ingredient);
}

void SandwichImpl::RemoveIngredient(const wchar_t* ingredient)
{
    auto it = find_if(m_ingredients.begin(), m_ingredients.end(), [=]
(wstring item) -> bool
    {
        return (item.compare(ingredient) == 0);
    });

    if (it != m_ingredients.end())
    {
        m_ingredients.erase(it);
    }
}

void SandwichImpl::SetBreadType(const wchar_t* breadType)
{
    m_breadType = breadType;
}

const wchar_t* SandwichImpl::GetSandwich(void)
{
    m_description.clear();
    m_description.append(L"A ");
    for (auto ingredient : m_ingredients)
    {
        m_description.append(ingredient);
        m_description.append(L", ");
    }
    m_description.erase(m_description.end() - 2, m_description.end());
    m_description.append(L" on ");
    m_description.append(m_breadType);
    m_description.append(L".");

    return m_description.c_str();
}

Sandwich::Sandwich(void)
    : m_pImpl(new SandwichImpl())
{
}

Sandwich::~Sandwich(void)
{
}

void Sandwich::AddIngredient(const wchar_t* ingredient)
{
    m_pImpl->AddIngredient(ingredient);
}

void Sandwich::RemoveIngredient(const wchar_t* ingredient)
{
    m_pImpl->RemoveIngredient(ingredient);
}
```
```