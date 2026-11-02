```
```cpp
#include <cmath>

namespace adevs
{

template <typename X> class linear_event_locator: public event_locator<X>
{
	public:
		linear_event_locator(ode_system<X>* sys, double err_tol);
		~linear_event_locator();
		bool find_events(bool* events, const double* qstart, double* qend,
				ode_solver<X>* solver, double& h);
	private:
		double *z[2]; // State events at the start and end of [0,h]
		const double err_tol; // Error tolerance
};

template <typename X>
linear_event_locator<X>::linear_event_locator(ode_system<X>* sys,
		double err_tol):
	event_locator<X>(sys),err_tol(err_tol)
{
	z[0] = new double[sys->numEvents()];
	z[1] = new double[sys->numEvents()];
}

template <typename X>
linear_event_locator<X>::~linear_event_locator()
{
	delete [] z[0]; delete [] z[1];
}

template <typename X>
bool linear_event_locator<X>::find_events(bool* events,
		const double* qstart, double* qend, ode_solver<X>* solver, double& h)
{
	// Look for events at the start of the interval
	this->sys->state_event_func(qstart,z[0]);
	for (int i = 0; i < this->sys->numEvents(); i++) {
		events[i] = fabs(z[0][i]) <= err_tol;
		// If an event was found, the event time is zero
		if (events[i]) h = 0.0;
	}
	// If an event was found at zero, put qstart in qend and return
	if (h == 0.0) {
		for (int i = 0; i < this->sys->numVars(); i++) qend[i] = qstart[i];
		return true;
	}
	// Look for events inside of the interval [0,h]
```
```