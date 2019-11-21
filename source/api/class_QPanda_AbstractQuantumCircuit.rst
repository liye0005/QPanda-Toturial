.. index:: pair: class; QPanda::AbstractQuantumCircuit
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit:

class QPanda::AbstractQuantumCircuit
====================================

.. toctree::
	:hidden:

Overview
~~~~~~~~

Quantum circuit basic abstract class. :ref:`More...<details-class_q_panda_1_1_abstract_quantum_circuit>`


.. ref-code-block:: cpp
	:class: doxyrest-overview-code-block

	#include <QCircuit.h>
	
	class AbstractQuantumCircuit
	{
	public:
		// methods
	
		virtual :ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>` :target:`getFirstNodeIter<doxid-class_q_panda_1_1_abstract_quantum_circuit_1ad13a60e0771b9bf6a984aff13967c15e>`() = 0;
		virtual :ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>` :target:`getLastNodeIter<doxid-class_q_panda_1_1_abstract_quantum_circuit_1a0c958083867fb03f0606ccc74ed13800>`() = 0;
		virtual :ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>` :target:`getEndNodeIter<doxid-class_q_panda_1_1_abstract_quantum_circuit_1a4732224c13dc949d2ed26388138dd0d3>`() = 0;
		virtual :ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>` :target:`getHeadNodeIter<doxid-class_q_panda_1_1_abstract_quantum_circuit_1af6f1864ea355c13eaa4e14bddf64934c>`() = 0;
	
		virtual :ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>` :target:`insertQNode<doxid-class_q_panda_1_1_abstract_quantum_circuit_1aeabd63772ee53de4c41141b7afef6d5f>`(
			:ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>`&,
			std::shared_ptr<:ref:`QNode<doxid-class_q_panda_1_1_q_node>`>
			) = 0;
	
		virtual :ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>` :target:`deleteQNode<doxid-class_q_panda_1_1_abstract_quantum_circuit_1aded25dd1af1558f04d6ad72736ab2ce9>`(:ref:`NodeIter<doxid-class_q_panda_1_1_node_iter>`&) = 0;
		virtual void :ref:`pushBackNode<doxid-class_q_panda_1_1_abstract_quantum_circuit_1a99f9d60e21e0e4d49c64e3253ff03001>`(std::shared_ptr<:ref:`QNode<doxid-class_q_panda_1_1_q_node>`>) = 0;
		virtual bool :ref:`isDagger<doxid-class_q_panda_1_1_abstract_quantum_circuit_1a9901ebf6ad22292cba7f9911ec3b600f>`() const = 0;
		virtual bool :ref:`getControlVector<doxid-class_q_panda_1_1_abstract_quantum_circuit_1ac4e834af252b8cefb1a9de6ae8781a7d>`(:ref:`QVec<doxid-class_q_panda_1_1_q_vec>`&) = 0;
		virtual void :ref:`setDagger<doxid-class_q_panda_1_1_abstract_quantum_circuit_1ad25e733d7f1a6bb837ca764135db1c8b>`(bool isDagger) = 0;
		virtual void :ref:`setControl<doxid-class_q_panda_1_1_abstract_quantum_circuit_1a0d810051304b282991d6fd1b87bb437d>`(:ref:`QVec<doxid-class_q_panda_1_1_q_vec>`) = 0;
		virtual void :ref:`clearControl<doxid-class_q_panda_1_1_abstract_quantum_circuit_1a3e61c68f5be51f3716506b42e6cf2359>`() = 0;
	};

	// direct descendants

	class :ref:`OriginCircuit<doxid-class_q_panda_1_1_origin_circuit>`;
	class :ref:`QCircuit<doxid-class_q_panda_1_1_q_circuit>`;
.. _details-class_q_panda_1_1_abstract_quantum_circuit:

Detailed Documentation
~~~~~~~~~~~~~~~~~~~~~~

Quantum circuit basic abstract class.

Methods
-------

.. index:: pair: function; pushBackNode
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit_1a99f9d60e21e0e4d49c64e3253ff03001:

.. ref-code-block:: cpp
	:class: doxyrest-title-code-block

	virtual void pushBackNode(std::shared_ptr<:ref:`QNode<doxid-class_q_panda_1_1_q_node>`>) = 0

Insert new Node at the end of current quantum circuit node.



.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- QNode\*

		- quantum node



.. rubric:: Returns:

void



.. rubric:: See also:

:ref:`QNode <doxid-class_q_panda_1_1_q_node>`

.. index:: pair: function; isDagger
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit_1a9901ebf6ad22292cba7f9911ec3b600f:

.. ref-code-block:: cpp
	:class: doxyrest-title-code-block

	virtual bool isDagger() const = 0

Judge current quantum circuit is dagger.



.. rubric:: Returns:

bool

.. index:: pair: function; getControlVector
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit_1ac4e834af252b8cefb1a9de6ae8781a7d:

.. ref-code-block:: cpp
	:class: doxyrest-title-code-block

	virtual bool getControlVector(:ref:`QVec<doxid-class_q_panda_1_1_q_vec>`&) = 0

Get control vector fron current quantum circuit node.



.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- QVec&

		- qubits vector



.. rubric:: Returns:

bool



.. rubric:: See also:

:ref:`QVec <doxid-class_q_panda_1_1_q_vec>`

.. index:: pair: function; setDagger
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit_1ad25e733d7f1a6bb837ca764135db1c8b:

.. ref-code-block:: cpp
	:class: doxyrest-title-code-block

	virtual void setDagger(bool isDagger) = 0

Set dagger to current quantum circuit.



.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- bool

		- is dagger

.. index:: pair: function; setControl
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit_1a0d810051304b282991d6fd1b87bb437d:

.. ref-code-block:: cpp
	:class: doxyrest-title-code-block

	virtual void setControl(:ref:`QVec<doxid-class_q_panda_1_1_q_vec>`) = 0

Set control qubits to current quantum circuit.



.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- :ref:`QVec <doxid-class_q_panda_1_1_q_vec>`

		- control qubits vector



.. rubric:: See also:

:ref:`QVec <doxid-class_q_panda_1_1_q_vec>`

.. index:: pair: function; clearControl
.. _doxid-class_q_panda_1_1_abstract_quantum_circuit_1a3e61c68f5be51f3716506b42e6cf2359:

.. ref-code-block:: cpp
	:class: doxyrest-title-code-block

	virtual void clearControl() = 0

Clear the control qubits for current quantum circuit.



.. rubric:: Parameters:

.. list-table::
	:widths: 20 80

	*
		- :ref:`QVec <doxid-class_q_panda_1_1_q_vec>`

		- control qubits vector



.. rubric:: See also:

:ref:`QVec <doxid-class_q_panda_1_1_q_vec>`

