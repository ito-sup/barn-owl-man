`Classification`
================

barn-owl provides algorithms for the purpose of classification with endpoints `/v1/classification/<algorithm_name>`.


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

`Logistic Regression`
---------------------

.. class:: classification/logistic/

   Logistic Regression is a probability regression model with categorical target variable.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization_inverse : float
         Inverse of regularization parameter.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted value by using the model,
         | 'target' : target value of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      features : list
         A features list used for fitting.

      coefficient : float matrix (n_categories, n_features)
         A coefficients list for each calssification category associated with each features element.

      intercept : float list (n_categories)
         The list of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization_inverse : float
         Inverse of regularization parameter.

`Ridge Classification`
----------------------

.. class:: classification/ridge/

   Ridge Classification is a linear sparse model for classification analysis.
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

      coefficient : float matrix (n_categories, n_features)
         A coefficients list for each calssification category associated with each features element.

      intercept : float list (n_categories)
         The list of intercept term.

      target : string
         Target column's name.

      score : int
         This score represents coefficient :math:`R^2=1-\frac{\sum_{i}(y_i - f_i)^2}{\sum_{i}(y_i -\overline{y})^2}` ,
         where :math:`y_i,f_i,\overline{y}` is training data, predicted data and mean of training data respectively.

      regularization: float
         Used reegularization parameter of Ridge term.


`Bagging Classification`
------------------------

.. class:: classification/bagging/

   Bagging Classification is one of the unsemble classifier.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter.

      estimator: ChoiceField(default=DecisionTree)
         Choose at least one alogrithm from "DecisionTree", "SGD", "Ridge" and "SVC".

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


`AdaBoost Classification`
-------------------------

.. class:: classification/adaboost/

   AdaBoost Classification is one of the unsemble classifier.
   In addition to common parameters, you can use additional parameters as follows,

   Parameters:

      features : list
         A features list used for fitting.

      regularization: float
         Regularization parameter.

      estimator: ChoiceField(default=DecisionTree)
         Choose at least one alogrithm from "DecisionTree", "SGD", "Ridge" and "SVC".

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

.. class:: classification/dnn/

   Classification model based on deep neural network.

   Attributes:

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'prediction' :predicted category by using the model,
         | 'target' : target category of training data. If 'train_data' is a dataset for evaluation, the value is dumy.

      target : string
         Target column's name.

      loss : float
         Sum of loss function.

