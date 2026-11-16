# Appendix D

# Summarizing routine names

In many of the algorithms use is made of other routines. To simplify the matter all routines are summarised in one header file, fin_recipes.h. This appendix shows this file.

```
// file: fin_recipes.h
// author: Bernt Arne Oedegaard
// defines all routines in the financial numerical recipes "book"

#ifndef _PIN_RECIPES_H_
#define _PIN_RECIPES_H_

#include <vector>
#include <cmath>
using namespace std;

// ////////////////// present value ///////////////////////////////////
// discrete compounding
// discrete, annual compounding
double cash_flow_pv_discrete( const vector<double>& cflow_times, const vector<double>& cflow_amounts,
                              const double& r);
double cash_flow_irr_discrete(const vector<double>& cflow_times, const vector<double>& cflow_amounts);
bool cash_flow_unique_irr(const vector<double>& cflow_times, const vector<double>& cflow_amounts);
double bonds_price_discrete(const vector<double>& cashflow_times, const vector<double>& cashflows,
                            const double& r);
double bonds_yield_to_maturity_discrete(const vector<double>& cashflow_times, const vector<double>& cashflows,
                                        const double& bond_price);
double bonds_duration_discrete(const vector<double>& cashflow_times,
                               const vector<double>& cashflows,
                               const double& r);
double bonds_duration_macaulay_discrete(const vector<double>& cashflow_times,
                                        const vector<double>& cashflows,
                                        const double& bond_price);
double bonds_duration_modified_discrete(const vector<double>& cashflow_times,
                                        const vector<double>& cashflows,
                                        const double& bond_price);
double bonds_convexity_discrete(const vector<double>& cashflow_times,
                                const vector<double>& cashflows,
                                const double& r);
// ////////////////// continuous compounding ///////////////////////////////////
double cash_flow_pv(const vector<double>& cflow_times, const vector<double>& cflow_amounts,const double& r);
double cash_flow_irr(const vector<double>& cflow_times, const vector<double>& cflow_amounts);
double cash_flow_price(const vector<double>& cflow_times, const vector<double>& cflow_amounts, const vector<double>& cashflows, const double& r);
double bonds_price(const vector<double>& coupon_times, const vector<double>& coupon_amounts,
                   const vector<double>& principal_times, const vector<double>& principal_amounts,
                   const double& r);
```