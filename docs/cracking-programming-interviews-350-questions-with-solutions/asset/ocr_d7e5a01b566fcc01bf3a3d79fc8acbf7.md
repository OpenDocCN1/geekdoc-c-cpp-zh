```
```cpp
        copy(e.begin(), e.end(), std::
                ostream_iterator<int>(std::cout, " "));
        std::cout << std::endl;
    }
}

template <typename T>
void validate(const std::vector<std::vector<T>>& A)
{
    int k = 1;
    size_t len = A.size();

    for (int j = len - 1; j >= 0; --j)
    {
        for (int i = 0; i < len; ++i)
        {
            assert(k++ == A[i][j]);
        }
    }
}

template <typename T>
void copy_2darray(std::vector<std::vector<T>>& A,
                  const int &A_x_s,
                  const int &A_x_e,
                  const int &A_y_s,
                  const int &A_y_e,
                  const std::vector<std::vector<T>>
                  &S,
                  const int &S_x, const int &S_y)
{
    for (int i = 0; i < A_x_e - A_x_s; ++i)
    {
        copy(S[S_x + i].cbegin() + S_y,
             S[S_x + i].cbegin() + S_y + A_y_e -
             A_y_s,
             A[A_x_s + i].begin() + A_y_s);
    }
}

template <typename T>
void rotate_2darray_helper(std::vector<std::vector<
        T>>& A, const int &x_s,
        const int &x_e, const int
        &y_s, const int &y_e)
{
    if (x_e > x_s + 1)
    {
        int mid_x = x_s + ((x_e - x_s) >> 1);
        int mid_y = y_s + ((y_e - y_s) >> 1);

        // Move submatrices
```
```