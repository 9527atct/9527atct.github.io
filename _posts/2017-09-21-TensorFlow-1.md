---
layout: postarticle
title: TensorFlow 1
date: 2017-09-21 11:54:05 +1000
categories: ComputerVision
comments: true
--- 


### 安装TensorFlow    
---  
[TensorFlow官方网站](https://www.tensorflow.org) 推荐linux环境下，使用原生pip安装， 这里只考虑CPU版， GPU版参考官网。
```
pip install tensorflow
```

### 几个小概念    
---  

You maight think of **TensorFlow** Core programs as consisting of two discrete sections:
- Building the computational graph
- Running the computational graph

**computational graph** is a series of TensorFlow operations arranged into a graph of nodes.

**tf.placeholder**: is a promise to provide a value later.   
**tf.Variable** allow us to add trainable parameters to graph.  


###入门案例  
--- 

```
import tensorflow as tf
import numpy as np

def test_tf_is_installed():
    node1 = tf.constant(3.0, dtype=tf.float32)
    node2 = tf.constant(4.0)
    print(node1,node2) 
    
def using_tf_train():
    """
    TensorFlow provides optimizers that slowly change each variable in order to 
    minimize the loss function. The simplest optimizer is gradient_descent. It 
    modifies each variable according to the magnitude of the derivative of loss 
    w.r.t. that variable. In general, computing symbolic derivatives manually is 
    tedious and error-prone. Consequently, TensorFlow can automatically produce 
    derivatives given only a description of the model using the function tf.gradients.
    For simplicity, optimizers typically do this for you.
    """

    # Model parameters
    W = tf.Variable([.3], dtype=tf.float32)
    b = tf.Variable([-.3], dtype=tf.float32)
    
    # Model input and output
    x = tf.placeholder(tf.float32)
    linear_model = W * x + b
    y = tf.placeholder(tf.float32)
    
    # loss
    loss = tf.reduce_sum(tf.square(linear_model - y))
    
    # optimizer
    optimizer = tf.train.GradientDescentOptimizer(0.01)
    train = optimizer.minimize(loss)
    
    # train data
    x_train = [1,2,3,4]
    y_train = [0,-1,-2,-3]
    
    # train loop
    init = tf.global_variables_initializer()
    sess = tf.Session()
    sess.run(init)
    for i in range(1000):
        sess.run(train, {x:x_train, y:y_train})
        
        
    # evluate training accuracy
    curr_W, curr_b, curr_loss = sess.run([W,b,loss],{x:x_train, y:y_train})
    print("W:%s b:%s loss: %s"%(curr_W, curr_b, curr_loss))
    
    
def using_tf_estimator():
    
    feature_columns = [tf.feature_column.numeric_column("x",shape=[1])]
    
    estimator = tf.estimator.LinearRegressor(feature_columns=feature_columns)
    
    x_train = np.array([1.,2.,3.,4.])
    y_train = np.array([0.,-1.,-2.,-3.])
    x_eval = np.array([2.,5.,8.,1.])
    y_eval = np.array([-1.01,-4.1,-7,0.])
    
    input_fn = tf.estimator.inputs.numpy_input_fn(
            {"x":x_train},y_train,batch_size=4,  num_epochs=None, shuffle=True)
    train_input_fn = tf.estimator.inputs.numpy_input_fn(
            {"x":x_train}, y_train, batch_size=4, num_epochs=1000, shuffle=False)
    eval_input_fn = tf.estimator.inputs.numpy_input_fn(
            {"x":x_eval}, y_eval, batch_size=4, num_epochs=1000, shuffle=False)
    
    estimator.train(input_fn=input_fn, steps=1000)
    train_metric = estimator.evaluate(input_fn=train_input_fn)
    eval_metric = estimator.evaluate(input_fn=eval_input_fn)
    
    print("===============begin train==============\n")
    print("train metrics: %r" % train_metric)
    
    print("===============begin eval===============\n")
    print("eval metrics: %r" % eval_metric)    
    
    
    

if __name__=='__main__':
    #test_tf_is_installed()
    #using_tf_train()
    using_tf_estimator()
```