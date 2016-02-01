`Recommendation`
================

barn-owl provides Deep Q Network interface for the purpose of recommended action with endpoints `/v1/recommendation/dqn`.

`Deep Q Network`
----------------

.. class:: Parameters:

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

.. class:: Attributes:

      action_list: string list
         Enable action list. "best_action" in "data" list indicates index of the action_list.

      data : list of tuples
         Predicted list of tuples consisting of 'id', 'prediction' and 'target'.

         | 'id' : user id,
         | 'best_action' : Index of action_list with highest Q-value.
         | 'Qvalue' : Q-value of reignforcement learning for each enable action.

      target : string
         Target column's name.

