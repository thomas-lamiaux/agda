.. _command-line-options:

********************
Command-line options
********************

Command-line options
--------------------

Agda accepts the following options.

General options
~~~~~~~~~~~~~~~

.. option:: --help[={TOPIC}], -?[{TOPIC}]

     Show basically this help, or more help about ``TOPIC``. Current
     topics available: ``warning``.

.. option:: --interaction

     For use with the Emacs mode (no need to invoke yourself).

.. option:: --interaction-json

     .. versionadded:: 2.6.1

     For use with other editors such as Atom (no need to invoke
     yourself).

.. option:: --interaction-exit-on-error

     .. versionadded:: 2.6.3

     Makes Agda exit with a non-zero exit code if :option:`--interaction` or
     :option:`--interaction-json` are used and a type error is encountered. The
     option also makes Agda exit with exit code 113 if Agda fails to
     parse a command.

     This option might for instance be used if Agda is controlled from
     a script.

.. option:: --interactive, -I

     Start in interactive mode (not maintained).

.. option:: --trace-imports[=(0|1|2|3)]

     .. versionadded:: 2.6.4

     Configure printing of messages when an imported module is accessed during type-checking.

     .. list-table::

       * - ``0``
         - Do not print any messages about checking a module.
       * - ``1``
         - | Print only `Checking ...` when an access to an uncompiled module occurs.
           | This is the default behavior if ``--trace-imports`` is not specified.
       * - ``2``
         - | Use the effect of ``1``, but also print `Finished ...`
           | when a compilation of an uncompiled module is finished.
           | This is the behavior if ``--trace-imports`` is specified without a value.
       * - ``3``
         - | Use the effect of ``2``, but also print `Loading ...`
           | when a compiled module (interface) is accessed during the type-checking.

.. option:: --no-projection-like

     .. versionadded:: 2.6.1

     Turn off the analysis whether a type signature likens that of a
     projection.

     Projection-likeness is an optimization that reduces the size of
     terms by dropping parameter-like reconstructible function
     arguments. Thus, it is advisable to leave this optimization on,
     the flag is meant for debugging Agda.

     See also the :ref:`NOT_PROJECTION_LIKE<not_projection_like-pragma>` pragma.

.. option:: --only-scope-checking

     .. versionadded:: 2.5.3

     Only scope-check the top-level module, do not type-check it (see
     :ref:`quickLaTeX`).

.. option:: --version, -V

     Show version number.

.. option:: --print-agda-dir

     .. versionadded:: 2.6.2

     Outputs the root (:envvar:`AGDA_DIR`)
     of the directory structure holding Agda's data files
     such as core libraries, style files for the backends etc.

.. option:: --transliterate

     .. versionadded:: 2.6.3

     When writing to stdout or stderr Agda will (hopefully) replace
     code points that are not supported by the current locale or code
     page by something else, perhaps question marks.

     This option is not supported when :option:`--interaction` or
     :option:`--interaction-json` are used, because when those options
     are used Agda uses UTF-8 when writing to stdout (and when reading
     from stdin).

Compilation
~~~~~~~~~~~

See :ref:`compilers` for backend-specific options.

.. option:: --compile-dir={DIR}

     Set ``DIR`` as directory for compiler output (default: the
     project root).

.. option:: --no-main

     Do not treat the requested module as the main module of a program
     when compiling.

.. option:: --with-compiler={PATH}

     Set ``PATH`` as the executable to call to compile the backend's
     output (default: ghc for the GHC backend).

Generating highlighted source code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. option:: --count-clusters

     .. versionadded:: 2.5.3

     Count extended grapheme clusters when generating LaTeX code (see
     :ref:`grapheme-clusters`).
     Available only when Agda was built with Cabal flag :option:`enable-cluster-counting`.

     Pragma option since 2.5.4.

.. option:: --css={URL}

     Set URL of the CSS file used by the HTML files to ``URL`` (can be
     relative).

.. option:: --dependency-graph={FILE}

     .. versionadded:: 2.3.0

     Generate a Dot_ file ``FILE`` with a module dependency graph.

.. option:: --dependency-graph-include={LIBRARY}

     .. versionadded:: 2.6.3

     Include modules from the given library in the dependency graph.
     This option can be used multiple times to include modules from
     several libraries. If this option is not used at all, then all
     modules are included. (Note that the module given on the command
     line might not be included.)

     A module ``M`` is considered to be in the library ``L`` if ``L``
     is the ``name`` of a ``.agda-lib`` file ``A``
     :ref:`associated<The_agda-lib_files_associated_to_a_give_Agda_file>`
     to ``M`` (even if ``M``'s file can not be found via the
     ``include`` paths in ``A``).

.. option:: --html

     .. versionadded:: 2.2.0

     Generate HTML files with highlighted source code (see
     :ref:`generating-html`).

.. option:: --html-dir={DIR}

     Set directory in which HTML files are placed to ``DIR`` (default:
     html).

.. option:: --html-highlight=[code,all,auto]

     .. versionadded:: 2.6.0

     Whether to highlight non-Agda code as comments in generated HTML
     files (default: all; see :ref:`generating-html`).

.. option:: --latex

     .. versionadded:: 2.3.2

     Generate LaTeX with highlighted source code (see
     :ref:`generating-latex`).

.. option:: --latex-dir={DIR}

     .. versionadded:: 2.5.2

     Set directory in which LaTeX files are placed to ``DIR``
     (default: latex).

.. option:: --vim

     Generate Vim_ highlighting files.

Imports and libraries
~~~~~~~~~~~~~~~~~~~~~

(see :ref:`package-system`)

.. option:: --ignore-all-interfaces

     .. versionadded:: 2.6.0

     Ignore *all* interface files, including builtin and primitive
     modules; only use this if you know what you are doing!

.. option:: --ignore-interfaces

     Ignore interface files (re-type check everything, except for
     builtin and primitive modules).

.. option:: --include-path={DIR}, -i={DIR}

     Look for imports in ``DIR``.

.. option:: --library={DIR}, -l={LIB}

     .. versionadded:: 2.5.1

     Use library ``LIB``.

.. option:: --library-file={FILE}

     .. versionadded:: 2.5.1

     Use ``FILE`` instead of the standard ``libraries`` file.

.. option:: --local-interfaces

     .. versionadded:: 2.6.1

     Read and write interface files next to the Agda files they
     correspond to (i.e. do not attempt to regroup them in a
     ``_build/`` directory at the project's root).

.. option:: --no-default-libraries

     .. versionadded:: 2.5.1

     Don't use default library files.

.. option:: --no-libraries

     .. versionadded:: 2.5.2

     Don't use any library files.

.. _command-line-pragmas:

Command-line and pragma options
-------------------------------

The following options can also be given in ``.agda`` files using the
:ref:`OPTIONS<options-pragma>` pragma.

Caching
~~~~~~~

.. option:: --caching, --no-caching

     .. versionadded:: 2.5.4

     Enable or disable caching of typechecking.

     Default: ``--caching``.

Printing and debugging
~~~~~~~~~~~~~~~~~~~~~~

.. option:: --no-unicode

     .. versionadded:: 2.5.4

     Do not use unicode characters to print terms.

.. option:: --show-implicit

     Show implicit arguments when printing.

.. option:: --show-irrelevant

     .. versionadded:: 2.3.2

     Show irrelevant arguments when printing.

.. option:: --verbose={N}, -v={N}

     Set verbosity level to ``N``.

.. option:: --profile={PROF}

     .. versionadded:: 2.6.3

    Turn on profiling option ``PROF``. Available options are

    .. list-table::

       * - ``internal``
         - Measure time taken by various parts of the system (type checking, serialization, etc)
       * - ``modules``
         - Measure time spent on individual (Agda) modules
       * - ``definitions``
         - Measure time spent on individual (Agda) definitions
       * - ``sharing``
         - Measure things related to sharing
       * - ``serialize``
         - Collect detailed statistics about serialization
       * - ``constraints``
         - Collect statistics about constraint solving
       * - ``metas``
         - Count number of created metavariables
       * - ``interactive``
         - Measure time of interactive commands
       * - ``conversion``
         - Count number of times various steps of the conversion algorithm are
           used (reduction, eta-expansion, syntactic equality, etc)


    Only one of ``internal``, ``modules``, and ``definitions`` can be turned on
    at a time. You can also give ``--profile=all`` to turn on all profiling
    options (choosing ``internal`` over ``modules`` and ``definitions``, use
    ``--profile=modules --profile=all`` to pick ``modules`` instead).

Copatterns and projections
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. option:: --copatterns, --no-copatterns

     .. versionadded:: 2.4.0

     Enable or disable definitions by copattern matching (see
     :ref:`copatterns`).

     Default: ``--copatterns`` (since 2.4.2.4).

.. option:: --postfix-projections

     .. versionadded:: 2.5.2

     Make postfix projection notation the default.

Experimental features
~~~~~~~~~~~~~~~~~~~~~

.. option:: --allow-exec

     .. versionadded:: 2.6.2

     Enable system calls during type checking (see :ref:`reflection`).

.. option:: --confluence-check, --local-confluence-check

     .. versionadded:: 2.6.1

     Enable optional (global or local) confluence checking of REWRITE
     rules (see :ref:`confluence-check`).

.. option:: --cubical

     .. versionadded:: 2.6.0

     Enable cubical features. Turns on :option:`--cubical-compatible`
     and :option:`--without-K` (see :ref:`cubical`).

.. option:: --erased-cubical

     .. versionadded:: 2.6.3

     Enable a :ref:`variant<erased-cubical>` of Cubical Agda, and turn
     on :option:`--without-K`.

.. option:: --experimental-irrelevance

     .. versionadded:: 2.3.0

     Enable potentially unsound irrelevance features (irrelevant
     levels, irrelevant data matching) (see :ref:`irrelevance`).

.. option:: --guarded

     .. versionadded:: 2.6.2

     Enable locks and ticks for guarded recursion
     (see :ref:`Guarded Cubical Agda <guarded-cubical>`).

.. option:: --injective-type-constructors

     .. versionadded:: 2.2.8

     Enable injective type constructors (makes Agda anti-classical and
     possibly inconsistent).

.. option:: --prop, --no-prop

     .. versionadded:: 2.6.0

     Enable or disable declaration and use of
     definitionally proof-irrelevant propositions
     (see :ref:`proof-irrelevant propositions <prop>`).

     Default: `--no-prop`.

.. option:: --rewriting

     .. versionadded:: 2.4.2.4

     Enable declaration and use of REWRITE rules (see
     :ref:`rewriting`).

.. option:: --two-level

     .. versionadded:: 2.6.2

     Enable the use of strict (non-fibrant) type universes ``SSet``
     *(two-level type theory)*.



Errors and warnings
~~~~~~~~~~~~~~~~~~~

.. option:: --allow-incomplete-matches

     .. versionadded:: 2.6.1

     Succeed and create interface file regardless of incomplete
     pattern-matching definitions. See also the
     :ref:`NON_COVERING<non_covering-pragma>` pragma.

.. option:: --allow-unsolved-metas

     Succeed and create interface file regardless of unsolved meta
     variables (see :ref:`metavariables`).

.. option:: --no-positivity-check

     Do not warn about not strictly positive data types (see
     :ref:`positivity-checking`).

.. option:: --no-termination-check

     Do not warn about possibly nonterminating code (see
     :ref:`termination-checking`).

.. option:: --warning={GROUP|FLAG}, -W {GROUP|FLAG}

     .. versionadded:: 2.5.3

     Set warning group or flag (see :ref:`warnings`).

Pattern matching and equality
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. option:: --exact-split, --no-exact-split

     .. versionadded:: 2.5.1

     Require [do not require] all clauses in a definition to hold as
     definitional equalities unless marked ``CATCHALL`` (see
     :ref:`case-trees`).

     Default: ``--no-exact-split``.

.. option:: --no-eta-equality

     .. versionadded:: 2.5.1

     Default records to ``no-eta-equality`` (see :ref:`eta-expansion`).

.. option:: --cohesion

     .. versionadded:: 2.6.3

     Enable the cohesion modalities, in particular ``@♭`` (see
     :ref:`flat`).

.. option:: --flat-split

     .. versionadded:: 2.6.1

     Enable pattern matching on ``@♭`` arguments (see
     :ref:`pattern-matching-on-flat`).

.. option:: --no-pattern-matching

     .. versionadded:: 2.4.0

     Disable pattern matching completely.

.. option:: --with-K

     .. versionadded:: 2.4.2

     Overrides a global :option:`--without-K` in a file (see
     :ref:`without-K`).

.. option:: --without-K

     .. versionadded:: 2.2.10

     Disables reasoning principles incompatible with univalent type
     theory, most importantly Streicher's K axiom (see
     :ref:`without-K`).

.. option:: --cubical-compatible

     .. versionadded:: 2.6.3

     Generate internal support code necessary for use from Cubical Agda
     (see :ref:`cubical-compatible`). Implies :option:`--without-K`.

.. option:: --keep-pattern-variables

     .. versionadded:: 2.6.1

     Prevent interactive case splitting from replacing variables with
     dot patterns (see :ref:`dot-patterns`).

Search depth and instances
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. option:: --instance-search-depth={N}

     .. versionadded:: 2.5.2

     Set instance search depth to ``N`` (default: 500; see
     :ref:`instance-arguments`).

.. option:: --inversion-max-depth={N}

     .. versionadded:: 2.5.4

     Set maximum depth for pattern match inversion to ``N`` (default:
     50). Should only be needed in pathological cases.

.. option:: --termination-depth={N}

     .. versionadded:: 2.2.8

     Allow termination checker to count decrease/increase upto ``N``
     (default: 1; see :ref:`termination-checking`).

.. option:: --overlapping-instances, --no-overlapping-instances

     .. versionadded:: 2.6.0

     Consider [do not consider] recursive instance arguments during
     pruning of instance candidates.

     Default: ``--no-overlapping-instances``.

.. option:: --qualified-instances, --no-qualified-instances

     .. versionadded:: 2.6.2

     Consider [do not consider] instances that are (only) in scope
     under a qualified name.

     Default: ``--qualified-instances``.


Other features
~~~~~~~~~~~~~~

.. option:: --double-check

     Enable double-checking of all terms using the internal
     typechecker.
     Off by default.

.. option:: --no-double-check

     .. versionadded:: 2.6.2

     Opposite of :option:`--double-check`.  On by default.

.. option:: --guardedness, --no-guardedness

     .. versionadded:: 2.6.0

     Enable [disable] constructor-based guarded corecursion (see
     :ref:`coinduction`).

     The option ``--guardedness`` is inconsistent with sized types,
     thus, it cannot be used with both :option:`--safe` and
     :option:`--sized-types`.

     Default: ``--no-guardedness`` (since 2.6.2).

.. option:: --irrelevant-projections, --no-irrelevant-projections

     .. versionadded:: 2.5.4

     Enable [disable] projection of irrelevant record fields (see
     :ref:`irrelevance`). The option ``--irrelevant-projections``
     makes Agda inconsistent.

     Default (since version 2.6.1): ``--no-irrelevant-projections``.

.. option:: --auto-inline

     .. versionadded:: 2.6.2

     Turn on automatic compile-time inlining. See :ref:`inline-pragma` for more information.

.. option:: --no-auto-inline

     .. versionadded:: 2.5.4

     Disable automatic compile-time inlining (default). Only definitions marked
     ``INLINE`` will be inlined.
     On by default.

.. option:: --no-fast-reduce

     .. versionadded:: 2.6.0

     Disable reduction using the Agda Abstract Machine.

.. option:: --call-by-name

     .. versionadded:: 2.6.2

     Disable call-by-need evaluation in the Agda Abstract Machine.

.. option:: --no-forcing

     .. versionadded:: 2.2.10

     Disable the forcing optimisation. Since Agda 2.6.1 it is a pragma
     option.

.. option:: --no-print-pattern-synonyms

     .. versionadded:: 2.5.4

     Always expand :ref:`pattern-synonyms` during printing. With this
     option enabled you can use pattern synonyms freely, but Agda will
     not use any pattern synonyms when printing goal types or error
     messages, or when generating patterns for case splits.

.. option:: --no-syntactic-equality

     .. versionadded:: 2.6.0

     Disable the syntactic equality shortcut in the conversion
     checker.

.. option:: --syntactic-equality={N}

     .. versionadded:: 2.6.3

     Give the syntactic equality shortcut ``N`` units of fuel (``N``
     must be a natural number).

     If ``N`` is omitted, then the syntactic equality shortcut is
     enabled without any restrictions. (This is the default.)

     If ``N`` is given, then the syntactic equality shortcut is given
     ``N`` units of fuel. The exact meaning of this is
     implementation-dependent, but successful uses of the shortcut do
     not affect the amount of fuel.

     Note that this option is experimental and subject to change.

.. option:: --safe

     .. versionadded:: 2.3.0

     Disable postulates, unsafe :ref:`OPTIONS<options-pragma>` pragmas
     and ``primTrustMe``. Prevents to have both :option:`--sized-types` and
     :option:`--guardedness` on.
     Further reading: :ref:`safe-agda`.

.. option:: --sized-types, --no-sized-types

     .. versionadded:: 2.2.0

     Enable [disable] sized types (see :ref:`sized-types`).

     The option ``--sized-types`` is inconsistent with
     constructor-based guarded corecursion,
     thus, it cannot be used with both :option:`--safe`
     and :option:`--guardedness`.

     Default: ``--no-sized-types`` (since 2.6.2).

.. option:: --type-in-type

     Ignore universe levels (this makes Agda inconsistent; see
     :ref:`type-in-type <type-in-type>`).

.. option:: --omega-in-omega

     .. versionadded:: 2.6.0

     Enable typing rule ``Setω : Setω`` (this makes Agda inconsistent;
     see :ref:`omega-in-omega <omega-in-omega>`).

.. option:: --universe-polymorphism, --no-universe-polymorphism

     .. versionadded:: 2.3.0

     Enable [disable] universe polymorphism (see
     :ref:`universe-levels`).

     Default: ``--universe-polymorphism``.

.. option:: --cumulativity, --no-cumulativity

     .. versionadded:: 2.6.1

     Enable [disable] cumulative subtyping of universes, i.e.,
     if ``A : Set i`` then also ``A : Set j`` for all ``j >= i``.

     Default: ``--no-cumulativity``.

.. option:: --no-import-sorts

     .. versionadded:: 2.6.2

     Disable the implicit statement
     ``open import Agda.Primitive using (Set; Prop)``
     at the start of each top-level Agda module.

.. option:: --no-load-primitives

     .. versionadded:: 2.6.3

     Do not load the primitive modules (``Agda.Primitive``,
     ``Agda.Primitive.Cubical``) when type-checking this program. This is
     useful if you want to declare Agda's very magical primitives in a
     Literate Agda file of your choice.

     If you are using this option, it is your responsibility to ensure
     that all of the ``BUILTIN`` things defined in those modules are
     loaded. Agda will not work otherwise.

     Incompatible with :option:`--safe`.

.. option:: --save-metas, --no-save-metas

     .. versionadded:: 2.6.3

     Save [or do not save] meta-variables in ``.agdai`` files. The
     alternative is to expand the meta-variables to their definitions.
     This option can affect performance. The default is to not save
     the meta-variables.

.. option:: --erasure

     .. versionadded:: 2.6.4

     Allow use of the annotations `@0` and `@erased`; allow use of
     names defined in Cubical Agda in Erased Cubical Agda; and mark
     parameters as erased in the type signatures of constructors and
     record fields (if :option:`--with-K` is not active this is not
     done for indexed data types).

.. option:: --erased-matches

     .. versionadded:: 2.6.4

     Allow matching in erased positions for single-constructor,
     non-indexed data/record types. (This kind of matching is always
     allowed for record types with η-equality.)

     This option is implied by :option:`--with-K` (even implicit use
     of :option:`--with-K` through the absence of options like
     :option:`--without-K`).

.. option:: --erase-record-parameters

     .. versionadded:: 2.6.3

     Mark parameters as erased in record module telescopes.

     This option may only be used if :option:`--erasure` is used.

.. _warnings:

Warnings
~~~~~~~~

The :option:`-W` or :option:`--warning` option can be used to disable
or enable different warnings. The flag ``-W error`` (or
``--warning=error``) can be used to turn all warnings into errors,
while ``-W noerror`` turns this off again.

A group of warnings can be enabled by ``-W {group}``, where ``group``
is one of the following:

.. option:: all

     All of the existing warnings.

.. option:: warn.

     Default warning level.

.. option:: ignore

     Ignore all warnings.

The command ``agda --help=warning`` provides information about which
warnings are turned on by default.

Individual warnings can be turned on and off by ``-W {Name}`` and ``-W
{noName}`` respectively. The flags available are:

.. option:: AbsurdPatternRequiresNoRHS

     RHS given despite an absurd pattern in the LHS.

.. option:: CantGeneralizeOverSorts

     Attempt to generalize over sort metas in 'variable' declaration.

.. option:: CoInfectiveImport

     Importing a file not using e.g. :option:`--safe` from one which
     does.

.. option:: CoverageIssue

     Failed coverage checks.

.. option:: CoverageNoExactSplit

     Failed exact split checks.

.. option:: DeprecationWarning

     Feature deprecation.

.. option:: EmptyAbstract

     Empty ``abstract`` blocks.

.. option:: EmptyInstance

     Empty ``instance`` blocks.

.. option:: EmptyMacro

     Empty ``macro`` blocks.

.. option:: EmptyMutual

     Empty ``mutual`` blocks.

.. option:: EmptyPostulate

     Empty ``postulate`` blocks.

.. option:: EmptyPrimitive

     Empty ``primitive`` blocks.

.. option:: EmptyPrivate

     Empty ``private`` blocks.

.. option:: EmptyRewritePragma

     Empty ``REWRITE`` pragmas.

.. option:: IllformedAsClause

     Illformed ``as``-clauses in ``import`` statements.

.. option:: InfectiveImport

     Importing a file using e.g. :option:`--cubical` into one which
     doesn't.

.. option:: InstanceNoOutputTypeName

     Instance arguments whose type does not end in a named or variable
     type are never considered by instance search.

.. option:: InstanceArgWithExplicitArg

   Instance arguments with explicit arguments are never considered by
   instance search.

.. option:: InstanceWithExplicitArg

     Instance declarations with explicit arguments are never
     considered by instance search.

.. option:: InvalidCatchallPragma

     :ref:`CATCHALL<catchall-pragma>` pragmas before a non-function clause.

.. option:: InvalidNoPositivityCheckPragma

     No positivity checking pragmas before non-``data``, ``record`` or
     ``mutual`` blocks.

.. option:: InvalidTerminationCheckPragma

     Termination checking pragmas before non-function or ``mutual``
     blocks.

.. option:: InversionDepthReached

     Inversions of pattern-matching failed due to exhausted inversion
     depth.

.. option:: LibUnknownField

     Unknown field in library file.

.. option:: MissingDefinitions

     Names declared without an accompanying definition.

.. option:: ModuleDoesntExport

     Names mentioned in an import statement which are not exported by
     the module in question.

.. option:: NotAllowedInMutual

     Declarations not allowed in a mutual block.

.. option:: NotStrictlyPositive

     Failed strict positivity checks.

.. option:: OldBuiltin

     Deprecated :ref:`BUILTIN<built-ins>` pragmas.

.. option:: OverlappingTokensWarning

     Multi-line comments spanning one or more literate text blocks.

.. option:: PolarityPragmasButNotPostulates

     Polarity pragmas for non-postulates.

.. option:: PragmaCompiled

     :ref:`COMPILE<foreign-function-interface>` pragmas not allowed in safe mode.

.. option:: PragmaCompileErased

     :ref:`COMPILE<foreign-function-interface>` pragma targeting an erased symbol.

.. option:: PragmaNoTerminationCheck

     :ref:`NO_TERMINATION_CHECK<terminating-pragma>` pragmas are deprecated.

.. option:: RewriteMaybeNonConfluent

     Failed confluence checks while computing overlap.

.. option:: RewriteNonConfluent

     Failed confluence checks while joining critical pairs.

.. option:: SafeFlagNonTerminating

     :ref:`NON_TERMINATING<non_terminating-pragma>` pragmas with the safe flag.

.. option:: SafeFlagNoPositivityCheck

     :ref:`NO_POSITIVITY_CHECK<no_positivity_check-pragma>` pragmas with the safe flag.

.. option:: SafeFlagNoUniverseCheck

     :ref:`NO_UNIVERSE_CHECK<no_universe_check-pragma>` pragmas with the safe flag.

.. option:: SafeFlagPolarity

     :ref:`POLARITY<polarity-pragma>` pragmas with the safe flag.

.. option:: SafeFlagPostulate

     ``postulate`` blocks with the safe flag

.. option:: SafeFlagPragma

     Unsafe :ref:`OPTIONS<options-pragma>` pragmas with the safe flag.

.. option:: SafeFlagTerminating

     :ref:`TERMINATING<terminating-pragma>` pragmas with the safe flag.

.. option:: SafeFlagWithoutKFlagPrimEraseEquality

     ``primEraseEquality`` used with the safe and without-K flags.

.. option:: ShadowingInTelescope

     Repeated variable name in telescope.

.. option:: TerminationIssue

     Failed termination checks.

.. option:: UnknownFixityInMixfixDecl

     Mixfix names without an associated fixity declaration.

.. option:: UnknownNamesInFixityDecl

     Names not declared in the same scope as their syntax or fixity
     declaration.

.. option:: UnknownNamesInPolarityPragmas

     Names not declared in the same scope as their polarity pragmas.

.. option:: UnreachableClauses

     Unreachable function clauses.

.. option:: UnsolvedConstraints

     Unsolved constraints.

.. option:: UnsolvedInteractionMetas

     Unsolved interaction meta variables.

.. option:: UnsolvedMetaVariables

     Unsolved meta variables.

.. option:: UselessAbstract

     ``abstract`` blocks where they have no effect.

.. option:: UselessInline

     :ref:`INLINE<inline-pragma>` pragmas where they have no effect.

.. option:: UselessInstance

     ``instance`` blocks where they have no effect.

.. option:: UselessPrivate

     ``private`` blocks where they have no effect.

.. option:: UselessPublic

     ``public`` blocks where they have no effect.

.. option:: WithoutKFlagPrimEraseEquality

     ``primEraseEquality`` used with the without-K flags.

.. option:: WrongInstanceDeclaration

     Terms marked as eligible for instance search should end with a
     name.

Examples
--------

Run Agda with all warnings
enabled, except for warnings about empty ``abstract`` blocks:

.. code-block:: console

   agda -W all --warning=noEmptyAbstract file.agda

Run Agda on a file which uses the standard library.
Note that you must have already created a ``libraries`` file
as described in :ref:`package-system`.

.. code-block:: console

   agda -l standard-library -i. file.agda

(Or if you have added ``standard-library`` to your ``defaults`` file, simply ``agda file.agda``.)

.. _consistency-checking-options:

Consistency checking of options used
------------------------------------

Agda checks that options used in imported modules are consistent with
each other.

An *infective* option is an option that if used in one module, must be
used in all modules that depend on this module. The following options
are infective:

* :option:`--prop`
* :option:`--rewriting`
* :option:`--guarded`
* :option:`--two-level`
* :option:`--cumulativity`
* :option:`--cohesion`
* :option:`--flat-split`
* :option:`--erasure`
* :option:`--erased-matches`

Furthermore :option:`--cubical` and :option:`--erased-cubical` are
*jointly infective*: if one of them is used in one module, then one or
the other must be used in all modules that depend on this module.

A *coinfective* option is an option that if used in one module, must
be used in all modules that this module depends on. The following
options are coinfective:

* :option:`--safe`
* :option:`--without-K`
* :option:`--no-universe-polymorphism`
* :option:`--no-sized-types`
* :option:`--no-guardedness`

Furthermore the option :option:`--cubical-compatible` is mostly
coinfective. If a module uses :option:`--cubical-compatible` then all
modules that this module imports (directly) must also use
:option:`--cubical-compatible`, with the following exception: if a
module uses both :option:`--cubical-compatible` and
:option:`--with-K`, then it is not required to use
:option:`--cubical-compatible` in (directly) imported modules that use
:option:`--with-K`. (Note that one cannot use
:option:`--cubical-compatible` and :option:`--with-K` at the same time
if :option:`--safe` is used.)

Agda records the options used when generating an interface file. If
any of the following options differ when trying to load the interface
again, the source file is re-typechecked instead:

* :option:`--allow-exec`
* :option:`--allow-incomplete-matches`
* :option:`--allow-unsolved-metas`
* :option:`--call-by-name`
* :option:`--cohesion`
* :option:`--confluence-check`
* :option:`--copatterns`
* :option:`--cubical-compatible`
* :option:`--cubical`
* :option:`--cumulativity`
* :option:`--double-check`
* :option:`--erase-record-parameters`
* :option:`--erased-cubical`
* :option:`--erased-matches`
* :option:`--erasure`
* :option:`--exact-split`
* :option:`--experimental-irrelevance`
* :option:`--flat-split`
* :option:`--guarded`
* :option:`--injective-type-constructors`
* :option:`--instance-search-depth`
* :option:`--inversion-max-depth`
* :option:`--irrelevant-projections`
* ``--keep-covering-clauses``
* :option:`--local-confluence-check`
* ``--lossy-unification``
* :option:`--no-auto-inline`
* :option:`--no-eta-equality`
* :option:`--no-fast-reduce`
* :option:`--no-forcing`
* :option:`--no-guardedness`
* :option:`--no-import-sorts`
* :option:`--no-load-primitives`
* :option:`--no-pattern-matching`
* :option:`--no-positivity-check`
* :option:`--no-projection-like`
* :option:`--no-sized-types`
* :option:`--no-termination-check`
* :option:`--no-unicode`
* :option:`--no-universe-polymorphism`
* :option:`--omega-in-omega`
* :option:`--overlapping-instances`
* :option:`--prop`
* :option:`--qualified-instances`
* :option:`--rewriting`
* :option:`--safe`
* :option:`--save-metas`
* :option:`--syntactic-equality`
* :option:`--termination-depth`
* :option:`--two-level`
* :option:`--type-in-type`
* :option:`--warning`
* :option:`--without-K`


.. _Vim: https://www.vim.org/
.. _Dot: http://www.graphviz.org/content/dot-language
