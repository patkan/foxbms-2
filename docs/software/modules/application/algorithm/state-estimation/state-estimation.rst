.. include:: ./../../../../../macros.txt
.. include:: ./../../../../../units.txt

.. _STATE_ESTIMATION:

State estimation
================

|foxbms| performs various state estimations for the battery system:

 - state-of-charge (|soc|)
 - state-of-energy (|soe|)
 - state-of-health (|soh|)
 - state-of-function (|sof|)

The |soc| estimation is used to estimate the currently remaining charge (|Ah|)
within the battery system whereas the |soe| estimation provides the remaining
available energy (|Wh|) that can be drawn from the battery. The |soh| estimation
tries to assess the degradation state of the battery pack (aging) - how much
charge or energy can the battery pack store compared to its initial value.

The |sof| calculation provides a metric for the current capability of the
battery pack. For example, to prevent an accelerated degeneration of the
battery materials (aging) through operation near the limits given by their
electrochemical properties the |sof| is reduced. Especially fast charging at
low temperatures leads to accelerated aging. To attenuate these conditions, the
lowered current capability, the maximum recommended battery current is
calculated and communicated to other control units. The operator or the
supervisory control unit is encouraged to respect these suggested limits, but
violation of the current ranges is not resulting in an opening of the
contactors.

In an airborne application, where in extreme cases the full availability of the
system must be ensured, the operating area has to be widened at the expense of
the batteries health state. A typical automotive application would rather
prefer to enter a limp home mode with reduced system performance. Instead, a
stationary application would use more sensitive settings for the safe operating
area, as the long-term availability of the battery packs is of major importance.

Different estimation algorithms for |soc|, |soe| and |soh| can be selected via
the battery system configuration file (`bms.json`).

.. toctree::
    :maxdepth: 1
    :caption: List of available state estimation algorithms

    ./soc/soc_counting.rst
    ./soc/soc_debug.rst
    ./soc/soc_none.rst
    ./soe/soe_counting.rst
    ./soe/soe_debug.rst
    ./soe/soe_none.rst
    ./sof/trapezoid.rst
    ./soh/soh_debug.rst
    ./soh/soh_none.rst

This is achieved as all state estimation implementations follow the
:ref:`state_estimation_api`.

.. _state_estimation_api:

State estimation API
--------------------
