

.. _logging:

==============
Journalisation
==============

PHPUnit peut produire plusieurs types de fichiers de logs.

.. _logging.xml:

Résultats de test (XML)
#######################

Le fichier de log XML pour les tests produits par PHPUnit est basé sur celui
qui est utilisé par la tâche `JUnit
de Apache Ant <http://ant.apache.org/manual/Tasks/junit.html>`_. L'exemple suivant montre que le fichier
de log XML généré pour les tests dans ``TestTableau`` :

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <testsuites>
      <testsuite name="ArrayTest"
                 file="/home/sb/ArrayTest.php"
                 tests="2"
                 assertions="2"
                 failures="0"
                 errors="0"
                 time="0.016030">
        <testcase name="testNewArrayIsEmpty"
                  class="ArrayTest"
                  file="/home/sb/ArrayTest.php"
                  line="6"
                  assertions="1"
                  time="0.008044"/>
        <testcase name="testArrayContainsAnElement"
                  class="ArrayTest"
                  file="/home/sb/ArrayTest.php"
                  line="15"
                  assertions="1"
                  time="0.007986"/>
      </testsuite>
    </testsuites>

Le fichier de log XML suivant a été généré pour deux tests,
``testFailure`` et ``testError``,
à partir d'une classe de cas de test nommée ``FailureErrorTest`` et
montre comment les échecs et les erreurs sont signalés.

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <testsuites>
      <testsuite name="FailureErrorTest"
                 file="/home/sb/FailureErrorTest.php"
                 tests="2"
                 assertions="1"
                 failures="1"
                 errors="1"
                 time="0.019744">
        <testcase name="testFailure"
                  class="FailureErrorTest"
                  file="/home/sb/FailureErrorTest.php"
                  line="6"
                  assertions="1"
                  time="0.011456">
          <failure type="PHPUnit\Framework\ExpectationFailedException">
    testFailure(FailureErrorTest)
    Failed asserting that &lt;integer:2&gt; matches expected value &lt;integer:1&gt;.

    /home/sb/FailureErrorTest.php:8
    </failure>
        </testcase>
        <testcase name="testError"
                  class="FailureErrorTest"
                  file="/home/sb/FailureErrorTest.php"
                  line="11"
                  assertions="0"
                  time="0.008288">
          <error type="Exception">testError(FailureErrorTest)
    Exception:

    /home/sb/FailureErrorTest.php:13
    </error>
        </testcase>
      </testsuite>
    </testsuites>

.. _logging.codecoverage.xml:

Couverture de code (XML)
########################

Le format XML pour journaliser les informations de couverture de code produite par PHPUnit
est faiblement basé sur celui utilisé par `Clover <http://www.atlassian.com/software/clover/>`_. L'exemple suivant montre le fichier de log XML
généré pour les tests dans ``BankAccountTest``:

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <coverage generated="1184835473" phpunit="3.6.0">
      <project name="BankAccountTest" timestamp="1184835473">
        <file name="/home/sb/BankAccount.php">
          <class name="BankAccountException">
            <metrics methods="0" coveredmethods="0" statements="0"
                     coveredstatements="0" elements="0" coveredelements="0"/>
          </class>
          <class name="BankAccount">
            <metrics methods="4" coveredmethods="4" statements="13"
                     coveredstatements="5" elements="17" coveredelements="9"/>
          </class>
          <line num="77" type="method" count="3"/>
          <line num="79" type="stmt" count="3"/>
          <line num="89" type="method" count="2"/>
          <line num="91" type="stmt" count="2"/>
          <line num="92" type="stmt" count="0"/>
          <line num="93" type="stmt" count="0"/>
          <line num="94" type="stmt" count="2"/>
          <line num="96" type="stmt" count="0"/>
          <line num="105" type="method" count="1"/>
          <line num="107" type="stmt" count="1"/>
          <line num="109" type="stmt" count="0"/>
          <line num="119" type="method" count="1"/>
          <line num="121" type="stmt" count="1"/>
          <line num="123" type="stmt" count="0"/>
          <metrics loc="126" ncloc="37" classes="2" methods="4" coveredmethods="4"
                   statements="13" coveredstatements="5" elements="17"
                   coveredelements="9"/>
        </file>
        <metrics files="1" loc="126" ncloc="37" classes="2" methods="4"
                 coveredmethods="4" statements="13" coveredstatements="5"
                 elements="17" coveredelements="9"/>
      </project>
    </coverage>

.. _logging.codecoverage.text:

Couverture de code (TEXTE)
##########################

Un affichage de la couverture de code lisible pour la ligne de commandes ou un fichier texte.
Le but de ce format de sortie est de fournir un aperçu rapide de couverture
en travaillant sur un petit ensemble de classes. Pour des projets plus grand
cette sortie peut être utile pour obtenir un aperçu rapide de la couverture
des projets ou quand il est utilisé avec la fonctionnalité ``--filter``.
Quand c'est utilisé à partir de la ligne de commande en écrivant sur ``php://stdout``,
cela prend en compte le réglage ``--colors``.
Ecrire sur la sortie standard est l'option par défaut quand on utilise la ligne de commandes.
Par défaut, ceci ne montrera que les fichiers qui ont au moins une ligne couverte.
Ceci peut uniquement être modifié via l'option de configuration xml ``showUncoveredFiles``
Voir :ref:`appendixes.configuration.logging`.
Par défaut, tous les fichiers et leur status de couverture sont affichés dans le rapport détaillé.
Ceci peut être changé via l'option de configuration xml
``showOnlySummary``.


