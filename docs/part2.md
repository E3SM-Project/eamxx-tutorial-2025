---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---

# **POMPEI**

Practicing On Manually Adding Processes to EAMxx Interfaces

---

## Designing `pompei` process

- Idealized injection of a new volcanic tracer `ash`
- Injection details are defined in `pompei.hpp` and `pompei.cpp` files
- Interfacing with EAMxx via an `AtmosphereProcess` _instance_ (`*_interface.*pp` files)

---

## Add `pompei` skeleton to EAMxx

In the EAMxx physics directory, create a pompei folder and copy templates

```shell
cd components/eamxx/src/physics
mkdir pompei
cp /global/cfs/cdirs/e3sm/eamxx-tutorial-2025/source/eamxx_interface/eamxx_template_process_interface.*  .
mv eamxx_template_process_interface.cpp eamxx_pompei_process_interface.cpp
mv eamxx_template_process_interface.hpp eamxx_pompei_process_interface.hpp
cp /global/cfs/cdirs/e3sm/eamxx-tutorial-2025/source/pompei/pompei.* ./
```

---

## `pompei.hpp`

```cpp
#include "pompei.hpp"

#include <cmath>

namespace pompei {

double ash_emission_rate(const double days_since_eruption) {
  if(days_since_eruption <= 0) return 0;

  double initial_emission = 1e4;
  double decay_rate       = -0.05;
  return initial_emission * exp(days_since_eruption * decay_rate);
}

}  // namespace pompei
```

---

## An `AtmosphereProcess` in EAMxx

- Intantiated inside an interface layer and contains _at a minimum_:
  - `set_grid`
  - `initialize_impl`
  - `run_impl`
  - `finalize_impl`
- `pompei` is an _instance_ of `AtmosphereProcess`

---

## Add `pompei` skeleton to EAMxx

In the EAMxx physics directory, create a pompei folder and copy templates

```shell
cd components/eamxx/src/physics
mkdir pompei
cp /global/cfs/cdirs/e3sm/eamxx-tutorial-2025/source/eamxx_interface/eamxx_template_process_interface.*  .
mv eamxx_template_process_interface.cpp eamxx_pompei_process_interface.cpp
mv eamxx_template_process_interface.hpp eamxx_pompei_process_interface.hpp
cp /global/cfs/cdirs/e3sm/eamxx-tutorial-2025/source/pompei/pompei.* ./
```

---

