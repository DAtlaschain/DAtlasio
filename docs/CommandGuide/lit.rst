lit - LLVM Integrated Tester
SYNOPSIS
:program:`lit` [options] [tests]

DESCRIPTION
:program:`lit` is a portable tool for executing LLVM and Clang style test suites, summarizing their results, and providing indication of failures. :program:`lit` is designed to be a lightweight testing tool with as simple a user interface as possible.

:program:`lit` should be run with one or more tests to run specified on the command line. Tests can be either individual test files or directories to search for tests (see :ref:`test-discovery`).

Each specified test will be executed (potentially in parallel) and once all tests have been run :program:`lit` will print summary information on the number of tests which passed or failed (see :ref:`test-status-results`). The :program:`lit` program will execute with a non-zero exit code if any tests fail.

By default :program:`lit` will use a succinct progress display and will only print summary information for test failures. See :ref:`output-options` for options controlling the :program:`lit` progress display and output.

:program:`lit` also includes a number of options for controlling how tests are executed (specific features may depend on the particular test format). See :ref:`execution-options` for more information.

Finally, :program:`lit` also supports additional options for only running a subset of the options specified on the command line, see :ref:`selection-options` for more information.

Users interested in the :program:`lit` architecture or designing a :program:`lit` testing implementation should see :ref:`lit-infrastructure`.

GENERAL OPTIONS
.. option:: -h, --help

 Show the :program:`lit` help message.

.. option:: -j N, --threads=N

 Run ``N`` tests in parallel.  By default, this is automatically chosen to
 match the number of detected available CPUs.

.. option:: --config-prefix=NAME

 Search for :file:`{NAME}.cfg` and :file:`{NAME}.site.cfg` when searching for
 test suites, instead of :file:`lit.cfg` and :file:`lit.site.cfg`.

.. option:: -D NAME[=VALUE], --param NAME[=VALUE]

 Add a user defined parameter ``NAME`` with the given ``VALUE`` (or the empty
 string if not given).  The meaning and use of these parameters is test suite
 dependent.

OUTPUT OPTIONS
.. option:: -q, --quiet

 Suppress any output except for test failures.

.. option:: -s, --succinct

 Show less output, for example don't show information on tests that pass.

.. option:: -v, --verbose

 Show more information on test failures, for example the entire test output
 instead of just the test result.

.. option:: -vv, --echo-all-commands

 Echo all commands to stdout, as they are being executed.
 This can be valuable for debugging test failures, as the last echoed command
 will be the one which has failed.
 This option implies ``--verbose``.

.. option:: -a, --show-all

 Show more information about all tests, for example the entire test
 commandline and output.

.. option:: --no-progress-bar

 Do not use curses based progress bar.

.. option:: --show-unsupported

 Show the names of unsupported tests.

.. option:: --show-xfail

 Show the names of tests that were expected to fail.

EXECUTION OPTIONS
.. option:: --path=PATH

 Specify an additional ``PATH`` to use when searching for executables in tests.

.. option:: --vg

 Run individual tests under valgrind (using the memcheck tool).  The
 ``--error-exitcode`` argument for valgrind is used so that valgrind failures
 will cause the program to exit with a non-zero status.

 When this option is enabled, :program:`lit` will also automatically provide a
 "``valgrind``" feature that can be used to conditionally disable (or expect
 failure in) certain tests.

.. option:: --vg-arg=ARG

 When :option:`--vg` is used, specify an additional argument to pass to
 :program:`valgrind` itself.

.. option:: --vg-leak

 When :option:`--vg` is used, enable memory leak checks.  When this option is
 enabled, :program:`lit` will also automatically provide a "``vg_leak``"
 feature that can be used to conditionally disable (or expect failure in)
 certain tests.

.. option:: --time-tests

 Track the wall time individual tests take to execute and includes the results
 in the summary output.  This is useful for determining which tests in a test
 suite take the most time to execute.  Note that this option is most useful
 with ``-j 1``.

SELECTION OPTIONS
.. option:: --max-tests=N

 Run at most ``N`` tests and then terminate.

.. option:: --max-time=N

 Spend at most ``N`` seconds (approximately) running tests and then terminate.

.. option:: --shuffle

 Run the tests in a random order.

.. option:: --num-shards=M

 Divide the set of selected tests into ``M`` equal-sized subsets or
 "shards", and run only one of them.  Must be used with the
 ``--run-shard=N`` option, which selects the shard to run. The environment
 variable ``LIT_NUM_SHARDS`` can also be used in place of this
 option. These two options provide a coarse mechanism for paritioning large
 testsuites, for parallel execution on separate machines (say in a large
 testing farm).

.. option:: --run-shard=N

 Select which shard to run, assuming the ``--num-shards=M`` option was
 provided. The two options must be used together, and the value of ``N``
 must be in the range ``1..M``. The environment variable
 ``LIT_RUN_SHARD`` can also be used in place of this option.

.. option:: --filter=REGEXP

  Run only those tests whose name matches the regular expression specified in
  ``REGEXP``. The environment variable ``LIT_FILTER`` can be also used in place
  of this option, which is especially useful in environments where the call
  to ``lit`` is issued indirectly.

ADDITIONAL OPTIONS
.. option:: --debug

 Run :program:`lit` in debug mode, for debugging configuration issues and
 :program:`lit` itself.

.. option:: --show-suites

 List the discovered test suites and exit.

.. option:: --show-tests

 List all of the discovered tests and exit.
