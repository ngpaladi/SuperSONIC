-------------------
Getting Started
-------------------

Pre-requisites
~~~~~~~~~~~~~~~

   1. `Kubernetes <https://kubernetes.io>`_ cluster
   2. `Helm <https://helm.sh>`_
   3. Access to an existing `Prometheus <https://prometheus.io>`_ instance in the cluster, or sufficient permissions to deploy a custom instance (preferred).
   4. If using autoscaling, you may need to ask cluster administrators to install CustomResourceDefinitions for `KEDA <https://keda.sh>`_.

Installation
~~~~~~~~~~~~~~

   1. Create a values file with your configuration.

      - `Configuration guide <configuration-guide>`_
      - `Configuration reference <configuration-reference>`_
      - `Example values.yaml files <https://github.com/fastmachinelearning/SuperSONIC/tree/main/values>`_

   2. Install Helm plugin to handle SuperSONIC installation

      .. code:: shell

         helm plugin install https://github.com/fastmachinelearning/SuperSONIC/


      The Helm plugin is needed to ensure internal connectivity of the SuperSONIC
      components. Standard Helm installation without a plugin is also supported,
      but requires a lot more manual configuration.

   3. Modify the following command to install the chart at your cluster:

      .. code:: shell

         helm install-supersonic <release-name> -n <namespace> -f <your-values.yaml>

      Installer plugin usage:

      .. code:: shell

         Usage:
           helm install-supersonic [RELEASE_NAME] [flags]

         Flags:
         -h, --help              Show this help message
         -f, --values            Specify values file for custom configuration
         -n, --namespace         Specify Kubernetes namespace for deployment
         --version               Specify chart version (default: latest version)
                                 Note: Ignored if --local flag is set
         --local                 Install from local chart path instead of remote repository
         --path                  Local chart path (default: ./helm/supersonic)
                                 Only used when --local flag is set
         Additional flags will be passed directly to the 'helm install' command


      Use a unique meaningful lowercase value as <release-name>, for example
      ``supersonic-cms-run3``.
      This value will be used as a prefix for all resources created by the chart,
      unless ``nameOverride`` is specified in the values file.

      Successfully executed ``helm install`` command will print a link to auto-generated Grafana dashboard
      and other useful information.
   
   .. figure:: img/grafana.png
      :align: center
      :height: 250
      :alt: Supersonic Grafana dashboard

Uninstall SuperSONIC
~~~~~~~~~~~~~~~~~~~~~~~~~~

   .. code:: shell

      helm uninstall <release-name> -n <namespace>

Architecture
~~~~~~~~~~~~~~~

The SuperSONIC Helm chart will install
components depicted at the diagram below, excluding the model repository,
which must be connected by specifying relevant parameters in configuration file
(see :doc:`configuration guide <configuration-guide>`).

.. raw:: html

   <picture>
     <source srcset="img/diagram-dark.svg" media="(prefers-color-scheme: dark)">
     <source srcset="img/diagram.svg" media="(prefers-color-scheme: light)">
     <img src="img/diagram.svg" alt="SONIC Server Infrastructure">
   </picture>