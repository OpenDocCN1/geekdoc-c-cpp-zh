```
static void cb_sh(Address, Address addr) // callbacks
   { reference_to<W7>(addr).sh(); }
static void cb_mv(Address, Address addr)
   { reference_to<W7>(addr).mv(); }
static void cb_cd(Address, Address addr)
   { reference_to<W7>(addr).cd(); }
static void cb_ad(Address, Address addr)
   { reference_to<W7>(addr).ad(); }
};
```

However, a **W7** (Window experiment number 7) really has six buttons; it just keeps two hidden:

```
W7::W7(int w, int h, const string& t)
     :Window<w,h,t>,
     sh_left{true}, mv_left{true}, cd_left{true}, ad_left{true}
{
p1 = new Button{Point{100,100},50,20,"show",cb_sh};
p2 = new Button{Point{200,100},50,20,"hide",cb_sh};

mvp = new Button{Point{100,200},50,20,"move",cb_mv};

cdp = new Button{Point{100,300},50,20,"create",cb_cd};

adp1 = new Button{Point{100,400},50,20,"activate",cb_ad};
adp2 = new Button{Point{200,400},80,20,"deactivate",cb_ad};

attach(*p1);
attach(*p2);
attach(*mvp);
attach(*cdp);
p2->hide();
attach(*adp1);
}
```

There are four callbacks. Each makes it appear that the button you press disappears and a new one appears. However, this is achieved in four different ways:

```
void W7::sh() // hide a button, show another
{
if (sh_left) {
p1->hide();
p2->show();
}
```