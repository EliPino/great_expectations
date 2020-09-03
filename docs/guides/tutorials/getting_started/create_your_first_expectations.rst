.. _tutorials__getting_started__create_your_first_expectations:

Create your first Expectations
==============================

:ref:`Expectations` are the key concept in Great Expectations.

Each Expectation is a declarative, machine-verifiable assertion about the expected format, content, or behavior of your data. Great Expectations comes with :ref:`dozens of built-in Expectations <expectation_glossary>`, and it's possible to :ref:`develop your own custom Expectations <how_to_guides__creating_and_editing_expectations__how_to_create_custom_expectations>`, too.

.. admonition:: Admonition from Mr. Dickens.

    "Take nothing on its looks; take everything on evidence. There's no better rule."

The CLI will help you create your first Expectation Suite. :ref:`expectation_suites` are simply collections of Expectations. In order to create a new suite, we will use the ``scaffold`` command to automatically create an Expectation Suite called ``taxi.demo`` with the help of a built-in profiler. Type the following into your terminal:

.. code-block:: bash

    great_expectations suite scaffold taxi.demo

You will see the following output:

.. code-block:: bash

    Heads up! This feature is Experimental. It may change. Please give us your feedback!

    Which table would you like to use? (Choose one)
        1. yellow_tripdata_sample_2019_01 (table)
        2. yellow_tripdata_staging (table)
        Do not see the table in the list above? Just type the SQL query
    : 1


Which data should I choose when creating Expectations?
-------------------

You may now wonder how we know which table to choose in this step. Here's an explanation:

* In this example, we want to build an Expectation Suite based on what we know about our taxi data from the January 2019 data set: each taxi ride has a ``passenger_count`` between 1 and 6.
* We then want to use that Expectation Suite to validate any future data that is loaded into the ``staging`` table.
*  Hence, we choose the ``yellow_tripdata_sample_2019_01`` table when creating the new Expectation Suite, which we will then use to validate the ``yellow_tripdata_staging`` table **in a later step**.

Makes sense, right?

After selecting the table, Great Expectations will open a Jupyter notebook which will take you through the next part of the ``scaffold`` workflow.

.. warning::

   Don't execute the Jupyter notebook cells just yet!


Creating Expectations in Jupyter notebooks
-------------------

Notebooks are a simple way of interacting with the Great Expectations Python API. You could also just write all this in plain Python code, but for convenience, Great Expectations provides you some boilerplate code in notebooks.

Since notebooks are often less permanent, creating Expectations in a notebook also helps reinforce that the source of truth about Expectations is the Expectation Suite, **not** the code that generates the Expectations.


.. figure:: /images/jupyter_scaffold.gif


**Let's scroll through the notebook and see what's happening in each cell:**

#. The first cell does several things: It imports all the relevant libraries, loads a Data Context, and creates what we call a Batch of your data and Expectation Suite.

#. The second cell allows you to specify which columns you want to run the automated Profiler on. Remember how we want to add some tests on the ``passenger_count`` column to ensure that its values range between 1 and 6? **Let's uncomment just this one line:**

    .. code-block:: python

        included_columns = [
            # 'vendor_id',
            # 'pickup_datetime',
            # 'dropoff_datetime',
            'passenger_count',
            ...
        ]

#. The next cell passes the Profiler config to the ``BasicSuiteBuilderProfiler``, which will then profile the data and create the relevant Expectations to add to your ``taxi.demo`` suite.

#. The last cell does several things again: It saves the Expectation Suite to disk, runs the validation against the loaded data batch, and then builds and opens Data Docs, so you can look at the validation results.

**Let's execute all the cells** and wait for Great Expectations to open a browser window with Data Docs. **Go to the next step in the tutorial** for an explanation of what you see in Data Docs!