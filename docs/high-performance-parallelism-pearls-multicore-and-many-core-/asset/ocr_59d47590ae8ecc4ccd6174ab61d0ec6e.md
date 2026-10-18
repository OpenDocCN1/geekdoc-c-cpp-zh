```
float sigma_sqr = sigma*sigma;
float time_sqrt = sqrt(time);
float nn = 2.0*b/sigma_sqr;
float m = 2.0*r/sigma_sqr;
float K = 1.0-exp(-r*time);
float q2 = (-(nn-1)+sqrt(pow((nn-1),2.0)+(4*m/K)))*0.5;
float q2_inf =0.5*(-(nn-1) + sqrt(pow((nn-1),2.0)+4.0*m));
float S_star_inf = X / (1.0 - 1.0/q2_inf);
float h2=-(b*time+2.0*sigma*time_sqrt)*(X/(S_star_inf-X));
float S_seed = X + (S_star_inf-X)*(1.0-exp(h2));
int no_iterations=0;
float Si=S_seed;
float g=1;
float gprime=1.0;
while ( no_iterations++<100)
{
    float c  = euro_call_payout(Si,X,r,b,sigma,time);
    float d1 = (log(Si/X)+(b+0.5*sigma_sqr)*time)
/(sigma*time_sqrt);
    g=(1.0-1.0/q2)*Si-X-c+(1.0/q2)*Si*exp((b-r)*time)*CND(d1);
    gprime=( 1.0-1.0/q2)*(1.0-exp((b-r)*time)*CND(d1))+
(1.0/q2)*exp((b-r)*time)*n(d1)*(1.0/(sigma*time_sqrt));
    Si=Si-(g/gprime);
};
float S_star = 0;
if (fabs(g)>ACCURACY) {
    S_star = S_seed;
}
else {
    S_star = Si;
};
float C=0;
float c  = euro_call_payout(S,X,r,b,sigma,time);
if (S>=S_star) {
    C=S-X;
}
else {
    float d1 = (log(S_star/X)+(b+0.5*sigma_sqr)*time) /
(sigma*time_sqrt);
    float A2 =  (1.0-exp((b-r)*time)*CND(d1)) * (S_star/q2);
    C=c+A2*pow((S/S_star),q2);
};
return max(C,c);
};
```