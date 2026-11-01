```
struct SalaryDetails
{
    SalaryDetails(PayGrade grade_, int location_id_, int years_of_service_,
                int reports_count_);

    PayGrade pay_grade;
    int location_id;
    int years_of_service;
    int reports_count;
};
```