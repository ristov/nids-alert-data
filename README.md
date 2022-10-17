NIDS Alert Group Data Set
=========================


Introduction
------------
This repository contains a NIDS alert group data set that covers 60 days (January 2022 -- March 2022) and was produced with the customized version of the SCAS algorithm (https://github.com/ristov/nids-alert-proc). The data set was collected on the external network perimeter of a large institution and contains over 1.3 million data points. Each point represents a group of one or more network IDS alerts generated for the same external IP address and for the same signature in a short time frame (the time frame does not exceed 5 minutes).

The data set has been used for machine learning experiments with the tools from the https://github.com/ristov/nids-alert-proc repository, and is shared for facilitating similar research in the field of network IDS alert classification.

Since each data point was generated by the customized version of SCAS which is a stream clustering algorithm, data points have labels that indicate whether SCAS regarded the data point as an inlier or outlier. In addition, data points have labels assigned by a human that indicate if the data point represents an important or irrelevant alert group. Irrelevant alert groups correspond to either threats of low importance (such as scanning for old vulnerabilities) or false positives (such as alerts about attempts to resolve botnet C&C server DNS names which are actually generated by specific security applications).


Data set fields
---------------
Each data point has the following fields:

Timestamp -- alert group reporting time (seconds since Epoch)

SignatureText -- human readable alert text

SignatureID -- numerical signature ID

SignatureMatchesPerDay -- average number of matches per day by the signature

AlertCount -- the number of alerts in the current group

Proto -- numerical protocol ID (e.g., 6 denotes TCP and 17 UDP)

ExtIP -- anonymized external IP address (extipN, where N is a number that identifies the given IP address)

ExtPort -- port at the external host, set to -1 if alerts involved multiple external ports

IntIP -- anonymized internal IP address (intipN, where N is a number that identifies the given IP address), set to -1 if alerts involved multiple internal IP addresses

IntPort -- port at the internal host, set to -1 if alerts involved multiple internal ports

Similarity -- overall similarity with other alert groups from the same cluster (or with other outlier alert groups if the current alert group is an outlier)

Label -- label assigned by a human (0 denotes irrelevant and 1 important)

SCAS -- label assigned by SCAS (0 denotes inlier and 1 outlier)

AttrSimilarity -- similarity for the attribute Attr, set to -1 if the attribute Attr is not set for the given signature. The field indicates how often has the attribute value been observed in other alert groups from the same cluster (or in other outlier alert groups if the current alert group is an outlier) 


Author
------
Risto Vaarandi (ristov at users d0t s0urcef0rge d0t net)
