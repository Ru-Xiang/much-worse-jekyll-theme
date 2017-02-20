---
layout: page
permalink: /libble-spark/
---

## LIBBLE-Spark

### [Introduction](#introduction)

LIBBLE-Spark is part of the Project LIBBLE. The current version of LIBBLE-Spark includes the following machine learning algorithms:

> * Classification
>   * Logistic Regression (LR)
>   * Logistic Regression with L1-norm Regularization
>   * Support Vector Machine (SVM)
> * Regression
>   * Linear Regression
>   * Lasso
> * Collaborative Filtering
>   * Matrix Factorization
> * Dimensionality Reduction
>   * Principal Component Analysis (PCA)
>   * Singular Value Decomposition (SVD)
> * Clustering
>   * K-Means

### [Tutorial](#tutorial)

* #### Import LIBBLE

  * For maven

    Add repository:

    ~~~xml
    <repository>
        <id>libble-spark</id>
        <url>
            https://libble.github.io/mvn-repo/
        </url>
    </repository>
    ~~~

    Add dependency:

    ~~~xml
    <dependency>
        <groupId>libble</groupId>
        <artifactId>libble-spark_${scala.binary}</artifactId>
        <version>${libble.spark.version}</version>
    </dependency>
    ~~~

  * For sbt:

    Add follows into the build.sbt:

    ~~~javascript
    libraryDependencies +="libble"%%"libble-spark"%"1.0.1-SNAPSHOT"
    resolvers ++= Seq(
    "libble Releases" at "https://libble.github.io/mvn-repo/"
    )
    ~~~

* #### Load and Save Data

  LIBBLE-Spark supports two formats of input data: LIBSVM input format for sparse features; If the features are dense, each line is an instance, with the label and features separated by a space. The function for loading data is loadLIBBLEFile.

  ~~~scala
  val conf = new SparkConf()
  val sc = new SparkContext(conf)
  import libble.context.LibContext.sc2LibContext
  val training=sc.loadLIBBLEFile("sparse.data")
  ~~~

  We use the method saveAsLIBBLEFile to save Data to the File System:

  ~~~scala
  import libble.context.LibContext.RDD2LIBBLERDD
  training.saveAsLIBBLEFile("this.data")
  ~~~

* #### Classification and Regression

  Here, we give an example of using Logistic Regression. The usages of Linear Regression and SVM are similar. You can find the complete codes in the package "examples".

  ~~~scala
  val training = sc.loadLIBBLEFile(path, numPart)
  val m = new LogisticRegression(stepSize, regParam, elasticF, numIter,numPart)
      .setClassNum(10)
  m.train(training)
  ~~~

* #### Self-Defined Generalized Linear Model

  In our framework, you are allowed to define your own generalized linear models by using our learning engine to optimize. You can define your loss function by implementing the interface of the abstract class LossFunc. Here, we give an example of GeneralizedLinearModel:

  ~~~scala
  val training = sc.loadLIBBLEFile(args(0), numPart)
  val m=new GeneralizedLinearModel(stepSize, regParam, elasticF, numIter, numPart)
    .setLossFunc(new selfDefinedLoss())
    .setUpdater(new L1Updater)
  m.train(training)
  ~~~

* #### Collaborative Filtering

  Collaborative filtering is widly used in recommendation systems. An example to perform collaborative filtering with  the UV matrix factorization is shown as follows:
  ~~~scala
  val trainSet = sc.textFile(args(0), numParts)
      .map(_.split(',') match { case Array(user, item, rate) =>
          Rating(rate.toDouble, user.toInt, item.toInt)})
  val model = new MatrixFactorization()
    	.train(trainSet, numIters, numParts, rank, regParam_u, regParam_v,stepsize)
  ~~~

* #### Dimensionality Reduction

  Principal Component Analysis (PCA) is a widely used method for dimensionality reduction. An example to perform dimensionality reduction with PCA is shown as follows:

  ~~~scala
  val training = sc.loadLIBBLEFile(args(0), numPart)
  val mypca = new PCA(K, bound, stepSize, numIters, numPart, batchSize)
  val PCAModel = mypca.train(training)
  val pc = PCAModel._2
  val projected = mypca.transform(training, pc)
  projected.collect().foreach(x=>println(x.features))
  ~~~

  Singular value decomposition (SVD) is a popular matrix decomposition/factorization method in linear algebra and machine learning. An example to perform dimensionality reduction with SVD is shown as follows:

  ~~~scala
  val training = sc.loadLIBBLEFile(args(0), numPart)
  val mysvd = new SVD(K, bound, stepSize, numIters, numPart, batchSize)
  val SVDModel = mysvd.train(training)
  val sigma = SVDModel._1
  val v = SVDModel._2
  sigma.foreach(x=>print(x+","))
  v.foreach(x=>println(x))
  ~~~

* #### Clustering

  K-Means is a widely used prototype-based clustering algorithms. An example to perform clustering with K-Means is shown as follows:

  ~~~scala
  val training = sc.loadLIBBLEFile(args(0))
  val m = new KMeans(k, maxIters, stopBound)
  val data = training.map(e => (e.label, e.features))
  m.train(data)
  ~~~


### [Open Source](#open-source)

* GitHub URL: [https://github.com/LIBBLE/LIBBLE-Spark/](https://github.com/LIBBLE/LIBBLE-Spark/)
* Licence: This project follows [Apache Licence 2.0](https://www.apache.org/licenses/LICENSE-2.0)

### [API](#api)

Please click [here](api/) to check the Application Programming Interface documents.