```
P(Test=positive|Tran=good) = .3
P(Test=positive|Tran=bad) = .9
P(Tran=good|Car=lemon) = .4
P(Tran=good|Car=peach) = .9
P(Car=lemon) = .2
P(Car=peach) = .8
```

![](bbox=[0.17, 0.11, 0.78, 0.26])

```
r1 = Run test
r2 = Buy Spiffycar
r3 = Do not buy
d1 = Buy Spiffycar
d2 = Do not buy
U(r1,d1,good,fine) = $10,800
U(r1,d1,good,faulty) = $10,200
U(r1,d1,bad, fine) = $7800
U(r1,d1,bad,faulty) = $7200
U(r1,d2,t,a) = $9800
U(r2,d,good,fine) = $11,000
U(r2,d,good,faulty) = $10,400
U(r2,d,bad,fine) = $8000
U(r2,d,bad,faulty) = $7400
U(r3,d,t,a) = $10,000
```

Figure 8.18 An influence diagram modeling Sam's decision concerning buying the Spiffycar when the alternator may be faulty.

The CT scan can detect mediastinal metastases. The test is not absolutely accurate. Rather, if we let MedMet be a variable whose values are present and absent depending on whether or not mediastinal metastases are present and CTest be a variable whose values are cpos and cneg depending on whether or not the CT scan is positive, we have

```
P(CTest = cpos|MedMet = present) = .82
P(CTest = cpos|MedMet = absent) = .19.
```

The mediastinoscopy is an invasive test of mediastinal lymph nodes for determining whether the tumor has spread to those nodes. If we let Mtest be a variable whose values are mpos and mneg depending on whether or not the mediastinoscopy is positive, we have

```
P(MTest = mpos|MedMet = present) = .82
P(MTest = mpos|MedMet = absent) = .005.
```

The mediastinoscopy can cause death. If we let E be the decision concerning whether to have the mediastinoscopy, e1 be the choice to have it, e2 be the choice not to have it, and MedDeath be a variable whose values are mdie and mlive depending on whether the patient dies from the mediastinoscopy, we have

```
P(MedDeath = mdie|E = e1) = .005
P(MedDeath = mdie|E = e2) = 0.
```