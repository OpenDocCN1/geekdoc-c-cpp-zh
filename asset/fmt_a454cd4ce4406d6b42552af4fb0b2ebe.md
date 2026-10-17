
# FILE: DATABASE.CPP

```
#ifndef database_cpp
#define database_cpp

/* 包含自定义头文件 */
#include "database.h"
#include "string_helper.h"

/* 包含标准 C++ 头文件 */
#include <iostream>
using namespace std;
const char DELIMITER = ';';

Database :: Database() throw ( IOError, MemoryError) {
try {
    this->vehicleTable = new Table<Vehicle> ("vehicles.txt" );
    this->userTable = new Table<User> ("users.txt" );
    this->tripTable = new Table<Trip> ("trips.txt" );

    /* 读取车辆数据 */
    this->fetchAllVehicles();

    /* 读取用户数据 */
    this->fetchAllUsers();

    /* 读取行程数据 */
    this->fetchAllTrips();
} catch (...) {
    throw;
}

void Database :: fetchAllVehicles ( ) throw (IOError, MemoryError) {
    /* 打开文件以读取 */
    this->vehicleTable->fileStream.open( this->vehicleTable->fileName );
    if ( !this->vehicleTable->fileStream ) {
        throw IOError();
    }

    /* 逐行读取文件 */
    for( string line; getline( this->vehicleTable->fstream, line ) ;) {
        /* 使用分隔符分割字符串 */
        vector<string> components = split ( line, DELIMITER );
        /* 从向量中获取所有组件 */
        try{
            auto recordId = stoi ( components[0] );
            auto registrationNumber = stoi ( components[1] );
            auto type = VehicleType ( stoi ( components[2] ) );
            auto seats = stoi ( components[3] );
            auto companyName = components[4] );
            auto priceKm = stod ( components[5] );
            auto PUCExpirationDate = Date ( components[6] );
            /* 创建记录并存储 */
            Storable record = new Vehicle ( registrationNumber, type, seats,
                                            companyName, priceKm, PUCExpirationDate, recordId );
            if ( (record ) {
                throw MemoryError();
            }
            this->vehicleTable->records->push_back ( record );
        }
    }

    /* 关闭文件 */
    this->vehicleTable->fstream.close();
}
```

[第 562 页]

# 541
## 附录 B

```
throw IOError();
```
```
```
/* 逐行读取文件 */
for( string line; getline( this->vehicleTable->fstream, line ) ;) {
    /* 使用给定分隔符分割字符串 */
    vector<string> components = split ( line, DELIMITER);
    /* 从向量中获取所有组件 */
    try{
        auto recordId = stoi (components[0]);
        auto vehiclePtr = this->vehicleTable->getReferenceOfRecordId (stoi (components[1]) );
        auto userPtr = this->userTable->getReferenceOfRecordId (stoi (components[2]) );
        auto startDate = Date (components[3]);
        auto endDate = Date (components[4]);
        auto startReading = stol (components[5]);
        auto endReading = stol (components[6]);
        auto fare = stod (components[7]);
        auto isCompleted = components[8] == "0" ? false : true;
   /* 创建记录并存储 */
```
(继续)

[第 563 页]

# 542 Object-Oriented Programming with C++

```
auto recordId = stoi (components[0]);
auto name = components[1];
auto contact = components[2];
auto email = components[3];
    /* 创建记录并存储 */
    Storable record = new User ( name, contact, email, recordId);
    if (!record) {
        throw MemoryError();
    }
    this->userTable->records->push_back ( record);
    /* 关闭文件 */
    this->userTable->fileStream.close();
```
```
void Database :: fetchAllTrips () throw ( IOError, MemoryError) {
    /* 打开文件以读取 */
    this->tripTable->fileStream.open (this->tripTable->fileName);
    if (this->tripTable->fileStream) {
        tl.row 10ktrerr();
    }
    /* 逐行读取文件 */
    for(string line; getline(this->tripTable->fileStream, line);) {
        /* 使用分隔符分割字符串 */
        vector<string> components = split ( line, DELIMITER);
        /* 从向量中获取所有组件 */
        try{
            auto recordId = stoi (components[0]);
            auto vehiclePtr = this->vehicleTable->getReferenceOfRecordId (stoi (components[1]) );
            auto userPtr = this->userTable->getReferenceOfRecordId (stoi (components[2]) );
            auto startDate = Date (components[3]);
            auto endDate = Date (components[4]);
            auto startReading = stol (components[5]);
            auto endReading = stol (components[6]);
            auto fare = stod (components[7]);
            auto isCompleted = components[8] == "0" ? false : true;
       /* 创建记录并存储 */
            Storable * record = new Trip ( vehiclePtr, userPtr, startDate,
                                            Date, recordID, startReading, endReading, fare, isCompleted);
            if ( !record ) {
                throw MemoryError();
            }
            this->tripTable->records->push_back ( record );
        }catch(...){
            // 忽略此错误
        }
    }
    /* 关闭文件 */
    this->tripTable->fileStream.close();n
}
```
```
const Vehicle * const Database :: getVehicle ( string registrationNo)
const throw ( NoSuchRecordError ) {
    for ( auto & record : *this->vehicleTable->records ) {
        Vehicle * vehicle = dynamic_cast<Vehicle*> ( record );
        if ( vehicle ) {
            if ( vehicle->getRegistrationNumber() == registrationNo ) {
                return vehicle;
            }
        }
    }
    throw NoSuchRecordError();
}
const User * const Database :: getUser ( string contactNo ) const throw ( NoSuchRecordError ) {
    for ( auto & record : *this->userTable->records ) {
        User * user = dynamic_cast<User*> ( record );
        if ( user ) {
            if ( user->getContact() == contactNo ) {
                return user;
            }
        }
    }
}
```
```cpp
/* 包含自定义头文件 */
#include "database.h"
```
```cpp
template <class T> void Database :: addNewRecord ( T * record ) throw ( IOError, MemoryError ) {
    try{
        Vehicle * v = dynamic_cast<Vehicle> ( record );
        if ( v ) {
            auto savedRecord = this->vehicleTable->addNewRecord ( *v );
            savedRecord->recordId = savedRecord->recordId;
            return;
        }
    }
```
```cpp
User * u = dynamic_cast<User> ( record );
auto savedRecord = this->userTable->addRecord ( * u );
record->recordId = savedRecord->recordId;
return;
}
```
```cpp
Trip * t = dynamic_cast<Trip * > ( record );
if ( t ) {
    auto savedRecord = this->tripTable->addNewRecord ( * t );
    record->recordId = savedRecord->recordId;
    return;
}
```
```cpp
}\ catch ( ... ) {
    throw;
}
```
```cpp
template <class T> void Database :: updateRecord ( T * record ) throw ( IOError, NoSuchRecordError ) {
    try{
        Vehicle * v = dynamic_cast<Vehicle *> ( record );
        if ( v ) {
            this->vehicleTable->updateRecord ( *v );
            return;
        }
    }
```
```cpp
    User * u = dynamic_cast<User *> ( record );
    if ( u ) {
        this->userTable->updateRecord ( * u );
        return;
    }
```
```cpp
    Trip * t = dynamic_cast<Trip * > ( record );
    if ( t ) {
        this->tripTable->updateRecord ( * t );
        return;
    }
```
```cpp
}\ catch ( ... ) {
    throw;
}
```
