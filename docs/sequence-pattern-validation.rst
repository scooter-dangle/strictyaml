Sequence pattern validation
---------------------------

None


invalid_sequence_1.yaml:

.. code-block:: yaml
  - A
  - B
  - B

invalid_sequence_2.yaml:

.. code-block:: yaml
  - 3
  - 3
  - 3

valid_sequence.yaml:

.. code-block:: yaml
  - A
  - B
  - C

.. code-block:: python

    >>> from strictyaml import UniqueSeq, Str, YAMLValidationError, load
    >>> 
    >>> schema = UniqueSeq(Str())



.. code-block:: python

    >>> load(valid_sequence, schema) == ["A", "B", "C", ]
    True

.. code-block:: python

    >>> load(invalid_sequence_1, schema)
    EXCEPTION RAISED:
      while parsing a sequence
        in "<unicode string>", line 1, column 1:
          - A
           ^ (line: 1)
      duplicate found
        in "<unicode string>", line 3, column 1:
          - B
          ^ (line: 3)

.. code-block:: python

    >>> load(invalid_sequence_2, schema)
    EXCEPTION RAISED:
      while parsing a sequence
        in "<unicode string>", line 1, column 1:
          - '3'
           ^ (line: 1)
      duplicate found
        in "<unicode string>", line 3, column 1:
          - '3'
          ^ (line: 3)


Page automatically generated by hitchdoc from:
  hitch/sequence-pattern-validation.story