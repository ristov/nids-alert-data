NIDS Alert Group Data Set
=========================


Introduction
------------
This repository hosts the NIDS Alert Group Data Set (NIDSAGDS) that is stored in the file dataset-labeled-anon-ip.csv.bz2.

The data set covers 60 days (January 2022 -- March 2022) and was produced with the customized version of the SCAS algorithm (https://github.com/ristov/nids-alert-proc). The data set was collected on the external network perimeter of a large institution and contains over 1.3 million data points. Each data point represents a group of one or more network IDS alerts generated for the same external IP address and for the same signature in a short time frame (the maximum size of the time frame is 5 minutes).

The data set has been used for machine learning experiments with the tools from the https://github.com/ristov/nids-alert-proc repository, and is shared for facilitating similar research in the field of network IDS alert classification.

Since each data point was generated by the customized version of SCAS which is a stream clustering algorithm, data points have labels that indicate whether SCAS regarded the data point as an inlier or outlier. In addition, data points have labels assigned by a human that indicate if the data point represents an important or irrelevant alert group. Irrelevant alert groups correspond to either threats of low importance (such as frequent scanning for old vulnerabilities) or false positives (such as alerts about attempts to resolve botnet C&C server DNS names which are not originating from infected computers but specific security applications).


Data set fields
---------------
Each data point has 47 fields and their description is given below:

Timestamp -- alert group reporting time

SignatureText -- human readable alert text

SignatureID -- numerical signature ID

SignatureMatchesPerDay -- average number of matches per day by the signature that produced the current alert group (set to 0 if the signature has produced its first match less than 24 hours ago)

AlertCount -- the number of alerts in the current alert group

Proto -- numerical protocol ID (e.g., 6 denotes TCP and 17 UDP)

ExtIP -- anonymized IP address of the external host (extipN, where N is a number that identifies the given IP address)

ExtPort -- port at the external host, set to -1 if alerts involved multiple external ports

IntIP -- anonymized IP address of the internal host (intipN, where N is a number that identifies the given IP address), set to -1 if alerts involved multiple internal IP addresses

IntPort -- port at the internal host, set to -1 if alerts involved multiple internal ports

Similarity -- overall similarity with other alert groups from the same cluster (or with other outlier alert groups if the current alert group is an outlier), ranges from 0 to 1 (values close to 1 denote a high degree of similarity)

Label -- ground-truth label assigned by a human (0 denotes irrelevant and 1 important)

SCAS -- label assigned by the customized version of SCAS (0 denotes inlier and 1 outlier)

AttrSimilarity -- similarity for the network IDS alert attribute Attr (there are 34 attributes in total). Set to -1 if the attribute Attr is not set for the given signature, otherwise ranges from 0 to 1. The field indicates how often has the attribute value been observed in other alert groups from the same cluster (or in other outlier alert groups if the current alert group is an outlier) 

In order to use the ExtIP and IntIP fields during the experiments, the string tags extipN and intipN need to be replaced with IP addresses A.B.C.D of your preference.
Note that for the field value, the integer representation of the IP address has to be used: A * 256^3 + B * 256^2 + C * 256 + D.
For example, to map the string tags extipN to the 10.0.0.0/8 network, so that extip1 -> 10.0.0.1, extip2 -> 10.0.0.2, etc., you can use the following simple scheme: extipN -> 10 * 256^3 + N.


Academic attribution
--------------------
The creation of the NIDS Alert Group Data Set has been described in the following paper:

Risto Vaarandi and Alejandro Guerra-Manzanares, "Stream clustering guided supervised learning for classifying NIDS alerts," Future Generation Computer Systems, 2024, https://doi.org/10.1016/j.future.2024.01.032

Also, the following paper describes the experiments with the data set for active learning based NIDS alert classification:

Risto Vaarandi and Alejandro Guerra-Manzanares, "Network IDS alert classification with active learning techniques," Journal of Information Security and Applications, 2024, https://doi.org/10.1016/j.jisa.2023.103687

When you publish research results that have involved the use of the data set, please provide a reference to one of the above papers in your publication.


Licensing
---------
NIDS Alert Group Data Set, Copyright (C) 2022 Risto Vaarandi

NIDS Alert Group Data Set is licensed under a Creative Commons Attribution 4.0 International License.

You should have received a copy of the license along with this work. If not, see https://creativecommons.org/licenses/by/4.0/.


Author
------
Risto Vaarandi (firstname d0t lastname at gmail d0t c0m)
