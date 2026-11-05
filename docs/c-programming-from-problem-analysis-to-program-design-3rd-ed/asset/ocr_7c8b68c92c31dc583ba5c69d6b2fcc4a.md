```
namespace DBExample
{
    public class Member
    {
        private string id;
        private string firstName;
        private string lastName;
        private string phoneNumber;

        public Member()
        {
        }

        // Constructor
        public Member(string fname, string lname)
        {
            firstName = fname;
            lastName = lname;
        }

        public string FirstName
        {
            get
            {
                return firstName;
            }
        }

        public string LastName
        {
            get
            {
                return lastName;
            }
        }

        public string ID
        {
            get
            {
                return id;
            }
        }

        public string PhoneNumber
        {
            get
```