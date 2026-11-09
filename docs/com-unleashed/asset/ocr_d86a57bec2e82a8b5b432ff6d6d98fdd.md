# LISTING 11.12 Continued

```
```cpp
if (MyInterface::m_recordnumber>2)
{
    MyInterface::m_recordnumber = 0;
}
recordnumber = MyInterface::m_recordnumber;
}
else
{
    (recordnumber)++;
    if ((recordnumber>2) || (recordnumber<0))
    {
        recordnumber = 0;
    }
    MyInterface::m_recordnumber = recordnumber;
}

std::ofstream os;
os.open(MyInterface::m_szFilename,
        std::ios_base::out | std::ios_base::trunc |
        std::ios_base::binary);
os << array[MyInterface::m_recordnumber][0] << " "
   << array[MyInterface::m_recordnumber][1] << " "
   << array[MyInterface::m_recordnumber][2];
os << " " << recordnumber;
os.close();

::SetEvent(hack);
}

::CloseHandle(event);
::CloseHandle(hack);
::CloseHandle(hstop);
}
```
```

When you attempt to create the out-of-process server, COM+ will call the MyInterface::GetMarshalSizeMax(), MyInterface::GetUnmarshalClass(), and MyInterface::MarshalInterface() methods. The MyInterface::GetUnmarshalClass() method should return the CLSID of the proxy. The important call is to the MyInterface::MarshalInterface() method. This method must initiate the marshaling mechanism. In this case, I’m returning an OBJECTMARSHALDATA structure that holds the file-name where I will marshal data elements and the event name that will trigger the methods.

# Defining the Proxy Class

After returning from the MyInterface::MarshalInterface() method, COM+ then creates the proxy and calls the marshalproxy::UnmarshalInterface() method. The proxy