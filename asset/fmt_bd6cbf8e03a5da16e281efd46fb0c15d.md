
# 面向对象编程与 C++

```cpp
delete vehicle;
}
```

```cpp
void Application::renderViewVehicleMenu() const {
    string header = "Enter registration no. of vehicle: ";
    string registrationNo;
    system("clear");
    gotoXY(0, 1);
    cout << header;
    gotoXY(int(header.length()), 1);
    getline(cin, registrationNo);
    /* Find vehicle and display data */
    gotoXY(0, 3);
    try {
        auto vehicle = this->db->getVehicle(registrationNo);
        vehicle->display();

        cout << endl << "Press any key to continue";
        cin.get();
    } catch (Error e) {
        this->showDialog(e.getMessage());
    }
}
```

```cpp
void Application::renderEditVehicleMenu() const {
    string header = "Enter registration no. of vehicle you want to edit: ";
    string priceLabel = "Enter new price per km: ";
    string registrationNo;
    system("clear");
    gotoXY(0, 1);
    cout << header;
    gotoXY(int(header.length()), 1);
    getline(cin, registrationNo);
}
```

```cpp
void Application::renderAddNewUserMenu() const {
    string header = "Enter details of user: ";
    string userNameLabel = "Enter name of user: ";
    string usercontactLabel = "Enter contact no of user: ";
    string userEmailLabel = "Enter email of user (optional): ";

    string name;
    string contact;
    string email;

    system("clear");
    gotoXY(0, 1);
    cout << header;
    gotoXY(int(userNameLabel.length()), 3);
    getline(cin, name);

    gotoXY(int(usercontactLabel.length()), 4);
    getline(cin, contact);

    gotoXY(int(userEmailLabel.length()), 5);
    getline(cin, email);

    User* user;
    try {
        user = new User(name, contact, email);
        this->db->addRecord(user);
        stringstream ss;
        ss << "User Id: " << user->getRecordId();
        showDialog("User added successfully", ss.str());
    } catch (Error e) {
        showDialog(e.getMessage());
    }
    delete user;
}
```

```cpp
void Application::renderNewTripMenu() const {
    string header = "Enter details of trip (All fields are required): ";
    string userContactLabel = "Enter contact no of user: ";
    string startDate = "Enter start date of trip (d/m/yyyy): ";
    string endDateLabel = "Enter end date of trip (d/m/yyyy): ";
    string vehicleTypeLabel = "Enter vehicle type: ";
    string vehicleOptionLabel = "(1. Bike, 2. Car, 3. Tower): ";
    string registrationNoLabel = "Enter registration no of vehicle: ";

    string contactNo;
    string startDate;
    string endDate;
    int vehicleType;
    string registrationNo;

    const User* user;
    const Vehicle* vehicle;

    system("clear");
    gotoXY(0, 1);
    cout << userContactLabel;
    gotoXY(int(userContactLabel.length()), 1);
    getline(cin, contactNo);

    try {
        user = this->db->getUser(contactNo);
        gotoXY(0, 3);
        cout << "User found: " << user->getName();
    } catch (Error e) {
        this->showDialog(e.getMessage());
    }

    gotoXY(0, 5);
    cout << header;

    gotoXY(0, 7);
    cout << startDateLabel;

    gotoXY(0, 8);
    cout << endDateLabel;

    gotoXY(0, 9);
    cout << vehicleTypeLabel;
    gotoXY(0, 10);
    cout << vehicleOptionLabel;

    gotoXY(int(startDateLabel.length()), 7);
    getline(cin, startDate);

    gotoXY(int(endDateLabel.length()), 8);
    getline(cin, endDate);

    gotoXY(int(vehicleTypeLabel.length()), 9);
    cin >> vehicleType;
    cin.ignore(numeric_limits<streamsize>::max(), '\\n');

    /* Find vehicle as user's requirements, and if not found, ask the
    user to change the input */
    auto freeVehicles = this->db->getVehicle(Date(startDate), Date(endDate), Vehicle::Type(vehicleType));

    if (freeVehicles.size() <= 0) {
        this->showDialog("No vehicles are free in given date range");
        return;
    }

    gotoXY(0, 12);
    cout << "|Registration no |" << "| Seats |" << "|Price per Km |" << endl;

    for (auto & vehicle : freeVehicles) {
        string registrationNo = vehicle->getRegistrationNumber();
        string seats = to_string(vehicle->getSeats());

        stringstream ss;
        ss << std::fixed;
        ss << std::setprecision(2);
        ss << vehicle->getPricePerKm();

        string price = ss.str() + " Rs/Km";

        cout << "|" << registrationNo << string(7, ' ') << "|" << seats << string(7 - seats.length(), ' ') << "|" << price << string(14 - price.length(), ' ') << "|" << endl;
    }

    int offset = int(freeVehicles.size()) + 2;
    gotoXY(0, 12 + offset);
    cout << registrationNoLabel.length(), 12 + offset;
    getline(cin, registrationNo);

    try {
        vehicle = this->db->getVehicle(registrationNo);
    } catch (Error e) {
        this->showDialog(e.getMessage());
    }

    /* Find vehicle with given registration number and create a trip */
    try {
        vehicle = this->db->getVehicle(registrationNo);
    } catch (Error e) {
        this->showDialog(e.getMessage());
        return;
    }

    Trip* trip;
    try {
        trip = new Trip(this->db->getVehicleRef()->getRecordForId(
            (vehicleId, this->db->getUserRef())->getRecordForId(userId),
            Date(startDate), Date(endDate));
        this->db->addNewRecord(trip);
        stringstream ss;
        ss << "Trip " << trip->getTripId() << " added successfully";
        showDialog("Trip added successfully", ss.str());
    } catch (Error e) {
        showDialog(e.getMessage());
    }

    /* Release resources */
    delete trip;
}
```

```cpp
void Application::renderViewTrip() const {
    string header = "Enter trip id: ";
    long tripId;
    system("clear");

    gotoXY(0, 1);
    cout << header;
    gotoXY(int(header.length()), 1);
    cin >> tripId;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    /* Find Trip and display data */
    gotoXY(0, 3);
    try {
        auto trip = this->db->getTripRef()->getRecordForId(tripId);
        trip->display();

        cout << endl << "Press any key to continue";
        cin.get();
    } catch (Error e) {
        this->showDialog(e.getMessage());
    }
}
```

```cpp
void Application::renderStartTripMenu() const {
    string header = "Enter trip id: ";
    string readingLabel = "Enter odometer reading: ";

    long tripId;
    long startReading;

    system("clear");

    gotoXY(0, 1);
    cout << header;

    gotoXY(0, 2);
    cout << readingLabel;

    gotoXY(int(header.length()), 1);
    cin >> tripId;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    gotoXY(int(readingLabel.length()), 2);
    cin >> startReading;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    Trip* modifiedTrip;
    try {
        auto trip = this->db->getTripRef()->getRecordForId(tripId);
        modifiedTrip = new Trip(*trip);
        modifiedTrip->startTrip(startReading);

        this->db->updateRecord(modifiedTrip);
        showDialog("Trip started successfully");
    } catch (Error e) {
        this->showDialog(e.getMessage());
    }
    delete modifiedTrip;
}
```

```cpp
void Application::renderCompleteTripMenu() const {
    string header = "Enter trip id: ";
    string readingLabel = "Enter odometer reading: ";

    long tripId;
    long endReading;

    system("clear");

    gotoXY(0, 1);
    cout << header;

    gotoXY(0, 2);
    cout << readingLabel;

    gotoXY(int(header.length()), 1);
    cin >> tripId;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    gotoXY(int(readingLabel.length()), 2);
    cin >> endReading;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    try {
        auto trip = this->db->getTripRef()->getRecordForId(tripId);
        Trip* modifiedTrip = new Trip(*trip);
        auto fare = modifiedTrip->completeTrip(endReading);
        this->db->updateRecord(modifiedTrip);

        string ss;
        ss << "Total Fare: " << fare;
        showDialog("Trip completed successfully", ss.str());
    } catch (Error e) {
        this->showDialog(e.getMessage());
    }
}
```

```cpp
void Application::showDialog(const string& message, const string& id) const {
    int messageLength = int(message.length());
    string pressAnyKey = "Press any key to continue";
    int infoLength = int(pressAnyKey.length());

    int leftOffset = 15;
    int length = 50;
    int lineOffset = 9;
}
```

```cpp
system("clear");

/* Line 1 */
gotoXY(leftOffset, lineOffset++);
cout << "****************************************************";

/* Line 2 */
gotoXY(leftOffset, lineOffset);
cout << "*";
gotoXY(leftOffset + length - 1, lineOffset++);
cout << "*";

/* Line 3 */
gotoXY(leftOffset, lineOffset);
cout << "*";
gotoXY((80 - messageLength)/2, lineOffset);
cout << " message";
gotoXY(leftOffset + length - 1, lineOffset++);
cout << "*";

if(id == "1")
{
    /* Line 4 */
    gotoXY(leftOffset, lineOffset);
    cout << "*";
    gotoXY((int) (80 - int(id.length()))/2), lineOffset;
    cout << id;
    gotoXY(leftOffset + length - 1, lineOffset++);
    cout << "*";
}

/* Line 5 */
gotoXY(leftOffset, lineOffset);
cout << "*";
gotoXY((int) (80 - infoLength)/2, lineOffset);
cout << " pressAnyKey";
gotoXY(leftOffset + length - 1, lineOffset++);
cout << "*";

/* Line 6 */
gotoXY(leftOffset, lineOffset);
cout << "*";
gotoXY(leftOffset + length - 1, lineOffset++);
cout << "*";

/* Line 7 */
gotoXY(leftOffset, lineOffset++);
cout << "****************************************************";
```

```cpp
/* Wait until user press some key. */
cin.get();
}
void Application :: welcome () {
  system("clear");

  gotoXY(25, 5);
  cout << "Welcome To Vehicle Rental System" << endl;
  gotoXY(27, 23);
  cout << "Press any key to continue";

  /* Wait until user presses some key. */
  cin.get();
  this->renderMenu();
}

void Application :: start(){
  welcome();
}

void Application :: cleanMemory(){
  delete db;
}
```

## FILE: MAIN.CPP

```
********************************************************************************
********************************************************************************
VEHICLE RENTAL SYSTEM
COMPILED ON : LINUX (G++) WITH C++11 STANDARDS
********************************************************************************
********************************************************************************/
```

```cpp
/* Include custom headers */
#include "application.h"
```

# Object-Oriented Programming with C++

```cpp
/* Include standard cpp headers */

#include <iostream>

using namespace std;

int main(int argc, const char * argv[]) {

    Application * application = new Application();
    application->start();
}
```

# RUNNING THE APPLICATION

To run the application, create the above files in a directory and run the following command:

```
```
