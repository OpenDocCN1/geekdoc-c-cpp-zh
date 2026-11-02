```
~~~cpp
97 template <class X>
98 void Simulator<X>::getAllChildren(Network<X>* model, Set<Atomic<X>*>& s)
99 {
100     Set<Devs<X>*> tmp;
101     model->getComponents(tmp); // Get the set of components
102     // Put the atomic components into s and call getAllChildren for
103     // the network components
104     typename Set<Devs<X>*>::iterator iter;
105     for (iter = tmp.begin(); iter != tmp.end(); iter++) {
106         if ((*iter)->typeIsNetwork() != NULL)
107             getAllChildren((*iter)->typeIsNetwork(),s);
108         else
109             s.insert((*iter)->typeIsAtomic());
110     }
111 }
112
113
114 template <class X>
115 void Simulator<X>::computeNextOutput()
116 {
117     // If the imminent set is up to date, then just return
118     if (imm.empty() == false) return;
119     // Get the imminent models from the schedule. This sets the active flags.
120     sched.getImminent(imm);
121     // Compute output functions and route the events. The bags of output
122     // are held for garbage collection at a later time.
123     for (typename Bag<Atomic<X>*>::iterator imm_iter = imm.begin();
124          imm_iter != imm.end(); imm_iter++) {
125         Atomic<X>* model = *imm_iter;
126         // Don't recalculate the model's output if we already have it
127         if (model->y == NULL) {
128             model->y = io_pool.make_obj();
129             model->output_func(*model->y);
130             // Route each event in y
131             for (typename Bag<X>::iterator y_iter = model->y->begin();
132                  y_iter != model->y->end(); y_iter++)
133                 route(model->getParent(),model,*y_iter);
134         }
135     }
136 }
137
138
139 template <class X>
140 void Simulator<X>::computeNextState(Bag<Event<X> >& input, double t)
141 {
142     // If t is less than the next event time, make sure that
143     // computeNextOutput() has not been called
144     if (t < sched.minPriority() && !imm.empty())
145         throw exception("Input can not precede output");
146     // If the output function needs to be computed, then do it
~~~
```