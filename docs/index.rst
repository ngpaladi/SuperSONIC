
.. toctree::
    :maxdepth: 3
    :hidden:
    
    Home <self>
    Installation
    Parameters


SuperSONIC
========================================

The SuperSONIC project implements **common server infrastructure for GPU inference-as-a-service**
to accelerate machine learining algorithms at large high energy physics (HEP) and multimissenger astrophysics
(MMA) experiments. The server infrastructure is designed for deployment at
`Kubernetes <kubernetes.io>`_ clusters equipped with GPUs.

SuperSONIC Helm chart
~~~~~~~~~~~~~~~~~~~~~~~~

The `SuperSONIC Helm chart <https://github.com/fastmachinelearning/SuperSONIC/tree/master/helm>`_ will install
components depicted at the diagram below, excluding Prometheus and model repository,
which must be connected by specifying relevant parameters in configuration file
(see :doc:`configuration reference <Parameters>`).

In its current form, the chart allows to deploy multiple server
instances with different settings at once. This can be useful if you
need to host servers with different GPU models, different Triton server
versions, or different model repository mounts.

For correct behavior, the server saturation metric
(``servers[].prometheus.serverAvailabilityMetric``) used by Envoy proxy
and autoscaler must be carefully defined. It is recommended to start
with examining the metric in Prometheus interface, in order to define an
appropriate threshold and avoid typos in the metric definition.

The KEDA autoscaler can be enabled / disabled via the
``servers[].autoscaler.enabled`` parameter.

.. figure:: img/diagram.svg
   :alt: SONIC Server Infrastructure



