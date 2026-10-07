2. The code is as follows:
struct data {
int value1;
float value2;
float value3;
}
info ;

3. info.value1 = 100;

4. The code is as follows:
struct data *ptr;
ptr = &info;

5. The code is as follows:
ptr->value2 = 5.5;
(*ptr).value2 = 5.5;

6. The code is as follows:
struct data {
char name[21];
};

8. The following uses the values from quiz question 5 for the initialization:
RECORD myaddress = "RTSoftware",
"P.O. Box 1213",
"Carmel", "IN", "46032-1213" };

9. This code has two problems. The first is that the structure should contain a tag. The second is that the sign is initialized. The initialization values should be in braces.
struct zodiac {
char zodiac_sign[21];
int month;
sign = {"Leo", 8};