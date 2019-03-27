# Sensitivity Analysis

This repository is a companion page for the paper:

_“A Sensitivity Analysis for an Architectural Debt Index based on Architectural Smells”_. Antonela Tommasel, J. Andres Diaz-Pace, Ilaria Pigazzini, and Francesca Arcelli Fontana. (2019)


## Abstract

Architectural debt indexes are a common metric-based approach for assessing the quality of a software system, which focuses on (and tries to quantify) design degradation symptoms. To be of practical usage, an architectural debt index is expected to guide engineers in identifying design issues, such as smells, that might negatively affect system evolution. In this context, a decomposition approach of a particular debt index, called ADI, is proposed. The ADI computation is based on scoring features (e.g., severity and dependencies) related to the architectural smells of the system. On this basis, we perform a sensitivity analysis of the ADI features in order to determine the most influential elements causing ADI variations over system versions. By means of these decomposition and sensitivity analysis techniques, we can prioritize key architectural smells that, due to their variations or instability, should be brought to the engineers’ attention. An initial evaluation with a range of versions for three open-source systems has shown correlations between smells detected with our approach and maintenance/development issues reported for the systems.

## Replication material

This repository contains the datasets for the 3 analyzed systems, namely:
 - Apache Camel
 - Apache CxF
 - Hibernate

### Files

For each system, the following artefacts are provided:

1. **Smells and ADI features computed by Arcan for the different system versions**
   - _ArchitecturalDebtEstimation_smell_evolution__<system -version-span>_ (CSV file): It tracks the behavior of smells across system versions in terms of the four features on which the ADI score is based on (SeverityScore, PageRank, TotNumOfSetOfElements and NumSetOfElement). Each row of the file represents a smell and a feature (thus, a smell is described in four rows), and each column represents a system version.
  
2. **Results of both the Morris and Sobol sensitivity methods for key smells**
   - _parameters file_:  each variable (smell) and its range of value
   - _parameterValues file_: the values sampled by the sensitivity method for the parameters
   - _objectiveValues file_: the global ADI computed out of the parameter values
   - _morrisIndices file_: the Morris indices for the parameter and objective values
   - _sobolIndices file_: the Sobol indices for the parameter and objective values
   - _morrisSmellRanking_: the ranking of key smells resulting from the Morris indices
   - _sobolSmellRanking_: the ranking of key smells resulting from the Sobol indices


3. **Top-level packages for the different system versions**
   - _TXT file: it contains all system packages for all the analyzed versions. Only the last version was used in the experiments.

4. **Results of both the Morris and Sobol sensitivity methods for key packages**
   - _parameters file_:  each variable (smell) and its range of value
   - _parameterValues file_: the values sampled by the sensitivity method for the parameters
   - _objectiveValues file_: the global ADI computed out of the parameter values
   - _morrisIndices file_: the Morris indices for the parameter and objective values
   - _sobolIndices file_: the Sobol indices for the parameter and objective values
   - _morrisPackageRanking_: the ranking of key packages resulting from the Morris indices
   - _sobolPackageRanking_: the ranking of key packages resulting from the Sobol indices

5. **Analysis of issues for the different versions** 
The corresponding files are organized into folders named <project_name>_jira_issues that contains the csv files downloaded from the Jira platform. A single csv file contains the issues of a specific package of the analyzed project. Each file reports for each Jira issue the following information:
   - _Issue Type
   - _Patch available: a custom field indicating whether there is an available patch for the project
   - _Issue Key: issue name
   - _Issue id: issue identifier
   - _Parent id: the id of the eventual parent issue
   - _Summary: a brief description of the issues
   - _Assignee
   - _Reporter
   - _Priority
   - _Status: the current status of the issue
   - _Resolution
   - _Created: date of creation of the issue on the platform
   - _Updated: date of last update of the issue
   - _Due date: eventual issue expiring date

The files named smell_severity_issues*: contains the counts of the Jira issues used to assess whether key smells are related to actual design problems.
   - _smell_severity_issues_total_: contains the issue count for every type of AS and for every analyzed project. The columns of the file report the identifier of the AS, the rows report namely:
   - _Issues_: the number of issues
   - _median<project_name>_: the median value of issues for each analyzed project
   - _cover<project_name>_: the percentage of key AS related to design problems for each analyzed project.
   - _smell_severity_issues_cd_<project_name>: contains the issue count for the Cyclic Dependency smell, used to compute the mean of the number of issues for each smell instance. There is one file per analyzed project. Each file contains the issue count for each instance of CD. The columns report the name of the package involved, the rows indicate namely:
   - _Issues_: the number of issues
   - _Blocker, Critical, Major, Minor,Trivial_: the number of issues of a specific priority level
   - _mean_issues_: the mean number of issues of the CD instance
   - _median_issues_: the median number of issues of the CD instance

The file containing Camel results has more rows, since a detailed analysis was conducted on specific instances of this project, namely:
   - _in_other_smell_: the number of AS instances in which the package appears other than CD
   - _mean_blocker/critical/major/minor/trivial_: the mean number of issues of  a specific
   - _granularity level_

The files are organized according to the 3 projects analyzed in the study. A short description of smells found in each version is included. 


### System Versions used

_Apache Camel_
- apache-camel-2.2.0 	CD=48   	UD=10    	HL=3
- apache-camel-2.3.0 	CD=49   	UD=10    	HL=3
- apache-camel-2.4.0	CD=49   	UD=10    	HL=3
- apache-camel-2.5.0 	CD=49   	UD=10    	HL=3
- apache-camel-2.6.0 	CD=49   	UD=10    	HL=3
- apache-camel-2.7.0 	CD=26   	UD=6    	HL=3
- apache-camel-2.8.0 	CD=78   	UD=11  	HL=3
- apache-camel-2.9.0 	CD=90   	UD=11   	HL=3
- apache-camel-2.10.0 	CD=92   	UD=11    	HL=3
- apache-camel-2.11.0 	CD=97   	UD=11   	HL=3
- apache-camel-2.12.0 	CD=97   	UD=11    	HL=3
- apache-camel-2.13.0 	CD=98   	UD=11    	HL=3
- apache-camel-2.14.0 	CD=98   	UD=11    	HL=3
- apache-camel-2.15.0 	CD=98  	 UD=11   	HL=3

_Apache Cxf_
- apache-cxf-2.0.6 	CD=110   	UD=52    	HL=4
- apache-cxf-2.1.1 	CD=132   	UD=61    	HL=4
- apache-cxf-2.2.1 	CD=150   	UD=74    	HL=3
- apache-cxf-2.3.0 	CD=197   	UD=79    	HL=3
- apache-cxf-2.4.0 	CD=199   	UD=86    	HL=4
- apache-cxf-2.5.0 	CD=206   	UD=88   	HL=3
- apache-cxf-2.6.0 	CD=146   	UD=92    	HL=3
- apache-cxf-2.7.0 	CD=196   	UD=95    	HL=3

_Hibernate_
- hibernate-core-4.0.0.Final 	CD=153   	UD=30    	HL=5
- hibernate-core-4.1.0.Final 	CD=163   	UD=33    	HL=5
- hibernate-core-4.2.0.Final 	CD=171   	UD=32    	HL=6
- hibernate-core-4.3.0.Final 	CD=230   	UD=62    	HL=6


## Tools
The Arcan tool used for detecting the architectural smells is available here: http://essere.disco.unimib.it/wiki/arcan

- The SALib library (Python) for running the sensitivity analysis on input parameters (i.e., smells or packages) is available here: https://github.com/SALib/SALib 

These are quick tutorials on how to run SALib to process the sensitivity files above:
- For Morris https://waterprogramming.wordpress.com/2013/09/23/method-of-morris-elementary-effects-using-salib/
- For Sobol https://waterprogramming.wordpress.com/2013/08/05/running-sobol-sensitivity-analysis-using-salib/

The objective values (or model values) for the sensitivity analysis are obtained with the ADI formula: 

![ADI Formula](https://github.com/tommantonela/ecsa-2019/blob/gh-pages/adi-formula.png)

## Contact information

- _Antonela Tommasel_ (ISISTAN, CONICET-UNICEN. Argentina) antonela.tommasel@isistan.unicen.edu.ar 
- _J. Andres Diaz-Pace_ (ISISTAN, CONICET-UNICEN. Argentina) andres.diazpace@isistan.unicen.edu.ar 
- _Ilaria Pigazzini_ (Department of Informatics, Systems and Communication, Universita` of Milano-Bicocca, Italy) i.pigazzini@campus.unimib.it 
- _Francesca Arcelli Fontana_ (Department of Informatics, Systems and Communication, Universita` of Milano-Bicocca, Italy) arcelli@disco.unimib.it 
