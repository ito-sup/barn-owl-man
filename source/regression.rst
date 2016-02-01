`Regression`
============

barn-owl provides algorithms for the purpose of regression with endpoints `/v1/regression/<algorithm_name>`.

.. class:: Common Parameters:

   id : IntegerField, read only
         Unique and sequential number which is given automatically.

   title : CharField(max_length=100), optional (default='')
         A title of the model.

   code : TextField, optional (default='')
         An explanation of the model.

   owner : ForeignKey, read only
         Owner's username of the model.

   created : DateTimeField, read only
         Universal datetime when the model was created.

   updated : DateTimeField, read only
         Universal datetime when the model was updated.

   status : CharField, read only
      | Status represented from among the state list:``Created`` , ``Submitted Learning Request`` , ``Learning-in`` , ``Learned`` , ``Error`` .
      | Each status restricts some of request as follows,
      | ``Created`` : At the first time, a model is created with status 'Created'. `GET`, `PUT` and `DELETE` method are accepted,
        query parameter mode=evaluate with `GET` method, however, is NOT accepted.
      | ``Submitted Learning Request`` : When query parameter mode=learn with `PUT` method is accepted, state transitions to this.
         Query parameter mode=learn and evaluate is NOT accepted in this status.
      | ``Learning-in`` : When fitting process for the model is called, state transitions to this.
         Query parameter mode=learn and evaluate is NOT accepted in this status.
      | ``Learned`` : When fitting process for the model is finished, state transitions to this.
         Query parameter mode=evaluate with `GET` method is accepted,
         In order to avoid over fitting, query parameter mode=learn with same dataset is NOT accepted.
      | ``Error`` : When fitting process has stopped for some reason, state transitions to this.

   train_data : FileField
         Dataset used for fitting or evaluation process.

   trained_data : list like, read only
         List of dataset already used for fitting process.

   target : string
         Target column's name. Regression analysis usually has continuous variable for the target.



`Linear Regression`
-------------------


.. class:: regression/linear/

   Linear Regression fits a linear model with a dataset by least square method.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      coefficient : list
         A coefficients list associated with each features element.

      intercept : int
         The value of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.



`Lasso Regression`
------------------

.. class:: regression/lasso/

   Lasso Regression fits a linear sparse model with a dataset.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter of Lasso term.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      coefficient : list
         A coefficients list associated with each features element.

      intercept : int
         The value of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization: float
         Used egularization parameter of Lasso term.

`Ridge Regression`
------------------

.. class:: regression/ridge/

   Ridge Regression fits a linear dense model with a dataset.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter of Ridge term.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      coefficient : list
         A coefficients list associated with each features element.

      intercept : int
         The value of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization: float
         Used reegularization parameter of Ridge term.

`Elastic Net`
-------------

.. class:: regression/elasticnet/

   Elastic-Net Regression is a combination model of Lasso and Ridge Regression.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter of Lasso and Ridge term.

      l1_ratio: float
         ElasticNet mixing parameter(:math:`0.0 \leq l1\_ratio \leq 1.0`) of Lasso penalty against Ridge penalty.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      coefficient : list
         A coefficients list associated with each features element.

      intercept : int
         The value of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

`Bayesian Regression`
---------------------

.. class:: regression/bayesian/

   Bayesian Regression based on prior probability with gammma function.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization_rate: float(default=1e-06)
         Gamma rate parameter(inverse of scale parameter) of regularization term.

      regularization_shape: float(default=1e-06)
         Gamma shape factor of regularization term.

      noise_rate: float(default=1e-06)
         Gamma rate parameter(inverse of scale parameter) of noise term.

      noise_shape: float(default=1e-06)
         Gamma shape factor of noise term.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      coefficient : list
         A coefficients list associated with each features element.

      intercept : int
         The value of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization: float
         Used egularization parameter of Lasso term.


`Bagging Regression`
--------------------

.. class:: regression/bagging/

   Bagging Regression is one of the unsemble regressor.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter.

      estimator: ChoiceField(default=DecisionTree)
         Choose at least one alogrithm from "DecisionTree", "Linear", "Lasso", "Ridge" and "Bayesian".

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization: float
         Used reegularization parameter of Ridge term.

      estimator: string
         Choosed estimator algorithm.


`AdaBoost Regression`
---------------------

.. class:: regression/adaboost/

   AdaBoost Regression is one of the unsemble regressor.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter.

      estimator: ChoiceField(default=DecisionTree)
         Choose at least one alogrithm from "DecisionTree", "Linear", "Lasso", "Ridge" and "Bayesian".

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization: float
         Used reegularization parameter of Ridge term.

      estimator: string
         Choosed estimator algorithm.


`Deep Neural Network`
---------------------

.. class:: regression/dnn/

   Regression model based on deep neural network.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      loss : float
         Sum of loss function.

      target : string
         Target column's name.
