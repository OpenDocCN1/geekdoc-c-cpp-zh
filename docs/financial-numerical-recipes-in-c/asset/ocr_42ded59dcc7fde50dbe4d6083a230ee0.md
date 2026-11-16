```
const double& a, const double& b, const double& sigma);
/// defining classes wrapping the above term structure approximations
class term_structure::class_nelson_siegel : public term_structure::class {
private:
double beta0_, beta1_, beta2_, lambda_;
public:
term_structure::class_nelson_siegel(const double& beta0, const double& beta1,
const double& beta2, const double& lambda);
virtual double r(const double& t) const;
};
class term_structure::class_svensson : public term_structure::class {
private:
double beta0_, beta1_, beta2_, beta3_, tau1_, tau2_;
public:
term_structure::class_svensson(const double& beta0, const double& beta1, const double& beta2, const double& beta3,
const double& tau1, const double& tau2);
virtual double r(const double& T) const;
};
class term_structure::class_cubic_spline : public term_structure::class {
private:
double b_; double c_; double d_; vector<double> f_; vector<double> knots_;
public:
term_structure::class_cubic_spline(const double& b, const double& c, const double& d,
const vector<double>& f, const vector<double>& knots);
virtual double d(const double& t) const; // discount factor
};
class term_structure::class_cir : public term_structure::class {
private:
double r_; double kappa_; double lambda_; double theta_; double sigma_;
public:
term_structure::class_cir(const double& r, const double& k, const double& l,
const double& th, const double& sigma);
virtual double d(const double& t) const; // discount factor
};
class term_structure::class_vasicek : public term_structure::class {
private:
double r_; double a_; double b_; double sigma_;
public:
term_structure::class_vasicek(const double& r, const double& a, const double& b, const double& sigma);
virtual double d(const double& T) const;
};
///////////////
/// binomial term structure models
// bond option, rendleman bartter (binomial)
double bond_option_price_call_zero_american_rendleman_barter(const double& K, const double& option_maturity,
const double& S, const double& M,
const double& interest,
const double& bond_maturity,
const double& maturity_payment,
const int& no_steps);
vector< vector<double> > interest_rate_trees_gbm::build(const double& r0,
const double& u,
const double& d,
const int& n);
double interest_rate_trees_gbm::value_of_cashflows(const vector<double>& cflow,
const vector< vector<double> >& r_tree,
```