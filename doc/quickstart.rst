Getting Started
===============

The starting point for writing code is the :class:`~qiskit.QuantumCircuit`.
A circuit (or score if you are coming from the Quantum Experience) are
collections of :class:`~qiskit.ClassicalRegister` objects,
:class:`~qiskit.QuantumRegister` objects and
:mod:`gates <qiskit.extensions.standard>`. Through the
:ref:`top-level functions <qiskit_top_level_functions>`, the circuits can be
sent to remote quantum devices or local simulator backends and collect the
results for further analysis.

To compose and run a circuit on a simulator, which is distributed with
this project, one can do,

.. code-block:: python

    # Import the QISKit SDK
    from qiskit import QuantumCircuit, ClassicalRegister, QuantumRegister
    from qiskit import available_backends, execute

    # Create a Quantum Register with 2 qubits.
    q = QuantumRegister(2)
    # Create a Classical Register with 2 bits.
    c = ClassicalRegister(2)
    # Create a Quantum Circuit
    qc = QuantumCircuit(q, c)

    # Add a H gate on qubit 0, putting this qubit in superposition.
    qc.h(q[0])
    # Add a CX (CNOT) gate on control qubit 0 and target qubit 1, putting
    # the qubits in a Bell state.
    qc.cx(q[0], q[1])
    # Add a Measure gate to see the state.
    qc.measure(q, c)

    # See a list of available local simulators
    print("Local backends: ", available_backends({'local': True}))

    # Compile and run the Quantum circuit on a simulator backend
    job_sim = execute(qc, "local_qasm_simulator")
    sim_result = job_sim.result()

    # Show the results
    print("simulation: ", sim_result)
    print(sim_result.get_counts(qc))

The :func:`~qiskit.Result.get_counts` method outputs a dictionary of
``state:counts`` pairs;

.. code-block:: python

    {'00': 531, '11': 493}

Quantum Chips
-------------

You can execute your QASM circuits on a real chip by using the IBM Q experience (QX) cloud platform. 
Currently through QX you can use the following chips:

-   ``ibmqx4``: `5-qubit backend <https://ibm.biz/qiskit-ibmqx4>`_

-   ``ibmqx5``: `16-qubit backend <https://ibm.biz/qiskit-ibmqx5>`_

For chip details and realtime information about availability visit the
`IBM Q experience backend information <https://github.com/QISKit/ibmqx-backend-information>`_
and the `IBM Q experience devices page <https://quantumexperience.ng.bluemix.net/qx/devices>`_.

.. include:: example_real_backend.rst

Project Organization
--------------------

Python example programs can be found in the *examples* directory, and test scripts are
located in *test*. The *qiskit* directory is the main module of the SDK.
