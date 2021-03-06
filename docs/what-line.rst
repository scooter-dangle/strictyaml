What line
---------

Line numbers, the text of an item and text of surrounding lines
can be grabbed from returned YAML objects - using .start_line,
.end_line, lines(), lines_before(x) and lines_after(x).

.. code-block:: python

    from strictyaml import Map, Str, YAMLValidationError, load
    
    schema = Map({"y": Str(), "a": Str(), "b": Str(), "c": Str(), "d": Str()})

With variable 'commented_yaml':

.. code-block:: yaml

  y: p
  # Some comment
  
  a: |
    x
  
  # Another comment
  b: y
  c: a
  
  d: b



.. code-block:: python

    load(commented_yaml, schema)["a"].start_line == 2
    >>> True



.. code-block:: python

    load(commented_yaml, schema)["a"].end_line == 7
    >>> True



.. code-block:: python

    load(commented_yaml, schema)["d"].start_line == 10
    >>> True



.. code-block:: python

    load(commented_yaml, schema)["d"].end_line == 11
    >>> True



.. code-block:: python

    load(commented_yaml, schema).keys()[1].start_line == 2
    >>> True



.. code-block:: python

    load(commented_yaml, schema).start_line == 1
    >>> True



.. code-block:: python

    load(commented_yaml, schema).end_line == 11
    >>> True

With variable 'yaml_snippet':

.. code-block:: yaml

  # Some comment
  
  a: |
    x
  
  # Another comment



.. code-block:: python

    load(commented_yaml, schema)['a'].lines() == yaml_snippet.strip()
    >>> True



.. code-block:: python

    load(commented_yaml, schema)['a'].lines_before(1) == "y: p"
    >>> True



.. code-block:: python

    (load(commented_yaml, schema)['a'].lines_after(4)).should.be.equal("b: y\nc: a\n\nd: b"
    )
    >>> True

With variable 'yaml_with_list':

.. code-block:: yaml

  a:
    b:
    - 1
    # comment
    - 2
    - 3
    - 4



.. code-block:: python

    (load(yaml_with_list)['a']['b'][1].start_line).should.be.equal(4)
    >>> True



.. code-block:: python

    (load(yaml_with_list)['a']['b'][1].end_line).should.be.equal(5)
    >>> True


Page automatically generated by hitchdoc from:
  hitch/whatline.story