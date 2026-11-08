# 5.6.2.1 Clocks

Beside the wall clock `std::chrono::system_clock`⁴⁵, the monotonic clock `std::chrono::steady_clock`⁴⁶, and the most precise clock `std::chrono::high_resolution_clock`⁴⁷ in C++11, C++20 supports five additional clocks. The following table shows the characteristics of all C++ clocks and their epoch.

### Clocks and their Epoch (the namespace `std::chrono` is missing)

| Clock | Description | Epoch | Leap Seconds | C++Standard |
|---|---|---|---|---|
| `steady_clock` | Monotonic clock for measurement | Impl. specific |  | C++11 |
| `system_clock` | Clock of the operating system | 1 January 1970 | Not included | C++11 |
| `file_clock` | Alias for `file_time_type`⁴⁸ | Impl. specific |  | C++20 |
| `gps_clock` | GPS time (Global Positioning System⁴⁹) | 6 January 1980 | Not included | C++20 |
| `local_t` | Pseudo clock for local time | Without epoch |  | C++20 |
| `tai_clock` | TAI time (International Atomic Time⁵⁰) | 1 January 1958 | Not included | C++20 |
| `utc_clock` | Coordinated Universal Time (UTC) | 1 January 1970 | Included | C++20 |

The clocks `std::chrono::steady_clock`, and `std::chrono::file_clock` have an implementation specified epoch. The epochs of `std::chrono::system_clock`, `std::chrono::gps_clock`, `std::chrono::tai_clock`, and `std::chrono::utc_clock` start at 00:00:00. `std::chrono::file_clock` is the clock for file system entries.

Additionally, C++11 supports the `std::chrono::high_resolution_clock`. This clock is on all implementations not implemented and is an alias for `std::chrono::steady_clock` or `std::chrono::high_resolution_clock`.

You can convert a time point between the clocks.

# 5.6.2.1.1 Conversion of time points between clocks.

Thanks to the function `std::chrono::clock_cast`, you can convert time points between the clocks having an epoch. These are the clocks `std::chrono::system_clock`, `std::chrono::utc_clock`, `std::chrono::gps_clock`, and `std::chrono::tai_clock`. Additionally, `std::chrono::file_clock` supports conversion.

⁴⁵ https://www.modernescpp.com/index.php/the-three-clocks  
⁴⁶ https://www.modernescpp.com/index.php/the-three-clocks  
⁴⁷ https://www.modernescpp.com/index.php/the-three-clocks  
⁴⁸ https://en.cppreference.com/w/cpp/filesystem/file_time_t  
⁴⁹ https://en.wikipedia.org/wiki/Global_Positioning_System  
⁵⁰ https://en.wikipedia.org/wiki/International_Atomic_Time