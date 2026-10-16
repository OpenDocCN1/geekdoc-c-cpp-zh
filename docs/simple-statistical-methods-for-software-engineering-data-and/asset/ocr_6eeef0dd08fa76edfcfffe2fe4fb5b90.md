Software Engineering Institute (SEI) introduced the GQ(I)M paradigm [2] as a value adding refinement to the GQM paradigm. GQ(I)M uses Peter Singe’s mental models to drive metric choice and indicators to convey meaning. GQ(I)M certainly has helped to widen the reach of GQM.

> **BOX 5.1  FLYING A PLANE AND GQM**
> 
> Even the simplest propeller airplane would have meters to measure altitude and fuel. These measurements are intrinsic to the airplane design. The meters are fitted by the manufacturer and come with the airplane as basic parts of the airplane. One cannot fly without altitude, speed, and fuel level metrics. Flying a plane without altimeter is unthinkable. A plane without a speedometer is unrealistic. A pilot cannot make decisions without a fuel indicator. These metrics are not “goal driven” and certainly not business strategy driven but are driven by design requirements. One can think of purposes for each metric, but these purposes are not derived from business strategies and business goals; these purposes are implicitly inherent in product engineering. Whether there are goals or not, these meters will be fitted to the plane, almost spontaneously, like a reflex action triggered by survival needs. There are no options here. These metrics are indispensable and obvious. One does not need a GQM approach to figure them out.
> 
> Hence, cost, schedule, and quality metrics are also indispensable in a software development project. These are not “goal driven” but are based on operational needs. One does not have a choice.

# Difficulties with Applying GQM to
Designing a Metrics System

First, the intermediate stage (question) in the GQM paradigm is not very helpful. We simply map metrics to goal. The mapping phase in COSMIC size measurement is a great illustration.

Second, while applying GQM, people tend to start with corporate goals and attempt to drill down to metrics. This often turns out to be a futile attempt. Large organizations have spent days with GQM, getting lost in defining goals, subgoals, and sub-subgoals. All these goals go into goal translation and could never make it to metric definitions in a single workshop. Rather, we would first derive performance goals from business goals using a goal tree. This is a goal deployment, a leadership game. Designers of metrics should discriminate metrics mapping from goal deployment. Designers of metrics should pick up selected performance goals and map them to metrics.

Third, some metrics are specified by clients. Customer-specified metrics seem to run very well in organizations. Data collection is smooth. There is no need for a separate mechanism to identify and define these metrics.