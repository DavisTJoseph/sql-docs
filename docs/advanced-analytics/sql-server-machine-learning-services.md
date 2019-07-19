---
title: R and Python machine learning documentation
description: R and Python in SQL Server, with built-in data science modeling and machine learning algorithms for enterprise data analysis at scale.
ms.prod: sql
ms.technology: machine-learning

ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## SQL Server Machine Learning Services (R and Python) Documentation

Learn how to use R and Python external libraries and languages on resident, relational data with our quickstarts, tutorials, and how-to articles. R and Python libraries in [SQL Server Machine Learning Services](what-is-sql-server-machine-learning.md) include base distributions, data science models, machine learning algorithms, and functions for conducting high-performance analytics at scale, without having to transfer data across the network.

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> For the documentation on Java, see the [SQL Server Language Extensions documentation](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
::: moniker-end

|   |   |
|---|:--|
| ![R logo](media/index/logo_r.png) | Open-source R, extended with [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) and Microsoft AI algorithms in [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). These libraries give you forecasting and prediction models, statistical analysis, visualization, and data manipulation at scale.<br/>R integration starts in [SQL Server 2016](install/sql-r-services-windows-install.md) and is also in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Python logo](media/index/logo_python.png) | Python developers can use Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) and [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) libraries for predictive analytics and machine learning at scale. Anaconda and Python 3.5-compatible libraries are the baseline distribution.<br/>Python integration starts in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |

## 5-Minute Quickstarts

- [Create a predictive model in R](tutorials/rtsql-create-a-predictive-model-r.md)

- [Predict and plot from model using R](tutorials/rtsql-predict-and-plot-from-model.md)

## Step-by-Step Tutorials

- [How to install Machine Learning Services to SQL Server](install/sql-machine-learning-services-windows-install.md)

- [How to execute R from T-SQL and stored procedures](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [How to use embedded analytics in Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

## Video Introduction

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## Reference

| Package | Language | Description |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | Distributed and parallel processing for R tasks: data transformation, exploration, visualization, statistical and predictive analytics. |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | Functions based on Microsoft's AI algorithms, adapted for R. |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | Imports data from OLAP cube.s |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | Helper functions for encapsulating R and T-SQL. |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Distributed and parallel processing for Python tasks: data transformation, exploration, visualization, statistical and predictive analytics. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | Functions based on Microsoft's AI algorithms, adapted for Python. |
| &nbsp; | &nbsp; | &nbsp; |
